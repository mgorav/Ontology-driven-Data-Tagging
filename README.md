# Tagify: Unleashing the Power of Ontology-Driven Data Tagging

## Build Statues

[![CircleCI](https://dl.circleci.com/status-badge/img/gh/mgorav/Tagify/tree/main.svg?style=svg&circle-token=CCIPAT_8dsVTiu6F6romJqm99VA1B_b03d8b2a0a59b5911dc4c7c38640ed95f9494304)](https://dl.circleci.com/status-badge/redirect/gh/mgorav/Tagify/tree/main)

[![CircleCI](https://circleci.com/gh/mgorav/Tagify/tree/main.svg?style=shield&circle-token=e3c70c65cd695ed11883ffabd8c8a6e8aff9ee07)](https://circleci.com/gh/mgorav/Tagify/tree/main
)


**Tired of data silos, inconsistent metadata, and endless search for insights?**

Tagify revolutionizes data management, unlocking unprecedented value through a groundbreaking approach: ontology-driven tagging.

Imagine a world where:

* Data assets speak a common language, effortlessly understood across systems.
* Governance policies automate themselves, ensuring compliance and security.
* Insights surface effortlessly, accelerating innovation and decision-making.
* Tagify makes this a reality.

Here's how it works:

1. **A Unified Ontology:**

Concepts and relationships within your domain are meticulously modeled in RDF, a globally recognized knowledge representation standard.
This creates a shared semantic foundation, ensuring consistency and interoperability.

<img src="images/img_3.png" width="600" style="display: inline-block;">

2. **A Powerful Taxonomy:**

A hierarchical classification system emerges from the ontology, enabling granular organization of assets.
Tags become precise and meaningful, not merely arbitrary labels.

<img src="images/img_4.png" width="600" style="display: inline-block;">

3. **Smart Tagging APIs:**

Intuitive REST APIs empower seamless integration with data platforms like Databricks, Snowflake, and Hive.
Assets are tagged directly within your preferred environments, effortlessly weaving metadata into the fabric of your data ecosystem.

4. **Integration Symphony:**

Tagify seamlessly connects with policy catalogs and enforcement mechanisms.
Governance actions are triggered automatically based on tags, ensuring compliance and risk mitigation.

![img_5.png](images/img_5.png)

**_Experience the Benefits:_**

* Unified Metadata: Break down silos and create a cohesive knowledge graph.
* Enhanced Governance: Automate compliance, streamline access control, and streamline regulatory adherence.
* Accelerated Analytics: Discover insights faster and drive informed decision-making.
* Frictionless Adoption: Integrates seamlessly with leading data platforms.
* Robust Foundation: Built on industry-standard RDF and Spring Boot, ensuring reliability and scalability.
* Ready to transform your data landscape?

Dive into the Contents for technical details and embark on your semantic journey today!

## Contents
1.  [Introduction](docs/introduction.md)
2.  [Value Proposition](docs/value_proposition.md)
3.  [Overview](overview.md)
4.  [Taxonomy Foundation](docs/taxonomy_foundation.md)
5.  [Tagging & Taxonomy](docs/tagging_taxonomy.md)
6.  [Standards & Guidelines - RDF & Tagging](docs/standard_guidelines.md)
7.  [Taxonomy via APis](docs/taxonomy_apis.md)
8.  [Integration with Data Platforms & Architecture](docs/integrations.md)
9.  [Metadata Management](docs/mdm.md)
10. [Technology used & how to run](docs/tech.md)
11. [Integration Test](docs/integration_tests.md)
12. [Contact](docs/contact.md)

Let's go Tagify .....

```bash
 java -jar executable/Tagify-0.0.1-in-momory.jar
```
To test [Tagify APIs](apis/api-tests.rest) to execute APIs:

1. Save the content as a file named api-tests.rest.
2. Open IntelliJ IDEA.
3. Go to "View" -> "Tool Windows" -> "HTTP Client".
4. In the HTTP Client tab, you can create a new scratch file and paste the content.
5. Use the execute icon next to each request block to run the corresponding test.

![img_6.png](images/img_6.png)

## UI (wip)

![UI.png](images/UI.png)
![UI1.png](images/UI1.png)
![UI2.png](images/UI2.png)