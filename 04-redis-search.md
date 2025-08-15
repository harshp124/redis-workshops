# 🚀 Lab 04 – Working with RediSearch

Welcome to this hands-on RediSearch workshop! This lab is designed for developers with **no prior Redis experience**. Just follow the steps, run the code, and learn by doing.

You'll explore how to:

- Connect to Redis Enterprise  
- Create a full-text search index  
- Insert and query documents  
- Use filters (text, numeric, tag, geo)  
- Sort and aggregate data  
- Update and delete documents  

> 🧠 This workshop uses interactive prompts (`Press Enter to continue...`) to guide you step-by-step. It also encourages you to use **RedisInsight** to visualize and validate your data.

---

## 🛠️ Prerequisites

- Python 3.7+
- `redis-py` client with RediSearch support
- Redis Enterprise database (you can use [Redis Cloud](https://redis.com/try-free/) for free)
- [RedisInsight](https://redis.com/redis-enterprise/redis-insight/) installed (optional but recommended)

Install dependencies:

```bash
pip install redis
```

## 📁 Workshop Setup
Clone this repo and run the script:

```bash
python redis-search.py
```

## 🧪 Step-by-Step Walkthrough

## 🔌 Step 0: Connect to Redis
Edit the connection section in the script (`redis-search.py`) to match **your Redis instance details**:

```python
r = redis.Redis(
    host='YOUR_REDIS_HOST',
    port=YOUR_PORT,             
    username='YOUR_USERNAME',   
    password='YOUR_PASSWORD',   
    decode_responses=True
)
```
This connects to your Redis Enterprise instance using credentials. You can find these in your Redis Cloud dashboard.

## 📦 Step 1: Create a Search Index

```python
schema = (
    TextField("title", weight=5.0),
    TextField("body"),
    NumericField("price"),
    TagField("category"),
    GeoField("location")
)
```

- TextField: for full-text search
- NumericField: for filtering by price
- TagField: for filtering by categories
- GeoField: for location-based queries

```python
search = r.ft("idx:demo")
search.dropindex(delete_documents=True)  # Clean slate
search.create_index(schema, definition=IndexDefinition(prefix=["doc:"], index_type=IndexType.HASH))
```
✅ Use RedisInsight to confirm the index creation under the Search Indexes tab.

## 📝 Step 2: Insert Documents

```python
r.hset("doc:1", mapping={...})
```
We insert 4 sample documents with different titles, categories, prices, and locations.
📍 Locations are stored as longitude latitude strings for geo search.

## 🔍 Step 3: Full-Text Search

```python
res = search.search("red")
```
Searches for documents containing the word "red" in any text field.

## 💲 Step 4: Numeric Filtering

```python
query = Query("@price:[1 2]")
```
Finds documents with prices between $1 and $2.

## 🏷️ Step 5: Tag Filtering
```python
query = Query("@category:{vehicle}")
```
Filters documents tagged with vehicle.

## 🌍 Step 6: Geo Search
``` python
GeoFilter("location", -122.431297, 37.773972, 100, unit="km")
```

Finds documents within 100km of San Francisco.
🗺️ Use RedisInsight's geo visualization to confirm results.

## 📊 Step 7: Sort by Price
```python
query = Query("*").sort_by("price", asc=True).paging(0,3)
```
Returns the 3 cheapest items.

## 📈 Step 8: Aggregation
```python
AggregateRequest("*").group_by("@category", reducers.count().alias("count"))
```
Groups documents by category and counts how many are in each.

## ✏️ Step 9: Update a Document
```python
r.hset("doc:1", mapping={"price": 1.75})
```
Updates the price of doc:1.

## 🔁 Step 10: Confirm Update
```python
search.search("apple")
```
Searches for "apple" and shows updated price.

## 🗑️ Step 11: Delete a Document
```python
r.delete("doc:4")
```
Deletes doc:4 from Redis.

## ✅ Step 12: Confirm Deletion
```python
search.search("*")
```
Lists all remaining documents to verify deletion.

## 🎯 Final Notes
- The script uses input("Press Enter to continue...") to make the experience interactive and paced.
- Use RedisInsight throughout the workshop to:
- View inserted documents
- Explore indexes
- Run queries visually
- Validate geo and tag filters






