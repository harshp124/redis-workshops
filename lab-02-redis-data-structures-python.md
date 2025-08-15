# Lab 02 – Redis Data Structures

In this lab, you'll run a Python script that demonstrates **Redis core data structures** and how to interact with them using the `redis-py` client.

You’ll learn:
- How to connect to a Redis database
- How to store, retrieve, and manipulate data in various Redis data structures
- Real-world use cases for each data structure

---

## 🧩 Prerequisites

- Python 3.7+
- `pip` package manager
- Access to a Redis database (Redis Cloud, Redis Enterprise, or local Redis Stack)
- A terminal or IDE that can run Python scripts
- (Optional but Recommended) [Redis Insight](https://redis.io/insight/) to visually explore the data

---

## 📦 Install Dependencies

```bash
pip install redis
```

---

## 🔗 Set Up Redis Connection

Edit the connection section in the script (`redis-datastructures.py`) to match **your Redis instance details**:

```python
r = redis.Redis(
    host='YOUR_REDIS_HOST',
    port=YOUR_PORT,             
    username='YOUR_USERNAME',   
    password='YOUR_PASSWORD',   
    decode_responses=True
)
```

**Where to find these values (Redis Cloud):**
- **Host**: Shown as "Public Endpoint" in database details (remove `:port` part)
- **Port**: Number after the colon in "Public Endpoint"
- **Username**: Often `default`
- **Password**: Shown in the **Security** tab under "Default user password"

---

## 🚀 Run the Script

```bash
python redis-datastructures.py
```

The script will:
- Explain what it's doing
- Pause and wait for you to press **Enter** before each step
- Show the data being stored/retrieved


💡 **Tip:**: While inserting and retrieving data through the terminal, also open Redis Insight connected to your database (which we did in the previous lab) to visually explore the keys being created. You can:
	•	Navigate to Keys Browser
	•	Search for the key names shown in the script output (e.g., greeting, user:1001, searches)
	•	Inspect their values and structure in real-time

---

## 📚 Data Structures Covered

### 1. STRING
- **What it is:** Simple key-value pair.
- **Example in code:**  
  ```python
  r.set('greeting', 'Hello, Redis!')
  r.get('greeting')
  ```
- **Use cases:**
  - Caching values (e.g., HTML, API responses)
  - Storing counters or simple flags
- **Methods used:**
  - `set(key, value)`: Store a string
  - `get(key)`: Retrieve a string

---

### 2. HASH
- **What it is:** A collection of field-value pairs (like a mini JSON object).
- **Example in code:**  
  ```python
  r.hset('user:1001', mapping={'name': 'Alice', 'email': 'alice@example.com'})
  r.hgetall('user:1001')
  r.hget('user:1001', 'email')
  ```
- **Use cases:**
  - User profiles
  - Product attributes
- **Methods used:**
  - `hset(key, mapping=...)`: Set multiple fields
  - `hgetall(key)`: Get all fields
  - `hget(key, field)`: Get one field

---

### 3. LIST
- **What it is:** Ordered collection of strings.
- **Example in code:**  
  ```python
  r.rpush('searches', 'redis tutorial', 'python redis')
  r.lrange('searches', 0, -1)
  r.lindex('searches', 1)
  ```
- **Use cases:**
  - Task queues
  - Recent activity logs
- **Methods used:**
  - `rpush(key, value)`: Push to end of list
  - `lrange(key, start, end)`: Get elements
  - `lindex(key, index)`: Get specific element

---

### 4. SET
- **What it is:** Unordered collection of unique strings.
- **Example in code:**  
  ```python
  r.sadd('post:tags', 'python', 'redis')
  r.smembers('post:tags')
  r.sismember('post:tags', 'redis')
  ```
- **Use cases:**
  - Unique tags or categories
  - Friend lists
- **Methods used:**
  - `sadd(key, value)`: Add to set
  - `smembers(key)`: Get all members
  - `sismember(key, value)`: Check membership

---

### 5. SORTED SET
- **What it is:** Set of unique strings with a score for sorting.
- **Example in code:**  
  ```python
  r.zadd('game:leaderboard', {'Alice': 1500, 'Bob': 1800})
  r.zrevrange('game:leaderboard', 0, -1, withscores=True)
  r.zscore('game:leaderboard', 'Clara')
  ```
- **Use cases:**
  - Leaderboards
  - Priority queues
- **Methods used:**
  - `zadd(key, mapping)`: Add with score
  - `zrevrange(key, start, end, withscores=True)`: Get high-to-low
  - `zscore(key, member)`: Get score


---

## 🎯 Summary

After running this lab, you will:
- Understand and interact with Redis data structures from Python
- Know common use cases for each
- Be able to adapt this knowledge to your own projects

---

## 📚 Resources

- [Redis Data Types](https://redis.io/docs/latest/develop/data-types/)
- [redis-py Documentation](https://redis-py.readthedocs.io/en/stable/)
- [Redis CLI Reference](https://redis.io/commands/)
