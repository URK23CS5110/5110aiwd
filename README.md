


AIWD Lab – Full Code for All 15 Questions (Same Format)
Below, each question is given with the same file structure:

index.html

style.css

script.js

server.js

The CSS is mostly the same for all questions. The JavaScript and Node.js also follow the same pattern as much as possible. At the end of each question, a small note tells you what changed from the common pattern.

Question 1: Student Registration Website

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Student Registration</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Student Registration Website</h2>

        <form id="mainForm">
            <div class="mb-3">
                <label id="label1">Student Name</label>
                <input type="text" id="field1" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label2">Register Number</label>
                <input type="text" id="field2" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label3">Department</label>
                <input type="text" id="field3" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label4">Photo</label>
                <input type="text" id="field4" class="form-control" placeholder="Enter photo name or URL">
            </div>

            <div class="text-center">
                <button type="submit" class="btn btn-primary">Submit</button>
                <button type="button" class="btn btn-success" onclick="loadData()">Load Data</button>
            </div>
        </form>

        <div class="result-box" id="result">Output will appear here</div>
        <div id="listArea" class="mt-3"></div>
    </div>
</div>

<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}

.card-box {
    background: white;
    padding: 15px;
    margin-top: 10px;
    border-radius: 8px;
    box-shadow: 0 0 5px lightgray;
}

button {
    margin: 5px;
}
script.js

const apiUrl = "/api";

document.getElementById("mainForm")?.addEventListener("submit", async function(e) {
    e.preventDefault();

    let field1 = document.getElementById("field1").value;
    let field2 = document.getElementById("field2").value;
    let field3 = document.getElementById("field3").value;
    let field4 = document.getElementById("field4").value;

    if (field1 === "" || field2 === "" || field3 === "" || field4 === "") {
        alert("Please fill all fields");
        return;
    }

    let obj = { field1, field2, field3, field4 };

    let res = await fetch(apiUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(obj)
    });

    let msg = await res.text();
    document.getElementById("result").innerText = msg;
    loadData();
});

async function loadData() {
    let res = await fetch(apiUrl);
    let data = await res.json();

    let out = "";
    data.forEach(item => {
        out += `
        <div class="card-box">
            <p><b>Name:</b> ${item.field1 || ""}</p>
            <p><b>Register No:</b> ${item.field2 || ""}</p>
            <p><b>Department:</b> ${item.field3 || ""}</p>
            <p><b>Photo:</b> ${item.field4 || ""}</p>
        </div>`;
    });

    document.getElementById("listArea").innerHTML = out;
}
server.js

const express = require("express");
const mongoose = require("mongoose");
const path = require("path");

const app = express();

app.use(express.json());
app.use(express.static(path.join(__dirname, "public")));

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab")
    .then(() => console.log("MongoDB Connected"))
    .catch(err => console.log(err));

const DataSchema = new mongoose.Schema({
    field1: String,
    field2: String,
    field3: String,
    field4: String
});

const Data = mongoose.model("Student", DataSchema);

app.post("/api", async (req, res) => {
    try {
        await Data.create(req.body);
        res.send("Student Registered Successfully");
    } catch (err) {
        res.status(500).send("Error while saving data");
    }
});

app.get("/api", async (req, res) => {
    try {
        let data = await Data.find();
        res.json(data);
    } catch (err) {
        res.status(500).send("Error while fetching data");
    }
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Only labels, display names, model name Student, and success message changed.

Question 2: Responsive Event Registration Portal

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Event Registration</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Responsive Event Registration Portal</h2>

        <form id="mainForm">
            <div class="mb-3">
                <label id="label1">Name</label>
                <input type="text" id="field1" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label2">Email</label>
                <input type="email" id="field2" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label3">Event Name</label>
                <input type="text" id="field3" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label4">Phone Number</label>
                <input type="text" id="field4" class="form-control">
            </div>

            <div class="text-center">
                <button type="submit" class="btn btn-primary">Submit</button>
                <button type="button" class="btn btn-success" onclick="loadData()">Load Data</button>
            </div>
        </form>

        <div class="result-box" id="result">Output will appear here</div>
        <div id="listArea" class="mt-3"></div>
    </div>
</div>

<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}

.card-box {
    background: white;
    padding: 15px;
    margin-top: 10px;
    border-radius: 8px;
    box-shadow: 0 0 5px lightgray;
}

button {
    margin: 5px;
}
script.js

const apiUrl = "/api";

document.getElementById("mainForm")?.addEventListener("submit", async function(e) {
    e.preventDefault();

    let field1 = document.getElementById("field1").value;
    let field2 = document.getElementById("field2").value;
    let field3 = document.getElementById("field3").value;
    let field4 = document.getElementById("field4").value;

    if (field1 === "" || field2 === "" || field3 === "") {
        alert("Please fill required fields");
        return;
    }

    let obj = { field1, field2, field3, field4 };

    let res = await fetch(apiUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(obj)
    });

    let msg = await res.text();
    document.getElementById("result").innerText = msg;
    loadData();
});

async function loadData() {
    let res = await fetch(apiUrl);
    let data = await res.json();

    let out = "";
    data.forEach(item => {
        out += `
        <div class="card-box">
            <p><b>Name:</b> ${item.field1 || ""}</p>
            <p><b>Email:</b> ${item.field2 || ""}</p>
            <p><b>Event:</b> ${item.field3 || ""}</p>
            <p><b>Phone:</b> ${item.field4 || ""}</p>
        </div>`;
    });

    document.getElementById("listArea").innerHTML = out;
}
server.js

const express = require("express");
const mongoose = require("mongoose");
const path = require("path");

const app = express();

app.use(express.json());
app.use(express.static(path.join(__dirname, "public")));

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab")
    .then(() => console.log("MongoDB Connected"))
    .catch(err => console.log(err));

const DataSchema = new mongoose.Schema({
    field1: String,
    field2: String,
    field3: String,
    field4: String
});

const Data = mongoose.model("Event", DataSchema);

app.post("/api", async (req, res) => {
    try {
        await Data.create(req.body);
        res.send("Event Registration Successful");
    } catch (err) {
        res.status(500).send("Error while saving data");
    }
});

app.get("/api", async (req, res) => {
    try {
        let data = await Data.find();
        res.json(data);
    } catch (err) {
        res.status(500).send("Error while fetching data");
    }
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Labels changed to event fields, model name Event, display text updated.

Question 3: Quiz Web Application

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Quiz Web Application</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Quiz Web Application</h2>
        <div class="result-box" id="result">Question will appear here</div>
        <div id="listArea" class="mt-3"></div>
        <p><b>Time Left:</b> <span id="timer">10</span></p>
        <p><b>Score:</b> <span id="score">0</span></p>
        <div class="text-center">
            <button type="button" class="btn btn-primary" onclick="startQuiz()">Start Quiz</button>
        </div>
    </div>
</div>
<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}

.card-box {
    background: white;
    padding: 15px;
    margin-top: 10px;
    border-radius: 8px;
    box-shadow: 0 0 5px lightgray;
}

button {
    margin: 5px;
}
script.js

const apiUrl = "/api";

let questions = [
    { field1: "Capital of India?", field2: "Delhi", field3: "Mumbai", field4: "Chennai", answer: "Delhi" },
    { field1: "2 + 2 = ?", field2: "3", field3: "4", field4: "5", answer: "4" }
];

let currentIndex = 0;
let score = 0;
let time = 10;
let timer;

function startQuiz() {
    currentIndex = 0;
    score = 0;
    document.getElementById("score").innerText = score;
    showQuestion();
}

function showQuestion() {
    let q = questions[currentIndex];
    document.getElementById("result").innerHTML = `<b>${q.field1}</b>`;
    document.getElementById("listArea").innerHTML = `
        <button onclick="checkAnswer('${q.field2}')">${q.field2}</button>
        <button onclick="checkAnswer('${q.field3}')">${q.field3}</button>
        <button onclick="checkAnswer('${q.field4}')">${q.field4}</button>
    `;
    startTimer();
}

function startTimer() {
    clearInterval(timer);
    time = 10;
    document.getElementById("timer").innerText = time;

    timer = setInterval(() => {
        time--;
        document.getElementById("timer").innerText = time;
        if (time <= 0) {
            nextQuestion();
        }
    }, 1000);
}

function checkAnswer(ans) {
    if (ans === questions[currentIndex].answer) {
        score++;
        document.getElementById("score").innerText = score;
    }
    nextQuestion();
}

function nextQuestion() {
    clearInterval(timer);
    currentIndex++;

    if (currentIndex < questions.length) {
        showQuestion();
    } else {
        document.getElementById("result").innerText = "Quiz Completed";
        document.getElementById("listArea").innerHTML = "Final Score: " + score;
        saveScore();
    }
}

async function saveScore() {
    let obj = { field1: "Student", field2: score.toString(), field3: "Quiz", field4: "Completed" };

    await fetch(apiUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(obj)
    });
}
server.js

const express = require("express");
const mongoose = require("mongoose");
const path = require("path");

const app = express();

app.use(express.json());
app.use(express.static(path.join(__dirname, "public")));

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab")
    .then(() => console.log("MongoDB Connected"))
    .catch(err => console.log(err));

const DataSchema = new mongoose.Schema({
    field1: String,
    field2: String,
    field3: String,
    field4: String
});

const Data = mongoose.model("QuizScore", DataSchema);

app.post("/api", async (req, res) => {
    try {
        await Data.create(req.body);
        res.send("Quiz Score Saved Successfully");
    } catch (err) {
        res.status(500).send("Error while saving data");
    }
});

app.get("/api", async (req, res) => {
    try {
        let data = await Data.find();
        res.json(data);
    } catch (err) {
        res.status(500).send("Error while fetching data");
    }
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Form replaced by quiz display, timer and score logic added, model name QuizScore.

Question 4: Video Learning Page

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Video Learning Page</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Video Learning Page</h2>
        <video id="videoPlayer" width="100%" controls>
            <source src="sample.mp4" type="video/mp4">
        </video>
        <div class="result-box" id="result">Watch the video</div>
        <div id="listArea" class="mt-3"></div>
        <div class="text-center">
            <button type="button" class="btn btn-primary" onclick="saveProgress()">Save Progress</button>
        </div>
    </div>
</div>
<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}

.card-box {
    background: white;
    padding: 15px;
    margin-top: 10px;
    border-radius: 8px;
    box-shadow: 0 0 5px lightgray;
}

button {
    margin: 5px;
}
script.js

const apiUrl = "/api";
let watchedTime = 0;
let video = document.getElementById("videoPlayer");

video?.addEventListener("timeupdate", function() {
    watchedTime = Math.floor(video.currentTime);
    document.getElementById("result").innerText = "Watched Time: " + watchedTime + " seconds";
});

async function saveProgress() {
    let obj = { field1: "Video 1", field2: watchedTime.toString(), field3: "Progress Saved", field4: "" };

    let res = await fetch(apiUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(obj)
    });

    let msg = await res.text();
    document.getElementById("listArea").innerText = msg;
}
server.js

const express = require("express");
const mongoose = require("mongoose");
const path = require("path");

const app = express();

app.use(express.json());
app.use(express.static(path.join(__dirname, "public")));

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab")
    .then(() => console.log("MongoDB Connected"))
    .catch(err => console.log(err));

const DataSchema = new mongoose.Schema({
    field1: String,
    field2: String,
    field3: String,
    field4: String
});

const Data = mongoose.model("VideoProgress", DataSchema);

app.post("/api", async (req, res) => {
    try {
        await Data.create(req.body);
        res.send("Video Progress Saved");
    } catch (err) {
        res.status(500).send("Error while saving data");
    }
});

app.get("/api", async (req, res) => {
    try {
        let data = await Data.find();
        res.json(data);
    } catch (err) {
        res.status(500).send("Error while fetching data");
    }
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Video element added, timeupdate event added, model name VideoProgress.

Question 5: Product Catalog Page

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Product Catalog</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Product Catalog Page</h2>

        <div class="mb-3">
            <label>Select Category</label>
            <select id="field1" class="form-control" onchange="loadData()">
                <option value="All">All</option>
                <option value="Electronics">Electronics</option>
                <option value="Books">Books</option>
                <option value="Clothes">Clothes</option>
            </select>
        </div>

        <div class="result-box" id="result">Products loaded from server</div>
        <div id="listArea" class="mt-3"></div>
    </div>
</div>
<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}

.card-box {
    background: white;
    padding: 15px;
    margin-top: 10px;
    border-radius: 8px;
    box-shadow: 0 0 5px lightgray;
}

button {
    margin: 5px;
}
script.js

const apiUrl = "/api";

async function loadData() {
    let selectedCategory = document.getElementById("field1").value;
    let res = await fetch(apiUrl);
    let data = await res.json();

    let out = "";
    data.forEach(item => {
        if (selectedCategory === "All" || item.field2 === selectedCategory) {
            out += `
            <div class="card-box">
                <p><b>Product:</b> ${item.field1 || ""}</p>
                <p><b>Category:</b> ${item.field2 || ""}</p>
                <p><b>Price:</b> ${item.field3 || ""}</p>
                <p><b>Description:</b> ${item.field4 || ""}</p>
            </div>`;
        }
    });

    document.getElementById("listArea").innerHTML = out;
}

loadData();
server.js

const express = require("express");
const path = require("path");

const app = express();
app.use(express.static(path.join(__dirname, "public")));

app.get("/api", (req, res) => {
    res.json([
        { field1: "Laptop", field2: "Electronics", field3: "50000", field4: "Good product" },
        { field1: "Java Book", field2: "Books", field3: "500", field4: "Useful for study" },
        { field1: "Shirt", field2: "Clothes", field3: "1200", field4: "Cotton shirt" }
    ]);
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Category filter added in HTML and JS, backend returns static JSON products.

Question 6: Feedback Collection System

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Feedback Collection</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Feedback Collection System</h2>

        <form id="mainForm">
            <div class="mb-3">
                <label id="label1">Student Name</label>
                <input type="text" id="field1" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label2">Department</label>
                <input type="text" id="field2" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label3">Feedback</label>
                <input type="text" id="field3" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label4">Rating</label>
                <input type="text" id="field4" class="form-control">
            </div>

            <div class="text-center">
                <button type="submit" class="btn btn-primary">Submit</button>
                <button type="button" class="btn btn-success" onclick="loadData()">Load Data</button>
            </div>
        </form>

        <div class="result-box" id="result">Output will appear here</div>
        <div id="listArea" class="mt-3"></div>
    </div>
</div>

<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}

.card-box {
    background: white;
    padding: 15px;
    margin-top: 10px;
    border-radius: 8px;
    box-shadow: 0 0 5px lightgray;
}

button {
    margin: 5px;
}
script.js

const apiUrl = "/api";

document.getElementById("mainForm")?.addEventListener("submit", async function(e) {
    e.preventDefault();

    let field1 = document.getElementById("field1").value;
    let field2 = document.getElementById("field2").value;
    let field3 = document.getElementById("field3").value;
    let field4 = document.getElementById("field4").value;

    if (field1 === "" || field2 === "" || field3 === "") {
        alert("Please fill required fields");
        return;
    }

    let obj = { field1, field2, field3, field4 };

    let res = await fetch(apiUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(obj)
    });

    let msg = await res.text();
    document.getElementById("result").innerText = msg;
    loadData();
});

async function loadData() {
    let res = await fetch(apiUrl);
    let data = await res.json();

    let out = "";
    data.forEach(item => {
        out += `
        <div class="card-box">
            <p><b>Name:</b> ${item.field1 || ""}</p>
            <p><b>Department:</b> ${item.field2 || ""}</p>
            <p><b>Feedback:</b> ${item.field3 || ""}</p>
            <p><b>Rating:</b> ${item.field4 || ""}</p>
        </div>`;
    });

    document.getElementById("listArea").innerHTML = out;
}
server.js

const express = require("express");
const mongoose = require("mongoose");
const path = require("path");

const app = express();

app.use(express.json());
app.use(express.static(path.join(__dirname, "public")));

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab")
    .then(() => console.log("MongoDB Connected"))
    .catch(err => console.log(err));

const DataSchema = new mongoose.Schema({
    field1: String,
    field2: String,
    field3: String,
    field4: String
});

const Data = mongoose.model("Feedback", DataSchema);

app.post("/api", async (req, res) => {
    try {
        await Data.create(req.body);
        res.send("Feedback Submitted Successfully");
    } catch (err) {
        res.status(500).send("Error while saving data");
    }
});

app.get("/api", async (req, res) => {
    try {
        let data = await Data.find();
        res.json(data);
    } catch (err) {
        res.status(500).send("Error while fetching data");
    }
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Labels changed to feedback fields, display changed, model name Feedback.

Question 7: Dynamic Quote Generator

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Dynamic Quote Generator</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Dynamic Quote Generator</h2>
        <div class="result-box" id="result">Click button to get quote</div>
        <div class="text-center">
            <button type="button" class="btn btn-primary" onclick="loadData()">Show Quote</button>
        </div>
    </div>
</div>
<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}

button {
    margin: 5px;
}
script.js

const apiUrl = "/api";

async function loadData() {
    let res = await fetch(apiUrl);
    let data = await res.json();
    document.getElementById("result").innerText = data.field1;
}
server.js

const express = require("express");
const path = require("path");

const app = express();
app.use(express.static(path.join(__dirname, "public")));

app.get("/api", (req, res) => {
    let quotes = [
        { field1: "Success comes through hard work." },
        { field1: "Never give up." },
        { field1: "Practice daily." }
    ];
    let random = Math.floor(Math.random() * quotes.length);
    res.json(quotes[random]);
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Form removed, one button added, backend returns one random quote.

Question 8: Responsive Tour Booking Website

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Tour Booking</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Responsive Tour Booking Website</h2>

        <form id="mainForm">
            <div class="mb-3">
                <label id="label1">Customer Name</label>
                <input type="text" id="field1" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label2">Destination Price</label>
                <input type="text" id="field2" class="form-control" onkeyup="calculateTotal()" placeholder="Enter price">
            </div>

            <div class="mb-3">
                <label id="label3">Number of Persons</label>
                <input type="text" id="field3" class="form-control" onkeyup="calculateTotal()">
            </div>

            <div class="mb-3">
                <label id="label4">Total Price</label>
                <input type="text" id="field4" class="form-control" readonly>
            </div>

            <div class="text-center">
                <button type="submit" class="btn btn-primary">Submit</button>
                <button type="button" class="btn btn-success" onclick="loadData()">Load Data</button>
            </div>
        </form>

        <div class="result-box" id="result">Output will appear here</div>
        <div id="listArea" class="mt-3"></div>
    </div>
</div>

<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}

.card-box {
    background: white;
    padding: 15px;
    margin-top: 10px;
    border-radius: 8px;
    box-shadow: 0 0 5px lightgray;
}

button {
    margin: 5px;
}
script.js

const apiUrl = "/api";

function calculateTotal() {
    let price = parseInt(document.getElementById("field2").value) || 0;
    let count = parseInt(document.getElementById("field3").value) || 0;
    document.getElementById("field4").value = price * count;
}

document.getElementById("mainForm")?.addEventListener("submit", async function(e) {
    e.preventDefault();

    let field1 = document.getElementById("field1").value;
    let field2 = document.getElementById("field2").value;
    let field3 = document.getElementById("field3").value;
    let field4 = document.getElementById("field4").value;

    if (field1 === "" || field2 === "" || field3 === "") {
        alert("Please fill required fields");
        return;
    }

    let obj = { field1, field2, field3, field4 };

    let res = await fetch(apiUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(obj)
    });

    let msg = await res.text();
    document.getElementById("result").innerText = msg;
    loadData();
});

async function loadData() {
    let res = await fetch(apiUrl);
    let data = await res.json();

    let out = "";
    data.forEach(item => {
        out += `
        <div class="card-box">
            <p><b>Name:</b> ${item.field1 || ""}</p>
            <p><b>Destination Price:</b> ${item.field2 || ""}</p>
            <p><b>Persons:</b> ${item.field3 || ""}</p>
            <p><b>Total:</b> ${item.field4 || ""}</p>
        </div>`;
    });

    document.getElementById("listArea").innerHTML = out;
}
server.js

const express = require("express");
const mongoose = require("mongoose");
const path = require("path");

const app = express();

app.use(express.json());
app.use(express.static(path.join(__dirname, "public")));

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab")
    .then(() => console.log("MongoDB Connected"))
    .catch(err => console.log(err));

const DataSchema = new mongoose.Schema({
    field1: String,
    field2: String,
    field3: String,
    field4: String
});

const Data = mongoose.model("Tour", DataSchema);

app.post("/api", async (req, res) => {
    try {
        await Data.create(req.body);
        res.send("Tour Booked Successfully");
    } catch (err) {
        res.status(500).send("Error while saving data");
    }
});

app.get("/api", async (req, res) => {
    try {
        let data = await Data.find();
        res.json(data);
    } catch (err) {
        res.status(500).send("Error while fetching data");
    }
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Added calculateTotal() for instant price calculation, model name Tour.

Question 9: Live Match Score Website

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Live Match Score</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Live Match Score Website</h2>
        <div class="result-box" id="result">Loading score...</div>
    </div>
</div>
<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}
script.js

const apiUrl = "/api";

async function loadData() {
    let res = await fetch(apiUrl);
    let data = await res.json();

    document.getElementById("result").innerHTML = `
        <p><b>Match:</b> ${data.field1}</p>
        <p><b>Score:</b> ${data.field2}</p>
        <p><b>Status:</b> ${data.field3}</p>
    `;
}

loadData();
setInterval(loadData, 5000);
server.js

const express = require("express");
const path = require("path");

const app = express();
app.use(express.static(path.join(__dirname, "public")));

app.get("/api", (req, res) => {
    res.json({
        field1: "India vs Australia",
        field2: "180/4",
        field3: "Live",
        field4: ""
    });
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Form removed, setInterval(loadData, 5000) added for auto-refresh live score.

Question 10: Library Book Search

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Library Book Search</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Library Book Search</h2>
        <div class="mb-3">
            <label>Book Name</label>
            <input type="text" id="field1" class="form-control">
        </div>
        <div class="text-center">
            <button type="button" class="btn btn-primary" onclick="searchBook()">Search</button>
        </div>
        <div id="listArea" class="mt-3"></div>
    </div>
</div>
<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.card-box {
    background: white;
    padding: 15px;
    margin-top: 10px;
    border-radius: 8px;
    box-shadow: 0 0 5px lightgray;
}
script.js

const apiUrl = "/api";

async function searchBook() {
    let key = document.getElementById("field1").value;
    let res = await fetch(apiUrl + "?key=" + key);
    let data = await res.json();

    let out = "";
    data.forEach(item => {
        out += `
        <div class="card-box">
            <p><b>Book:</b> ${item.field1}</p>
            <p><b>Author:</b> ${item.field2}</p>
        </div>`;
    });

    document.getElementById("listArea").innerHTML = out;
}
server.js

const express = require("express");
const path = require("path");

const app = express();
app.use(express.static(path.join(__dirname, "public")));

app.get("/api", (req, res) => {
    let books = [
        { field1: "Java Programming", field2: "Balagurusamy" },
        { field1: "Web Technology", field2: "Kogent" },
        { field1: "Node JS", field2: "Author A" }
    ];

    let key = (req.query.key || "").toLowerCase();
    let result = books.filter(book => book.field1.toLowerCase().includes(key));
    res.json(result);
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Search input and searchBook() added, backend filters books using query string.

Question 11: Student Dashboard

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Student Dashboard</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Student Dashboard</h2>
        <div class="result-box" id="result">Loading dashboard...</div>
    </div>
</div>
<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}
script.js

const apiUrl = "/api";

async function loadData() {
    let res = await fetch(apiUrl);
    let data = await res.json();

    document.getElementById("result").innerHTML = `
        <p><b>Name:</b> ${data.field1}</p>
        <p><b>Department:</b> ${data.field2}</p>
        <p><b>Marks:</b> ${data.field3}</p>
        <p><b>Attendance:</b> ${data.field4}</p>
    `;
}

loadData();
server.js

const express = require("express");
const path = require("path");

const app = express();
app.use(express.static(path.join(__dirname, "public")));

app.get("/api", (req, res) => {
    res.json({
        field1: "Arun",
        field2: "CSE",
        field3: "450",
        field4: "92%"
    });
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Form removed, dashboard values loaded once from server.

Question 12: Countdown Timer for Online Exam

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Online Exam</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Countdown Timer for Online Exam</h2>
        <p><b>Time Left:</b> <span id="timer">60</span> seconds</p>

        <form id="mainForm">
            <div class="mb-3">
                <label id="label1">Answer</label>
                <input type="text" id="field1" class="form-control">
            </div>
            <div class="text-center">
                <button type="submit" class="btn btn-primary">Submit</button>
            </div>
        </form>

        <div class="result-box" id="result">Output will appear here</div>
    </div>
</div>
<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}
script.js

const apiUrl = "/api";
let time = 60;

let timer = setInterval(() => {
    time--;
    document.getElementById("timer").innerText = time;

    if (time <= 0) {
        clearInterval(timer);
        document.getElementById("mainForm").requestSubmit();
    }
}, 1000);

document.getElementById("mainForm")?.addEventListener("submit", async function(e) {
    e.preventDefault();

    let field1 = document.getElementById("field1").value;
    let obj = { field1, field2: "", field3: "", field4: "" };

    let res = await fetch(apiUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(obj)
    });

    let msg = await res.text();
    document.getElementById("result").innerText = msg;
});
server.js

const express = require("express");
const mongoose = require("mongoose");
const path = require("path");

const app = express();

app.use(express.json());
app.use(express.static(path.join(__dirname, "public")));

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab")
    .then(() => console.log("MongoDB Connected"))
    .catch(err => console.log(err));

const DataSchema = new mongoose.Schema({
    field1: String,
    field2: String,
    field3: String,
    field4: String
});

const Data = mongoose.model("ExamAnswer", DataSchema);

app.post("/api", async (req, res) => {
    try {
        await Data.create(req.body);
        res.send("Exam Submitted Successfully");
    } catch (err) {
        res.status(500).send("Error while saving data");
    }
});

app.get("/api", async (req, res) => {
    try {
        let data = await Data.find();
        res.json(data);
    } catch (err) {
        res.status(500).send("Error while fetching data");
    }
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Countdown timer added and form auto-submits when time reaches zero.

Question 13: Online Voting System

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Online Voting</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Online Voting System</h2>

        <form id="mainForm">
            <div class="mb-3">
                <label id="label1">Voter Name</label>
                <input type="text" id="field1" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label2">Candidate Name</label>
                <input type="text" id="field2" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label3">Voter ID</label>
                <input type="text" id="field3" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label4">Status</label>
                <input type="text" id="field4" class="form-control" value="Voted">
            </div>

            <div class="text-center">
                <button type="submit" class="btn btn-primary">Submit</button>
                <button type="button" class="btn btn-success" onclick="loadData()">Load Data</button>
            </div>
        </form>

        <div class="result-box" id="result">Output will appear here</div>
        <div id="listArea" class="mt-3"></div>
    </div>
</div>

<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}

.card-box {
    background: white;
    padding: 15px;
    margin-top: 10px;
    border-radius: 8px;
    box-shadow: 0 0 5px lightgray;
}

button {
    margin: 5px;
}
script.js

const apiUrl = "/api";

document.getElementById("mainForm")?.addEventListener("submit", async function(e) {
    e.preventDefault();

    let field1 = document.getElementById("field1").value;
    let field2 = document.getElementById("field2").value;
    let field3 = document.getElementById("field3").value;
    let field4 = document.getElementById("field4").value;

    if (field1 === "" || field2 === "" || field3 === "") {
        alert("Please fill required fields");
        return;
    }

    let obj = { field1, field2, field3, field4 };

    let res = await fetch(apiUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(obj)
    });

    let msg = await res.text();
    document.getElementById("result").innerText = msg;
    loadData();
});

async function loadData() {
    let res = await fetch(apiUrl);
    let data = await res.json();

    let out = "";
    data.forEach(item => {
        out += `
        <div class="card-box">
            <p><b>Voter:</b> ${item.field1 || ""}</p>
            <p><b>Candidate:</b> ${item.field2 || ""}</p>
            <p><b>Voter ID:</b> ${item.field3 || ""}</p>
            <p><b>Status:</b> ${item.field4 || ""}</p>
        </div>`;
    });

    document.getElementById("listArea").innerHTML = out;
}
server.js

const express = require("express");
const mongoose = require("mongoose");
const path = require("path");

const app = express();

app.use(express.json());
app.use(express.static(path.join(__dirname, "public")));

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab")
    .then(() => console.log("MongoDB Connected"))
    .catch(err => console.log(err));

const DataSchema = new mongoose.Schema({
    field1: String,
    field2: String,
    field3: String,
    field4: String
});

const Data = mongoose.model("Vote", DataSchema);

app.post("/api", async (req, res) => {
    try {
        await Data.create(req.body);
        res.send("Vote Submitted Successfully");
    } catch (err) {
        res.status(500).send("Error while saving data");
    }
});

app.get("/api", async (req, res) => {
    try {
        let data = await Data.find();
        res.json(data);
    } catch (err) {
        res.status(500).send("Error while fetching data");
    }
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Labels changed to voting details, model name Vote, success text changed.

Question 14: Movie Website

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Movie Website</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Movie Website</h2>
        <video id="videoPlayer" width="100%" controls>
            <source src="trailer.mp4" type="video/mp4">
        </video>
        <div class="result-box" id="result">Loading movie details...</div>
    </div>
</div>
<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}
script.js

const apiUrl = "/api";

async function loadData() {
    let res = await fetch(apiUrl);
    let data = await res.json();

    document.getElementById("result").innerHTML = `
        <p><b>Movie Name:</b> ${data.field1}</p>
        <p><b>Rating:</b> ${data.field2}</p>
        <p><b>Review:</b> ${data.field3}</p>
    `;
}

loadData();
server.js

const express = require("express");
const path = require("path");

const app = express();
app.use(express.static(path.join(__dirname, "public")));

app.get("/api", (req, res) => {
    res.json({
        field1: "Leo",
        field2: "4.5/5",
        field3: "Action packed movie",
        field4: ""
    });
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Trailer video added, backend returns movie details directly.

Question 15: Real-Time Attendance Marking System

index.html

<!DOCTYPE html>
<html>
<head>
    <title>Attendance System</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
</head>
<body>
<div class="container">
    <div class="main-box">
        <h2 id="pageTitle">Real-Time Attendance Marking System</h2>

        <form id="mainForm">
            <div class="mb-3">
                <label id="label1">Student Name</label>
                <input type="text" id="field1" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label2">Register Number</label>
                <input type="text" id="field2" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label3">Department</label>
                <input type="text" id="field3" class="form-control">
            </div>

            <div class="mb-3">
                <label id="label4">Date</label>
                <input type="text" id="field4" class="form-control">
            </div>

            <div class="text-center">
                <button type="submit" class="btn btn-primary">Submit</button>
                <button type="button" class="btn btn-success" onclick="loadData()">Load Data</button>
            </div>
        </form>

        <div class="result-box" id="result">Output will appear here</div>
        <div id="listArea" class="mt-3"></div>
    </div>
</div>

<script src="script.js"></script>
</body>
</html>
style.css

body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

.main-box {
    max-width: 800px;
    margin: 40px auto;
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 0 10px gray;
}

h2 {
    text-align: center;
    margin-bottom: 20px;
}

.result-box {
    margin-top: 20px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    min-height: 50px;
}

.card-box {
    background: white;
    padding: 15px;
    margin-top: 10px;
    border-radius: 8px;
    box-shadow: 0 0 5px lightgray;
}

button {
    margin: 5px;
}
script.js

const apiUrl = "/api";
document.getElementById("field4").value = new Date().toLocaleDateString();

document.getElementById("mainForm")?.addEventListener("submit", async function(e) {
    e.preventDefault();

    let field1 = document.getElementById("field1").value;
    let field2 = document.getElementById("field2").value;
    let field3 = document.getElementById("field3").value;
    let field4 = document.getElementById("field4").value;

    if (field1 === "" || field2 === "" || field3 === "") {
        alert("Please fill required fields");
        return;
    }

    let obj = { field1, field2, field3, field4 };

    let res = await fetch(apiUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(obj)
    });

    let msg = await res.text();
    document.getElementById("result").innerText = msg;
    loadData();
});

async function loadData() {
    let res = await fetch(apiUrl);
    let data = await res.json();

    let out = "";
    data.forEach(item => {
        out += `
        <div class="card-box">
            <p><b>Name:</b> ${item.field1 || ""}</p>
            <p><b>Register No:</b> ${item.field2 || ""}</p>
            <p><b>Department:</b> ${item.field3 || ""}</p>
            <p><b>Date:</b> ${item.field4 || ""}</p>
        </div>`;
    });

    document.getElementById("listArea").innerHTML = out;
}
server.js

const express = require("express");
const mongoose = require("mongoose");
const path = require("path");

const app = express();

app.use(express.json());
app.use(express.static(path.join(__dirname, "public")));

mongoose.connect("mongodb://127.0.0.1:27017/aiwdlab")
    .then(() => console.log("MongoDB Connected"))
    .catch(err => console.log(err));

const DataSchema = new mongoose.Schema({
    field1: String,
    field2: String,
    field3: String,
    field4: String
});

const Data = mongoose.model("Attendance", DataSchema);

app.post("/api", async (req, res) => {
    try {
        await Data.create(req.body);
        res.send("Attendance Marked Successfully");
    } catch (err) {
        res.status(500).send("Error while saving data");
    }
});

app.get("/api", async (req, res) => {
    try {
        let data = await Data.find();
        res.json(data);
    } catch (err) {
        res.status(500).send("Error while fetching data");
    }
});

app.listen(3000, () => {
    console.log("Server running on http://localhost:3000");
});
Small change from main: Current date is auto-filled, model name Attendance, labels/display changed.

