# Lab 03 – Working with RedisJSON

In this lab, we’ll explore **how to store, retrieve, update, and query JSON documents** in Redis using the **RedisJSON module** and the `redis-py` client.  
We’ll go step-by-step, so even if you’ve never worked with JSON in Redis before, you’ll be able to follow along.

---

## 🧩 Prerequisites

- Python 3.7+
- `pip` package manager
- Access to a Redis database with the **RedisJSON module enabled** (Redis Cloud, Redis Enterprise, or local Redis Stack)
- A terminal or IDE that can run Python scripts
- (Optional but Recommended) [Redis Insight](https://redis.io/insight/) to visually explore JSON data

---

## 📦 Install Dependencies

```bash
pip install redis
```

---

## 🔗 Set Up Redis Connection

Edit the connection variables in the script (`redis-json.py`) with **your Redis instance details**:

```python
REDIS_HOST = 'YOUR_REDIS_HOST'
REDIS_PORT = YOUR_PORT
REDIS_USER = 'YOUR_USERNAME' 
REDIS_PASS = 'YOUR_PASSWORD'
```

Example for Redis Cloud:
- **Host**: Shown as "Public Endpoint" in database details (remove `:port` part)
- **Port**: Number after the colon in "Public Endpoint"
- **Username**: Often `default`
- **Password**: Found under the **Security** tab in database settings

---

## 🚀 Run the Script

```bash
python redis-json.py
```

The script:
- Stores a nested JSON document
- Retrieves specific fields from it
- Updates parts of it
- Shows how to query inside arrays
- Displays the updated JSON

💡 **Pro Tip:** While running the commands in the terminal, open **Redis Insight** connected to your database so you can:
- Browse to the **Keys** tab
- Search for `user:1002`
- Inspect the JSON visually
- See updates happen in real-time as you run the script

---

## 🧠 Understanding the Script Step-by-Step

### 1. **Store a nested JSON**
We first define a nested Python dictionary:

```python
nested_json = {
    "user": {
        "id": 1002,
        "name": "Alice",
        "address": {"city": "New York", "zip": "10001"},
        "contacts": [
            {"type": "email", "value": "alice@example.com"},
            {"type": "phone", "value": "555-1234"}
        ],
        "stats": {"visits": 34, "is_active": True}
    }
}
```

Then we store it in Redis with:
```python
r.json().set('user:1002', '$', nested_json)
```
- `'user:1002'` → Redis key name
- `'$'` → JSONPath root (store the object at the root)

**Use case:** Store structured objects like user profiles, products, or documents.

---

### 2. **Fetch a nested field**
We retrieve only the city name from `user.address.city`:
```python
city = r.json().get('user:1002', '$.user.address.city')
```
- **JSONPath** `$` = root, `.user.address.city` = drill down into nested fields
- This allows fetching **just what you need** without retrieving the whole object

---

### 3. **Increment a numeric field**
We increase the `visits` count:
```python
r.json().numincrby('user:1002', '$.user.stats.visits', 1)
```
- `numincrby` lets you atomically increment numeric fields **inside** JSON documents
- Great for counters, points, scores, etc.

---

### 4. **Filter inside arrays**
We only want contacts where `type` is `"email"`:
```python
email_contacts = r.json().get('user:1002', '$.user.contacts[?(@.type=="email")]')
```
- The `[?(@.type=="email")]` is a JSONPath filter
- Perfect for querying specific objects inside arrays without scanning them in your app

---

### 5. **Update a specific field**
We change the city from `"New York"` to `"San Francisco"`:
```python
r.json().set('user:1002', '$.user.address.city', "San Francisco")
```
- Directly updates only that part of the JSON without rewriting the whole object

---

### 6. **Fetch the entire updated JSON**
Finally, we grab the whole updated document:
```python
updated_json = r.json().get('user:1002', '$')
```
- Useful for debugging or returning the final state to an API client

---

## 🎯 Summary

By the end of this lab, you will:
- Understand how to store, query, update, and increment fields inside JSON documents in Redis
- Use JSONPath to access and filter data
- Know when to fetch partial vs. full documents
- Be able to **visually verify** all changes in Redis Insight

---

## 📚 Resources

- [RedisJSON Documentation](https://redis.io/docs/latest/develop/data-types/json/)
- [redis-py JSON API Docs](https://redis-py.readthedocs.io/en/stable/examples/redisjson_examples.html)
- [JSONPath Syntax](https://redis.io/docs/latest/develop/data-types/json/path/)
- [Redis Insight](https://redis.io/insight/)
