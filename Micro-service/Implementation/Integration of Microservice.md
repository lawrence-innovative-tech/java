#### **Purpose
- Microservice are used develop high scalability, design focus on micro business logic, single responsibility, resilience(strong enough to illness), Control based individual services with loose coupling. 
- **Important 
	1. **Single Responsibility -** Every service develop and focus on individual application. And easy to maintain priority based and achieved agile methodologies.
	2. **Database per Service -** Each data base connect per service for loose coupling as connection or data share using eventual consistency or saga pattern.
	3. **Communication -** Communication through event driven for asynchronous or http/rest, gRPC for synchronous communication.
	4. **Resilience or Fault Toleration -** Circuit breaker (e.g., via Hystrix or Resilience4j), retries, timeout to prevent cascading failures.
	5. **Observability -** 
	6. **CI/CD Pipelines -** 
	7. **Security -**
	8. **Containerization and Orchestration -** 