# 🍃 MongoDB & NoSQL Essentials

A comprehensive guide to understanding NoSQL databases, the transition from SQL, and core MongoDB operations.

---

## 📊 The Data Landscape
Data exists in three primary forms:
1. **Structured:** Organized in tables with fixed schemas (SQL).
2. **Unstructured:** Raw data, such as logs or metadata.
3. **Semi-structured:** Flexible formats like **JSON**, **BSON**, and **XML**.

### 🛑 Problems with MySQL (SQL)
* **Predefined Schema:** Every row must have the exact same columns and data types.
* **NULL Hell:** Optional form fields lead to sparse tables filled with `NULL` entries, wasting storage and complicating logic.

---

## 🚀 NoSQL Overview
**NoSQL** stands for "Not Only SQL." These databases are schema-free and don't rely on traditional tables.

### Types of NoSQL Databases
| Type | Examples |
| :--- | :--- |
| **Key-Value Pair** | Redis, DynamoDB, Riak |
| **Column-Oriented** | Cassandra, HBase |
| **Graph-Based** | Neo4j |
| **Document-Oriented** | **MongoDB** |

### 🕒 Database Evolution
* **2000:** Graph Databases
* **2004:** Google BigTable
* **2007:** Amazon Dynamo
* **2008:** Cassandra
* **2009:** NoSQL with MongoDB

---

## 🍃 MongoDB Core Concepts
* **Hierarchy:** Database ➔ Collections ➔ Documents.
* **Documents:** Similar to JSON objects; each can have a varying number of fields.
* **Deployment:** Use **Atlas** for cloud and **Compass** for local GUI management.

### 🛠️ Collection Management
- **Enter Shell:** `mongosh`
- **Create/Switch DB:** `use db_name`
- **Create Collection:** `db.createCollection("collectionName")`
- **Show All Collections:** `show collections`

#### Capped Collections (Fixed Size)
Used for high-speed logging where you only need the most recent data.
* **Create Capped:** `db.createCollection("logs", {capped: true, size: 1000000, max: 5})`
* **Check Status:** `db.students.isCapped()`
* **Logic:** Follows **FIFO** (First-In, First-Out). When the limit is reached, the oldest document is deleted to make room for the new one.

---

## 📝 CRUD Operations

### 1. Create (Insert)
```javascript
// Insert one document
db.students.insertOne({
    name: "John Doe",
    age: 22,
    courses: ["Math", "Physics"]
});

// Insert multiple documents
db.students.insertMany([
    { name: "Jane Smith", age: 20 },
    { name: "Mike Johnson", gpa: 3.8 }
]);

### 2. Read (Fetch)
```javascript
// Fetch all documents
db.collection.find();

// Fetch first match
db.collection.findOne({ name: "John Doe" });

// Projection (Filter fields: 1 to show, 0 to hide)
db.logs.find({ status: "failed" }, { event: 1, _id: 0 });

// Count documents
db.logs.countDocuments();
