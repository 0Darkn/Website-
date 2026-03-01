# 🌐 Welcome Project (Flask + Qt + Web)

## 🛠 Technologies Used

* 🐍 **Flask** (Web Server)
* 🖥 **PyQt5** (Desktop window to control the server)
* 🌐 **HTML**
* 🎨 **CSS**
* ⚡ **JavaScript**

📌 Main page: **“Welcome”**

💻 Compatible with:

* Windows 10
* Ubuntu
* Raspberry Pi

---

# 📁 Project Structure

```
welcome_project/
│
├── app.py
├── templates/
│     └── index.html
│
└── static/
      ├── style.css
      └── script.js
```

---

# 🐍 1️⃣ app.py (Flask + Qt)

## 📦 Install Dependencies

```bash
pip install flask PyQt5
```

## 💻 Code

```python
import sys
import threading
from flask import Flask, render_template
from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QVBoxLayout, QLabel
from PyQt5.QtCore import QUrl
from PyQt5.QtGui import QDesktopServices

# ==============================
# FLASK
# ==============================

app = Flask(__name__)

@app.route("/")
def home():
    return render_template("index.html")


def run_flask():
    app.run(host="127.0.0.1", port=5000, debug=False)


# ==============================
# QT GUI
# ==============================

class Window(QWidget):
    def __init__(self):
        super().__init__()

        self.setWindowTitle("Flask Server - Welcome")
        self.setGeometry(200, 200, 300, 200)

        layout = QVBoxLayout()

        self.label = QLabel("Flask Server Control")
        layout.addWidget(self.label)

        self.btn_start = QPushButton("Start Server")
        self.btn_start.clicked.connect(self.start_server)
        layout.addWidget(self.btn_start)

        self.btn_browser = QPushButton("Open Web Page")
        self.btn_browser.clicked.connect(self.open_browser)
        layout.addWidget(self.btn_browser)

        self.btn_exit = QPushButton("Exit")
        self.btn_exit.clicked.connect(self.close)
        layout.addWidget(self.btn_exit)

        self.setLayout(layout)

    def start_server(self):
        self.thread = threading.Thread(target=run_flask)
        self.thread.daemon = True
        self.thread.start()
        self.label.setText("Server Running at http://127.0.0.1:5000")

    def open_browser(self):
        QDesktopServices.openUrl(QUrl("http://127.0.0.1:5000"))


# ==============================
# MAIN
# ==============================

if __name__ == "__main__":
    app_qt = QApplication(sys.argv)
    window = Window()
    window.show()
    sys.exit(app_qt.exec_())
```

---

# 🌐 2️⃣ templates/index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Welcome</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>

    <div class="container">
        <h1 id="title">Welcome 👋</h1>
        <p>Flask server with Qt interface + HTML + CSS + JavaScript</p>

        <button onclick="showMessage()">Click Here</button>

        <div id="message"></div>
    </div>

<script src="{{ url_for('static', filename='script.js') }}"></script>
</body>
</html>
```

---

# 🎨 3️⃣ static/style.css

```css
body {
    margin: 0;
    padding: 0;
    background: linear-gradient(135deg, #1e3c72, #2a5298);
    font-family: Arial, sans-serif;
    color: white;
    text-align: center;
}

.container {
    margin-top: 150px;
}

h1 {
    font-size: 50px;
    animation: fadeIn 2s ease-in-out;
}

button {
    padding: 15px 30px;
    font-size: 18px;
    border: none;
    border-radius: 8px;
    background-color: #ff9800;
    color: white;
    cursor: pointer;
    transition: 0.3s;
}

button:hover {
    background-color: #e68900;
    transform: scale(1.1);
}

#message {
    margin-top: 20px;
    font-size: 20px;
}

@keyframes fadeIn {
    from {opacity: 0;}
    to {opacity: 1;}
}
```

---

# ⚡ 4️⃣ static/script.js

```javascript
function showMessage() {
    const div = document.getElementById("message");
    div.innerHTML = "🚀 Full Stack Python + Qt + Flask Application!";
}
```

---

# 🚀 How to Run

## 1️⃣ Create folders

Create the folders:

```
templates
static
```

## 2️⃣ Place each file in its respective location

## 3️⃣ Run the application

```bash
python app.py
```

## 4️⃣ In the Qt window:

* Click **Start Server**
* Click **Open Web Page**

---

# 🧠 What This Project Does

✔ Qt controls the server
✔ Flask serves HTML
✔ HTML structures the page
✔ CSS provides animation and design
✔ JavaScript adds interaction

---
