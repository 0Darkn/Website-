# 🌐 Projeto Bem-Vindo (Flask + Qt + Web)

## 🛠 Tecnologias Utilizadas

* 🐍 **Flask** (Servidor Web)
* 🖥 **PyQt5** (Janela Desktop para controlar o servidor)
* 🌐 **HTML**
* 🎨 **CSS**
* ⚡ **JavaScript**

📌 Página principal: **“Bem-Vindo”**

💻 Compatível com:

* Windows 10
* Ubuntu
* Raspberry Pi

---

# 📁 Estrutura do Projeto

```
projeto_bem_vindo/
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

## 📦 Instalar Dependências

```bash
pip install flask PyQt5
```

## 💻 Código

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

class Janela(QWidget):
    def __init__(self):
        super().__init__()

        self.setWindowTitle("Servidor Flask - Bem Vindo")
        self.setGeometry(200, 200, 300, 200)

        layout = QVBoxLayout()

        self.label = QLabel("Servidor Flask Control")
        layout.addWidget(self.label)

        self.btn_start = QPushButton("Ligar Servidor")
        self.btn_start.clicked.connect(self.iniciar_servidor)
        layout.addWidget(self.btn_start)

        self.btn_browser = QPushButton("Abrir Página Web")
        self.btn_browser.clicked.connect(self.abrir_browser)
        layout.addWidget(self.btn_browser)

        self.btn_exit = QPushButton("Sair")
        self.btn_exit.clicked.connect(self.close)
        layout.addWidget(self.btn_exit)

        self.setLayout(layout)

    def iniciar_servidor(self):
        self.thread = threading.Thread(target=run_flask)
        self.thread.daemon = True
        self.thread.start()
        self.label.setText("Servidor Ligado em http://127.0.0.1:5000")

    def abrir_browser(self):
        QDesktopServices.openUrl(QUrl("http://127.0.0.1:5000"))


# ==============================
# MAIN
# ==============================

if __name__ == "__main__":
    app_qt = QApplication(sys.argv)
    janela = Janela()
    janela.show()
    sys.exit(app_qt.exec_())
```

---

# 🌐 2️⃣ templates/index.html

```html
<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <title>Bem Vindo</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>

    <div class="container">
        <h1 id="titulo">Bem-Vindo 👋</h1>
        <p>Servidor Flask com interface Qt + HTML + CSS + JavaScript</p>

        <button onclick="mostrarMensagem()">Clica Aqui</button>

        <div id="mensagem"></div>
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

#mensagem {
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
function mostrarMensagem() {
    const div = document.getElementById("mensagem");
    div.innerHTML = "🚀 Aplicação Full Stack Python + Qt + Flask!";
}
```

---

# 🚀 Como Executar

## 1️⃣ Criar pastas

Criar as pastas:

```
templates
static
```

## 2️⃣ Colocar cada ficheiro no respetivo local

## 3️⃣ Executar

```bash
python app.py
```

## 4️⃣ Na janela Qt:

* Clicar **Ligar Servidor**
* Clicar **Abrir Página Web**

---

# 🧠 O que este projeto faz

✔ Qt controla o servidor
✔ Flask serve HTML
✔ HTML estrutura a página
✔ CSS cria animações e design
✔ JavaScript adiciona interação

---
