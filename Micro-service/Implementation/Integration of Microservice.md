#### **Purpose
- Microservice are used develop high scalability, design focus on micro business logic, single responsibility, resilience(strong enough to illness), Control based individual services with loose coupling. 
- **Important 
	1. **Single Responsibility -** Every service develop and focus on individual application. And easy to maintain priority based and achieved agile methodologies.
	2. **Database per Service -** Each data base connect per service for loose coupling as connection or data share using eventual consistency or saga pattern.
	3. **Communication -** Communication through event driven for asynchronous or http/rest, gRPC for synchronous communication.
	4. **Resilience or Fault Toleration -** Circuit breaker (e.g., via Hystrix or Resilience4j), retries, timeout to prevent cascading failures.
	5. **Observability -** ELK to monitor logs.
	6. **CI/CD Pipelines -** Automate to integration CI/CD pipelines.
	7. **Security -** using JWT or oauth protect application.
	8. **Containerization and Orchestration -** integrate docker and Kubernetes or OpenShift.
	9. **API gateway for Routing - ** Generalize access to handles api.

#### **Differentiate between Monolithic and Microservice
| **Feature**                        | **Monolith**                                                                                           | **Microservices**                                                                                                            |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| **Resilient and Fault Toleration** | Monolith is vertical scaling application structure, it's hard scale the application.                   | Horizontal Scale we can scale individual service without affecting another.                                                  |
| **Structure**                      | **Single Unit:** All code (UI, business logic, database access) is packed into one deployable file.    | **Collection of Services:** The app is broken into small, independent pieces that talk to each other (usually via APIs).     |
| **Database**                       | **Shared:** The entire application usually shares one massive database.                                | **Decentralized:** Each service ideally has its own database to ensure independence.                                         |
| **Deployment**                     | **All-or-Nothing:** If you change one line of code, you must redeploy the _entire_ application.        | **Independent:** You can update and deploy just the "Payment Service" without touching the "User Profile Service."           |
| **Tech Stack**                     | **Unified:** You are generally locked into one language/framework (e.g., the whole app is Java).       | **Flexible:** You can write the Search service in Python, the Frontend in React, and the Payment service in Go.              |
| **Scalability**                    | **Vertical:** Harder to scale. You usually have to clone the whole app, even if only one part is busy. | **Horizontal:** Precise. If "Search" is slow, you can add more servers _just_ for Search, without paying to scale the rest.  |
| **Failure**                        | **Fragile:** A memory leak or bug in one module can crash the entire system.                           | **Resilient:** If one service fails, the others continue to work (e.g., you can browse products even if "Checkout" is down). |
| **Methodologies**                  | Everytime redeploy whole thinks.                                                                       | develop and release are easy to handles. and achieve agile methodologies.                                                    |


#### **Doubts
1. how does track the single transaction
2. how does handles fault Toleration & Resilience