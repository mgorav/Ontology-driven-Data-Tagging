# Tagify - Ontology-driven Data Tagging

[![CircleCI](https://dl.circleci.com/status-badge/img/gh/mgorav/Tagify/tree/main.svg?style=svg&circle-token=CCIPAT_8dsVTiu6F6romJqm99VA1B_b03d8b2a0a59b5911dc4c7c38640ed95f9494304)](https://dl.circleci.com/status-badge/redirect/gh/mgorav/Tagify/tree/main)

Tagify leverages a formal ontology to classify data assets and expose tags through a robust API.The Tagify taxonomy engineering service purposefully traverses key dimensions to bridge ontology and organization:

Modularity → Methodically compose coherent modules with crisp focus areas to organize knowledge into intuitive bundles. This prevents fragmentation by grouping related concepts.

Consistency → Aligning vocabulary and semantics is woven across modules so taxonomy consumers have clarity, not chaos. Controlled vocabularies become second nature.

Extensibility → Future-proof taxonomies, ensuring ontologies can evolve without brittleness. Dot notation provides durable links that gracefully adapt domains.

Customizability → Taxonomies aren’t one-size-fits all. We collaborate with customers to incorporate proprietary elements that meet specialized needs.

Accessibility → Dot notation taxonomy conventions remove complexity barriers.

REST APIs encourage programmatic integration into existing flows.

The outcome is a scalable medium exchanging meaning across teams and tools tackling data challenges – from security to compliance to analytics and more!

![img_2.png](img_2.png)

## Overview

An ontology formally defines the concepts, entities, relationships and properties within a domain. It provides a shared conceptual model of the knowledge in that domain.

For example, an ontology could model:

- Products
- Customers
- Orders
- Inventory

And relationships like:

- Customer "places" Order
- Order "includes" Product

A taxonomy categorizes entities into hierarchical classifications, often derived from the ontology relationships.

For example, the product taxonomy could be:

- Product
    - Electronics
        - Computers
            - Laptops
            - Desktops
        - Phones
            - Smartphones
    - Home
        - Furniture
        - Appliances

## Key Benefits

Using an ontology and taxonomy provides benefits like:

- Standard terminology for interoperability
- Reasoning to derive new knowledge
- Classification for governance and analysis

## Tagging for Governance

For data governance, tags can be derived from the ontology and taxonomy to classify data assets like:

```
acme.customer.PII -> Labels customer PII data
acme.product.inventory -> Tags product inventory datasets 
```

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

The tagging REST APIs could enable this as:

Endpoint | Description | Example Response
--- | --- | ---
GET /tags/namespaces | Get all namespaces | ["acme"]
GET /tags/acme/semantics | Get semantic tags | ["acme.customer", "acme.product"]  
GET /tags/acme/customer | Get all customer tags | ["acme.customer.PII", "acme.customer.profile"]
GET /tags/acme/product | Get all product tags | ["acme.product.inventory", "acme.product.pricing"]



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

## Architecture Design

Tagify leverages a layered architecture aligned to its ontology-based classification capabilities.

The architecture consists of 3 key layers - Ontology, Service and Integration:

![img_1.png](img_1.png)

**Ontology Layer**

This models the core RDF Ontology which formally defines the concepts, relationships and taxonomy for the domain. Key components:

- RDF Ontology: Formal conceptual model in RDF format
- Taxonomy Classification: Organizes concepts into hierarchical taxonomies
- Metadata Repositories: Links ontology to external systems

The ontology provides the foundation for deriving standardized taxonomy tags consistently across tools.

**Service Layer**

This exposes APIs for tagging operations and handles taxonomy business logic:

- Tagify API: REST endpoints for tagging APIs aligned to taxonomy
- Tagify Logic: Business logic for retrieving ontology-based tags
- Triple Store: Manages taxonomy terms modeled in RDF graphs

The service layer leverages the ontology terms to deliver unified tagging capabilities.

**Integration Layer**

This connects the taxonomy to data assets and policy catalogs:

- Tagged Assets: Annotates datasets with classification tags
- Policy Rules: Links governance policies to specific tags
- Enforcement Actions: Executes actions like access restrictions based on tags

The integration later enables scalable governance workflows driven by shared taxonomy.

The ontology ties the components together by providing common semantics accessible via consistent RDF graphs and taxonomy structure across systems.


## Technologies Used

- Java 17
- Spring Boot 3.2.1
- Spring Web MVC
- SpringDoc OpenAPI 3.0 for documentation
- Eclipse RDF4J for RDF data management

## Running Tagify

The application is packaged as a Java Spring Boot application.

### Prerequisites

- Java 17
- Maven

### Steps

1. Clone the repository
2. Navigate to the project directory
3. Build using Maven: `mvn clean install`
4. Run the application: `java -jar Tagify-0.0.1-in-momory.jar`
5. Access Swagger UI documentation on http://localhost:8080/swagger-ui/index.html

The application exposes REST APIs for taxonomy and tagging operations. The RDF ontology is loaded in an in-memory store on startup.

The main components are:

- `TaggingController` - REST API endpoints
- `TaggingService` - Business logic
- `TaggingRepository` - RDF4J based data access

### NOTE
For more information and to request a demo, please contact our team at gonnect.ask@gmail.com. We would be happy to schedule a call to discuss our solutions in more detail and answer any questions you may have.
