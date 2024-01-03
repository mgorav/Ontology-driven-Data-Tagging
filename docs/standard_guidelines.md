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