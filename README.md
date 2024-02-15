# rest-webservice-cors

This Spring Boot project is a simple RESTful web service that provides a greeting message. It includes Cross-Origin Resource Sharing (CORS) configuration to allow requests from a specific origin.

## GreetingController
The `GreetingController` class is the main controller responsible for handling HTTP requests. It includes CORS configuration for specific endpoints.

- **Endpoint**: The web service exposes a single endpoint /greeting.
    - Includes CORS configuration for allowing requests from "http://localhost:9000" origin.
- **Controller Method**:
    - The `greeting` method is annotated with @GetMapping("/greeting") to handle GET requests to the /greeting endpoint.
    - It takes an optional name parameter (default value is "World").
    - The method returns a Greeting object, which includes a unique ID generated using AtomicLong and a formatted greeting message.
      AtomicLong:
- The AtomicLong instance (counter) ensures that the counter is updated atomically, making it suitable for concurrent access by multiple threads.

## Greeting Class

The `Greeting` class is a record class, and it automatically generates an immutable class with a constructor and accessor methods.

## Usage

To run the application, ensure you have Gradle installed. Then, run the following command in the project directory:
```bash
./gradlew bootRun
```

The application will start, and you can access the web service at http://localhost:8080/greeting. You can also customize the greeting message by providing a name parameter:

## CORS Testing

1. To test CORS behaviour, start the client from a different port than 9000. Keep the service running at localhost:8080. Then, using Gradle, run this command:
```bash
./gradlew bootRun --args="--server.port=9000"
```
You should see the ID and content output since the service response includes the relevant CORS headers.

2. To test how CORS doesn't allow a Javascript client from another origin to access the service, run this command:
```bash
./gradlew bootRun --args="--server.port=9001"
```
You should see an **empty** ID and **empty** content output since the values are not rendered on the DOM because the CORS headers are missing.