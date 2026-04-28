# 具体RDF/OWL示例（台风/洪涝因果链）

**来源**：灾害事件画像知识框架具体示例
**说明**：可直接导入Protégé，导出Turtle格式后加载到GraphDB/Jena等工具，支持OWL推理 + SHACL验证 + SWRL规则

---

## 1. 基础类与属性定义（RDFS/OWL Schema）

```turtle
@prefix : <http://example.org/disaster#> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix owl: <http://www.w3.org/2002/07/owl#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

# 核心类
:DisasterEvent rdf:type owl:Class .
:Hazard rdf:type owl:Class ; rdfs:subClassOf :DisasterEvent .
:Disaster rdf:type owl:Class ; rdfs:subClassOf :DisasterEvent .
:Impact rdf:type owl:Class ; rdfs:subClassOf :DisasterEvent .
:ElementAtRisk rdf:type owl:Class .

# 属性 + domain/range（大幅提升NL匹配准确率）
:causes rdf:type owl:ObjectProperty ;
        rdfs:domain :DisasterEvent ;
        rdfs:range :DisasterEvent ;
        rdfs:label "导致"@zh ;
        skos:altLabel "引发" , "causes" .

:hasPart rdf:type owl:ObjectProperty , owl:TransitiveProperty ;  # 传递性：A部分B，B部分C → A部分C
         rdfs:domain :DisasterEvent ;
         rdfs:range :DisasterEvent ;
         owl:inverseOf :partOf .

:partOf rdf:type owl:ObjectProperty ;
        rdfs:domain :DisasterEvent ;
        rdfs:range :DisasterEvent .

:implies rdf:type owl:ObjectProperty ;  # 蕴含关系
         rdfs:domain :DisasterEvent ;
         rdfs:range :DisasterEvent .

# 实例示例（从对话中提取）
:Typhoon2025 rdf:type :Hazard ;
              :hasHazardType "台风" ;
              :location "台湾中部" ;
              :time "2025-09" .

:Flood rdf:type :Disaster ;
       :partOf :Typhoon2025 ;   # 部分关系
       :causes :InfrastructureDamage .  # 因果
```

**收益**：Agent解析对话"台风带来大雨，导致中部洪水，淹没道路"时，通过domain/range自动过滤非法匹配（如不能"洪水 causes 台风"），并用传递性自动推导多级关系。

---

## 2. OWL属性特性 + 重构因果关系（处理n元因果）

简单因果可能丢失"强度""条件"。建议重构为关系类（Reification）：

```turtle
:CausalRelation rdf:type owl:Class .

:hasCause rdf:type owl:ObjectProperty ;
          rdfs:domain :CausalRelation ;
          rdfs:range :DisasterEvent .

:hasEffect rdf:type owl:ObjectProperty ;
           rdfs:domain :CausalRelation ;
           rdfs:range :DisasterEvent .

:strength rdf:type owl:DatatypeProperty ;
          rdfs:domain :CausalRelation ;
          rdfs:range xsd:string .  # "high"/"medium"

# 示例实例
:TyphoonFloodCausal rdf:type :CausalRelation ;
                    :hasCause :Typhoon2025 ;
                    :hasEffect :Flood ;
                    :strength "high" .
```

这支持Agent从碎片化对话中提取完整因果链，并用OWL限制强制"每个因果必须有cause和effect"。

---

## 3. SWRL规则示例（自动推理隐含知识，提升准确率）

在Protégé中添加SWRL规则（或Jena规则）：

```swrl
# 规则1：部分导致整体的因果传递
DisasterEvent(?e1) ^ partOf(?e1, ?e2) ^ causes(?e2, ?e3) → causes(?e1, ?e3)

# 规则2：台风蕴含洪水风险（领域特定）
Hazard(?h) ^ hasHazardType(?h, "台风") ^ implies(?h, ?d) → possibleDisaster(?d, "洪涝")

# 规则3：因果强度推断影响严重度
CausalRelation(?cr) ^ hasCause(?cr, ?c) ^ hasEffect(?cr, ?e) ^ strength(?cr, "high") → severeImpact(?e)
```

**实际效果**：对话中只提到"台风部分影响引发局部积水"，推理引擎自动补全"可能导致区域洪灾 + 基础设施严重损失"，无需Agent每次全量扫描框架。

---

## 4. SHACL Shapes（验证模板，提升提取质量）

定义"完整灾害画像"的约束，Agent提取后自动验证：

```turtle
@prefix sh: <http://www.w3.org/ns/shacl#> .

:DisasterEventShape rdf:type sh:NodeShape ;
    sh:targetClass :DisasterEvent ;
    sh:property [
        sh:path :hasLocation ;          # 必须有时空
        sh:minCount 1 ;
        sh:datatype xsd:string
    ] ;
    sh:property [
        sh:path :causes ;
        sh:minCount 0 ;                 # 可选，但若有则必须合法
        sh:node :CausalRelationShape
    ] ;
    sh:property [
        sh:path :hasPart ;
        sh:maxCount 10 ;                # 限制规模，避免过度碎片
    ] .
```

**落地流程**：LLM从对话提取RDF → SHACL验证器检查（不符则重提prompt）→ 通过后入KG推理。

---

## 5. 词汇映射层（SKOS + altLabel，提升NL grounding速度）

```turtle
:Typhoon rdf:type :Hazard ;
         rdfs:label "台风"@zh ;
         skos:altLabel "typhoon", "热带气旋", "hurricane" (跨语言) .

:Flood rdf:type :Disaster ;
       skos:altLabel "洪水", "flooding", "水灾" .
```

结合embedding检索时，Agent可快速将"强烈热带风暴"映射到:Typhoon，大幅降低零样本歧义。

---

## 6. 实际对话处理示例流程（提升速度与准确率）

对话片段：
"昨天台风过境台湾中部，带来暴雨，部分地区出现洪涝，道路被淹，影响居民出行。"

处理流程：

1. **LLM初步提取** → RDF triples（使用altLabel匹配）
2. **SHACL验证** → 确保时空、因果完整
3. **OWL + SWRL推理** → 自动推导"台风 → 洪涝（部分）→ 基础设施损失（因果传递）"
4. **输出结构化画像** + 置信度（结合PROV-O追踪来源）

---

## 7. 后续资源

- 如需生成特定灾害（如地震或干旱）的完整小本体片段
- 或需SPARQL查询模板
- 或需Agent pipeline代码（Python + rdflib + pyshacl）

请提供具体字段列表（如上位/下位关系表，或某个灾害场景的完整框架）

---

**文件结束**