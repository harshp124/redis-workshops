# Redis Workshop Lab: Getting Started with Redis Cloud + RedisInsight

Welcome to the Redis Workshop! This lab will walk you through:

- Setting up a **free Redis Cloud database**
- Retrieving connection details
- Connecting it to **RedisInsight**

---

## 🧩 Prerequisites

- A web browser
- Access to https://redis.io/try-free/
- RedisInsight app installed (https://redis.com/redis-enterprise/redis-insight/)

---

## 🚀 Step 1: Sign Up for Redis Cloud

1. Go to 👉 [https://redis.io/try-free/](https://redis.io/try-free/)


2. Sign up with your email.
3. Check your email to activate your account.
4. Once activated, you’ll be taken to the **Create Database** page.

---

## 🏗️ Step 2: Create a Free Redis Database

1. Select the **Free** option.
2. Scroll down to configure:

| Field         | Example Value          | Notes                                     |
|---------------|------------------------|-------------------------------------------|
| Name          | `redis-db`             | Name your Redis database                  |
| Cloud Vendor  | `Amazon Web Services`  | Choose any listed cloud provider          |
| Region        | `us-east-1`            | Pick a region close to your application   |

> 💡 Free plan includes 30MB of Redis memory

3. Click **Create Database**.

You’ll now be taken to your database details page.

---

## 🔍 Step 3: Get Connection Details

From the **Database Details Page**:

### Copy the following:

- **Public endpoint** (e.g., `redis-12345.c6.us-east-1-4.ec2.cloud.redislabs.com:12345`)
- **Username**: `default`
- **Password**:
  1. Scroll to **Security**
  2. Click the copy icon next to **Default user password**

---

## 🧠 Key Configuration Fields

| Field                | Meaning                                           |
|---------------------|---------------------------------------------------|
| **Vendor**           | Cloud provider hosting the database               |
| **Region**           | Geographic location of the Redis instance         |
| **Public Endpoint**  | Hostname + port to connect to Redis               |
| **Redis Version**    | Engine version                                    |
| **Advanced Modules** | Additional Redis capabilities (Search, JSON, etc) |
| **Dataset Size**     | Max memory (e.g., 30MB in free tier)              |
| **Durability**       | AOF/RDB support                                   |
| **Eviction Policy**  | Key eviction behavior on memory limit             |

---

## 🔗 Step 4: Connect Using RedisInsight

1. Open **RedisInsight**
2. Click **+ Add Redis Database**
3. Click **Connection Settings**
4. Fill in the following:

| Field            | Value                          |
|------------------|--------------------------------|
| Database Alias   | `redis-db`                     |
| Host             | `<Paste your public endpoint>` |
| Port             | (auto-filled)                  |
| Username         | `default`                      |
| Password         | `<Paste password copied earlier>` |

5. Click **Test Connection**
   - ✅ Should say: “Connection is successful”
6. Click **Add Redis Database**

---

## 🎉 You're Done!

You should now see your Redis Cloud database listed in RedisInsight!

Happy exploring! 🚀

---

## 🧰 Resources

- [Redis Cloud Docs](https://docs.redis.com/latest/rc/)
- [RedisInsight Download](https://redis.com/redis-enterprise/redis-insight/)
