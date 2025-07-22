# 🧪 Redis AllKeys-LRU Eviction Workshop (Java + Redis Enterprise)

## 🎯 Objective

Simulate memory pressure on Redis Enterprise and observe how it evicts keys using the `allkeys-lru` policy—**no TTL required**.

---

## 📚 Prerequisites

You’ll need:

- ✅ Redis Enterprise (Cloud or On-Prem)
- ✅ Java 8+
- ✅ Maven
- ✅ Git
- ✅ IDE (e.g., IntelliJ IDEA / VS Code)

---

## 📦 Clone the Java App

Get the app from GitHub:

```bash
git clone https://github.com/harshp124/redis-demo.git
cd redis-demo

⚙️ Redis Enterprise Configuration
Create a Redis database with these settings:

Setting	Value
Database Name	lru-allkeys-test
Memory Limit	e.g., 50MB
Eviction Policy	allkeys-lru
Replication	Disabled
Flash	Optional
💡 The allkeys-lru policy automatically evicts the least recently used keys when memory is full, regardless of TTL.

Record your Redis host, port, and password.

🖊️ Configure the Java App
In src/main/java/com/example/redis/TestEviction.java, update:

java
Jedis jedis = new Jedis("your_redis_host", 6379);
jedis.auth("your_redis_password");
Remove or comment out any usage of setex() or TTL. Use simple set():

java
jedis.set("key-123", largeValue);
You can add logic to insert thousands of keys with random values to quickly exhaust memory.

🔨 Build and Run the App
Compile and run:

bash
mvn clean install
java -cp target/redis-demo-1.0-SNAPSHOT.jar com.example.redis.TestEviction
Expected behavior:

Keys inserted continuously until Redis reaches memory limit

Least recently used keys are evicted automatically
