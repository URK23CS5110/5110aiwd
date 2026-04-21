1 book entry form

HTML-----
<!DOCTYPE html>
<html>
<head>
  <title>Book Entry Form</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h2>Book Entry Form</h2>

    <form id="bookForm">
      <input type="text" id="title" placeholder="Enter Book Title">
      <input type="text" id="author" placeholder="Enter Author Name">
      <button type="submit">Add Book</button>
    </form>

    <input type="text" id="search" placeholder="Search Book by Title">

    <div id="bookList"></div>
  </div>

  <script src="script.js"></script>
</body>
</html>

style.css----
body {
  font-family: Arial;
  background-color: #f2f2f2;
  margin: 0;
  padding: 20px;
} 

.container {
  width: 400px;
  margin: auto;
  background: white;
  padding: 20px;
  border: 1px solid #ccc;
}

h2 {
  text-align: center;
}

input {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  box-sizing: border-box;
}

button {
  margin-top: 10px;
  padding: 10px;
  width: 100%;
  background: blue;
  color: white;
  border: none;
}

.item {
  border: 1px solid #ccc;
  padding: 10px;
  margin-top: 10px;
}

script.js-------
const form = document.getElementById("bookForm");
const bookList = document.getElementById("bookList");
const search = document.getElementById("search");

form.addEventListener("submit", async function(e) {
  e.preventDefault();

  const book = {
    title: document.getElementById("title").value,
    author: document.getElementById("author").value
  };

  if (book.title === "" || book.author === "") {
    alert("Fill all fields");
    return;
  }

  await fetch("http://localhost:3000/addBook", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(book)
  });

  form.reset();
  loadBooks();
});

async function loadBooks() {
  const res = await fetch("http://localhost:3000/books");
  const data = await res.json();

  bookList.innerHTML = "";
  data.forEach(book => {
    bookList.innerHTML += `
      <div class="item">
        <b>Title:</b> ${book.title} <br>
        <b>Author:</b> ${book.author}
      </div>
    `;
  });
}

search.addEventListener("keyup", async function() {
  const res = await fetch("http://localhost:3000/searchBook?title=" + search.value);
  const data = await res.json();

  bookList.innerHTML = "";
  data.forEach(book => {
    bookList.innerHTML += `
      <div class="item">
        <b>Title:</b> ${book.title} <br>
        <b>Author:</b> ${book.author}
      </div>
    `;
  });
});

loadBooks();

-------server.js
const express = require("express");
const mongoose = require("mongoose");
const cors = require("cors");

const app = express();
app.use(cors());
app.use(express.json());

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab");

const bookSchema = new mongoose.Schema({
  title: String,
  author: String
});

const Book = mongoose.model("Book", bookSchema);

app.post("/addBook", async (req, res) => {
  await Book.create(req.body);
  res.send("Book Added");
});

app.get("/books", async (req, res) => {
  const books = await Book.find();
  res.json(books);
});

app.get("/searchBook", async (req, res) => {
  const books = await Book.find({
    title: new RegExp(req.query.title, "i")
  });
  res.json(books);
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});

BLOG SUBMISSION PAGE
HTML
<!DOCTYPE html>
<html>
<head>
  <title>Blog Submission Page</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h2>Blog Submission Page</h2>

    <form id="blogForm">
      <input type="text" id="title" placeholder="Enter Blog Title">
      <input type="text" id="content" placeholder="Enter Blog Content">
      <button type="submit">Add Blog</button>
    </form>

    <div id="blogList"></div>
  </div>

  <script src="script.js"></script>
</body>
</html>
---------STYLE.CSS
body {
  font-family: Arial;
  background-color: #f2f2f2;
  margin: 0;
  padding: 20px;
}

.container {
  width: 400px;
  margin: auto;
  background: white;
  padding: 20px;
  border: 1px solid #ccc;
}

h2 {
  text-align: center;
}

input {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  box-sizing: border-box;
}

button {
  margin-top: 10px;
  padding: 10px;
  width: 100%;
  background: green;
  color: white;
  border: none;
}

.item {
  border: 1px solid #ccc;
  padding: 10px;
  margin-top: 10px;
}
------SCRIPT.JS
const form = document.getElementById("blogForm");
const blogList = document.getElementById("blogList");

form.addEventListener("submit", async function(e) {
  e.preventDefault();

  const blog = {
    title: document.getElementById("title").value,
    content: document.getElementById("content").value
  };

  if (blog.title === "" || blog.content === "") {
    alert("Fill all fields");
    return;
  }

  await fetch("http://localhost:3000/addBlog", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(blog)
  });

  form.reset();
  loadBlogs();
});

async function loadBlogs() {
  const res = await fetch("http://localhost:3000/blogs");
  const data = await res.json();

  blogList.innerHTML = "";
  data.forEach(blog => {
    blogList.innerHTML += `
      <div class="item">
        <b>Title:</b> ${blog.title} <br>
        <b>Content:</b> ${blog.content}
      </div>
    `;
  });
}

loadBlogs();

------SERVER.JS

const express = require("express");
const mongoose = require("mongoose");
const cors = require("cors");

const app = express();
app.use(cors());
app.use(express.json());

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab");

const blogSchema = new mongoose.Schema({
  title: String,
  content: String
});

const Blog = mongoose.model("Blog", blogSchema);

app.post("/addBlog", async (req, res) => {
  await Blog.create(req.body);
  res.send("Blog Added");
});

app.get("/blogs", async (req, res) => {
  const blogs = await Blog.find();
  res.json(blogs);
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});

3 PRODUCT LISTING PAGE WITH CART TOTAL
index.html

<!DOCTYPE html>
<html>
<head>
  <title>Product Listing Page</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h2>Product Listing Page</h2>

    <form id="productForm">
      <input type="text" id="name" placeholder="Enter Product Name">
      <input type="number" id="price" placeholder="Enter Price">
      <button type="submit">Add Product</button>
    </form>

    <h3>Total Cost: Rs. <span id="total">0</span></h3>

    <div id="productList"></div>
  </div>

  <script src="script.js"></script>
</body>
</html>

-------style.css
body {
  font-family: Arial;
  background-color: #f2f2f2;
  margin: 0;
  padding: 20px;
}

.container {
  width: 400px;
  margin: auto;
  background: white;
  padding: 20px;
  border: 1px solid #ccc;
}

h2, h3 {
  text-align: center;
}

input {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  box-sizing: border-box;
}

button {
  margin-top: 10px;
  padding: 10px;
  width: 100%;
  background: orange;
  color: white;
  border: none;
}

.small-btn {
  width: auto;
  padding: 5px 10px;
  margin-top: 10px;
}

.item {
  border: 1px solid #ccc;
  padding: 10px;
  margin-top: 10px;
}

script.js--------
const form = document.getElementById("productForm");
const productList = document.getElementById("productList");
const totalSpan = document.getElementById("total");

let total = 0;

form.addEventListener("submit", async function(e) {
  e.preventDefault();

  const product = {
    name: document.getElementById("name").value,
    price: document.getElementById("price").value
  };

  if (product.name === "" || product.price === "") {
    alert("Fill all fields");
    return;
  }

  await fetch("http://localhost:3000/addProduct", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(product)
  });

  form.reset();
  loadProducts();
});

async function addToCart(price) {
  total = total + Number(price);
  totalSpan.innerText = total;

  await fetch("http://localhost:3000/addCart", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ price: price })
  });
}

async function loadProducts() {
  const res = await fetch("http://localhost:3000/products");
  const data = await res.json();

  productList.innerHTML = "";
  data.forEach(product => {
    productList.innerHTML += `
      <div class="item">
        <b>Name:</b> ${product.name} <br>
        <b>Price:</b> ${product.price} <br>
        <button class="small-btn" onclick="addToCart(${product.price})">Add to Cart</button>
      </div>
    `;
  });
}

loadProducts();

--------------------server.js
const express = require("express");
const mongoose = require("mongoose");
const cors = require("cors");

const app = express();
app.use(cors());
app.use(express.json());

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab");

const productSchema = new mongoose.Schema({
  name: String,
  price: Number
});

const cartSchema = new mongoose.Schema({
  price: Number
});

const Product = mongoose.model("Product", productSchema);
const Cart = mongoose.model("Cart", cartSchema);

app.post("/addProduct", async (req, res) => {
  await Product.create(req.body);
  res.send("Product Added");
});

app.get("/products", async (req, res) => {
  const products = await Product.find();
  res.json(products);
});

app.post("/addCart", async (req, res) => {
  await Cart.create(req.body);
  res.send("Added to Cart");
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});

4 EMPLOYEE REGISTRATION SYSTEM
index.html

<!DOCTYPE html>
<html>
<head>
  <title>Employee Registration</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h2>Employee Registration</h2>

    <form id="empForm">
      <input type="text" id="name" placeholder="Enter Employee Name">
      <input type="text" id="department" placeholder="Enter Department">
      <button type="submit">Add Employee</button>
    </form>

    <div id="empList"></div>
  </div>

  <script src="script.js"></script>
</body>
</html>

----------style.css
body {
  font-family: Arial;
  background-color: #f2f2f2;
  margin: 0;
  padding: 20px;
}

.container {
  width: 400px;
  margin: auto;
  background: white;
  padding: 20px;
  border: 1px solid #ccc;
}

h2 {
  text-align: center;
}

input {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  box-sizing: border-box;
}

button {
  margin-top: 10px;
  padding: 8px;
  background: purple;
  color: white;
  border: none;
}

.item {
  border: 1px solid #ccc;
  padding: 10px;
  margin-top: 10px;
}

------------script.js
const form = document.getElementById("empForm");
const empList = document.getElementById("empList");

form.addEventListener("submit", async function(e) {
  e.preventDefault();

  const emp = {
    name: document.getElementById("name").value,
    department: document.getElementById("department").value
  };

  if (emp.name === "" || emp.department === "") {
    alert("Fill all fields");
    return;
  }

  await fetch("http://localhost:3000/addEmployee", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(emp)
  });

  form.reset();
  loadEmployees();
});

async function loadEmployees() {
  const res = await fetch("http://localhost:3000/employees");
  const data = await res.json();

  empList.innerHTML = "";
  data.forEach(emp => {
    empList.innerHTML += `
      <div class="item">
        <b>Name:</b> ${emp.name} <br>
        <b>Department:</b> ${emp.department} <br><br>
        <button onclick="deleteEmployee('${emp._id}')">Delete</button>
        <button onclick="updateEmployee('${emp._id}')">Update</button>
      </div>
    `;
  });
}

async function deleteEmployee(id) {
  await fetch("http://localhost:3000/deleteEmployee/" + id, {
    method: "DELETE"
  });
  loadEmployees();
}

async function updateEmployee(id) {
  const newName = prompt("Enter new name");
  const newDept = prompt("Enter new department");

  await fetch("http://localhost:3000/updateEmployee/" + id, {
    method: "PUT",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ name: newName, department: newDept })
  });

  loadEmployees();
}

loadEmployees();

----------server.js
const express = require("express");
const mongoose = require("mongoose");
const cors = require("cors");

const app = express();
app.use(cors());
app.use(express.json());

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab");

const employeeSchema = new mongoose.Schema({
  name: String,
  department: String
});

const Employee = mongoose.model("Employee", employeeSchema);

app.post("/addEmployee", async (req, res) => {
  await Employee.create(req.body);
  res.send("Employee Added");
});

app.get("/employees", async (req, res) => {
  const employees = await Employee.find();
  res.json(employees);
});

app.delete("/deleteEmployee/:id", async (req, res) => {
  await Employee.findByIdAndDelete(req.params.id);
  res.send("Employee Deleted");
});

app.put("/updateEmployee/:id", async (req, res) => {
  await Employee.findByIdAndUpdate(req.params.id, req.body);
  res.send("Employee Updated");
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
