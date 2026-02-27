<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>rapXploit666 - DDoS & Malware</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --bg-color: #0c0c0c;
            --text-color: #00ff00;
            --warning-color: #ffaa00;
            --error-color: #ff0000;
            --info-color: #00ffff;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            background: #000;
            color: var(--text-color);
            font-family: 'Courier New', monospace;
            overflow: hidden;
            height: 100vh;
            display: flex;
        }
        
        .main-container {
            width: 100%;
            display: grid;
            grid-template-columns: 1fr 1fr;
            grid-gap: 20px;
            padding: 20px;
            height: 100vh;
        }
        
        .panel {
            background: rgba(10, 10, 10, 0.9);
            border: 1px solid var(--info-color);
            border-radius: 5px;
            padding: 20px;
            position: relative;
            overflow: hidden;
            box-shadow: 0 0 15px rgba(0, 255, 255, 0.3);
        }
        
        .panel-title {
            font-size: 1.5em;
            text-align: center;
            margin-bottom: 15px;
            text-transform: uppercase;
            letter-spacing: 3px;
            position: relative;
            z-index: 1;
        }
        
        
        }
        
        .terminal {
            background: #000;
            border: 1px solid #333;
            border-radius: 3px;
            padding: 10px;
            height: calc(100% - 100px);
            overflow-y: auto;
            font-size: 0.9em;
            position: relative;
        }
        
        .terminal-line {
            margin: 3px 0;
            opacity: 0;
            animation: fadeIn 0.5s forwards;
        }
        
        .terminal-line.error { color: var(--error-color); }
        .terminal-line.warning { color: var(--warning-color); }
        .terminal-line.info { color: var(--info-color); }
        .terminal-line.success { color: #00ff00; }
        
        @keyframes fadeIn {
            to { opacity: 1; }
        }
        
        .status-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            background: #1a1a1a;
            margin-top: 10px;
            border-top: 1px solid #333;
        }
        
        .metric {
            text-align: center;
        }
        
        .metric-value {
            font-size: 1.8em;
            font-weight: bold;
            text-shadow: 0 0 5px currentColor;
        }
        
        .metric-label {
            font-size: 0.8em;
            color: #666;
            text-transform: uppercase;
        }
        
        .progress-container {
            width: 100%;
            height: 20px;
            background: #111;
            border: 1px solid #333;
            margin: 10px 0;
            overflow: hidden;
            position: relative;
        }
        
        .progress-bar {
            height: 100%;
            width: 0;
            background: linear-gradient(90deg, var(--info-color), var(--text-color));
            transition: width 0.3s ease;
        }
        
        .button {
            background: var(--error-color);
            color: #000;
            border: none;
            padding: 10px 20px;
            font-family: inherit;
            text-transform: uppercase;
            font-weight: bold;
            cursor: pointer;
            border-radius: 3px;
            transition: all 0.3s;
            margin: 5px;
        }
        
        .button:hover {
            box-shadow: 0 0 15px var(--error-color);
            transform: scale(1.05);
        }
        
        .button:disabled {
            background: #333;
            color: #666;
            cursor: not-allowed;
            transform: none;
        }
        
        .attack-controls {
            display: flex;
            justify-content: center;
            margin: 15px 0;
        }
        
        .lock-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.98);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: all 0.5s ease;
        }
        
        .lock-overlay.active {
            opacity: 1;
            visibility: visible;
        }
        
        .lock-content {
            text-align: center;
            animation: glitch 1s infinite;
        }
        
        @keyframes glitch {
            0% { transform: translate(0); }
            20% { transform: translate(-2px, 2px); }
            40% { transform: translate(-2px, -2px); }
            60% { transform: translate(2px, 2px); }
            80% { transform: translate(2px, -2px); }
            100% { transform: translate(0); }
        }
        
        .lock-icon {
            font-size: 5em;
            color: var(--error-color);
            margin-bottom: 20px;
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        
        .lock-message {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 0 0 10px var(--error-color);
        }
        
        .lock-timer {
            font-size: 1.5em;
            color: var(--info-color);
            margin: 20px 0;
        }
        
        .bot-list {
            display: flex;
            flex-wrap: wrap;
            gap: 5px;
            margin: 10px 0;
        }
        
        .bot-item {
            background: #1a1a1a;
            padding: 5px 10px;
            border-radius: 3px;
            font-size: 0.8em;
            border: 1px solid #333;
            animation: botConnect 0.5s forwards;
        }
        
        @keyframes botConnect {
            from { opacity: 0; transform: scale(0.8); }
            to { opacity: 1; transform: scale(1); }
        }
        
        .encrypted {
            text-decoration: line-through;
            color: var(--error-color);
        }
        
        .device-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin: 10px 0;
        }
        
        .device-item {
            display: flex;
            justify-content: space-between;
            padding: 8px;
            background: #1a1a1a;
            border: 1px solid #333;
            border-radius: 3px;
            align-items: center;
        }
        
        .device-icon {
            margin-right: 10px;
        }
        
        .device-status {
            font-size: 0.8em;
            padding: 3px 8px;
            border-radius: 3px;
        }
        
        .status-online { background: #00ff00; color: #000; }
        .status-compromised { background: var(--error-color); color: #fff; }
        
        @media (max-width: 768px) {
            .main-container {
                grid-template-columns: 1fr;
            }
        }
        
        /* Backdrop flicker effect */
        .flicker {
            animation: flicker 0.1s infinite alternate;
        }
        
        @keyframes flicker {
            0% { opacity: 0.98; }
            100% { opacity: 1; }
        }
    </style>
</head>
<body>
    <div class="main-container">
        <!-- DDoS Panel -->
        <div class="panel">
            <h2 class="panel-title">DDoS Attack</h2>
            <div class="terminal" id="ddosTerminal">
                <!-- DDoS logs will appear here -->
            </div>
            
            <div class="status-bar">
                <div class="metric">
                    <div class="metric-value" id="connections">0</div>
                    <div class="metric-label">Botnets</div>
                </div>
                <div class="metric">
                    <div class="metric-value" id="requests">0</div>
                    <div class="metric-label">Req/sec</div>
                </div>
                <div class="metric">
                    <div class="metric-value" id="bandwidth">0</div>
                    <div class="metric-label">Gbps</div>
                </div>
            </div>
            
            <div class="attack-controls">
                <button class="button" id="startDDoS">Initiate rapXploit666</button>
                <button class="button" id="stopDDoS" disabled>Abort Mission</button>
            </div>
            
            <div class="bot-list" id="botList"></div>
        </div>
        
        <!-- Malware Panel -->
        <div class="panel">
            <h2 class="panel-title">Malware Operations</h2>
            <div class="terminal" id="malwareTerminal">
                <!-- Malware logs will appear here -->
            </div>
            
            <div class="status-bar">
                <div class="metric">
                    <div class="metric-value" id="infected">0</div>
                    <div class="metric-label">Infected</div>
                </div>
                <div class="metric">
                    <div class="metric-value" id="encrypted">0</div>
                    <div class="metric-label">Encrypted</div>
                </div>
                <div class="metric">
                    <div class="metric-value" id="exfiltrated">0</div>
                    <div class="metric-label">Exfiltrated</div>
                </div>
            </div>
            
            <div class="progress-container">
                <div class="progress-bar" id="malwareProgress"></div>
            </div>
            
            <div class="device-list" id="deviceList">
                <!-- Infected devices will appear here -->
            </div>
        </div>
    </div>
    
    <!-- Lock Overlay -->
    <div class="lock-overlay" id="lockOverlay">
        <div class="lock-content">
            <i class="fas fa-lock lock-icon"></i>
            <div class="lock-message">RAPXploit666 BREACHED</div>
            <div class="lock-message">SYSTEM ENCRYPTED</div>
            <div class="lock-timer">DECRYPTION TIME: <span id="decryptTime">99999999999999999</span> HOURS</div>
        </div>
    </div>
    
    <script>
        // DDoS Simulation
        class DDOSimulator {
            constructor() {
                this.terminal = document.getElementById('ddosTerminal');
                this.connectionsEl = document.getElementById('connections');
                this.requestsEl = document.getElementById('requests');
                this.bandwidthEl = document.getElementById('bandwidth');
                this.botList = document.getElementById('botList');
                this.isRunning = false;
                this.bots = [];
                this.requestRate = 0;
                this.bandwidth = 0;
            }
            
            start() {
                this.isRunning = true;
                this.addLog('info', 'Initializing rapXploit666 DDoS module...');
                
                // Start simulating bot connections
                this.botInterval = setInterval(() => {
                    if (this.bots.length < 50) {
                        this.addBot();
                    }
                }, 200);
                
                // Update metrics
                this.metricInterval = setInterval(() => {
                    this.updateMetrics();
                }, 500);
                
                // Random messages
                this.messageInterval = setInterval(() => {
                    if (Math.random() > 0.7) {
                        this.addLog('warning', `WAF detected attack attempting mitigation...`);
                    }
                }, 3000);
            }
            
            stop() {
                this.isRunning = false;
                clearInterval(this.botInterval);
                clearInterval(this.metricInterval);
                clearInterval(this.messageInterval);
                
                this.addLog('success', 'rapXploit666 DDoS module terminated');
            }
            
            addBot() {
                const ip = this.generateIP();
                const bot = { ip, lastRequest: Date.now() };
                this.bots.push(bot);
                
                const botEl = document.createElement('div');
                botEl.className = 'bot-item';
                botEl.textContent = ip;
                this.botList.appendChild(botEl);
                
                this.addLog('success', `Bot connected: ${ip}`);
            }
            
            generateIP() {
                return `${Math.floor(Math.random() * 256)}.${Math.floor(Math.random() * 256)}.${Math.floor(Math.random() * 256)}.${Math.floor(Math.random() * 256)}`;
            }
            
            updateMetrics() {
                if (!this.isRunning) return;
                
                // Simulate request rate
                this.requestRate = Math.floor(Math.random() * 50000) + (this.bots.length * 1000);
                this.bandwidth = (this.requestRate * 0.000001).toFixed(2);
                
                this.connectionsEl.textContent = this.bots.length;
                this.requestsEl.textContent = this.requestRate.toLocaleString();
                this.bandwidthEl.textContent = this.bandwidth;
                
                // Simulate logs
                if (Math.random() > 0.8) {
                    const victim = this.generateIP();
                    this.addLog('info', `Attacking: ${victim} (Port: ${Math.floor(Math.random() * 65535) + 1})`);
                }
            }
            
            addLog(type, message) {
                const line = document.createElement('div');
                line.className = `terminal-line ${type}`;
                line.textContent = `[${new Date().toLocaleTimeString('id-ID')}] ${message}`;
                this.terminal.appendChild(line);
                this.terminal.scrollTop = this.terminal.scrollHeight;
            }
        }
        
        // Malware Simulation
        class MalwareSimulator {
            constructor() {
                this.terminal = document.getElementById('malwareTerminal');
                this.infectedEl = document.getElementById('infected');
                this.encryptedEl = document.getElementById('encrypted');
                this.exfiltratedEl = document.getElementById('exfiltrated');
                this.progressBar = document.getElementById('malwareProgress');
                this.deviceList = document.getElementById('deviceList');
                this.isRunning = false;
                this.targets = [];
                this.infected = 0;
                this.encrypted = 0;
                this.exfiltrated = 0;
                this.decryptTime = 99999999999999999;
            }
            
            start() {
                this.isRunning = true;
                this.addLog('info', 'Starting rapXploit666 malware deployment...');
                
                // Generate targets
                this.generateTargets();
                
                // Start infection process
                this.infectInterval = setInterval(() => {
                    if (this.infected < this.targets.length && this.isRunning) {
                        this.infectTarget();
                    }
                }, 1000);
                
                // Start encryption process
                this.encryptInterval = setInterval(() => {
                    if (this.encrypted < this.infected && this.isRunning) {
                        this.encryptFile();
                    }
                }, 2000);
                
                // Start exfiltration
                this.exfilInterval = setInterval(() => {
                    if (this.exfiltrated < this.encrypted && this.isRunning) {
                        this.exfiltrateData();
                    }
                }, 1500);
                
                // Trigger lock after 70% progress
                this.lockInterval = setInterval(() => {
                    if (this.progressBar.style.width === '70%' || parseFloat(this.progressBar.style.width) >= 70) {
                        this.triggerLock();
                    }
                }, 1000);
            }
            
            generateTargets() {
                const devices = [
                    { name: 'CEO-Laptop', icon: 'fa-laptop', ip: '192.168.1.101' },
                    { name: 'HR-Database', icon: 'fa-database', ip: '192.168.1.102' },
                    { name: 'Finance-Server', icon: 'fa-server', ip: '192.168.1.103' },
                    { name: 'Dev-Workstation', icon: 'fa-desktop', ip: '192.168.1.104' },
                    { name: 'Backup-NAS', icon: 'fa-hdd', ip: '192.168.1.105' },
                    { name: 'Security-Camera', icon: 'fa-video', ip: '192.168.1.106' },
                    { name: 'IoT-Gateway', icon: 'fa-network-wired', ip: '192.168.1.107' },
                    { name: 'Mail-Server', icon: 'fa-envelope', ip: '192.168.1.108' }
                ];
                
                this.targets = devices;
            }
            
            infectTarget() {
                if (this.targets.length === 0) return;
                
                const target = this.targets[this.infected];
                const deviceEl = document.createElement('div');
                deviceEl.className = 'device-item';
                deviceEl.innerHTML = `
                    <div>
                        <i class="fas ${target.icon} device-icon"></i>
                        <span>${target.name}</span>
                    </div>
                    <span class="device-status status-online">Online</span>
                `;
                this.deviceList.appendChild(deviceEl);
                
                this.infected++;
                this.infectedEl.textContent = this.infected;
                this.progressBar.style.width = `${(this.infected / this.targets.length) * 100}%`;
                
                this.addLog('success', `Infected: ${target.name} (${target.ip})`);
            }
            
            encryptFile() {
                const device = this.deviceList.children[this.encrypted];
                if (device) {
                    device.innerHTML = device.innerHTML.replace(/Online/g, 'Compromised');
                    device.querySelector('.device-status').classList.remove('status-online');
                    device.querySelector('.device-status').classList.add('status-compromised');
                    device.querySelector('.device-status').textContent = 'Encrypted';
                    
                    // Cross out device name
                    const nameSpan = device.querySelector('span');
                    nameSpan.classList.add('encrypted');
                }
                
                this.encrypted++;
                this.encryptedEl.textContent = this.encrypted;
                this.addLog('warning', `Encrypted files: ${this.encrypted} devices`);
            }
            
            exfiltrateData() {
                this.exfiltrated++;
                this.exfiltratedEl.textContent = this.exfiltrated;
                
                const device = this.deviceList.children[this.exfiltrated];
                if (device) {
                    device.querySelector('.device-status').textContent = 'Exfiltrated';
                    device.querySelector('.device-status').style.background = 'var(--info-color)';
                    device.querySelector('.device-status').style.color = '#000';
                }
                
                this.addLog('info', `Exfiltrated ${this.exfiltrated}MB of sensitive data`);
            }
            
            triggerLock() {
                clearInterval(this.infectInterval);
                clearInterval(this.encryptInterval);
                clearInterval(this.exfilInterval);
                
                document.getElementById('lockOverlay').classList.add('active');
                this.addLog('error', 'RAPXploit666: SYSTEM LOCKED - DECRYPTION INITIATED');
                
                // Simulate decryption time
                this.updateDecryptTime();
            }
            
            updateDecryptTime() {
                this.decryptInterval = setInterval(() => {
                    if (this.decryptTime > 0) {
                        this.decryptTime -= Math.floor(Math.random() * 1000) + 500;
                        if (this.decryptTime < 0) this.decryptTime = 0;
                        document.getElementById('decryptTime').textContent = this.decryptTime.toLocaleString();
                    } else {
                        clearInterval(this.decryptInterval);
                        document.getElementById('lockOverlay').innerHTML = `
                            <div class="lock-content">
                                <i class="fas fa-check-circle lock-icon" style="color: #00ff00;"></i>
                                <div class="lock-message" style="color: #00ff00;">SYSTEM DECRYPTED</div>
                                <div class="lock-message">RAPXploit666 MISSION COMPLETE</div>
                            </div>
                        `;
                    }
                }, 100);
            }
            
            addLog(type, message) {
                const line = document.createElement('div');
                line.className = `terminal-line ${type}`;
                line.textContent = `[${new Date().toLocaleTimeString('id-ID')}] rapXploit666: ${message}`;
                this.terminal.appendChild(line);
                this.terminal.scrollTop = this.terminal.scrollHeight;
            }
        }
        
        // Initialize simulators
        const ddosSim = new DDOSimulator();
        const malwareSim = new MalwareSimulator();
        
        // Event listeners
        document.getElementById('startDDoS').addEventListener('click', () => {
            ddosSim.start();
            document.getElementById('startDDoS').disabled = true;
            document.getElementById('stopDDoS').disabled = false;
        });
        
        document.getElementById('stopDDoS').addEventListener('click', () => {
            ddosSim.stop();
            document.getElementById('startDDoS').disabled = false;
            document.getElementById('stopDDoS').disabled = true;
        });
        
        // Auto-start malware
        setTimeout(() => {
            malwareSim.start();
            document.body.classList.add('flicker');
        }, 2000);
    </script>
</body>
</html>
