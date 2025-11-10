# CacheCraft

An **adaptive caching system** using **Caffeine (in-memory)** and **Redis (distributed)**, with **metrics collection**, **REST APIs**, and **Dockerized deployment**.  

---

## Features

- Dual-layer caching with **Caffeine (L1)** and **Redis (L2)**  
- **Adaptive TTL engine** adjusts cache expiration based on access frequency  
- **Metrics collection and monitoring** for cache performance  
- RESTful API for cache operations (add/get/clear/configure cache)  
- **Dockerized deployment** for easy setup  
- Swagger/OpenAPI documentation for easy testing  

---

## Prerequisites

- **Java 17**  
- **Maven 3.8+**  
- **Docker and Docker Compose** (optional, for containerized deployment)  
- **Redis server** (if running without Docker)  

---

## Project Structure

# CacheCraft

An **adaptive caching system** using **Caffeine (in-memory)** and **Redis (distributed)**, with **metrics collection**, **REST APIs**, and **Dockerized deployment**.  

---

## Features

- Dual-layer caching with **Caffeine (L1)** and **Redis (L2)**  
- **Adaptive TTL engine** adjusts cache expiration based on access frequency  
- **Metrics collection and monitoring** for cache performance  
- RESTful API for cache operations (add/get/clear/configure cache)  
- **Dockerized deployment** for easy setup  
- Swagger/OpenAPI documentation for easy testing  

---

## Prerequisites

- **Java 17**  
- **Maven 3.8+**  
- **Docker and Docker Compose** (optional, for containerized deployment)  
- **Redis server** (if running without Docker)  

---

## Project Structure

# CacheCraft

An **adaptive caching system** using **Caffeine (in-memory)** and **Redis (distributed)**, with **metrics collection**, **REST APIs**, and **Dockerized deployment**.  

---

## Features

- Dual-layer caching with **Caffeine (L1)** and **Redis (L2)**  
- **Adaptive TTL engine** adjusts cache expiration based on access frequency  
- **Metrics collection and monitoring** for cache performance  
- RESTful API for cache operations (add/get/clear/configure cache)  
- **Dockerized deployment** for easy setup  
- Swagger/OpenAPI documentation for easy testing  

---

## Prerequisites

- **Java 17**  
- **Maven 3.8+**  
- **Docker and Docker Compose** (optional, for containerized deployment)  
- **Redis server** (if running without Docker)  

---

## Project Structure

com.cachecraft
├── config # Configuration classes (Caffeine, Redis, etc.)
├── controller # REST API controllers
├── metrics # Metrics collection and monitoring
├── model # Data models
├── service # Business logic
└── CacheCraftApplication.java # Main application class


---

## Building the Application

```bash
mvn clean package

## Running the Application

### Option 1: Direct Execution

1. Start a Redis server on `localhost:6379`

2. Run the application:

```bash
mvn spring-boot:run
```
Or:

```bash
java -jar target/cachecraft-0.0.1-SNAPSHOT.jar
```

## API Endpoints

- `GET /api/data/{key}` - Retrieve data by key
- `GET /api/cache/stats` - Get cache statistics
- `PUT /api/cache/config` - Update TTL configuration
- `DELETE /api/cache/clear` - Clear all cache entries
- `GET /swagger-ui.html` - Swagger UI documentation

---

## Testing

Run unit tests:

```bash
mvn test
```

## Monitoring

- Application metrics are available at `http://localhost:8081/actuator`
- Cache metrics endpoint: `http://localhost:8081/actuator/metrics`
- Health check: `http://localhost:8081/actuator/health`

---

## Configuration

The application can be configured via `src/main/resources/application.yml`:

- Redis connection settings
- Caffeine cache configuration
- Actuator and metrics settings

---

## How CacheCraft Works

CacheCraft acts as a **smart caching layer** between your API and data source.

1. **POST /api/data** → Add data to cache (also stores in temporary DB/test data)
2. **GET /api/data/{key}** → Fetch data:
   - If key exists in cache → **Cache Hit** → returned instantly
   - If key not in cache → **Cache Miss** → fetched from DB/test data and cached
3. **Cache metrics** track hits, misses, evictions, and memory usage
4. **PUT /api/cache/config** → Adjust TTL policies dynamically
5. **DELETE /api/cache/clear** → Clear all cached entries

---

### Flow Diagram

```
Client Request
|
v
[Cache Layer: Caffeine L1]
|-- Hit --> Return Data
|
|-- Miss
v
[Cache Layer: Redis L2]
|-- Hit --> Return Data & update L1
|
|-- Miss
v
[Temporary DB / Data Source]
|
v
Return Data -> Update L1 & L2 caches
```

- **Cache Hit:** Fast response from memory  
- **Cache Miss:** Data fetched from DB, then stored in cache  
- **Evictions:** Old or unused entries removed automatically
