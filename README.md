

COMMON ANSWER FORMAT FOR ALL 15

For every question, you can write in this order:

HTML5 Structure
CSS3 / Bootstrap Design
JavaScript / jQuery Function
JSON Data Format
Node.js Backend
NoSQL Database
Conclusion / Working
Sample Code
1) Student Registration Website

1. HTML5 Structure

HTML5 is used to create a student registration form with fields like name, register number, department, and photo upload.

<!DOCTYPE html>
<html>
<head>
    <title>Student Registration</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="container">
        <div class="form-box">
            <h2>Student Registration Form</h2>
            <form id="studentForm" enctype="multipart/form-data">
                <div class="mb-3">
                    <label>Student Name</label>
                    <input type="text" id="name" class="form-control" placeholder="Enter student name" required>
                </div>

                <div class="mb-3">
                    <label>Register Number</label>
                    <input type="text" id="regno" class="form-control" placeholder="Enter register number" required>
                </div>

                <div class="mb-3">
                    <label>Department</label>
                    <input type="text" id="dept" class="form-control" placeholder="Enter department" required>
                </div>

                <div class="mb-3">
                    <label>Upload Photo</label>
                    <input type="file" id="photo" class="form-control" required>
                </div>

                <div class="text-center">
                    <button type="submit" class="btn btn-primary">Register Student</button>
                    <button type="reset" class="btn btn-secondary">Clear</button>
                </div>
            </form>

            <div id="msg" class="mt-3 text-success text-center"></div>
        </div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

CSS3 and Bootstrap are used to make the page responsive and attractive.

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
<style>
    body {
        background-color: #f2f2f2;
        font-family: Arial, sans-serif;
    }
    .form-box {
        max-width: 650px;
        margin: 40px auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0px 0px 10px gray;
    }
    h2 {
        text-align: center;
        margin-bottom: 20px;
    }
</style>
3. JavaScript / jQuery Function

JavaScript validates the form and sends data to server.

<script>
document.getElementById("studentForm").addEventListener("submit", async function(e) {
    e.preventDefault();

    let name = document.getElementById("name").value;
    let regno = document.getElementById("regno").value;
    let dept = document.getElementById("dept").value;
    let photo = document.getElementById("photo").files[0];

    if (name === "" || regno === "" || dept === "" || !photo) {
        alert("Please fill all fields");
        return;
    }

    let formData = new FormData();
    formData.append("name", name);
    formData.append("regno", regno);
    formData.append("dept", dept);
    formData.append("photo", photo);

    let res = await fetch("/register", {
        method: "POST",
        body: formData
    });

    let msg = await res.text();
    document.getElementById("msg").innerHTML = msg;
});
</script>
4. JSON Data Format

The student data can be represented in JSON format.

{
  "name": "Ravi",
  "regno": "23CSE101",
  "dept": "CSE",
  "photo": "photo.jpg"
}
5. Node.js Backend

Node.js with Express handles the incoming request.

const express = require("express");
const mongoose = require("mongoose");
const multer = require("multer");
const app = express();

mongoose.connect("mongodb://127.0.0.1:27017/collegeDB");

const Student = mongoose.model("Student", {
    name: String,
    regno: String,
    dept: String,
    photo: String
});

const upload = multer({ dest: "uploads/" });

app.post("/register", upload.single("photo"), async (req, res) => {
    const student = new Student({
        name: req.body.name,
        regno: req.body.regno,
        dept: req.body.dept,
        photo: req.file.filename
    });

    await student.save();
    res.send("Student Registered Successfully");
});

app.listen(3000);
6. NoSQL Database

MongoDB stores the student details as document records.

7. Conclusion / Working

The user fills the form, JavaScript validates the values, Node.js receives the data, and MongoDB stores it successfully.

2) Responsive Event Registration Portal

1. HTML5 Structure

HTML5 form elements are used to create the event registration page.

<!DOCTYPE html>
<html>
<head>
    <title>Event Registration</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="container mt-4">
        <div class="form-box">
            <h2 class="text-center">Event Registration Portal</h2>

            <form id="eventForm">
                <div class="mb-3">
                    <label>User Name</label>
                    <input type="text" id="uname" class="form-control" placeholder="Enter your name" required>
                </div>

                <div class="mb-3">
                    <label>Email Address</label>
                    <input type="email" id="email" class="form-control" placeholder="Enter email" required>
                </div>

                <div class="mb-3">
                    <label>Event Name</label>
                    <input type="text" id="event" class="form-control" placeholder="Enter event name" required>
                </div>

                <div class="mb-3">
                    <label>Phone Number</label>
                    <input type="text" id="phone" class="form-control" placeholder="Enter phone number">
                </div>

                <div class="text-center">
                    <button type="submit" class="btn btn-success">Submit Registration</button>
                </div>
            </form>

            <div id="result" class="mt-4 alert alert-info"></div>
        </div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

Bootstrap layout makes the form responsive for mobile and desktop screens.

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
<style>
    .form-box {
        max-width: 650px;
        margin: auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0 0 10px lightgray;
    }
</style>
3. JavaScript / jQuery Function

jQuery submit event sends data without refreshing the page.

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
$("#eventForm").submit(function(e) {
    e.preventDefault();

    let data = {
        uname: $("#uname").val(),
        email: $("#email").val(),
        event: $("#event").val(),
        phone: $("#phone").val()
    };

    $.ajax({
        url: "/event",
        type: "POST",
        contentType: "application/json",
        data: JSON.stringify(data),
        success: function(response) {
            $("#result").html(response);
        }
    });
});
</script>
4. JSON Data Format

{
  "uname": "Kavi",
  "email": "kavi@gmail.com",
  "event": "Web Development Workshop",
  "phone": "9876543210"
}
5. Node.js Backend

const express = require("express");
const app = express();
app.use(express.json());

app.post("/event", (req, res) => {
    res.send("Registration Successful for " + req.body.event);
});

app.listen(3000);
6. NoSQL Database

The event details can also be stored in MongoDB if permanent storage is needed.

7. Conclusion / Working

The user enters event details, jQuery sends JSON to Node.js, and the confirmation message is shown immediately without page refresh.

3) Quiz Web Application

1. HTML5 Structure

HTML5 is used to display question, options, timer, and score.

<!DOCTYPE html>
<html>
<head>
    <title>Quiz Web Application</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="quiz-box">
        <h2>Online Quiz</h2>

        <div class="question-area">
            <h4 id="question">Question comes here</h4>
        </div>

        <div id="options" class="mb-3"></div>

        <div class="timer-box">
            <p>Time Left: <span id="timer">10</span> seconds</p>
        </div>

        <div class="text-center">
            <button onclick="nextQuestion()">Next Question</button>
        </div>

        <div class="mt-3">
            <h4 id="score"></h4>
        </div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

<style>
    body {
        font-family: Arial;
        background: #f4f4f4;
    }
    .quiz-box {
        max-width: 700px;
        margin: 40px auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0 0 10px gray;
    }
    button {
        padding: 8px 16px;
        margin-top: 5px;
    }
</style>
3. JavaScript / jQuery Function

JavaScript handles timer, DOM updates, and automatic score calculation.

<script>
let questions = [
    { q: "Capital of India?", options: ["Delhi", "Mumbai", "Chennai"], ans: "Delhi" },
    { q: "2 + 2 = ?", options: ["3", "4", "5"], ans: "4" }
];

let index = 0;
let score = 0;
let time = 10;
let timer;

function loadQuestion() {
    document.getElementById("question").innerText = questions[index].q;
    let data = "";

    questions[index].options.forEach(function(opt) {
        data += `<button onclick="checkAnswer('${opt}')">${opt}</button><br><br>`;
    });

    document.getElementById("options").innerHTML = data;
    startTimer();
}

function startTimer() {
    time = 10;
    document.getElementById("timer").innerText = time;
    clearInterval(timer);

    timer = setInterval(() => {
        time--;
        document.getElementById("timer").innerText = time;
        if (time === 0) {
            nextQuestion();
        }
    }, 1000);
}

function checkAnswer(ans) {
    if (ans === questions[index].ans) {
        score++;
    }
    nextQuestion();
}

function nextQuestion() {
    clearInterval(timer);
    index++;

    if (index < questions.length) {
        loadQuestion();
    } else {
        document.getElementById("score").innerText = "Final Score: " + score;
        document.getElementById("question").innerText = "Quiz Completed";
        document.getElementById("options").innerHTML = "";
    }
}

loadQuestion();
</script>
4. JSON Data Format

[
  {
    "q": "Capital of India?",
    "options": ["Delhi", "Mumbai", "Chennai"],
    "ans": "Delhi"
  }
]
5. Node.js Backend

const express = require("express");
const app = express();

app.get("/questions", (req, res) => {
    res.json([
        { q: "Capital of India?", options: ["Delhi", "Mumbai", "Chennai"], ans: "Delhi" }
    ]);
});

app.listen(3000);
6. NoSQL Database

Questions, answers, and user scores can be stored in MongoDB.

7. Conclusion / Working

Questions are loaded one by one, timer runs for each question, score is calculated automatically, and result is shown at the end.

4) Video Learning Page

1. HTML5 Structure

HTML5 video tag is used for playing educational videos.

<!DOCTYPE html>
<html>
<head>
    <title>Video Learning Page</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="video-box">
        <h2>Video Learning Page</h2>

        <video id="videoPlayer" width="100%" controls>
            <source src="lesson.mp4" type="video/mp4">
        </video>

        <div class="mt-3">
            <p>Watched Time: <span id="watchTime">0</span> seconds</p>
            <p>Video Progress: <span id="progressText">Not Saved</span></p>
        </div>

        <div class="text-center">
            <button onclick="saveProgress()">Save Progress</button>
        </div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

<style>
    body {
        background: #f0f0f0;
        font-family: Arial;
    }
    .video-box {
        max-width: 750px;
        margin: 40px auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0 0 8px gray;
    }
</style>
3. JavaScript / jQuery Function

JavaScript tracks time spent and saves progress.

<script>
let video = document.getElementById("videoPlayer");
let watched = 0;

video.addEventListener("timeupdate", function() {
    watched = Math.floor(video.currentTime);
    document.getElementById("watchTime").innerText = watched;
});

async function saveProgress() {
    let data = { watchedTime: watched };

    let res = await fetch("/saveProgress", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    });

    let msg = await res.text();
    document.getElementById("progressText").innerText = msg;
}
</script>
4. JSON Data Format

{
  "watchedTime": 120
}
5. Node.js Backend

const express = require("express");
const app = express();
app.use(express.json());

app.post("/saveProgress", (req, res) => {
    res.send("Progress saved: " + req.body.watchedTime + " seconds");
});

app.listen(3000);
6. NoSQL Database

MongoDB can store watched time and video progress for each student.

7. Conclusion / Working

Students watch video lessons, JavaScript tracks time spent, and Node.js stores the progress on the server.

5) Product Catalog Page

1. HTML5 Structure

HTML layout is used to show products and filter options.

<!DOCTYPE html>
<html>
<head>
    <title>Product Catalog</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="container mt-4">
        <h2 class="text-center">Product Catalog Page</h2>

        <div class="row mb-4">
            <div class="col-md-6 mx-auto">
                <label>Select Category</label>
                <select id="category" class="form-control">
                    <option value="All">All</option>
                    <option value="Electronics">Electronics</option>
                    <option value="Clothing">Clothing</option>
                    <option value="Books">Books</option>
                </select>
            </div>
        </div>

        <div class="row" id="productList"></div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

Bootstrap grid system displays products in rows and columns.

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
<style>
    .card {
        margin-bottom: 20px;
        box-shadow: 0 0 5px gray;
    }
</style>
3. JavaScript / jQuery Function

jQuery loads and filters products dynamically.

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
function loadProducts(cat = "All") {
    $.get("/products", function(data) {
        let output = "";

        data.forEach(function(p) {
            if (cat === "All" || p.category === cat) {
                output += `
                    <div class="col-md-4">
                        <div class="card p-3">
                            <h5>${p.name}</h5>
                            <p>Category: ${p.category}</p>
                            <p>Price: ₹${p.price}</p>
                        </div>
                    </div>
                `;
            }
        });

        $("#productList").html(output);
    });
}

$("#category").change(function() {
    loadProducts($(this).val());
});

loadProducts();
</script>
4. JSON Data Format

[
  { "name": "Laptop", "category": "Electronics", "price": 50000 },
  { "name": "Shirt", "category": "Clothing", "price": 1200 }
]
5. Node.js Backend

const express = require("express");
const app = express();

app.get("/products", (req, res) => {
    res.json([
        { name: "Laptop", category: "Electronics", price: 50000 },
        { name: "Shirt", category: "Clothing", price: 1200 },
        { name: "Book", category: "Books", price: 500 }
    ]);
});

app.listen(3000);
6. NoSQL Database

Product details can be stored in MongoDB collection.

7. Conclusion / Working

Products are loaded from server in JSON format, and users can filter them by category dynamically.

6) Feedback Collection System

1. HTML5 Structure

HTML5 form is used to collect student feedback.

<!DOCTYPE html>
<html>
<head>
    <title>Feedback Form</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="form-box">
        <h2>Student Feedback Form</h2>

        <form id="feedbackForm">
            <div class="mb-3">
                <label>Student Name</label>
                <input type="text" id="name" class="form-control" placeholder="Enter name" required>
            </div>

            <div class="mb-3">
                <label>Department</label>
                <input type="text" id="dept" class="form-control" placeholder="Enter department" required>
            </div>

            <div class="mb-3">
                <label>Feedback Message</label>
                <textarea id="feedback" class="form-control" rows="4" placeholder="Enter feedback" required></textarea>
            </div>

            <div class="mb-3">
                <label>Rating</label>
                <select id="rating" class="form-control">
                    <option>Excellent</option>
                    <option>Good</option>
                    <option>Average</option>
                </select>
            </div>

            <button type="submit" class="btn btn-primary">Submit Feedback</button>
        </form>

        <div id="msg" class="mt-3"></div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

CSS and Bootstrap improve appearance and responsiveness.

<style>
    .form-box {
        max-width: 650px;
        margin: 40px auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0 0 10px lightgray;
    }
</style>
3. JavaScript / jQuery Function

JavaScript validates and sends feedback data.

<script>
document.getElementById("feedbackForm").addEventListener("submit", async function(e) {
    e.preventDefault();

    let data = {
        name: document.getElementById("name").value,
        dept: document.getElementById("dept").value,
        feedback: document.getElementById("feedback").value,
        rating: document.getElementById("rating").value
    };

    if (data.name === "" || data.dept === "" || data.feedback === "") {
        alert("Please fill all fields");
        return;
    }

    let res = await fetch("/feedback", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    });

    let msg = await res.text();
    document.getElementById("msg").innerHTML = msg;
});
</script>
4. JSON Data Format

{
  "name": "Arun",
  "dept": "IT",
  "feedback": "The portal is very useful",
  "rating": "Excellent"
}
5. Node.js Backend

const express = require("express");
const mongoose = require("mongoose");
const app = express();

app.use(express.json());
mongoose.connect("mongodb://127.0.0.1:27017/collegeDB");

const Feedback = mongoose.model("Feedback", {
    name: String,
    dept: String,
    feedback: String,
    rating: String
});

app.post("/feedback", async (req, res) => {
    await Feedback.create(req.body);
    res.send("Feedback Submitted Successfully");
});

app.listen(3000);
6. NoSQL Database

MongoDB stores student feedback as separate documents.

7. Conclusion / Working

Students fill the feedback form, validation is done using JavaScript, and feedback is stored in MongoDB through Node.js.

7) Dynamic Quote Generator

1. HTML5 Structure

HTML is used to create a quote box and a button.

<!DOCTYPE html>
<html>
<head>
    <title>Dynamic Quote Generator</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="quote-box">
        <h2>Motivational Quote Generator</h2>

        <div class="quote-area">
            <p id="quoteText">Click the button to view a quote</p>
        </div>

        <div class="text-center">
            <button id="btnQuote">Show Random Quote</button>
        </div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

<style>
    body {
        background: #f7f7f7;
        font-family: Arial;
    }
    .quote-box {
        max-width: 650px;
        margin: 40px auto;
        background: white;
        padding: 30px;
        text-align: center;
        border-radius: 10px;
        box-shadow: 0 0 8px gray;
    }
    .quote-area {
        margin: 20px 0;
        font-size: 22px;
        color: darkblue;
    }
</style>
3. JavaScript / jQuery Function

jQuery handles button click and gets a random quote from server.

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
$("#btnQuote").click(function() {
    $.get("/quote", function(data) {
        $("#quoteText").text(data.quote);
    });
});
</script>
4. JSON Data Format

{
  "quote": "Success comes through hard work."
}
5. Node.js Backend

const express = require("express");
const app = express();

const quotes = [
    { quote: "Success comes through hard work." },
    { quote: "Never give up." },
    { quote: "Practice makes a man perfect." }
];

app.get("/quote", (req, res) => {
    let random = Math.floor(Math.random() * quotes.length);
    res.json(quotes[random]);
});

app.listen(3000);
6. NoSQL Database

Quotes can also be stored in MongoDB collection if needed.

7. Conclusion / Working

When the user clicks the button, jQuery requests a quote from Node.js server, and the quote is displayed dynamically.

8) Responsive Tour Booking Website

1. HTML5 Structure

HTML form is used to select destination, number of people, and booking options.

<!DOCTYPE html>
<html>
<head>
    <title>Tour Booking</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="booking-box">
        <h2>Tour Booking Website</h2>

        <form id="tourForm">
            <div class="mb-3">
                <label>Customer Name</label>
                <input type="text" id="cname" class="form-control" placeholder="Enter name">
            </div>

            <div class="mb-3">
                <label>Select Destination</label>
                <select id="place" class="form-control">
                    <option value="5000">Ooty - ₹5000</option>
                    <option value="7000">Goa - ₹7000</option>
                    <option value="10000">Kashmir - ₹10000</option>
                </select>
            </div>

            <div class="mb-3">
                <label>Number of Persons</label>
                <input type="number" id="count" class="form-control" value="1">
            </div>

            <div class="text-center">
                <button type="button" onclick="calculateTotal()" class="btn btn-primary">Calculate Total</button>
                <button type="button" onclick="bookTour()" class="btn btn-success">Book Now</button>
            </div>
        </form>

        <h4 class="mt-4">Total Price: ₹<span id="total">0</span></h4>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

Bootstrap responsive layout adjusts the form for all screens.

<style>
    .booking-box {
        max-width: 650px;
        margin: 40px auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0 0 10px lightgray;
    }
</style>
3. JavaScript / jQuery Function

JavaScript calculates total instantly and books the tour.

<script>
function calculateTotal() {
    let price = parseInt(document.getElementById("place").value);
    let count = parseInt(document.getElementById("count").value);
    let total = price * count;
    document.getElementById("total").innerText = total;
}

async function bookTour() {
    let data = {
        cname: document.getElementById("cname").value,
        place: document.getElementById("place").options[document.getElementById("place").selectedIndex].text,
        count: document.getElementById("count").value,
        total: document.getElementById("total").innerText
    };

    let res = await fetch("/bookTour", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    });

    alert(await res.text());
}
</script>
4. JSON Data Format

{
  "cname": "Ravi",
  "place": "Goa",
  "count": 2,
  "total": 14000
}
5. Node.js Backend

const express = require("express");
const app = express();
app.use(express.json());

app.post("/bookTour", (req, res) => {
    res.send("Tour Booked Successfully");
});

app.listen(3000);
6. NoSQL Database

Tour booking details can be stored in MongoDB.

7. Conclusion / Working

Users choose destination and count, JavaScript calculates the total price immediately, and booking data is sent to server.

9) Live Match Score Website

1. HTML5 Structure

HTML displays match details and live score section.

<!DOCTYPE html>
<html>
<head>
    <title>Live Match Score</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="score-box">
        <h2>Live Match Scores</h2>

        <div class="match-card">
            <h4 id="teamNames">Team A vs Team B</h4>
            <p id="scoreText">Score loading...</p>
            <p id="statusText">Status: Live</p>
        </div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

<style>
    .score-box {
        max-width: 700px;
        margin: 40px auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        text-align: center;
        box-shadow: 0 0 10px gray;
    }
</style>
3. JavaScript / jQuery Function

JavaScript timer and jQuery update scores every few seconds.

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
function loadScore() {
    $.get("/score", function(data) {
        $("#teamNames").text(data.match);
        $("#scoreText").text(data.score);
        $("#statusText").text("Status: " + data.status);
    });
}

setInterval(loadScore, 5000);
loadScore();
</script>
4. JSON Data Format

{
  "match": "India vs Australia",
  "score": "India 150/3",
  "status": "Live"
}
5. Node.js Backend

const express = require("express");
const app = express();

app.get("/score", (req, res) => {
    res.json({
        match: "India vs Australia",
        score: "India 150/3",
        status: "Live"
    });
});

app.listen(3000);
6. NoSQL Database

Live score history can be stored in MongoDB if needed.

7. Conclusion / Working

The web page automatically fetches the updated score from Node.js server every few seconds and displays it dynamically.

10) Library Book Search

1. HTML5 Structure

HTML page contains search box and result section.

<!DOCTYPE html>
<html>
<head>
    <title>Library Book Search</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="search-box">
        <h2>Search Books</h2>

        <div class="mb-3">
            <input type="text" id="searchKey" class="form-control" placeholder="Enter book name">
        </div>

        <div class="text-center">
            <button id="searchBtn" class="btn btn-primary">Search</button>
        </div>

        <div id="resultArea" class="mt-4"></div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

<style>
    .search-box {
        max-width: 700px;
        margin: 40px auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0 0 8px gray;
    }
    .book-card {
        padding: 12px;
        border: 1px solid lightgray;
        margin-top: 10px;
        border-radius: 8px;
    }
</style>
3. JavaScript / jQuery Function

jQuery handles search event and displays books dynamically.

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
$("#searchBtn").click(function() {
    let key = $("#searchKey").val();

    $.get("/books?key=" + key, function(data) {
        let output = "";

        data.forEach(function(book) {
            output += `
                <div class="book-card">
                    <h5>${book.title}</h5>
                    <p>Author: ${book.author}</p>
                </div>
            `;
        });

        $("#resultArea").html(output);
    });
});
</script>
4. JSON Data Format

[
  { "title": "Java Programming", "author": "Balagurusamy" }
]
5. Node.js Backend

const express = require("express");
const app = express();

let books = [
    { title: "Java Programming", author: "Balagurusamy" },
    { title: "Web Technology", author: "Kogent" }
];

app.get("/books", (req, res) => {
    let key = req.query.key.toLowerCase();
    let result = books.filter(b => b.title.toLowerCase().includes(key));
    res.json(result);
});

app.listen(3000);
6. NoSQL Database

Book details can be stored and searched from MongoDB database.

7. Conclusion / Working

Users search a book name, request goes to server, and matching books are displayed dynamically.

11) Student Dashboard

1. HTML5 Structure

HTML is used to show student personal details, marks, and attendance.

<!DOCTYPE html>
<html>
<head>
    <title>Student Dashboard</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="dashboard-box">
        <h2>Student Dashboard</h2>

        <div class="student-info">
            <h4>Personal Details</h4>
            <p id="name">Name: </p>
            <p id="dept">Department: </p>
        </div>

        <div class="marks-info">
            <h4>Marks</h4>
            <p id="marks">Marks: </p>
        </div>

        <div class="attendance-info">
            <h4>Attendance</h4>
            <p id="attendance">Attendance: </p>
        </div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

<style>
    .dashboard-box {
        max-width: 700px;
        margin: 40px auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0 0 8px gray;
    }
</style>
3. JavaScript / jQuery Function

JavaScript fetches data and updates DOM.

<script>
async function loadDashboard() {
    let res = await fetch("/dashboard");
    let data = await res.json();

    document.getElementById("name").innerText = "Name: " + data.name;
    document.getElementById("dept").innerText = "Department: " + data.dept;
    document.getElementById("marks").innerText = "Marks: " + data.marks;
    document.getElementById("attendance").innerText = "Attendance: " + data.attendance;
}

loadDashboard();
</script>
4. JSON Data Format

{
  "name": "Arun",
  "dept": "CSE",
  "marks": 450,
  "attendance": "92%"
}
5. Node.js Backend

const express = require("express");
const app = express();

app.get("/dashboard", (req, res) => {
    res.json({
        name: "Arun",
        dept: "CSE",
        marks: 450,
        attendance: "92%"
    });
});

app.listen(3000);
6. NoSQL Database

Student records, marks, and attendance can be stored in MongoDB.

7. Conclusion / Working

After login, the dashboard requests student details from server and displays them dynamically on the page.

12) Countdown Timer for Online Exam

1. HTML5 Structure

HTML form is used to display exam question and answer area.

<!DOCTYPE html>
<html>
<head>
    <title>Online Exam Timer</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="exam-box">
        <h2>Online Exam</h2>

        <p>Time Remaining: <span id="time">60</span> seconds</p>

        <form id="examForm">
            <div class="mb-3">
                <label>Question 1: What is HTML?</label>
                <textarea id="answer1" class="form-control" rows="4"></textarea>
            </div>

            <div class="text-center">
                <button type="submit">Submit Answers</button>
            </div>
        </form>

        <div id="msg" class="mt-3"></div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

<style>
    .exam-box {
        max-width: 700px;
        margin: 40px auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0 0 8px gray;
    }
</style>
3. JavaScript / jQuery Function

JavaScript countdown timer automatically submits answers when time ends.

<script>
let timeLeft = 60;

let timer = setInterval(function() {
    timeLeft--;
    document.getElementById("time").innerText = timeLeft;

    if (timeLeft <= 0) {
        clearInterval(timer);
        submitExam();
    }
}, 1000);

document.getElementById("examForm").addEventListener("submit", function(e) {
    e.preventDefault();
    submitExam();
});

async function submitExam() {
    let data = {
        answer1: document.getElementById("answer1").value
    };

    let res = await fetch("/submitExam", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    });

    document.getElementById("msg").innerText = await res.text();
}
</script>
4. JSON Data Format

{
  "answer1": "HTML is HyperText Markup Language"
}
5. Node.js Backend

const express = require("express");
const app = express();
app.use(express.json());

app.post("/submitExam", (req, res) => {
    res.send("Exam Submitted Successfully");
});

app.listen(3000);
6. NoSQL Database

Exam answers and results can be stored in MongoDB.

7. Conclusion / Working

The timer counts down using JavaScript, and when time ends the answers are automatically sent to the server.

13) Online Voting System

1. HTML5 Structure

HTML form is used to select a candidate and submit vote.

<!DOCTYPE html>
<html>
<head>
    <title>Online Voting</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="vote-box">
        <h2>Online Voting System</h2>

        <form id="voteForm">
            <div class="mb-3">
                <label>Voter Name</label>
                <input type="text" id="voter" class="form-control" placeholder="Enter your name">
            </div>

            <div class="mb-3">
                <label>Select Candidate</label>
                <select id="candidate" class="form-control">
                    <option value="">Select</option>
                    <option value="Candidate A">Candidate A</option>
                    <option value="Candidate B">Candidate B</option>
                    <option value="Candidate C">Candidate C</option>
                </select>
            </div>

            <div class="text-center">
                <button type="submit" class="btn btn-primary">Submit Vote</button>
            </div>
        </form>

        <div id="msg" class="mt-3"></div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

<style>
    .vote-box {
        max-width: 650px;
        margin: 40px auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0 0 10px gray;
    }
</style>
3. JavaScript / jQuery Function

JavaScript validates candidate selection and sends vote data.

<script>
document.getElementById("voteForm").addEventListener("submit", async function(e) {
    e.preventDefault();

    let voter = document.getElementById("voter").value;
    let candidate = document.getElementById("candidate").value;

    if (voter === "" || candidate === "") {
        alert("Please fill all fields");
        return;
    }

    let data = { voter, candidate };

    let res = await fetch("/vote", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    });

    document.getElementById("msg").innerText = await res.text();
});
</script>
4. JSON Data Format

{
  "voter": "Kavi",
  "candidate": "Candidate A"
}
5. Node.js Backend

const express = require("express");
const mongoose = require("mongoose");
const app = express();

app.use(express.json());
mongoose.connect("mongodb://127.0.0.1:27017/voteDB");

const Vote = mongoose.model("Vote", {
    voter: String,
    candidate: String
});

app.post("/vote", async (req, res) => {
    await Vote.create(req.body);
    res.send("Vote Submitted Successfully");
});

app.listen(3000);
6. NoSQL Database

MongoDB securely stores the vote details as documents.

7. Conclusion / Working

The user selects a candidate, validation checks the input, and Node.js stores the vote in MongoDB.

14) Movie Website

1. HTML5 Structure

HTML media and display elements are used for trailer, rating, and review section.

<!DOCTYPE html>
<html>
<head>
    <title>Movie Website</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="movie-box">
        <h2>Movie Details</h2>

        <video id="trailer" width="100%" controls>
            <source src="trailer.mp4" type="video/mp4">
        </video>

        <div class="mt-3">
            <h4 id="movieName">Movie Name</h4>
            <p id="rating">Rating: </p>
            <p id="review">Review: </p>
        </div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

<style>
    .movie-box {
        max-width: 750px;
        margin: 40px auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0 0 10px gray;
    }
</style>
3. JavaScript / jQuery Function

jQuery loads movie details dynamically from server.

<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script>
$(document).ready(function() {
    $.get("/movie", function(data) {
        $("#movieName").text(data.name);
        $("#rating").text("Rating: " + data.rating);
        $("#review").text("Review: " + data.review);
    });
});
</script>
4. JSON Data Format

{
  "name": "Leo",
  "rating": "4.5/5",
  "review": "Action packed movie"
}
5. Node.js Backend

const express = require("express");
const app = express();

app.get("/movie", (req, res) => {
    res.json({
        name: "Leo",
        rating: "4.5/5",
        review: "Action packed movie"
    });
});

app.listen(3000);
6. NoSQL Database

Movie reviews, ratings, and trailer details can be stored in MongoDB.

7. Conclusion / Working

Movie details are loaded from server and shown dynamically using jQuery on the web page.

15) Real-Time Attendance Marking System

1. HTML5 Structure

HTML interface is used to mark attendance with a button.

<!DOCTYPE html>
<html>
<head>
    <title>Attendance Marking</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <div class="attendance-box">
        <h2>Real-Time Attendance System</h2>

        <div class="mb-3">
            <label>Student Name</label>
            <input type="text" id="name" class="form-control" placeholder="Enter student name">
        </div>

        <div class="mb-3">
            <label>Register Number</label>
            <input type="text" id="regno" class="form-control" placeholder="Enter register number">
        </div>

        <div class="text-center">
            <button id="markBtn" class="btn btn-success">Mark Attendance</button>
        </div>

        <div id="msg" class="mt-4 alert alert-info"></div>
    </div>
</body>
</html>
2. CSS3 / Bootstrap Design

<style>
    .attendance-box {
        max-width: 650px;
        margin: 40px auto;
        background: white;
        padding: 25px;
        border-radius: 10px;
        box-shadow: 0 0 10px lightgray;
    }
</style>
3. JavaScript / jQuery Function

JavaScript or jQuery handles click event and gives immediate confirmation.

<script>
document.getElementById("markBtn").addEventListener("click", async function() {
    let data = {
        name: document.getElementById("name").value,
        regno: document.getElementById("regno").value
    };

    if (data.name === "" || data.regno === "") {
        alert("Please enter all details");
        return;
    }

    let res = await fetch("/attendance", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
    });

    document.getElementById("msg").innerText = await res.text();
});
</script>
4. JSON Data Format

{
  "name": "Arun",
  "regno": "23IT101"
}
5. Node.js Backend

const express = require("express");
const mongoose = require("mongoose");
const app = express();

app.use(express.json());
mongoose.connect("mongodb://127.0.0.1:27017/attendanceDB");

const Attendance = mongoose.model("Attendance", {
    name: String,
    regno: String,
    date: String
});

app.post("/attendance", async (req, res) => {
    await Attendance.create({
        name: req.body.name,
        regno: req.body.regno,
        date: new Date().toLocaleDateString()
    });
    res.send("Attendance Marked Successfully");
});

app.listen(3000);
6. NoSQL Database

MongoDB stores attendance records for each student.

7. Conclusion / Working

Students click the attendance button, the request is sent to Node.js, and confirmation is shown immediately on the same page.
