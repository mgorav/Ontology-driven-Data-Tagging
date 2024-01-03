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
    4. Run the application: `java -jar target//Tagify-0.0.1-SNAPSHOT.jar` or `mvn spring-boot:run`
    5. Access Swagger UI documentation on http://localhost:8080/swagger-ui/index.html

The application exposes REST APIs for taxonomy and tagging operations. The RDF ontology is loaded in an in-memory store on startup.

The main components are:

- `TaggingController` - REST API endpoints
    - `TaggingService` - Business logic
    - `TaggingRepository` - RDF4J based data access
