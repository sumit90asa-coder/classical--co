<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>RetroForum</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

      <style>
/* ===== GLOBAL RESET ===== */
* {
  box-sizing: border-box;
}

/* ===== BODY ===== */
body {
  margin: 0;
  font-family: "Courier New", monospace;
  background:
    radial-gradient(circle at top, #2b0f38 0%, #0d0613 60%);
  color: #e8e6e3;
  letter-spacing: 0.5px;
}

/* CRT scanline effect */
body::before {
  content: "";
  position: fixed;
  inset: 0;
  background: repeating-linear-gradient(
    to bottom,
    rgba(255,255,255,0.03),
    rgba(255,255,255,0.03) 1px,
    transparent 1px,
    transparent 3px
  );
  pointer-events: none;
  z-index: 9999;
}

/* ===== HEADER ===== */
header {
  background: linear-gradient(90deg, #2d0f3a, #1b0625);
  padding: 18px 24px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 2px solid #f5c542;
  box-shadow: 0 0 20px rgba(245,197,66,0.3);
}

header h1 {
  margin: 0;
  color: #f5c542;
  font-size: 26px;
  text-shadow: 0 0 8px rgba(245,197,66,0.8);
}

/* ===== NAV ===== */
nav a {
  color: #e8e6e3;
  margin-left: 18px;
  text-decoration: none;
  position: relative;
  font-size: 15px;
}

nav a::after {
  content: "";
  position: absolute;
  left: 0;
  bottom: -4px;
  width: 0;
  height: 2px;
  background: #f5c542;
  transition: width 0.3s ease;
}

nav a:hover::after {
  width: 100%;
}

/* ===== CONTAINER ===== */
.container {
  padding: 28px;
  max-width: 900px;
  margin: auto;
}

/* ===== CARDS ===== */
.card {
  background: linear-gradient(145deg, #2b1038, #1b0824);
  padding: 18px;
  margin-bottom: 18px;
  border-radius: 8px;
  border: 1px solid rgba(245,197,66,0.3);
  box-shadow:
    inset 0 0 15px rgba(0,0,0,0.7),
    0 0 15px rgba(245,197,66,0.15);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-2px);
  box-shadow:
    inset 0 0 15px rgba(0,0,0,0.7),
    0 0 25px rgba(245,197,66,0.35);
}

.card a {
  color: #f5c542;
  text-decoration: none;
  font-size: 18px;
  text-shadow: 0 0 5px rgba(245,197,66,0.6);
}

/* ===== INPUTS ===== */
input, textarea {
  width: 100%;
  padding: 10px;
  margin-bottom: 12px;
  background: #07040b;
  color: #e8e6e3;
  border: 1px solid #444;
  border-radius: 4px;
  font-family: inherit;
  box-shadow: inset 0 0 10px rgba(0,0,0,0.8);
}

input:focus, textarea:focus {
  outline: none;
  border-color: #f5c542;
  box-shadow: 0 0 12px rgba(245,197,66,0.6);
}

/* ===== BUTTONS ===== */
button {
  background: linear-gradient(145deg, #f5c542, #c99c2c);
  border: none;
  padding: 10px 18px;
  cursor: pointer;
  font-weight: bold;
  border-radius: 4px;
  color: #1a0b1f;
  box-shadow:
    0 0 12px rgba(245,197,66,0.6),
    inset 0 0 5px rgba(255,255,255,0.3);
  transition: transform 0.15s ease, box-shadow 0.15s ease;
}

button:hover {
  transform: scale(1.05);
  box-shadow:
    0 0 20px rgba(245,197,66,0.9),
    inset 0 0 6px rgba(255,255,255,0.4);
}

/* ===== WARNING ===== */
.warning {
  color: #ff6b6b;
  font-size: 14px;
  margin-bottom: 8px;
  text-shadow: 0 0 6px rgba(255,107,107,0.7);
}

/* ===== HEADINGS ===== */
h2, h3 {
  color: #f5c542;
  text-shadow: 0 0 6px rgba(245,197,66,0.6);
}

/* ===== HIDDEN ===== */
.hidden {
  display: none;
}

/* ===== FOOTER VIBE (OPTIONAL) ===== */
.container::after {
  content: "▲ RetroForum • Classic Communities Reimagined ▲";
  display: block;
  text-align: center;
  margin-top: 40px;
  font-size: 12px;
  opacity: 0.5;
}
</style>

</head>

<body>

<header>
  <h1>RetroForum</h1>
  <nav>
    <a href="#" onclick="showPage('home')">Home</a>
    <a href="#" onclick="showPage('login')">Login</a>
    <a href="#" onclick="showPage('register')">Register</a>
  </nav>
</header>

<!-- HOME -->
<div class="container" id="home">
  <h2>Forum Threads</h2>

  <div class="card">
    <a href="#" onclick="openThread(1)">Welcome to RetroForum</a>
  </div>

  <div class="card">
    <a href="#" onclick="openThread(2)">Why old forums were better</a>
  </div>
</div>

<!-- THREAD -->
<div class="container hidden" id="thread">
  <h2 id="threadTitle"></h2>

  <div class="card">
    <p>This is a classic forum discussion. Long conversations live here.</p>
  </div>

  <h3>Reply</h3>
  <textarea id="replyText" placeholder="Write your reply..."></textarea>
  <div id="toxicWarning" class="warning hidden">⚠ Toxic language detected</div>

  <button onclick="postReply()">Post Reply</button>
  <button onclick="summarizeThread()" style="margin-left:10px;">
    AI Summarize Thread
  </button>

  <div class="card hidden" id="summaryBox">
    <strong>AI Summary:</strong>
    <p>This thread discusses the nostalgia of classic forums and community-driven discussions.</p>
  </div>
</div>

<!-- LOGIN -->
<div class="container hidden" id="login">
  <h2>Login</h2>
  <input placeholder="Email">
  <input type="password" placeholder="Password">
  <button>Login</button>
</div>

<!-- REGISTER -->
<div class="container hidden" id="register">
  <h2>Register</h2>
  <input placeholder="Username">
  <input placeholder="Email">
  <input type="password" placeholder="Password">
  <button>Register</button>
</div>

<script>
  function showPage(page) {
    document.querySelectorAll('.container').forEach(div => {
      div.classList.add('hidden');
    });
    document.getElementById(page).classList.remove('hidden');
  }

  function openThread(id) {
    showPage('thread');
    document.getElementById('threadTitle').innerText =
      id === 1 ? 'Welcome to RetroForum' : 'Why old forums were better';
  }

  function summarizeThread() {
    document.getElementById('summaryBox').classList.remove('hidden');
  }

  function postReply() {
    const text = document.getElementById('replyText').value.toLowerCase();
    const warning = document.getElementById('toxicWarning');

    if (text.includes("hate") || text.includes("stupid")) {
      warning.classList.remove('hidden');
    } else {
      warning.classList.add('hidden');
      alert("Reply posted successfully!");
      document.getElementById('replyText').value = "";
    }
  }
</script>

</body>
</html>
