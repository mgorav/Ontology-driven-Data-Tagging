# Tagify - Ontology-driven Data Tagging

[![CircleCI](https://dl.circleci.com/status-badge/img/gh/mgorav/Tagify/tree/main.svg?style=svg&circle-token=CCIPAT_8dsVTiu6F6romJqm99VA1B_b03d8b2a0a59b5911dc4c7c38640ed95f9494304)](https://dl.circleci.com/status-badge/redirect/gh/mgorav/Tagify/tree/main)
Tagify leverages a formal ontology to classify data assets and expose tags through a robust API.

## Conceptual Overview

An ontology defines concepts and relationships to model a domain. Tagify uses this ontology to tag assets like databases and APIs using the dot notation taxonomy:

```
[Namespace].[Category].[Classification]
```

For example, `acme.inventory.SupplierTable` attaches a classification tag. The taxonomy is derived from ontology relationships.

### Comparing Classification and Categorization

Classification and categorization offer complementary approaches for organizing elements which can be compared across several key dimensions:

Feature | Classification | Categorization
-|-|-
Defining Property | Necessary and sufficient conditions for membership | Family resemblances centered on prototypes
Mathematical Formalization | Rigid set membership based on feature possession m ∈ C ⟺ D(C) ⊆ M | Graded membership based on typicality ratings T(m,C) → [0,1]
Architectural Instantiation | Hierarchical taxonomies with superordinate and subordinate classes | Flexible conceptual clusterings responsive to contexts
Examples | Nike product database organized by attributes like sport, use case, gender, etc. | Nike shoes grouped into running, training, lifestyle based on style cues 
Key Advantages | Supports robust knowledge encoding and inferences via inheritance relationships | Adaptable to interdisciplinary content and innovative cases
Key Disadvantages | Brittleness to atypical instances and aerial views | Lacks persistent systematicity hindering transmission

In short, classification relies on rigid, formal conditions for set membership in hierarchical structures enabling inference. In contrast, categorization uses flexible typicality-based clustering sensitive to real-world contexts and new content.

Hybrid approaches can integrate these mechanisms to balance tradeoffs. The organizing principles match use case goals - classification for inference-based reasoning leveraging knowledge bases, categorization for pragmatic similarity judgments adjusting to new observations.

## Technical Details

The ontology is modeled in W3C standard RDF (Resource Description Framework):

```
acme:Semantics a rdf:Class .
acme:Confidential a rdf:Class;
                 rdf:type acme:Access.
```

## Unified Tagging Taxonomy

The tag structure is:

| Tag Type      | Description            | Example               |
| ------------- | ---------------------- | --------------------- |
| **Semantics** | Defines meaning        | acme.order.Customer   |
| **Discovery** | Links assets           | acme.product.replacement |
| **Access**    | Classifies access      | acme.sales.Confidential |
| **Lifecycle** | Manages lifespan       | acme.customer.Retention |

## Direct RDF Mapping

Each tag type directly maps to its RDF class:

```
acme:Confidential rdf:type acme:Access
```

This enables consistent semantics across tools leveraging the ontology.

### OAS UI

![img.png](img.png)

## RDF Ontology Modeling

The ontology represents the taxonomy in RDF:

```
# Semantic Tag
acme:Semantics a rdf:Class .
acme:CustomerInfo a rdf:Class;
                  rdf:type acme:Semantics .

# Discovery Tag                 
acme:Discovery a rdf:Class .  
acme:Replacement a rdf:Class;
                  rdf:type acme:Discovery .

# Access Tag    
acme:Access a rdf:Class .
acme:Confidential a rdf:Class;
                   rdf:type acme:Access .
                   
# Lifecycle Tag
acme:DataLifecycle a rdf:Class .   
acme:Retention a rdf:Class;
                 rdf:type acme:DataLifecycle .
```

This demonstrates modeling examples of mapping the unified taxonomy types to formal RDF ontology concepts and relationships.

## Tagging APIs

The APIs follow the dot notation tagging convention:

```
GET /tags/acme.customer/semantics
```

The underlying RDF ontology models the concepts:

```
acme:Semantics a rdf:Class .
acme:CustomerInfo a rdf:Class; 
                  rdf:type acme:Semantics.
```

This enables the api to return the matching tags:

```
[
  "acme.customer.CustomerInfo"
]
```

Additional examples for other tag types:

```
# RDF Ontology
acme:Access a rdf:Class .  
acme:Public a rdf:Class;
             rdf:type acme:Access.
             
# API Call            
GET /tags/acme.data/access

# Response Tags 
[
  "acme.data.Public"
]
```

And lifecycle tags:

``` 
# RDF Ontology
acme:Retention a rdf:Class;
                rdf:type acme:DataLifecycle.
                
# API Call                  
GET /tags/acme.order/lifecycle  

# Response Tags
[
  "acme.order.Retention"  
]
```

## Integrations with Data Platforms

Tagify provides seamless integration with leading data engineering platforms like Databricks, Snowflake, and Hive to enable unified data governance through consistent classification.

The taxonomy APIs classify assets and expose ontology-aligned tags:

```
GET /tags/acme.customer/semantics
```

These tags can then be applied to data objects like tables and columns:

**Databricks**

```python
# Classify customer table
CREATE TABLE customers (id INT, name STRING) TAGGED "acme.customer.PII" 

# Classify order table  
CREATE TABLE orders (order_id INT, customer_id INT) TAGGED "acme.order.TransactionData"
```

**Snowflake**

```sql 
-- Classify customer table
CREATE TABLE customers (id INT, name STRING) TAG acme.customer.PII

-- Classify order table
CREATE TABLE orders (order_id INT, customer_id INT) TAG acme.order.TransactionData 
```

**Hive**

```sql
-- Classify customer table 
CREATE TABLE customers (id INT, name STRING) TBLPROPERTIES ('acme.customer.PII'='true')

-- Classify order table 
CREATE TABLE orders (order_id INT, customer_id INT) TBLPROPERTIES ('acme.order.TransactionData'='true') 
```

This demonstrates direct application of Tagify taxonomy tags to data assets within platform native syntax. The tags become first class metadata aligning meaning across systems.

Key benefits include:

- Unified semantics for interoperability
- Consistent access controls
- Streamlined data discovery
- Automated lifecycle management


###NOTE
For more information and to request a demo, please contact our team at gonnect.ask@gmail.com. We would be happy to schedule a call to discuss our solutions in more detail and answer any questions you may have.
