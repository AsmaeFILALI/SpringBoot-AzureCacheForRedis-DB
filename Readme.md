# Spring boot Azure Cache for Redis Example With DB
This application serves as an example of how to call Azure Cache for Redis using a private endpoint from a Spring Boot application

# Scenario 

- Inserting Data In H2 DB 
- Retrieving Data from DB and Caching the Data during 5 Mins
## Maven dependencies for Redis

```xml
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-redis</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-cache</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
```

## Spring properties

```
#redis config
spring.redis.host=${REDIS_HOST}
spring.redis.port=6380
spring.redis.password=${PWD}
spring.redis.ssl=true
spring.cache.redis.key-prefix=myapp
spring.cache.redis.use-key-prefix=true
spring.redis.timeout=3000
spring.cache.redis.time-to-live=10800000
# db config
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=password
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true

```

## Endpoints

- POST : /product/add : Adds A product that will be stored in Azure cache for Redis
  jsonBody:
  ```json
	{
    "name": "tajine"
	}
  ```
- GET : /product/{id} : Gets the product by id from Azure Cache for Redis - **Cached Response**
- GET : /products : Gets the list of the products stored in Azure Cache for Redis - **Cached Response**

## Test From Postman

To call the endpoitns bellow you can import the postman collection loocated in the folder /postman

## Configure Azure Cache for Redis with private endpoint 

- [Azure Cache for Redis with Azure Private Link](https://learn.microsoft.com/en-us/azure/azure-cache-for-redis/cache-private-link)

## Note 

ApplicationS should connect to {cachename}.redis.cache.windows.net on port 6380. Microsoft recommends avoiding the use of {cachename}.privatelink.redis.cache.windows.net in configuration or connection string.