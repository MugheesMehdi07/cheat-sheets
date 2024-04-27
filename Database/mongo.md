# MongoDB Cheat Sheet & Q/A

## MongoDB Cheat Sheet

### 1. Basic Database Operations
- **Show Databases**: `show dbs`
- **Create/Use Database**: `use [db_name]`
- **Show Current Database**: `db`
- **Drop Database**: `db.dropDatabase()`

### 2. Collections
- **Show Collections**: `show collections`
- **Create Collection**: `db.createCollection('[collection_name]')`
- **Drop Collection**: `db.[collection_name].drop()`

### 3. CRUD Operations
- **Create/Insert Document**: `db.[collection_name].insert({key: 'value'})`
- **Read/Find Document**: `db.[collection_name].find({key: 'value'})`
- **Update Document**: `db.[collection_name].update({key: 'value'}, {$set: {key: 'new_value'}})`
- **Delete Document**: `db.[collection_name].remove({key: 'value'})`

### 4. Querying
- **Find One**: `db.[collection_name].findOne()`
- **Query with Condition**: `db.[collection_name].find({age: {$gt: 25}})`
- **Limiting Results**: `db.[collection_name].find().limit(5)`
- **Count Documents**: `db.[collection_name].find({key: 'value'}).count()`

### 5. Indexing
- **Create Index**: `db.[collection_name].createIndex({key: 1})`
- **List Indexes**: `db.[collection_name].getIndexes()`
- **Drop Index**: `db.[collection_name].dropIndex('index_name')`

### 6. Aggregation
- **Aggregate Example**: `db.[collection_name].aggregate([{$group: {_id: '$key', total: {$sum: 1}}}])`

### 7. Replication and Sharding
- **Replica Sets**: Replication for redundancy and high availability.
- **Sharding**: Distributes data across multiple machines.



### Q1: How do you create a unique index in MongoDB?
- **A1:** To create a unique index, use `db.collection.createIndex({field: 1}, {unique: true})`. Example: `db.users.createIndex({email: 1}, {unique: true})`.

### Q2: Write a MongoDB query to find documents where the field `age` is greater than 30.
- **A2:** Use `db.collection.find({age: {$gt: 30}})`. Example: `db.users.find({age: {$gt: 30}})`.

### Q3: How do you update multiple documents in MongoDB?
- **A3:** Use `db.collection.update(query, update, {multi: true})`. Example: `db.users.update({active: false}, {$set: {status: 'inactive'}}, {multi: true})`.

### Q4: How can you delete documents based on a condition?
- **A4:** Use `db.collection.remove(condition)`. Example: `db.orders.remove({status: 'cancelled'})`.

### Q5: Explain how to perform a left outer join in MongoDB.
- **A5:** Use the `$lookup` stage in the aggregation pipeline. Example: `db.orders.aggregate([{$lookup: {from: 'customers', localField: 'customer_id', foreignField: '_id', as: 'customer_details'}}])`.

## MongoDB Interview Questions & Answers

### Q6: What is the role of `_id` in MongoDB?
- **A6:** In MongoDB, `_id` is a special field that acts as a unique identifier for each document in a collection. It is automatically added by MongoDB to each document if not provided. It's commonly of the BSON `ObjectId` type, which is designed to be unique across collections.

### Q7: Explain the concept of 'upsert' in MongoDB.
- **A7:** In MongoDB, 'upsert' refers to an operation that updates documents if they exist, or inserts a new document if they do not. It's a combination of "update" and "insert". The `upsert` option in the `update()` function enables this behavior.

### Q8: How does MongoDB ensure data consistency?
- **A8:** MongoDB ensures data consistency through features like write concern, read concern, and transactions. Write concern specifies how many replica set members must acknowledge a write operation. Read concern defines the consistency and isolation properties of read operations. Transactions in MongoDB, especially multi-document transactions, help in maintaining atomicity.

### Q9: What are some common performance issues in MongoDB and how can they be resolved?
- **A9:** Common performance issues in MongoDB include slow queries, index misses, and replication lag. These can be resolved by optimizing query patterns, ensuring proper indexing, using efficient schema design, monitoring server performance, and scaling the database (sharding or adding replica sets) as needed.

### Q10: Describe the difference between embedding and referencing in MongoDB.
- **A10:** Embedding and referencing are two ways of handling relationships between data in MongoDB. Embedding stores related data in a single document as nested subdocuments, which is fast for read operations but can lead to large documents. Referencing stores relations as references (usually `_id` values) to documents in other collections, which is more normalized but requires additional queries to resolve references.

### Q11: What is the Aggregation Pipeline in MongoDB?
- **A11:** The Aggregation Pipeline in MongoDB is a framework for data aggregation, modeled as a pipeline of stages. Each stage processes the documents as they pass through and transforms them into aggregated results. It's used for complex data processing tasks like filtering, grouping, and calculating aggregates.

### Q12: Explain the role of sharding in MongoDB.
- **A12:** Sharding in MongoDB is the process of distributing data across multiple servers or clusters. It's a method to scale horizontally by splitting large datasets and distributing them across multiple machines, which helps in handling larger data sets and higher throughput operations.

### Q13: How do you handle relationships in MongoDB?
- **A13:** Relationships in MongoDB can be handled either by embedding subdocuments (for one-to-many relationships, where the related data is directly nested inside a document) or by referencing (where a document includes references to another document, typically through the `_id` field).

### Q14: What is a covered query in MongoDB?
- **A14:** A covered query in MongoDB is a query in which all the fields requested in the query (including sort and projection) are in the same index. It's called 'covered' because the query can be satisfied entirely using data from indexes, without having to look up full documents, leading to more efficient query execution.

### Q15: How does MongoDB handle transactional data?
- **A15:** MongoDB handles transactional data using multi-document ACID transactions. Introduced in version 4.0, these transactions allow for multiple read and write operations across multiple documents to be executed atomically. This is crucial for maintaining data integrity in applications requiring consistent state across multiple operations.
