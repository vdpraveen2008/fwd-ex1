# EX01 Developing a Simple Webserver
## Date:11/11/2026
## REF NO:26018957

## AIM:
To develop a simple webserver to serve html pages and display the list of protocols in TCP/IP Protocol Suite.

## DESIGN STEPS:
### Step 1: 
HTML content creation.
### Step 2:
Design of webserver workflow.

### Step 3:
Implementation using Python code.

### Step 4:
Import the necessary modules.

### Step 5:
Define a custom request handler.

### Step 6:
Start an HTTP server on a specific port.

### Step 7:
Run the Python script to serve web pages.

### Step 8:
Serve the HTML pages.

### Step 9:
Start the server script and check for errors.

### Step 10:
Open a browser and navigate to http://127.0.0.1:8000 (or the assigned port).

## PROGRAM:
~~~
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Internet Control Center</title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@500;700&family=Inter:wght@400;500;700&display=swap');

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    background: #101513;
    color: #e8eee9;
    font-family: Inter, sans-serif;
    padding: 25px;
}

.dashboard {
    max-width: 1200px;
    margin: auto;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 15px;
    border-bottom: 1px solid #3b4840;
    padding-bottom: 20px;
}

.logo {
    font-family: Orbitron, sans-serif;
    font-size: 20px;
    color: #b9ff65;
}

.status {
    font-size: 12px;
    color: #b9ff65;
    letter-spacing: 2px;
}

h1 {
    font-family: Orbitron, sans-serif;
    font-size: clamp(25px, 4vw, 45px);
    margin: 35px 0 10px;
}

.subtitle {
    color: #829087;
    margin-bottom: 35px;
}

.main {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 25px;
}

.panel {
    background: #1a211d;
    border: 1px solid #39473d;
    padding: 25px;
    border-radius: 12px;
}

.panel-title {
    font-size: 12px;
    color: #91a195;
    letter-spacing: 2px;
    margin-bottom: 25px;
}

.layers {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.layer {
    cursor: pointer;
    padding: 18px;
    border: 1px solid #3b4940;
    background: #202923;
    display: grid;
    grid-template-columns: 45px 1fr auto;
    align-items: center;
    gap: 12px;
    transition: .3s;
}

.layer:hover,
.layer.active {
    background: #34442f;
    border-color: #b9ff65;
    transform: translateX(5px);
}

.number {
    font-family: Orbitron, sans-serif;
    font-size: 22px;
    color: #b9ff65;
}

.layer h3 {
    font-size: 15px;
}

.layer small {
    color: #91a195;
    display: block;
    margin-top: 5px;
}

.arrow {
    text-align: center;
    color: #b9ff65;
}

.right {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.visual {
    min-height: 250px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    overflow: hidden;
}

.globe {
    width: 160px;
    height: 160px;
    border: 2px solid #b9ff65;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 65px;
    position: relative;
}

.globe::before {
    content: "";
    position: absolute;
    width: 210px;
    height: 210px;
    border: 1px dashed #64765b;
    border-radius: 50%;
    animation: rotate 12s linear infinite;
}

.globe::after {
    content: "";
    position: absolute;
    width: 230px;
    height: 90px;
    border: 1px solid #64765b;
    border-radius: 50%;
    transform: rotate(-35deg);
}

@keyframes rotate {
    to { transform: rotate(360deg); }
}

.detail h2 {
    color: #b9ff65;
    font-family: Orbitron, sans-serif;
    margin-bottom: 15px;
}

.detail p {
    line-height: 1.8;
    color: #b8c4ba;
}

.info-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-top: 20px;
}

.info-box {
    background: #111713;
    padding: 15px;
    border-left: 3px solid #b9ff65;
}

.info-box small {
    color: #819086;
}

.info-box strong {
    display: block;
    margin-top: 8px;
    font-size: 14px;
}

button {
    background: #b9ff65;
    border: none;
    color: #101513;
    font-weight: bold;
    padding: 15px;
    cursor: pointer;
    border-radius: 5px;
    width: 100%;
    margin-top: 20px;
}

button:hover {
    background: #d4ff9c;
}

.progress {
    height: 6px;
    background: #354138;
    margin-top: 20px;
    overflow: hidden;
}

.bar {
    height: 100%;
    width: 0%;
    background: #b9ff65;
    transition: width .6s;
}

#message {
    margin-top: 15px;
    color: #b9ff65;
    line-height: 1.7;
}

footer {
    margin-top: 30px;
    padding-top: 20px;
    border-top: 1px solid #39473d;
    color: #657269;
    font-size: 12px;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 10px;
}

@media(max-width: 750px) {
    .main {
        grid-template-columns: 1fr;
    }
}
</style>
</head>

<body>

<div class="dashboard">

<header>
    <div class="logo">NETCORE / SYSTEMS</div>
    <div class="status">● NETWORK STATUS: OPERATIONAL</div>
</header>

<h1>INTERNET CONTROL CENTER</h1>
<p class="subtitle">
    TCP/IP Protocol Architecture // Interactive Network Explorer
</p>

<div class="main">

<!-- LEFT SIDE -->
<div class="panel">

    <div class="panel-title">NETWORK PROTOCOL STACK</div>

    <div class="layers">

        <div class="layer active" onclick="selectLayer(0)">
            <div class="number">04</div>
            <div>
                <h3>APPLICATION</h3>
                <small>User services & interfaces</small>
            </div>
            <span>↗</span>
        </div>

        <div class="arrow">↓</div>

        <div class="layer" onclick="selectLayer(1)">
            <div class="number">03</div>
            <div>
                <h3>TRANSPORT</h3>
                <small>Process communication</small>
            </div>
            <span>↗</span>
        </div>

        <div class="arrow">↓</div>

        <div class="layer" onclick="selectLayer(2)">
            <div class="number">02</div>
            <div>
                <h3>INTERNET</h3>
                <small>Routing & addressing</small>
            </div>
            <span>↗</span>
        </div>

        <div class="arrow">↓</div>

        <div class="layer" onclick="selectLayer(3)">
            <div class="number">01</div>
            <div>
                <h3>NETWORK ACCESS</h3>
                <small>Local network transmission</small>
            </div>
            <span>↗</span>
        </div>

    </div>

    <button onclick="startTransmission()">
        INITIATE DATA TRANSMISSION
    </button>

    <div class="progress">
        <div class="bar" id="bar"></div>
    </div>

    <div id="message">
        System ready. Select a layer or initiate transmission.
    </div>

</div>

<!-- RIGHT SIDE -->
<div class="right">

    <div class="panel visual">
        <div class="globe">🌍</div>
    </div>

    <div class="panel detail">

        <div class="panel-title">LAYER ANALYSIS</div>

        <h2 id="layerTitle">APPLICATION LAYER</h2>

        <p id="description">
            The Application Layer provides network services to user
            applications. It enables web browsing, email, file transfer,
            and communication between software applications.
        </p>

        <div class="info-grid">

            <div class="info-box">
                <small>PROTOCOLS</small>
                <strong id="protocol">HTTP, HTTPS, DNS</strong>
            </div>

            <div class="info-box">
                <small>DATA UNIT</small>
                <strong id="unit">Data</strong>
            </div>

            <div class="info-box">
                <small>FUNCTION</small>
                <strong id="function">User services</strong>
            </div>

            <div class="info-box">
                <small>REAL-WORLD EXAMPLE</small>
                <strong id="example">Opening a website</strong>
            </div>

        </div>

    </div>

</div>
</div>

<footer>
    <span>NETCORE NETWORK SYSTEMS</span>
    <span>TCP/IP ARCHITECTURE // V1.0</span>
</footer>

</div>

<script>

const layers = [
{
    title: "APPLICATION LAYER",
    description: "Provides services to applications and allows users to browse websites, send emails, and transfer files.",
    protocol: "HTTP, HTTPS, DNS, SMTP",
    unit: "Data",
    function: "Network services",
    example: "Opening a website"
},
{
    title: "TRANSPORT LAYER",
    description: "Provides communication between applications. TCP provides reliable delivery while UDP provides connectionless transmission.",
    protocol: "TCP, UDP",
    unit: "Segment / Datagram",
    function: "Delivery & port numbers",
    example: "Sending application data"
},
{
    title: "INTERNET LAYER",
    description: "Handles logical addressing and routes packets across interconnected networks toward their destination.",
    protocol: "IPv4, IPv6, ICMP",
    unit: "Packet",
    function: "Routing & IP addressing",
    example: "Finding a remote server"
},
{
    title: "NETWORK ACCESS LAYER",
    description: "Transmits data across the local network using framing, hardware addressing, and network technologies.",
    protocol: "Ethernet, Wi-Fi",
    unit: "Frame",
    function: "Local transmission",
    example: "Sending data through Wi-Fi"
}
];

function selectLayer(index) {

    document.querySelectorAll(".layer").forEach((el, i) => {
        el.classList.toggle("active", i === index);
    });

    const data = layers[index];

    document.getElementById("layerTitle").textContent = data.title;
    document.getElementById("description").textContent = data.description;
    document.getElementById("protocol").textContent = data.protocol;
    document.getElementById("unit").textContent = data.unit;
    document.getElementById("function").textContent = data.function;
    document.getElementById("example").textContent = data.example;
}

let running = false;

async function startTransmission() {

    if (running) return;
    running = true;

    const message = document.getElementById("message");
    const bar = document.getElementById("bar");

    const steps = [
        "Application: Website request created.",
        "Transport: TCP organizes data for delivery.",
        "Internet: IP packet addressing and routing.",
        "Network Access: Frame transmitted over network.",
        "Transmission complete! Data has been sent."
    ];

    bar.style.width = "0%";

    for (let i = 0; i < steps.length; i++) {

        message.textContent = steps[i];

        if (i < 4) selectLayer(i);

        bar.style.width = ((i + 1) / steps.length * 100) + "%";

        await new Promise(resolve => setTimeout(resolve, 1200));
    }

    message.textContent =
        "✓ Transmission simulation completed successfully.";

    running = false;
}

</script>

</body>
</html>
~~~

## OUTPUT:
![alt text](<Screenshot 2026-11-10 085451.png>)
![alt text](<Screenshot 2026-11-10 085417.png>)

## RESULT:
The program for implementing simple webserver is executed successfully.

