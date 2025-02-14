# MongoDB Fundamentals Assignment

## **Objective**

This assignment demonstrates my understanding of MongoDB by applying key concepts such as CRUD operations, data modeling, aggregation, and indexing.

---

## **Setup MongoDB**

### **Installation**

- Install MongoDB locally from [MongoDB Official Website](https://www.mongodb.com/try/download/community) OR
- Create a free cluster on [MongoDB Atlas](https://www.mongodb.com/atlas/database)

### **Starting the Server**

- If installed locally, start MongoDB:
  ```sh
  mongod
  ```
- Verify installation:
  ```sh
  mongo --version
  ```

---

## **Database and Collection Creation**

### **Create a new database and collection**

```javascript
use library;
db.createCollection("books");
```

---

## **Inserting Data**

### **Insert multiple book records**

```javascript
db.books.insertMany([
  { title: "The Pragmatic Programmer", author: "Andrew Hunt", publishedYear: 1999, genre: "Technology", ISBN: "978-0201616224" },
  { title: "Clean Code", author: "Robert C. Martin", publishedYear: 2008, genre: "Technology", ISBN: "978-0132350884" },
  { title: "The Great Gatsby", author: "F. Scott Fitzgerald", publishedYear: 1925, genre: "Fiction", ISBN: "978-0743273565" },
  { title: "Atomic Habits", author: "James Clear", publishedYear: 2018, genre: "Self-Help", ISBN: "978-0735211292" },
  { title: "1984", author: "George Orwell", publishedYear: 1949, genre: "Dystopian", ISBN: "978-0451524935" }
]);
```

---

## **Retrieving Data**

- **Retrieve all books:**
  ```javascript
  db.books.find().pretty();
  ```
- **Query books by a specific author:**
  ```javascript
  db.books.find({ author: "Robert C. Martin" });
  ```
- **Find books published after 2000:**
  ```javascript
  db.books.find({ publishedYear: { $gt: 2000 } });
  ```

---

## **Updating Data**

- **Update ****`publishedYear`**** for a specific book:**
  ```javascript
  db.books.updateOne({ title: "1984" }, { $set: { publishedYear: 1950 } });
  ```
- **Add a new field ****`rating`**** to all books:**
  ```javascript
  db.books.updateMany({}, { $set: { rating: 5 } });
  ```

---

## **Deleting Data**

- **Delete a book by ISBN:**
  ```javascript
  db.books.deleteOne({ ISBN: "978-0451524935" });
  ```
- **Remove all books of a particular genre:**
  ```javascript
  db.books.deleteMany({ genre: "Dystopian" });
  ```

---

## **Data Modeling for E-Commerce**

### **Collections & Structure**

#### **Users Collection**

```javascript
{
  _id: ObjectId(),
  name: "John Doe",
  email: "john@example.com",
  password: "hashed_password",
  address: "123 Main St, City",
  orders: [ObjectId("order_id")]
}
```

#### **Products Collection**

```javascript
{
  _id: ObjectId(),
  name: "Laptop",
  description: "High-performance laptop",
  price: 1200.99,
  category: "Electronics",
  stock: 50
}
```

#### **Orders Collection**

```javascript
{
  _id: ObjectId(),
  userId: ObjectId("user_id"),
  products: [ { productId: ObjectId("product_id"), quantity: 1 } ],
  total: 1200.99,
  status: "Shipped"
}
```

---

## **Aggregation Pipeline**

- **Find the total number of books per genre:**
  ```javascript
  db.books.aggregate([
    { $group: { _id: "$genre", totalBooks: { $sum: 1 } } }
  ]);
  ```
- **Calculate the average published year:**
  ```javascript
  db.books.aggregate([
    { $group: { _id: null, avgPublishedYear: { $avg: "$publishedYear" } } }
  ]);
  ```
- **Find the top-rated book:**
  ```javascript
  db.books.find().sort({ rating: -1 }).limit(1);
  ```

---

## **Indexing**

- **Create an index on the ****`author`**** field:**
  ```javascript
  db.books.createIndex({ author: 1 });
  ```

### **Benefits of Indexing:**

- **Speeds up queries** by reducing scan time.
- **Optimizes sorting and search performance.**
- **Reduces resource consumption** during data retrieval.

---

## **Testing & Verification**

- Use **MongoDB Compass** or **MongoDB Shell** (`mongosh`) to verify data.
- Ensure queries return expected results.
- Check indexing with:
  ```javascript
  db.books.getIndexes();
  ```

---
