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

### RDF Creation Standards

- Use common RDF namespaces like RDF, RDFS, OWL to leverage existing semantics
- Define a standard domain namespace, e.g. `tagify:`
- Create abbreviations for long namespaces to simplify entity IRIs
- Follow CamelCase convention for class names
- Use descriptive labels and comments on classes and relations
- Specify domain and range for properties

###  RDF Taxonomy Guidelines

- Top-level branch for main classifications like `tagify:Semantics`
- Second level for data sensitivity, access levels etc
- Third level for specific categories
- Fourth level for actual asset tags

###  Tagging Conventions

| Taxonomy Level | Example Prefix | Description |
|--|--|--| 
| Namespace | tagify: | Top level domain |   
| Level 1 Class | tagify:Semantics | High-level classification |
| Level 2 Class | tagify:Sensitive | Data sensitivity |
| Level 3 Class |  tagify:Confidential | Sensitive subtype |
| Tag | tagify:Confidential | Actual asset tag |

**Sample Taxonomy**

```
tagify:Semantics
  tagify:Sensitive
    tagify:Confidential
  
tagify:Access
  tagify:Permission
    tagify:Read
    tagify:Write
```  