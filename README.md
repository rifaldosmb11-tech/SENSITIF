<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Phoenix Credential Vault - Cosmic Edition</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --bg-color: #030308;
            --card-bg: rgba(14, 14, 24, 0.72);
            --accent-orange: #ff4b2b;
            --accent-yellow: #ffb703;
            --accent-cyan: #00f2fe;
            --accent-purple: #7928ca;
            --text-main: #f1f1f5;
            --text-muted: #9a9ab0;
            --danger: #ef233c;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow-x: hidden;
            position: relative;
        }

        /* --- ADVANCED COSMIC & PLANET BACKGROUND --- */
        .cosmic-background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            overflow: hidden;
            pointer-events: none;
        }

        /* NEBULA GLOWS */
        .nebula {
            position: absolute;
            border-radius: 50%;
            filter: blur(100px);
            opacity: 0.4;
            animation: floatNebula 25s infinite alternate ease-in-out;
        }

        .nebula-1 {
            width: 650px;
            height: 650px;
            background: radial-gradient(circle, var(--accent-purple) 0%, rgba(0,0,0,0) 70%);
            top: -15%;
            left: -10%;
        }

        .nebula-2 {
            width: 750px;
            height: 750px;
            background: radial-gradient(circle, #ff007f 0%, rgba(0,0,0,0) 70%);
            bottom: -20%;
            right: -10%;
            animation-delay: -7s;
        }

        .nebula-3 {
            width: 550px;
            height: 550px;
            background: radial-gradient(circle, var(--accent-cyan) 0%, rgba(0,0,0,0) 70%);
            top: 30%;
            left: 45%;
            animation-delay: -12s;
        }

        @keyframes floatNebula {
            0% { transform: translate(0, 0) scale(1); }
            50% { transform: translate(60px, 40px) scale(1.1); }
            100% { transform: translate(-50px, -30px) scale(0.95); }
        }

        /* 3D PLANET WITH ROTATING RINGS & ORBITING MOONS */
        .planet-container {
            position: absolute;
            top: 15%;
            right: 8%;
            width: 320px;
            height: 320px;
            display: flex;
            justify-content: center;
            align-items: center;
            opacity: 0.75;
            transform: rotate(-25deg);
        }

        .planet-body {
            position: absolute;
            width: 140px;
            height: 140px;
            border-radius: 50%;
            background: radial-gradient(circle at 30% 30%, #ff6b4a, #7928ca 60%, #080814 100%);
            box-shadow: inset -15px -15px 40px rgba(0, 0, 0, 0.9),
                        0 0 40px rgba(255, 75, 43, 0.4),
                        0 0 80px rgba(121, 40, 202, 0.2);
            animation: rotatePlanet 40s linear infinite;
        }

        @keyframes rotatePlanet {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* PLANET RINGS */
        .planet-ring {
            position: absolute;
            width: 280px;
            height: 70px;
            border-radius: 50%;
            border: 8px solid rgba(0, 242, 254, 0.35);
            border-top-color: transparent;
            box-shadow: 0 0 20px rgba(0, 242, 254, 0.5), inset 0 0 15px rgba(255, 75, 43, 0.4);
            transform: rotateX(75deg);
            animation: ringGlow 6s ease-in-out infinite alternate;
        }

        .planet-ring-2 {
            position: absolute;
            width: 330px;
            height: 85px;
            border-radius: 50%;
            border: 2px dashed rgba(255, 183, 3, 0.5);
            transform: rotateX(75deg);
        }

        @keyframes ringGlow {
            0% { border-color: rgba(0, 242, 254, 0.35); box-shadow: 0 0 20px rgba(0, 242, 254, 0.5); }
            100% { border-color: rgba(255, 75, 43, 0.6); box-shadow: 0 0 35px rgba(255, 75, 43, 0.8); }
        }

        /* ORBITING PARTICLES AROUND PLANET */
        .orbit-path {
            position: absolute;
            width: 360px;
            height: 360px;
            border-radius: 50%;
            animation: spinOrbit 18s linear infinite;
        }

        .orbit-moon {
            position: absolute;
            top: 0;
            left: 50%;
            width: 14px;
            height: 14px;
            background: #00f2fe;
            border-radius: 50%;
            box-shadow: 0 0 15px #00f2fe, 0 0 25px #00f2fe;
            transform: translate(-50%, -50%);
        }

        .orbit-moon-2 {
            position: absolute;
            bottom: 10%;
            right: 15%;
            width: 10px;
            height: 10px;
            background: #ffb703;
            border-radius: 50%;
            box-shadow: 0 0 12px #ffb703;
        }

        @keyframes spinOrbit {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        #spaceCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
            pointer-events: none;
        }

        .container {
            position: relative;
            z-index: 10;
            width: 100%;
            max-width: 900px;
            padding: 20px;
        }

        /* --- VAULT CARD GLASSMORPHISM --- */
        .vault-card {
            background: var(--card-bg);
            backdrop-filter: blur(25px);
            -webkit-backdrop-filter: blur(25px);
            border: 1px solid rgba(255, 255, 255, 0.12);
            border-radius: 24px;
            padding: 30px;
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.8),
                        inset 0 1px 1px rgba(255, 255, 255, 0.2);
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .title-group {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .title-group i {
            font-size: 1.8rem;
            color: var(--accent-orange);
            filter: drop-shadow(0 0 12px rgba(255, 75, 43, 0.8));
        }

        .title-group h2 {
            font-size: 1.5rem;
            font-weight: 700;
            letter-spacing: 0.5px;
            background: linear-gradient(135deg, #ffffff, #c0c0e0);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .search-box {
            position: relative;
            flex: 1;
            max-width: 300px;
        }

        .search-box input {
            width: 100%;
            padding: 10px 15px 10px 40px;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.12);
            border-radius: 30px;
            color: var(--text-main);
            outline: none;
            transition: all 0.3s;
        }

        .search-box input:focus {
            border-color: var(--accent-orange);
            box-shadow: 0 0 12px rgba(255, 75, 43, 0.4);
            background: rgba(255, 255, 255, 0.08);
        }

        .search-box i {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-muted);
        }

        .add-form {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr auto;
            gap: 12px;
            margin-bottom: 25px;
            background: rgba(0, 0, 0, 0.3);
            padding: 15px;
            border-radius: 14px;
            border: 1px solid rgba(255, 255, 255, 0.06);
        }

        @media (max-width: 768px) {
            .add-form { grid-template-columns: 1fr; }
            .search-box { max-width: 100%; }
            .planet-container { display: none; }
        }

        /* --- INPUT FIELD DENGAN BORDER BERCASAYA WARNA-WARNI --- */
        .form-input {
            padding: 11px 15px;
            background: #0d0d18;
            border: 2px solid transparent;
            border-radius: 10px;
            color: var(--text-main);
            outline: none;
            background-image: linear-gradient(#0d0d18, #0d0d18), linear-gradient(135deg, #ff4b2b, #7928ca, #00f2fe, #ffb703);
            background-origin: border-box;
            background-clip: padding-box, border-box;
            background-size: 200% 200%;
            animation: borderGlowMove 4s linear infinite;
            box-shadow: 0 0 10px rgba(121, 40, 202, 0.25), 0 0 15px rgba(0, 242, 254, 0.15);
            transition: box-shadow 0.3s ease, transform 0.2s;
        }

        .form-input:focus {
            box-shadow: 0 0 15px rgba(255, 75, 43, 0.6), 0 0 25px rgba(0, 242, 254, 0.5);
            transform: translateY(-1px);
        }

        .btn-add {
            background: linear-gradient(135deg, var(--accent-orange), #ff6b4a);
            color: #fff;
            border: none;
            border-radius: 10px;
            padding: 10px 20px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .btn-add:hover {
            box-shadow: 0 0 20px rgba(255, 75, 43, 0.6);
            transform: translateY(-2px);
        }

        /* --- LIST KREDENSIAL --- */
        .credential-list {
            display: flex;
            flex-direction: column;
            gap: 14px;
            max-height: 400px;
            overflow-y: auto;
            padding: 4px;
        }

        .credential-list::-webkit-scrollbar { width: 6px; }
        .credential-list::-webkit-scrollbar-thumb {
            background: rgba(255, 255, 255, 0.2);
            border-radius: 4px;
        }

        /* --- KARTU ITEM KREDENSIAL DENGAN BORDER BERCASAYA WARNA-WARNI --- */
        .credential-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background: #0d0d18;
            border: 2px solid transparent;
            border-radius: 16px;
            padding: 14px 18px;
            gap: 15px;
            background-image: linear-gradient(#0c0c16, #0c0c16), linear-gradient(135deg, #ff4b2b, #7928ca, #00f2fe, #ffb703);
            background-origin: border-box;
            background-clip: padding-box, border-box;
            background-size: 200% 200%;
            animation: borderGlowMove 6s linear infinite;
            box-shadow: 0 0 12px rgba(255, 75, 43, 0.2), 0 0 20px rgba(121, 40, 202, 0.2);
            transition: all 0.3s ease;
        }

        .credential-item:hover {
            transform: translateY(-2px) scale(1.005);
            box-shadow: 0 0 25px rgba(255, 75, 43, 0.5), 0 0 35px rgba(0, 242, 254, 0.4);
        }

        @keyframes borderGlowMove {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .platform-col {
            display: flex;
            align-items: center;
            gap: 16px;
            min-width: 180px;
        }

        /* LINGKARAN MENU */
        .platform-icon-wrapper {
            position: relative;
            width: 48px;
            height: 48px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            background: linear-gradient(135deg, #ff4b2b, #7928ca, #00f2fe);
            background-size: 200% 200%;
            animation: borderGlowMove 4s ease infinite;
            padding: 2px;
            box-shadow: 0 0 15px rgba(255, 75, 43, 0.5), 0 0 30px rgba(121, 40, 202, 0.3);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .platform-icon-inner {
            width: 100%;
            height: 100%;
            background: #0d0d18;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.25rem;
            color: #ffffff;
            transition: background 0.3s ease;
        }

        .credential-item:hover .platform-icon-wrapper {
            transform: scale(1.1) rotate(5deg);
            box-shadow: 0 0 25px rgba(255, 75, 43, 0.8), 0 0 45px rgba(0, 242, 254, 0.6);
        }

        .credential-item:hover .platform-icon-inner {
            background: rgba(13, 13, 24, 0.7);
        }

        .platform-name {
            font-weight: 600;
            font-size: 0.95rem;
            color: var(--text-main);
            white-space: nowrap;
        }

        .user-col {
            display: flex;
            align-items: center;
            gap: 8px;
            flex: 1;
            min-width: 200px;
            overflow: hidden;
        }

        .user-col-text {
            font-size: 0.9rem;
            color: var(--text-main);
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .quick-copy-email {
            background: transparent;
            border: none;
            color: var(--text-muted);
            cursor: pointer;
            font-size: 0.85rem;
            padding: 4px;
            transition: color 0.2s;
        }

        .quick-copy-email:hover { color: var(--accent-orange); }

        .pass-col {
            font-family: monospace;
            letter-spacing: 2px;
            color: var(--accent-yellow);
            min-width: 130px;
            text-align: center;
        }

        .action-col {
            display: flex;
            gap: 8px;
        }

        .action-btn {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            color: var(--text-main);
            width: 36px;
            height: 36px;
            border-radius: 8px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s;
        }

        .action-btn:hover {
            background: rgba(255, 255, 255, 0.15);
            color: #fff;
        }

        .action-btn.del:hover {
            background: var(--danger);
            border-color: var(--danger);
        }

        /* PIN LOCKSCREEN */
        #pinLockscreen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(3, 3, 8, 0.93);
            backdrop-filter: blur(25px);
            z-index: 100;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            transition: opacity 0.5s ease, visibility 0.5s ease;
        }

        #pinLockscreen.unlocked {
            opacity: 0;
            visibility: hidden;
            pointer-events: none;
        }

        .pin-box {
            text-align: center;
            background: rgba(255, 255, 255, 0.03);
            padding: 40px;
            border-radius: 24px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 20px 40px rgba(0,0,0,0.6);
        }

        .pin-dots {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin: 25px 0 35px 0;
        }

        .dot {
            width: 16px;
            height: 16px;
            border-radius: 50%;
            border: 2px solid var(--text-muted);
            transition: all 0.2s;
        }

        .dot.filled {
            background: var(--accent-orange);
            border-color: var(--accent-orange);
            box-shadow: 0 0 12px var(--accent-orange);
        }

        .dot.error {
            background: var(--danger);
            border-color: var(--danger);
            box-shadow: 0 0 12px var(--danger);
        }

        .keypad {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            max-width: 260px;
            margin: 0 auto;
        }

        .key-btn {
            width: 65px;
            height: 65px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            color: var(--text-main);
            font-size: 1.4rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .key-btn:hover {
            background: rgba(255, 75, 43, 0.25);
            border-color: var(--accent-orange);
        }

        /* TOAST NOTIFICATION */
        .toast {
            position: fixed;
            bottom: 25px;
            right: 25px;
            background: rgba(20, 20, 28, 0.95);
            border-left: 4px solid var(--accent-yellow);
            border-radius: 8px;
            padding: 14px 20px;
            display: flex;
            align-items: center;
            gap: 12px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            transform: translateY(100px);
            opacity: 0;
            transition: all 0.3s ease;
            z-index: 1000;
        }

        .toast.show {
            transform: translateY(0);
            opacity: 1;
        }

        .toast-icon {
            font-size: 1.2rem;
            color: var(--accent-yellow);
        }
    </style>
</head>
<body>

    <!-- COSMIC PLANET & NEBULA BACKGROUND -->
    <div class="cosmic-background">
        <div class="nebula nebula-1"></div>
        <div class="nebula nebula-2"></div>
        <div class="nebula nebula-3"></div>

        <!-- PLANET BERGERAK & BERPUTAR -->
        <div class="planet-container">
            <div class="planet-body"></div>
            <div class="planet-ring"></div>
            <div class="planet-ring-2"></div>
            <div class="orbit-path">
                <div class="orbit-moon"></div>
                <div class="orbit-moon-2"></div>
            </div>
        </div>
    </div>

    <!-- CANVAS BINTANG & BINTANG JATUH -->
    <canvas id="spaceCanvas"></canvas>

    <!-- LOCKSCREEN -->
    <div id="pinLockscreen">
        <div class="pin-box">
            <i class="fas fa-shield-halved" style="font-size: 3rem; color: var(--accent-orange); margin-bottom: 10px;"></i>
            <h2>Vault Terkunci</h2>
            <p style="color: var(--text-muted); font-size: 0.9rem; margin-top: 5px;">Masukkan PIN (Default: 1234)</p>
            
            <div class="pin-dots" id="pinDots">
                <div class="dot"></div>
                <div class="dot"></div>
                <div class="dot"></div>
                <div class="dot"></div>
            </div>

            <div class="keypad">
                <button class="key-btn" onclick="pressKey('1')">1</button>
                <button class="key-btn" onclick="pressKey('2')">2</button>
                <button class="key-btn" onclick="pressKey('3')">3</button>
                <button class="key-btn" onclick="pressKey('4')">4</button>
                <button class="key-btn" onclick="pressKey('5')">5</button>
                <button class="key-btn" onclick="pressKey('6')">6</button>
                <button class="key-btn" onclick="pressKey('7')">7</button>
                <button class="key-btn" onclick="pressKey('8')">8</button>
                <button class="key-btn" onclick="pressKey('9')">9</button>
                <button class="key-btn" onclick="clearKey()"><i class="fas fa-trash-arrow-up" style="font-size:1rem;"></i></button>
                <button class="key-btn" onclick="pressKey('0')">0</button>
                <button class="key-btn" onclick="deleteKey()"><i class="fas fa-backspace" style="font-size:1rem;"></i></button>
            </div>
        </div>
    </div>

    <!-- MAIN APP CONTAINER -->
    <div class="container">
        <div class="vault-card">
            <div class="header">
                <div class="title-group">
                    <i class="fas fa-fire-flame-curved"></i>
                    <h2>Daftar Kredensial Tersimpan</h2>
                </div>
                <div class="search-box">
                    <i class="fas fa-search"></i>
                    <input type="text" id="searchInput" placeholder="Cari kredensial..." oninput="filterCredentials()">
                </div>
            </div>

            <form class="add-form" id="vaultForm">
                <input type="text" class="form-input" id="platformInput" placeholder="Platform (e.g. Google)" required>
                <input type="text" class="form-input" id="userInput" placeholder="Username / Email" required>
                <input type="password" class="form-input" id="passInput" placeholder="Password" required>
                <button type="submit" class="btn-add"><i class="fas fa-plus"></i> Simpan</button>
            </form>

            <div class="credential-list" id="credentialList"></div>
        </div>
    </div>

    <!-- TOAST NOTIFICATION -->
    <div class="toast" id="toastNotif">
        <div class="toast-icon"><i class="fas fa-check"></i></div>
        <div>
            <div id="toastTitle" style="font-weight: 600; font-size: 0.95rem;"></div>
            <div id="toastMessage" style="color: var(--text-muted); font-size: 0.85rem;"></div>
        </div>
    </div>

    <script>
        /* --- AUDIO SYNTHESIZER --- */
        function playUnlockSound() {
            try {
                const AudioContext = window.AudioContext || window.webkitAudioContext;
                const ctx = new AudioContext();
                const osc1 = ctx.createOscillator();
                const osc2 = ctx.createOscillator();
                const gain = ctx.createGain();

                osc1.type = 'sine';
                osc2.type = 'triangle';
                osc1.frequency.setValueAtTime(440, ctx.currentTime);
                osc1.frequency.exponentialRampToValueAtTime(880, ctx.currentTime + 0.2);
                osc2.frequency.setValueAtTime(554.37, ctx.currentTime);
                osc2.frequency.exponentialRampToValueAtTime(1108.73, ctx.currentTime + 0.2);

                gain.gain.setValueAtTime(0.2, ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.35);

                osc1.connect(gain);
                osc2.connect(gain);
                gain.connect(ctx.destination);

                osc1.start(); osc2.start();
                osc1.stop(ctx.currentTime + 0.35);
                osc2.stop(ctx.currentTime + 0.35);
            } catch (e) {}
        }

        function playErrorSound() {
            try {
                const AudioContext = window.AudioContext || window.webkitAudioContext;
                const ctx = new AudioContext();
                const osc = ctx.createOscillator();
                const gain = ctx.createGain();

                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(150, ctx.currentTime);
                osc.frequency.linearRampToValueAtTime(80, ctx.currentTime + 0.25);

                gain.gain.setValueAtTime(0.3, ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.25);

                osc.connect(gain);
                gain.connect(ctx.destination);

                osc.start();
                osc.stop(ctx.currentTime + 0.25);
            } catch (e) {}
        }

        function playKeyBeep() {
            try {
                const AudioContext = window.AudioContext || window.webkitAudioContext;
                const ctx = new AudioContext();
                const osc = ctx.createOscillator();
                const gain = ctx.createGain();

                osc.type = 'sine';
                osc.frequency.setValueAtTime(600, ctx.currentTime);

                gain.gain.setValueAtTime(0.05, ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + 0.05);

                osc.connect(gain);
                gain.connect(ctx.destination);

                osc.start();
                osc.stop(ctx.currentTime + 0.05);
            } catch (e) {}
        }

        /* --- LOCKSCREEN PIN LOGIC --- */
        const CORRECT_PIN = "1234";
        let currentPin = "";

        function updatePinDots() {
            const dots = document.querySelectorAll('#pinDots .dot');
            dots.forEach((dot, index) => {
                if (index < currentPin.length) {
                    dot.classList.add('filled');
                } else {
                    dot.classList.remove('filled', 'error');
                }
            });
        }

        function pressKey(num) {
            if (currentPin.length < 4) {
                playKeyBeep();
                currentPin += num;
                updatePinDots();

                if (currentPin.length === 4) {
                    setTimeout(verifyPin, 150);
                }
            }
        }

        function deleteKey() {
            if (currentPin.length > 0) {
                playKeyBeep();
                currentPin = currentPin.slice(0, -1);
                updatePinDots();
            }
        }

        function clearKey() {
            playKeyBeep();
            currentPin = "";
            updatePinDots();
        }

        function verifyPin() {
            if (currentPin === CORRECT_PIN) {
                playUnlockSound();
                document.getElementById('pinLockscreen').classList.add('unlocked');
                showToast("Akses Diberikan", "Berhasil masuk ke dalam Vault");
            } else {
                playErrorSound();
                const dots = document.querySelectorAll('#pinDots .dot');
                dots.forEach(dot => dot.classList.add('error'));
                showToast("Akses Ditolak", "PIN yang Anda masukkan salah!", true);
                setTimeout(() => {
                    currentPin = "";
                    updatePinDots();
                }, 600);
            }
        }

        document.addEventListener('keydown', (e) => {
            const lockscreen = document.getElementById('pinLockscreen');
            if (!lockscreen.classList.contains('unlocked')) {
                if (e.key >= '0' && e.key <= '9') {
                    pressKey(e.key);
                } else if (e.key === 'Backspace') {
                    deleteKey();
                } else if (e.key === 'Escape') {
                    clearKey();
                }
            }
        });

        /* --- TOAST SYSTEM --- */
        function showToast(title, message, isError = false) {
            const toast = document.getElementById('toastNotif');
            const toastTitle = document.getElementById('toastTitle');
            const toastMessage = document.getElementById('toastMessage');
            const icon = toast.querySelector('.toast-icon i');

            toastTitle.innerText = title;
            toastMessage.innerText = message;

            if (isError) {
                toast.style.borderLeftColor = 'var(--danger)';
                icon.className = 'fas fa-exclamation-triangle';
                toast.querySelector('.toast-icon').style.color = 'var(--danger)';
            } else {
                toast.style.borderLeftColor = 'var(--accent-yellow)';
                icon.className = 'fas fa-check';
                toast.querySelector('.toast-icon').style.color = 'var(--accent-yellow)';
            }

            toast.classList.add('show');
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3500);
        }

        /* --- CREDENTIAL VAULT DATA & CRUD --- */
        let credentials = JSON.parse(localStorage.getItem('phoenix_vault_db')) || [
            { id: 1, platform: 'BK', user: 'rifaldosmb11@gmail.com', pass: 'P@ssw0rd123!', icon: 'fa-solid fa-globe' },
            { id: 2, platform: 'GitHub', user: 'rifaldo-nst', pass: 'P@ssw0rd123!', icon: 'fa-brands fa-github' },
            { id: 3, platform: 'Google Account', user: 'rifaldonataniel.siregar@gmail.com', pass: 'C1oudS3cur3#', icon: 'fa-brands fa-google' },
            { id: 4, platform: 'Discord', user: 'Rifaldo#0001', pass: 'N1ghtOw12024$', icon: 'fa-brands fa-discord' }
        ];

        function saveToStorage() {
            localStorage.setItem('phoenix_vault_db', JSON.stringify(credentials));
        }

        function getIconForPlatform(platform) {
            const lower = platform.toLowerCase();
            if (lower.includes('github')) return 'fa-brands fa-github';
            if (lower.includes('google') || lower.includes('gmail')) return 'fa-brands fa-google';
            if (lower.includes('discord')) return 'fa-brands fa-discord';
            if (lower.includes('twitter') || lower.includes('x')) return 'fa-brands fa-twitter';
            if (lower.includes('facebook')) return 'fa-brands fa-facebook';
            if (lower.includes('instagram')) return 'fa-brands fa-instagram';
            if (lower.includes('steam')) return 'fa-brands fa-steam';
            return 'fa-solid fa-globe';
        }

        function renderCredentials(data = credentials) {
            const listEl = document.getElementById('credentialList');
            listEl.innerHTML = '';

            if (data.length === 0) {
                listEl.innerHTML = `<div style="text-align:center; padding: 2rem; color: var(--text-muted); font-size: 0.9rem;">Tidak ada kredensial yang ditemukan.</div>`;
                return;
            }

            data.forEach(item => {
                const div = document.createElement('div');
                div.className = 'credential-item';
                div.innerHTML = `
                    <div class="platform-col">
                        <div class="platform-icon-wrapper">
                            <div class="platform-icon-inner">
                                <i class="${item.icon}"></i>
                            </div>
                        </div>
                        <div class="platform-name" title="${item.platform}">${item.platform}</div>
                    </div>
                    <div class="user-col">
                        <span class="user-col-text" title="${item.user}">${item.user}</span>
                        <button class="quick-copy-email" onclick="copyText('${item.user}', 'Username/Email')" title="Salin Email"><i class="fas fa-copy"></i></button>
                    </div>
                    <div class="pass-col" id="pass-${item.id}">••••••••••••</div>
                    <div class="action-col">
                        <button class="action-btn" onclick="togglePassword(${item.id}, '${item.pass}')" title="Tampilkan/Sembunyikan"><i class="fas fa-eye" id="eye-${item.id}"></i></button>
                        <button class="action-btn" onclick="copyText('${item.pass}', 'Password')" title="Salin Password"><i class="fas fa-key"></i></button>
                        <button class="action-btn del" onclick="deleteCredential(${item.id})" title="Hapus"><i class="fas fa-trash-can"></i></button>
                    </div>
                `;
                listEl.appendChild(div);
            });
        }

        function togglePassword(id, realPass) {
            const passEl = document.getElementById(`pass-${id}`);
            const eyeEl = document.getElementById(`eye-${id}`);
            if (passEl.innerText === '••••••••••••') {
                passEl.innerText = realPass;
                eyeEl.className = 'fas fa-eye-slash';
            } else {
                passEl.innerText = '••••••••••••';
                eyeEl.className = 'fas fa-eye';
            }
        }

        function copyText(text, type) {
            navigator.clipboard.writeText(text);
            showToast("Berhasil Disalin", `${type} telah disalin ke clipboard.`);
        }

        function deleteCredential(id) {
            credentials = credentials.filter(item => item.id !== id);
            saveToStorage();
            renderCredentials();
            showToast("Kredensial Dihapus", "Data berhasil dihapus dari vault.");
        }

        function filterCredentials() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = credentials.filter(item => 
                item.platform.toLowerCase().includes(query) || 
                item.user.toLowerCase().includes(query)
            );
            renderCredentials(filtered);
        }

        document.getElementById('vaultForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const platform = document.getElementById('platformInput').value;
            const user = document.getElementById('userInput').value;
            const pass = document.getElementById('passInput').value;

            const newItem = {
                id: Date.now(),
                platform,
                user,
                pass,
                icon: getIconForPlatform(platform)
            };

            credentials.unshift(newItem);
            saveToStorage();
            renderCredentials();

            document.getElementById('vaultForm').reset();
            showToast("Kredensial Disimpan", `Data untuk ${platform} telah diamankan.`);
        });

        /* --- CANVAS SPACE: BINTANG BERKELIP & BINTANG JATUH --- */
        const spaceCanvas = document.getElementById('spaceCanvas');
        const spaceCtx = spaceCanvas.getContext('2d');
        let stars = [];
        let shootingStars = [];

        function resizeSpaceCanvas() {
            spaceCanvas.width = window.innerWidth;
            spaceCanvas.height = window.innerHeight;
        }

        class Star {
            constructor() { this.reset(); }
            reset() {
                this.x = Math.random() * spaceCanvas.width;
                this.y = Math.random() * spaceCanvas.height;
                this.size = Math.random() * 1.8;
                this.alpha = Math.random();
                this.speed = Math.random() * 0.015 + 0.005;
                const colors = ['#ffffff', '#b9d5ff', '#ffdfb9', '#f3b9ff'];
                this.color = colors[Math.floor(Math.random() * colors.length)];
            }
            update() {
                this.alpha += this.speed;
                if (this.alpha > 1 || this.alpha < 0) this.speed = -this.speed;
            }
            draw() {
                spaceCtx.save();
                spaceCtx.globalAlpha = Math.abs(this.alpha);
                spaceCtx.fillStyle = this.color;
                spaceCtx.beginPath();
                spaceCtx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                spaceCtx.fill();
                spaceCtx.restore();
            }
        }

        class ShootingStar {
            constructor() { this.reset(); }
            reset() {
                this.x = Math.random() * spaceCanvas.width;
                this.y = Math.random() * (spaceCanvas.height / 2);
                this.len = Math.random() * 80 + 40;
                this.speed = Math.random() * 10 + 6;
                this.size = Math.random() * 1.5 + 0.5;
                this.waitTime = Math.floor(Math.random() * 300) + 100;
                this.active = false;
            }
            update() {
                if (!this.active) {
                    this.waitTime--;
                    if (this.waitTime <= 0) this.active = true;
                    return;
                }
                this.x -= this.speed;
                this.y += this.speed;

                if (this.x < -this.len || this.y > spaceCanvas.height + this.len) {
                    this.reset();
                }
            }
            draw() {
                if (!this.active) return;
                spaceCtx.save();
                const grad = spaceCtx.createLinearGradient(this.x, this.y, this.x + this.len, this.y - this.len);
                grad.addColorStop(0, 'rgba(255, 255, 255, 1)');
                grad.addColorStop(1, 'rgba(255, 255, 255, 0)');

                spaceCtx.strokeStyle = grad;
                spaceCtx.lineWidth = this.size;
                spaceCtx.beginPath();
                spaceCtx.moveTo(this.x, this.y);
                spaceCtx.lineTo(this.x + this.len, this.y - this.len);
                spaceCtx.stroke();
                spaceCtx.restore();
            }
        }

        function initSpace() {
            stars = [];
            shootingStars = [];
            for (let i = 0; i < 200; i++) stars.push(new Star());
            for (let i = 0; i < 5; i++) shootingStars.push(new ShootingStar());
        }

        function animateSpace() {
            spaceCtx.clearRect(0, 0, spaceCanvas.width, spaceCanvas.height);
            stars.forEach(star => {
                star.update();
                star.draw();
            });
            shootingStars.forEach(sStar => {
                sStar.update();
                sStar.draw();
            });
            requestAnimationFrame(animateSpace);
        }

        window.addEventListener('resize', () => {
            resizeSpaceCanvas();
        });

        window.onload = () => {
            resizeSpaceCanvas();
            initSpace();
            animateSpace();
            renderCredentials();
        };
    </script>
</body>
</html>
