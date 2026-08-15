<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PHOENIX VAULT | RGB Animated Border Edition</title>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --bg-dark: #030002;
            --accent-red: #ff003c;
            --accent-crimson: #d90429;
            --accent-orange: #ff5400;
            --accent-yellow: #ffcc00;
            --accent-pink: #ff0077;
            --card-glass: rgba(12, 3, 7, 0.85);
            --text-main: #fff0f3;
            --text-muted: #a38890;
            --danger: #ff2a2a;
            --transition-smooth: all 0.35s cubic-bezier(0.16, 1, 0.3, 1);
        }

        /* REGISTER PROPERTY UNTUK ANIMATED GRADIENT ROTATION */
        @property --angle {
            syntax: '<angle>';
            initial-value: 0deg;
            inherits: false;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Plus Jakarta Sans', sans-serif;
            user-select: none;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-main);
            min-height: 100vh;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 2rem;
            position: relative;
        }

        #spaceCanvas {
            position: fixed;
            top: 0; left: 0;
            width: 100vw; height: 100vh;
            z-index: 0;
            pointer-events: none;
        }

        .bg-glow-container {
            position: fixed;
            top: 0; left: 0;
            width: 100vw; height: 100vh;
            z-index: 1;
            overflow: hidden;
            pointer-events: none;
        }

        .nebula-orb {
            position: absolute;
            border-radius: 50%;
            filter: blur(140px);
            opacity: 0.35;
            animation: nebulaFloat 18s ease-in-out infinite alternate;
        }

        .nebula-1 {
            width: 700px; height: 700px;
            background: radial-gradient(circle, var(--accent-red), var(--accent-pink), transparent);
            top: -200px; left: -150px;
        }

        .nebula-2 {
            width: 800px; height: 800px;
            background: radial-gradient(circle, var(--accent-crimson), var(--accent-orange), transparent);
            bottom: -250px; right: -200px;
            animation-delay: -6s;
        }

        @keyframes nebulaFloat {
            0% { transform: scale(1) translate(0, 0); opacity: 0.25; }
            50% { transform: scale(1.2) translate(50px, -40px); opacity: 0.45; }
            100% { transform: scale(0.95) translate(-30px, 40px); opacity: 0.3; }
        }

        /* LOCKSCREEN PIN */
        .pin-lockscreen {
            position: fixed;
            top: 0; left: 0;
            width: 100vw; height: 100vh;
            z-index: 999;
            background: rgba(3, 0, 2, 0.95);
            backdrop-filter: blur(25px);
            display: flex;
            justify-content: center;
            align-items: center;
            transition: opacity 0.6s ease, transform 0.6s ease, visibility 0.6s;
        }

        .pin-lockscreen.unlocked {
            opacity: 0;
            visibility: hidden;
            transform: scale(1.1);
            pointer-events: none;
        }

        .pin-box {
            position: relative;
            background: rgba(18, 2, 6, 0.9);
            border-radius: 28px;
            padding: 2.5rem 2rem;
            width: 100%;
            max-width: 380px;
            text-align: center;
            border: 1px solid rgba(255, 0, 60, 0.3);
            box-shadow: 0 0 40px rgba(255, 0, 60, 0.25), inset 0 0 20px rgba(255, 84, 0, 0.1);
        }

        .pin-header { margin-bottom: 1.8rem; }
        .pin-icon {
            font-size: 2.5rem;
            color: var(--accent-orange);
            filter: drop-shadow(0 0 12px var(--accent-red));
            animation: flameFlicker 0.2s infinite alternate;
            margin-bottom: 0.8rem;
        }

        @keyframes flameFlicker {
            0% { transform: scale(1); filter: drop-shadow(0 0 10px var(--accent-red)); }
            100% { transform: scale(1.08); filter: drop-shadow(0 0 18px var(--accent-yellow)); }
        }

        .pin-title {
            font-size: 1.4rem; font-weight: 800; letter-spacing: 1.5px;
            background: linear-gradient(to right, #fff, var(--accent-orange));
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
        }

        .pin-subtitle { font-size: 0.78rem; color: var(--text-muted); margin-top: 4px; }
        .pin-dots { display: flex; justify-content: center; gap: 16px; margin-bottom: 2rem; }

        .dot {
            width: 18px; height: 18px; border-radius: 50%;
            background: rgba(255, 0, 60, 0.15);
            border: 2px solid rgba(255, 0, 60, 0.4);
            transition: var(--transition-smooth);
        }

        .dot.filled {
            background: var(--accent-orange); border-color: var(--accent-yellow);
            box-shadow: 0 0 15px var(--accent-red), 0 0 25px var(--accent-yellow);
            transform: scale(1.2);
        }

        .dot.error { background: var(--danger); border-color: #fff; box-shadow: 0 0 20px var(--danger); animation: shake 0.4s ease; }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            20%, 60% { transform: translateX(-8px); }
            40%, 80% { transform: translateX(8px); }
        }

        .keypad { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; }
        .key-btn {
            background: rgba(255, 0, 60, 0.08); border: 1px solid rgba(255, 0, 60, 0.2);
            border-radius: 16px; color: #fff; font-size: 1.25rem; font-weight: 800;
            padding: 1rem 0; cursor: pointer; transition: var(--transition-smooth);
            box-shadow: 0 4px 10px rgba(0,0,0,0.5);
        }

        .key-btn:hover {
            background: linear-gradient(135deg, rgba(255, 0, 60, 0.4), rgba(255, 84, 0, 0.3));
            border-color: var(--accent-orange); color: var(--accent-yellow);
            transform: translateY(-2px); box-shadow: 0 8px 20px rgba(255, 0, 60, 0.4);
        }

        .toast-notification {
            position: fixed; top: -100px; right: 30px; z-index: 1000;
            background: rgba(18, 2, 6, 0.95); border: 1px solid var(--accent-orange);
            border-left: 5px solid var(--accent-yellow); border-radius: 14px;
            padding: 1rem 1.4rem; display: flex; align-items: center; gap: 14px;
            box-shadow: 0 10px 30px rgba(255, 0, 60, 0.4); backdrop-filter: blur(15px);
            transition: all 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55); opacity: 0;
        }

        .toast-notification.show { top: 30px; opacity: 1; }
        .toast-icon {
            width: 36px; height: 36px;
            background: linear-gradient(135deg, var(--accent-orange), var(--accent-yellow));
            border-radius: 10px; display: flex; align-items: center; justify-content: center;
            color: #000; font-size: 1.1rem; box-shadow: 0 0 12px var(--accent-orange);
        }
        .toast-text h4 { font-size: 0.9rem; font-weight: 800; color: #fff; }
        .toast-text p { font-size: 0.75rem; color: var(--text-muted); }

        .fire-border-wrapper {
            position: relative; z-index: 2; width: 100%; max-width: 1280px; height: 860px;
            border-radius: 30px; padding: 1.5px;
            background: linear-gradient(135deg, rgba(255,0,60,0.6), rgba(255,84,0,0.3), rgba(255,0,119,0.4));
            box-shadow: 0 0 30px rgba(255, 0, 60, 0.25), 0 0 60px rgba(255, 84, 0, 0.15);
        }

        .app-container {
            width: 100%; height: 100%; background: var(--card-glass);
            backdrop-filter: blur(35px); border-radius: 28px;
            display: grid; grid-template-columns: 280px 1fr; overflow: hidden; position: relative;
        }

        /* --- SIDEBAR CONTAINER --- */
        aside.sidebar {
            background: rgba(8, 1, 3, 0.95); border-right: 1px solid rgba(255, 0, 60, 0.15);
            padding: 2.2rem 1.4rem; display: flex; flex-direction: column; justify-content: space-between;
            position: relative; z-index: 5; overflow: hidden;
        }

        #menuFireCanvas {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none; z-index: 1; opacity: 0.85;
        }

        .brand-logo { display: flex; align-items: center; gap: 14px; padding-left: 0.4rem; margin-bottom: 3rem; position: relative; z-index: 2; }
        .logo-icon-wrapper {
            width: 48px; height: 48px; border-radius: 14px;
            background: linear-gradient(135deg, var(--accent-red), var(--accent-orange));
            display: flex; align-items: center; justify-content: center;
            font-size: 1.4rem; color: #ffffff; box-shadow: 0 0 20px rgba(255, 0, 60, 0.6);
            animation: logoPulse 2.5s infinite alternate;
        }

        @keyframes logoPulse {
            0% { box-shadow: 0 0 15px rgba(255, 0, 60, 0.4); transform: scale(1); }
            100% { box-shadow: 0 0 30px rgba(255, 84, 0, 0.8); transform: scale(1.05); }
        }

        .brand-name {
            font-size: 1.3rem; font-weight: 800; letter-spacing: -0.5px;
            background: linear-gradient(to right, #fff, var(--accent-red));
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
        }
        .brand-tag { font-size: 0.65rem; color: var(--accent-red); letter-spacing: 2.5px; text-transform: uppercase; font-weight: 800; }
        
        .nav-wrapper { position: relative; z-index: 2; }
        .nav-menu { list-style: none; display: flex; flex-direction: column; gap: 18px; }

        /* --- MULTI-COLOR RAINBOW ANIMATED BORDER MENU ITEMS --- */
        .nav-item {
            position: relative;
            border-radius: 18px;
            padding: 2px; /* Tebal border */
            background: conic-gradient(
                from var(--angle),
                #ff003c 0%,
                #ff5400 18%,
                #ffcc00 36%,
                #00ffcc 54%,
                #7000ff 72%,
                #ff0077 90%,
                #ff003c 100%
            );
            animation: rotateRainbow 3.5s linear infinite;
            transition: var(--transition-smooth);
            cursor: pointer;
        }

        @keyframes rotateRainbow {
            0% { --angle: 0deg; }
            100% { --angle: 360deg; }
        }

        .nav-link {
            position: relative; display: flex; align-items: center; gap: 16px; padding: 1.1rem 1.3rem;
            color: var(--text-muted); text-decoration: none; font-weight: 700; font-size: 0.95rem;
            border-radius: 16px; background: rgba(14, 2, 7, 0.95);
            transition: var(--transition-smooth); overflow: hidden; z-index: 2;
        }

        .nav-link i { font-size: 1.1rem; transition: var(--transition-smooth); color: var(--text-muted); }

        /* TAMPILAN ACTIVE MENU */
        .nav-item.active {
            box-shadow: 0 0 25px rgba(255, 0, 60, 0.5), 0 0 35px rgba(0, 255, 204, 0.3);
        }

        .nav-item.active .nav-link {
            background: rgba(22, 3, 9, 0.98);
            color: #ffffff;
        }

        .nav-item.active .nav-link i {
            color: var(--accent-yellow);
            filter: drop-shadow(0 0 10px var(--accent-orange));
            transform: scale(1.15);
        }

        /* HOVER EFFEK PADA MENU TIDAK AKTIF */
        .nav-item:not(.active):hover {
            transform: translateX(6px);
            box-shadow: 0 0 25px rgba(255, 84, 0, 0.5), 0 0 30px rgba(112, 0, 255, 0.35);
        }

        .nav-item:not(.active):hover .nav-link {
            background: rgba(25, 4, 12, 0.95);
            color: #ffffff;
        }

        .nav-item:not(.active):hover .nav-link i {
            color: var(--accent-red);
            transform: scale(1.2) rotate(-6deg);
            filter: drop-shadow(0 0 8px var(--accent-red));
        }

        .sidebar-footer {
            position: relative; z-index: 2; padding: 1rem; background: rgba(255, 0, 60, 0.04);
            border-radius: 16px; border: 1px solid rgba(255, 0, 60, 0.18); display: flex;
            align-items: center; gap: 12px; font-size: 0.75rem; color: var(--text-muted);
        }

        main.main-content { padding: 2.5rem 3rem; overflow-y: auto; display: flex; flex-direction: column; gap: 2rem; }
        main.main-content::-webkit-scrollbar { width: 5px; }
        main.main-content::-webkit-scrollbar-thumb { background: rgba(255, 0, 60, 0.4); border-radius: 10px; }

        .top-bar { display: flex; justify-content: space-between; align-items: center; }
        .page-title h2 {
            font-size: 2.2rem; font-weight: 900; letter-spacing: 2px;
            background: linear-gradient(0deg, #ff003c 0%, #ff5400 40%, #ffcc00 80%, #ffffff 100%);
            background-size: 100% 200%; -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            animation: privatFlameFlow 2s ease-in-out infinite alternate, privatTextGlow 1.5s infinite alternate;
        }

        @keyframes privatFlameFlow { 0% { background-position: 0% 0%; } 100% { background-position: 0% 100%; } }
        @keyframes privatTextGlow {
            0% { filter: drop-shadow(0 0 8px rgba(255, 0, 60, 0.8)); }
            100% { filter: drop-shadow(0 0 18px rgba(255, 0, 60, 1)) drop-shadow(0 0 32px rgba(255, 204, 0, 0.9)); }
        }

        .user-profile {
            display: flex; align-items: center; gap: 14px; background: rgba(255, 0, 60, 0.05);
            padding: 6px 16px 6px 8px; border-radius: 30px; border: 1px solid rgba(255, 0, 60, 0.25);
        }
        .avatar {
            width: 38px; height: 38px; border-radius: 50%;
            background: linear-gradient(135deg, var(--accent-red), var(--accent-orange));
            display: flex; align-items: center; justify-content: center; font-weight: bold; font-size: 0.85rem;
            border: 2px solid var(--accent-red); box-shadow: 0 0 12px rgba(255, 0, 60, 0.6);
        }

        .form-card {
            position: relative; border-radius: 20px; padding: 1.8rem;
            background: rgba(15, 3, 7, 0.85);
            border: 1px solid rgba(255, 0, 60, 0.25);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5), inset 0 0 15px rgba(255, 0, 60, 0.05);
            backdrop-filter: blur(20px);
        }

        .card-header-title {
            font-size: 1rem; font-weight: 700; margin-bottom: 1.2rem; display: flex; align-items: center;
            gap: 10px; color: var(--accent-red); text-shadow: 0 0 10px rgba(255, 0, 60, 0.5);
        }
        .form-grid { display: grid; grid-template-columns: 1fr 1.2fr 1fr 160px; gap: 1rem; align-items: center; }
        .input-group { position: relative; }
        .input-group i { position: absolute; left: 14px; top: 50%; transform: translateY(-50%); color: var(--text-muted); }
        .input-group input {
            width: 100%; padding: 0.85rem 1rem 0.85rem 2.8rem; background: rgba(8, 0, 2, 0.8);
            border: 1px solid rgba(255, 0, 60, 0.2); border-radius: 12px; color: #fff; font-size: 0.88rem;
            transition: var(--transition-smooth);
        }
        .input-group input:focus {
            outline: none; border-color: var(--accent-red);
            box-shadow: 0 0 18px rgba(255, 0, 60, 0.4); background: rgba(15, 0, 4, 0.95);
        }

        .btn-glow {
            width: 100%; padding: 0.85rem; border: none; border-radius: 12px;
            background: linear-gradient(135deg, var(--accent-red), var(--accent-orange));
            color: #fff; font-weight: 800; font-size: 0.85rem; cursor: pointer;
            transition: var(--transition-smooth); display: flex; align-items: center; justify-content: center;
            gap: 8px; box-shadow: 0 0 20px rgba(255, 0, 60, 0.5);
        }
        .btn-glow:hover { transform: translateY(-2px); box-shadow: 0 0 30px rgba(255, 0, 60, 0.8); }

        .vault-section { display: flex; flex-direction: column; gap: 1rem; }
        .vault-header { display: flex; justify-content: space-between; align-items: center; }
        .vault-header h3 { font-size: 1.1rem; font-weight: 700; }
        .search-box { position: relative; width: 240px; }
        .search-box input {
            width: 100%; padding: 0.55rem 1rem 0.55rem 2.2rem; background: rgba(255, 0, 60, 0.04);
            border: 1px solid rgba(255, 0, 60, 0.2); border-radius: 20px; color: #fff; font-size: 0.8rem;
        }
        .search-box i { position: absolute; left: 12px; top: 50%; transform: translateY(-50%); font-size: 0.75rem; color: var(--text-muted); }

        .credential-list { display: flex; flex-direction: column; gap: 14px; }

        .credential-item {
            position: relative; border-radius: 18px; padding: 1.1rem 1.6rem;
            display: grid; grid-template-columns: 200px 1fr 140px 150px; align-items: center; gap: 16px;
            background: rgba(14, 3, 8, 0.82); border: 1px solid rgba(255, 0, 60, 0.22);
            backdrop-filter: blur(16px); box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
            transition: var(--transition-smooth);
        }

        .credential-item:hover {
            transform: translateY(-2px); border-color: var(--accent-orange);
            background: rgba(20, 4, 11, 0.92); box-shadow: 0 12px 35px rgba(255, 0, 60, 0.25), 0 0 20px rgba(255, 84, 0, 0.2);
        }

        .platform-col { display: flex; align-items: center; gap: 14px; font-weight: 700; min-width: 0; }
        .platform-icon {
            width: 44px; height: 44px; border-radius: 12px;
            background: rgba(255, 0, 60, 0.1); border: 1px solid rgba(255, 0, 60, 0.3);
            display: flex; align-items: center; justify-content: center;
            color: var(--accent-red); font-size: 1.25rem; box-shadow: 0 0 12px rgba(255, 0, 60, 0.2); flex-shrink: 0;
        }

        .platform-name { white-space: nowrap; overflow: hidden; text-overflow: ellipsis; font-size: 0.95rem; color: #ffffff; }
        
        .user-col { color: var(--text-muted); font-size: 0.88rem; display: flex; align-items: center; gap: 10px; word-break: break-all; }
        .user-col-text { white-space: normal; overflow: visible; color: #e2d7dc; }

        .quick-copy-email {
            font-size: 0.75rem; color: var(--accent-orange); cursor: pointer; opacity: 0.8;
            transition: var(--transition-smooth); padding: 4px 8px; border-radius: 8px;
            background: rgba(255, 84, 0, 0.12); border: 1px solid rgba(255, 84, 0, 0.25); flex-shrink: 0;
        }

        .quick-copy-email:hover { opacity: 1; color: #fff; background: var(--accent-orange); box-shadow: 0 0 10px var(--accent-orange); }
        .pass-col { font-family: 'JetBrains Mono', monospace; letter-spacing: 2px; font-size: 0.9rem; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; color: var(--accent-yellow); }
        
        .action-col { display: flex; justify-content: flex-end; gap: 8px; position: relative; z-index: 3; }
        .action-btn {
            width: 38px; height: 38px; border-radius: 10px;
            border: 1px solid rgba(255, 0, 60, 0.2); background: rgba(255, 0, 60, 0.06);
            color: var(--text-muted); cursor: pointer; display: flex; align-items: center;
            justify-content: center; transition: var(--transition-smooth); font-size: 0.9rem;
        }

        .action-btn:hover {
            color: #fff; border-color: var(--accent-orange);
            background: linear-gradient(135deg, rgba(255, 0, 60, 0.3), rgba(255, 84, 0, 0.3));
            box-shadow: 0 0 15px rgba(255, 84, 0, 0.4); transform: translateY(-2px);
        }

        .action-btn.del:hover { border-color: var(--danger); background: rgba(255, 42, 42, 0.3); color: #fff; box-shadow: 0 0 18px rgba(255, 42, 42, 0.6); }

        @media (max-width: 1024px) {
            .fire-border-wrapper { height: auto; }
            .app-container { grid-template-columns: 220px 1fr; }
            .form-grid { grid-template-columns: 1fr 1fr; }
            .btn-glow { grid-column: span 2; }
            .credential-item { grid-template-columns: 1fr 1fr; gap: 12px; }
            .action-col { grid-column: span 2; justify-content: flex-start; }
        }

        @media (max-width: 768px) {
            .app-container { grid-template-columns: 1fr; }
            aside.sidebar { display: none; }
            .credential-item { grid-template-columns: 1fr; gap: 12px; }
            .action-col { justify-content: flex-start; }
            .form-grid { grid-template-columns: 1fr; }
            .btn-glow { grid-column: span 1; }
        }
    </style>
</head>
<body>

    <!-- NOTIFIKASI TOAST -->
    <div class="toast-notification" id="toastNotif">
        <div class="toast-icon"><i class="fas fa-check"></i></div>
        <div class="toast-text">
            <h4 id="toastTitle">Akses Diberikan</h4>
            <p id="toastMessage">Berhasil masuk ke dalam Vault</p>
        </div>
    </div>

    <!-- LOCKSCREEN PIN OVERLAY -->
    <div class="pin-lockscreen" id="pinLockscreen">
        <div class="pin-box">
            <div class="pin-header">
                <i class="fas fa-fire-flame-curved pin-icon"></i>
                <div class="pin-title">SECURITY ACCESS</div>
                <div class="pin-subtitle">Masukkan PIN Keamanan (Default: 1234)</div>
            </div>

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
                <button class="key-btn" onclick="clearKey()"><i class="fas fa-undo" style="font-size:0.9rem;"></i></button>
                <button class="key-btn" onclick="pressKey('0')">0</button>
                <button class="key-btn" onclick="deleteKey()"><i class="fas fa-backspace" style="font-size:0.9rem;"></i></button>
            </div>
        </div>
    </div>

    <!-- SPACE ANIMATED CANVAS -->
    <canvas id="spaceCanvas"></canvas>

    <!-- NEBULA BACKGROUND ORBS -->
    <div class="bg-glow-container">
        <div class="nebula-orb nebula-1"></div>
        <div class="nebula-orb nebula-2"></div>
    </div>

    <!-- MAIN CONTAINER -->
    <div class="fire-border-wrapper">
        <div class="app-container">

            <!-- SIDEBAR DENGAN MULTI-COLOR ANIMATED MENU BORDER -->
            <aside class="sidebar">
                <canvas id="menuFireCanvas"></canvas>

                <div>
                    <div class="brand-logo">
                        <div class="logo-icon-wrapper"><i class="fas fa-shield-halved"></i></div>
                        <div>
                            <div class="brand-name">PHOENIX</div>
                            <div class="brand-tag">RED VAULT</div>
                        </div>
                    </div>

                    <div class="nav-wrapper">
                        <ul class="nav-menu">
                            <li class="nav-item active" onclick="switchTab(this)">
                                <a href="#" class="nav-link">
                                    <i class="fas fa-chart-pie"></i>
                                    <span>Dashboard</span>
                                </a>
                            </li>
                            <li class="nav-item" onclick="switchTab(this)">
                                <a href="#" class="nav-link">
                                    <i class="fas fa-vault"></i>
                                    <span>Credentials Vault</span>
                                </a>
                            </li>
                        </ul>
                    </div>
                </div>

                <div class="sidebar-footer">
                    <i class="fas fa-lock" style="color:var(--accent-red); font-size:1.2rem;"></i>
                    <div>
                        <div style="font-weight:700; color:#fff;">AES-256 GCM</div>
                        <div>Cosmic Hardware Active</div>
                    </div>
                </div>
            </aside>

            <!-- MAIN CONTENT AREA -->
            <main class="main-content">
                <div class="top-bar">
                    <div class="page-title">
                        <h2>PRIVAT</h2>
                        <p>Encrypted Space Security Platform</p>
                    </div>
                    <div class="user-profile">
                        <div class="avatar">RN</div>
                        <div class="user-info">
                            <div style="font-size:0.85rem; font-weight:700;">RIFALDO NST</div>
                            <div style="font-size:0.7rem; color:var(--accent-red); font-weight:600;"><i class="fas fa-circle" style="font-size:0.5rem;"></i> Active Vault</div>
                        </div>
                    </div>
                </div>

                <!-- ADD CREDENTIAL FORM -->
                <div class="form-card">
                    <div class="card-header-title">
                        <i class="fas fa-plus-circle"></i> Tambah Kredensial Baru
                    </div>
                    <form id="vaultForm">
                        <div class="form-grid">
                            <div class="input-group">
                                <input type="text" id="platformInput" placeholder="Nama Layanan / Situs" required>
                                <i class="fas fa-globe"></i>
                            </div>
                            <div class="input-group">
                                <input type="text" id="userInput" placeholder="Username / Email" required>
                                <i class="fas fa-user"></i>
                            </div>
                            <div class="input-group">
                                <input type="password" id="passInput" placeholder="Password" required>
                                <i class="fas fa-key"></i>
                            </div>
                            <button type="submit" class="btn-glow">
                                <i class="fas fa-shield"></i> Simpan
                            </button>
                        </div>
                    </form>
                </div>

                <!-- VAULT LIST -->
                <div class="vault-section">
                    <div class="vault-header">
                        <h3>Daftar Kredensial Tersimpan</h3>
                        <div class="search-box">
                            <i class="fas fa-search"></i>
                            <input type="text" id="searchInput" onkeyup="filterCredentials()" placeholder="Cari kredensial...">
                        </div>
                    </div>

                    <div class="credential-list" id="credentialList"></div>
                </div>
            </main>
        </div>
    </div>

    <script>
        function switchTab(element) {
            document.querySelectorAll('.nav-item').forEach(item => item.classList.remove('active'));
            element.classList.add('active');
        }

        /* --- SIDEBAR EMBERS CANVAS --- */
        const menuCanvas = document.getElementById('menuFireCanvas');
        const menuCtx = menuCanvas.getContext('2d');
        let fireEmbers = [];

        function resizeMenuCanvas() {
            const sidebar = document.querySelector('aside.sidebar');
            if (sidebar) {
                menuCanvas.width = sidebar.clientWidth;
                menuCanvas.height = sidebar.clientHeight;
            }
        }

        class EmberParticle {
            constructor() { this.reset(); }
            reset() {
                this.x = Math.random() * menuCanvas.width;
                this.y = menuCanvas.height + Math.random() * 20;
                this.size = Math.random() * 2.5 + 0.8;
                this.speedY = Math.random() * 1.5 + 0.5;
                this.speedX = (Math.random() - 0.5) * 0.6;
                this.opacity = Math.random() * 0.8 + 0.2;
                this.color = Math.random() > 0.4 ? '#ff003c' : (Math.random() > 0.5 ? '#ff5400' : '#ffcc00');
            }
            update() {
                this.y -= this.speedY;
                this.x += this.speedX;
                this.opacity -= 0.003;
                if (this.y < -10 || this.opacity <= 0) this.reset();
            }
            draw() {
                menuCtx.save();
                menuCtx.globalAlpha = this.opacity;
                menuCtx.fillStyle = this.color;
                menuCtx.shadowBlur = 8;
                menuCtx.shadowColor = this.color;
                menuCtx.beginPath();
                menuCtx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                menuCtx.fill();
                menuCtx.restore();
            }
        }

        function initMenuFire() {
            fireEmbers = [];
            for (let i = 0; i < 35; i++) fireEmbers.push(new EmberParticle());
        }

        function animateMenuFire() {
            menuCtx.clearRect(0, 0, menuCanvas.width, menuCanvas.height);
            fireEmbers.forEach(ember => {
                ember.update();
                ember.draw();
            });
            requestAnimationFrame(animateMenuFire);
        }

        /* --- AUDIO SYNTHESIS ENGINE --- */
        function playUnlockSound() {
            try {
                const AudioContext = window.AudioContext || window.webkitAudioContext;
                const ctx = new AudioContext();

                const osc1 = ctx.createOscillator();
                const gain1 = ctx.createGain();
                
                osc1.type = 'sine';
                osc1.frequency.setValueAtTime(440, ctx.currentTime);
                osc1.frequency.exponentialRampToValueAtTime(880, ctx.currentTime + 0.15);
                
                gain1.gain.setValueAtTime(0.3, ctx.currentTime);
                gain1.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.35);

                osc1.connect(gain1);
                gain1.connect(ctx.destination);

                const osc2 = ctx.createOscillator();
                const gain2 = ctx.createGain();

                osc2.type = 'triangle';
                osc2.frequency.setValueAtTime(220, ctx.currentTime);
                osc2.frequency.exponentialRampToValueAtTime(554.37, ctx.currentTime + 0.2);

                gain2.gain.setValueAtTime(0.2, ctx.currentTime);
                gain2.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.3);

                osc2.connect(gain2);
                gain2.connect(ctx.destination);

                osc1.start();
                osc2.start();
                osc1.stop(ctx.currentTime + 0.35);
                osc2.stop(ctx.currentTime + 0.35);
            } catch (e) {
                console.log("Audio not supported or blocked by browser", e);
            }
        }

        /* --- PIN LOCKSCREEN SYSTEM --- */
        const CORRECT_PIN = "0799";
        let enteredPin = "";

        function pressKey(num) {
            if (enteredPin.length < 4) {
                enteredPin += num;
                updateDots();
                if (enteredPin.length === 4) setTimeout(checkPin, 150);
            }
        }

        function deleteKey() {
            if (enteredPin.length > 0) {
                enteredPin = enteredPin.slice(0, -1);
                updateDots();
            }
        }

        function clearKey() {
            enteredPin = "";
            updateDots();
        }

        function updateDots() {
            const dots = document.querySelectorAll('.pin-dots .dot');
            dots.forEach((dot, idx) => {
                if (idx < enteredPin.length) dot.classList.add('filled');
                else dot.classList.remove('filled', 'error');
            });
        }

        function checkPin() {
            const dots = document.querySelectorAll('.pin-dots .dot');
            if (enteredPin === CORRECT_PIN) {
                playUnlockSound();
                document.getElementById('pinLockscreen').classList.add('unlocked');
                showToast("Akses Diberikan", "Berhasil masuk ke dalam Vault");
            } else {
                dots.forEach(dot => dot.classList.add('error'));
                setTimeout(() => {
                    clearKey();
                }, 500);
            }
        }

        /* --- TOAST NOTIFICATION --- */
        function showToast(title, message) {
            const toast = document.getElementById('toastNotif');
            document.getElementById('toastTitle').innerText = title;
            document.getElementById('toastMessage').innerText = message;
            
            toast.classList.add('show');
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }

        /* --- VAULT STORAGE SYSTEM --- */
        let credentials = JSON.parse(localStorage.getItem('phoenix_vault_data')) || [
            { id: 1, platform: 'Google Account', user: 'rifaldo.nataniel.siregar@gmail.com', pass: 'p@ssw0rd123!', icon: 'fa-brands fa-google' },
            { id: 2, platform: 'GitHub', user: 'rifaldonst.dev.official@gmail.com', pass: 'git_secure_99', icon: 'fa-brands fa-github' },
            { id: 3, platform: 'Spotify Premium', user: 'rifaldo.music.listener@gmail.com', pass: 'music_fire_2026', icon: 'fa-brands fa-spotify' }
        ];

        function renderCredentials(dataToRender = credentials) {
            const listContainer = document.getElementById('credentialList');
            listContainer.innerHTML = '';

            if (dataToRender.length === 0) {
                listContainer.innerHTML = `<div style="text-align:center; color:var(--text-muted); padding:2rem;">Tidak ada kredensial yang ditemukan.</div>`;
                return;
            }

            dataToRender.forEach(item => {
                const card = document.createElement('div');
                card.className = 'credential-item';
                card.innerHTML = `
                    <div class="platform-col">
                        <div class="platform-icon"><i class="${item.icon || 'fas fa-globe'}"></i></div>
                        <span class="platform-name">${escapeHtml(item.platform)}</span>
                    </div>
                    <div class="user-col">
                        <span class="user-col-text">${escapeHtml(item.user)}</span>
                        <span class="quick-copy-email" onclick="copyToClipboard('${escapeJs(item.user)}', 'Email/Username')" title="Salin Email">
                            <i class="fas fa-copy"></i>
                        </span>
                    </div>
                    <div class="pass-col" id="pass-${item.id}">••••••••••••</div>
                    <div class="action-col">
                        <button class="action-btn" onclick="togglePasswordVisibility(${item.id}, '${escapeJs(item.pass)}')" title="Lihat/Sembunyikan">
                            <i class="fas fa-eye" id="eye-${item.id}"></i>
                        </button>
                        <button class="action-btn" onclick="copyToClipboard('${escapeJs(item.pass)}', 'Password')" title="Salin Password">
                            <i class="fas fa-clipboard"></i>
                        </button>
                        <button class="action-btn del" onclick="deleteCredential(${item.id})" title="Hapus">
                            <i class="fas fa-trash-can"></i>
                        </button>
                    </div>
                `;
                listContainer.appendChild(card);
            });
        }

        function addCredential(e) {
            e.preventDefault();
            const platform = document.getElementById('platformInput').value.trim();
            const user = document.getElementById('userInput').value.trim();
            const pass = document.getElementById('passInput').value.trim();

            if (!platform || !user || !pass) return;

            let icon = 'fas fa-globe';
            const lowerPlat = platform.toLowerCase();
            if (lowerPlat.includes('google')) icon = 'fa-brands fa-google';
            else if (lowerPlat.includes('github')) icon = 'fa-brands fa-github';
            else if (lowerPlat.includes('spotify')) icon = 'fa-brands fa-spotify';
            else if (lowerPlat.includes('facebook')) icon = 'fa-brands fa-facebook';
            else if (lowerPlat.includes('discord')) icon = 'fa-brands fa-discord';

            const newItem = { id: Date.now(), platform, user, pass, icon };

            credentials.unshift(newItem);
            saveAndRender();
            document.getElementById('vaultForm').reset();
            showToast("Berhasil Disimpan", `Kredensial ${platform} telah ditambahkan.`);
        }

        function deleteCredential(id) {
            credentials = credentials.filter(item => item.id !== id);
            saveAndRender();
            showToast("Dihapus", "Kredensial telah dihapus dari Vault.");
        }

        function togglePasswordVisibility(id, realPass) {
            const passElem = document.getElementById(`pass-${id}`);
            const eyeIcon = document.getElementById(`eye-${id}`);

            if (passElem.innerText === '••••••••••••') {
                passElem.innerText = realPass;
                eyeIcon.className = 'fas fa-eye-slash';
            } else {
                passElem.innerText = '••••••••••••';
                eyeIcon.className = 'fas fa-eye';
            }
        }

        function copyToClipboard(text, label) {
            navigator.clipboard.writeText(text).then(() => {
                showToast("Tersalin!", `${label} berhasil disalin ke clipboard.`);
            });
        }

        function filterCredentials() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = credentials.filter(item => 
                item.platform.toLowerCase().includes(query) || 
                item.user.toLowerCase().includes(query)
            );
            renderCredentials(filtered);
        }

        function saveAndRender() {
            localStorage.setItem('phoenix_vault_data', JSON.stringify(credentials));
            renderCredentials();
        }

        function escapeHtml(str) {
            return str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;").replace(/"/g, "&quot;").replace(/'/g, "&#039;");
        }

        function escapeJs(str) {
            return str.replace(/\\/g, '\\\\').replace(/'/g, "\\'");
        }

        /* --- BACKGROUND PARTICLES --- */
        const canvas = document.getElementById('spaceCanvas');
        const ctx = canvas.getContext('2d');
        let particles = [];

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            resizeMenuCanvas();
        }

        window.addEventListener('resize', resizeCanvas);

        class Particle {
            constructor() { this.reset(); }
            reset() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.size = Math.random() * 2 + 0.5;
                this.speedX = (Math.random() - 0.5) * 0.3;
                this.speedY = (Math.random() - 0.5) * 0.3;
                this.opacity = Math.random() * 0.7 + 0.2;
            }
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                if (this.x < 0 || this.x > canvas.width || this.y < 0 || this.y > canvas.height) this.reset();
            }
            draw() {
                ctx.fillStyle = `rgba(255, 200, 210, ${this.opacity})`;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        for (let i = 0; i < 80; i++) particles.push(new Particle());

        function animateCanvas() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach(p => { p.update(); p.draw(); });
            requestAnimationFrame(animateCanvas);
        }

        document.addEventListener('DOMContentLoaded', () => {
            document.getElementById('vaultForm').addEventListener('submit', addCredential);
            renderCredentials();
            resizeCanvas();
            initMenuFire();
            animateMenuFire();
            animateCanvas();
        });
    </script>
</body>
</html>
