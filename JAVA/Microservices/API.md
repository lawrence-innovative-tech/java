#### **API (Application Programming Interface)
- Api is an bridge between two [[0 Fundamentals#**Software|software]] or Two software can talk each other using API.
#### **Types of API
1. Open api (Public)
	1. [[#**Rest API|REST Api]] and [[#**RESTFULL API|RESTFULL api]]
	2. soap api
	3. GraphQL api
	4. gRPC
2. Internal api (Private)
	1. Backend-to Backend - Token Verify or Microservice
	2. Service-to-Database
3. Partner api
	1. Data-sharing api
	2. Payment Gateway
	3. ABIS

#### **REST API
- REST - Representational State Transfer
- It does not maintenance state of every request, It will consider each request as new.
- Rest api are happens through HTTP or HTTPS protocols.
- Spring Security expects the JWT token for every api calls. because does not maintains session.

#### **RESTFULL API
- RESTFULL api same as rest api, but additionally six rules to be included.