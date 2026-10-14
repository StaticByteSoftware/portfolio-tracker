# portfolio-tracker

A small full-stack app for tracking investment holdings: a Spring Boot REST API with a React and TypeScript front end. I built it in October 2026 to learn Spring Boot and React end to end, with tests at each layer.

## Stack

- **API (`api/`):** Java 21, Spring Boot 4, Spring Web MVC, Spring Data JPA, Bean Validation, H2 in-memory database, JUnit 5, Mockito, MockMvc
- **UI (`ui/`):** React, TypeScript, Vite, Vitest, React Testing Library
- **CI:** GitHub Actions runs the API tests and the UI tests and build on every push

## Run it

```bash
# API on http://localhost:8080
cd api
./mvnw spring-boot:run

# UI on http://localhost:5173 (in a second terminal; requests to /api go to the API)
cd ui
npm install
npm run dev
```

## API

| Method | Path | Returns |
| --- | --- | --- |
| GET | `/api/holdings` | 200 and every holding |
| GET | `/api/holdings/{id}` | 200 and the holding, or 404 |
| GET | `/api/holdings/summary` | 200 with the number of holdings and the total cost |
| POST | `/api/holdings` | 201 with a `Location` header, or 400 with the field errors |
| PUT | `/api/holdings/{id}` | 200 and the updated holding, 400, or 404 |
| DELETE | `/api/holdings/{id}` | 204, or 404 |

A holding has a `symbol` (1-10 capital letters), a `quantity` (at least 1) and an `averageCost` (more than 0).

## How it is built

`HoldingController` handles HTTP and validation, `HoldingService` holds the business logic, and `HoldingRepository` is a Spring Data JPA interface over the `holdings` table. Errors are turned into consistent JSON by one `@RestControllerAdvice`.

## Tests

```bash
cd api && ./mvnw test     # controller tests with MockMvc, service tests with Mockito, repository tests with @DataJpaTest
cd ui && npm test         # component tests with React Testing Library
```

## Status

In progress: the API first (Oct 14-15), then the UI (Oct 16-17).
