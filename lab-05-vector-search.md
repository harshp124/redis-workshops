# 🚀 Redis Vector Search Workshop

Welcome to this hands-on Redis **Vector Search** workshop!  
This lab will walk you **step-by-step** through building and running a **vector similarity search** app using Redis, Python, and sentence embeddings.  
No prior Redis experience is required — just follow along and run the commands.  

💡 Throughout the lab, the script will **pause and ask you to press Enter**.  
This makes the workshop interactive and ensures you understand each step before moving forward.  

---

## 🧰 Prerequisites

Before you begin, make sure you have:

- **Python 3.8+** installed  
- **pip** (Python package manager)  
- A **Redis Stack / Redis Cloud** instance with RediSearch enabled  
- **Redis Insight** (optional but highly recommended) to visualize data  
  - Download: [https://redis.io/insight/](https://redis.io/insight/)

---

## 📦 Step 1 — Install Dependencies

We’ll need:
- `redis` — Python client for Redis
- `numpy` — numerical computing
- `sentence-transformers` — to generate embeddings for text

Run:

```bash
pip install redis numpy sentence-transformers
```

---

## 🔗 Set Up Redis Connection

Edit the connection variables in the script (`redis-vector-search.py`) with **your Redis instance details**:

```python
host = 'YOUR_REDIS_HOST'
port = YOUR_PORT
username = 'YOUR_USERNAME' 
password = 'YOUR_PASSWORD'
```

Example for Redis Cloud:
- **Host**: Shown as "Public Endpoint" in database details (remove `:port` part)
- **Port**: Number after the colon in "Public Endpoint"
- **Username**: Often `default`
- **Password**: Found under the **Security** tab in database settings

---

## 📄 Step 3 — Run the Script

``` bash
python vector_search_lab.py
```
Follow the on-screen prompts.
Whenever the script pauses, press Enter to move to the next step.

## 🔍 How It Works
	1.	Connect to Redis — Uses Python’s redis library to connect.
	2.	Create Index — FT.CREATE defines a vector field (embedding) and text fields (id, content).
	3.	Generate Embeddings — Uses sentence-transformers to convert text into a 384-dimensional normalized vector.
	4.	Store Data — Each product is stored as a Redis Hash (doc:<id>).
	5.	Search by Similarity — FT.SEARCH with KNN retrieves the most similar vectors using cosine similarity.
	6.	Interactive Pauses — The script waits for Enter between steps so you can follow along.
	7.	Redis Insight Check — You can open Redis Insight and inspect:
	•	Keys: doc:vs1, doc:vs2, …
	•	Field embedding: stored as binary vector


## 🎯 Expected Output

Example search for “wireless headphones” might look like:

``` bash
Found 5 results.
Result 1: content='wireless noise-cancelling headphones', similarity score=0.00000
Result 2: content='smartphone with OLED display', similarity score=0.21954
Result 3: content='LED desk lamp', similarity score=0.35288
...
```

## ✅ You’ve just built a Redis Vector Search app from scratch!
You connected to Redis, created a vector index, inserted embeddings, and ran similarity searches.

