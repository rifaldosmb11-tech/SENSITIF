<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PHOENIX VAULT | Living Fire Edition</title>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet">
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
            --card-glass: rgba(15, 2, 6, 0.88);
            --text-main: #fff0f3;
            --text-muted: #a38890;
            --danger: #ff2a2a;
            --transition-smooth: all 0.35s cubic-bezier(0.16, 1, 0.3, 1);
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
            overflow-x: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 2rem;
            position: relative;
        }

        /* --- SPACE CANVAS BACKGROUND --- */
        #spaceCanvas {
            position: fixed;
            top: 0; left: 0;
            width: 100vw; height: 100vh;
            z-index: 0;
            pointer-events: none;
        }

        /* --- NEBULA GLOW ORBS --- */
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
            opacity: 0.45;
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
            0% { transform: scale(1) translate(0, 0); opacity: 0.35; }
            50% { transform: scale(1.2) translate(50px, -40px); opacity: 0.55; }
            100% { transform: scale(0.95) translate(-30px, 40px); opacity: 0.4; }
        }

        /* --- FIRE ANIMATED BORDER WRAPPER --- */
        @property --fire-angle {
            syntax: '<angle>';
            initial-value: 0deg;
            inherits: false;
        }

        .fire-border-wrapper {
            position: relative;
            z-index: 2;
            width: 100%;
            max-width: 1240px;
            height: 800px;
            border-radius: 30px;
            padding: 3px;
            background: conic-gradient(
                from var(--fire-angle), 
                #ff003c 0deg, 
                #ff5400 60deg, 
                #ff0077 120deg, 
                #ffcc00 180deg, 
                #ff003c 240deg, 
                #ff5400 300deg, 
                #ff003c 360deg
            );
            animation: rotateFire 4s linear infinite, firePulse 2.5s ease-in-out infinite alternate;
            box-shadow: 
                0 0 25px rgba(255, 0, 60, 0.6),
                0 0 50px rgba(255, 84, 0, 0.4),
                0 0 80px rgba(255, 0, 119, 0.2);
        }

        @keyframes rotateFire {
            0% { --fire-angle: 0deg; }
            100% { --fire-angle: 360deg; }
        }

        @keyframes firePulse {
            0% { box-shadow: 0 0 20px rgba(255, 0, 60, 0.5), 0 0 40px rgba(255, 84, 0, 0.3); }
            100% { box-shadow: 0 0 35px rgba(255, 0, 60, 0.8), 0 0 70px rgba(255, 84, 0, 0.6), 0 0 110px rgba(255, 204, 0, 0.4); }
        }

        /* --- INNER DASHBOARD CONTAINER --- */
        .app-container {
            width: 100%;
            height: 100%;
            background: var(--card-glass);
            backdrop-filter: blur(35px);
            -webkit-backdrop-filter: blur(35px);
            border-radius: 27px;
            display: grid;
            grid-template-columns: 280px 1fr;
            overflow: hidden;
            position: relative;
        }

        /* --- SIDEBAR MENU WITH LIVING FIRE --- */
        aside.sidebar {
            background: rgba(8, 1, 3, 0.94);
            border-right: 1px solid rgba(255, 0, 60, 0.2);
            padding: 2.2rem 1.4rem;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            position: relative;
            z-index: 5;
            overflow: hidden;
        }

        /* CANVAS UNTUK PARTIKEL API MENU */
        #menuFireCanvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .brand-logo {
            display: flex;
            align-items: center;
            gap: 14px;
            padding-left: 0.4rem;
            margin-bottom: 3rem;
            position: relative;
            z-index: 2;
        }

        .logo-icon-wrapper {
            width: 48px; height: 48px;
            border-radius: 14px;
            background: linear-gradient(135deg, var(--accent-red), var(--accent-orange));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.4rem;
            color: #ffffff;
            box-shadow: 0 0 25px rgba(255, 0, 60, 0.8);
            animation: logoPulse 2.5s infinite alternate;
        }

        @keyframes logoPulse {
            0% { box-shadow: 0 0 15px rgba(255, 0, 60, 0.4); transform: scale(1); }
            100% { box-shadow: 0 0 35px rgba(255, 84, 0, 0.9); transform: scale(1.05); }
        }

        .brand-name {
            font-size: 1.3rem;
            font-weight: 800;
            letter-spacing: -0.5px;
            background: linear-gradient(to right, #fff, var(--accent-red));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .brand-tag {
            font-size: 0.65rem;
            color: var(--accent-red);
            letter-spacing: 2.5px;
            text-transform: uppercase;
            font-weight: 800;
            text-shadow: 0 0 8px rgba(255, 0, 60, 0.6);
        }

        /* MENU NAVIGASI DENGAN EFEK HIDUP & API BERKOBAR */
        .nav-wrapper {
            position: relative;
            z-index: 2;
        }

        .nav-menu {
            list-style: none;
            display: flex;
            flex-direction: column;
            gap: 14px;
            position: relative;
            z-index: 2;
        }

        /* SLIDER INDIKATOR DENGAN API PUDAR */
        .nav-indicator {
            position: absolute;
            left: 0;
            width: 100%;
            height: 52px;
            background: linear-gradient(90deg, rgba(255, 0, 60, 0.35), rgba(255, 84, 0, 0.15));
            border: 1px solid var(--accent-red);
            border-radius: 16px;
            box-shadow: 
                0 0 25px rgba(255, 0, 60, 0.6),
                inset 0 0 15px rgba(255, 84, 0, 0.4);
            pointer-events: none;
            transition: all 0.35s cubic-bezier(0.25, 1, 0.5, 1);
            opacity: 0;
            z-index: 1;
        }

        /* EFEK API LIFELIKE PADA SLIDER MENU */
        .nav-indicator::after {
            content: '';
            position: absolute;
            bottom: -4px;
            left: 10%;
            width: 80%;
            height: 8px;
            background: radial-gradient(ellipse at center, var(--accent-yellow), var(--accent-orange), transparent);
            filter: blur(4px);
            animation: flameFlicker 0.15s infinite alternate;
        }

        @keyframes flameFlicker {
            0% { opacity: 0.7; transform: scaleY(1) scaleX(0.95); }
            100% { opacity: 1; transform: scaleY(1.4) scaleX(1.05); }
        }

        .nav-item {
            position: relative;
            z-index: 3;
        }

        .nav-link {
            display: flex;
            align-items: center;
            gap: 16px;
            padding: 0.95rem 1.2rem;
            color: var(--text-muted);
            text-decoration: none;
            font-weight: 700;
            font-size: 0.92rem;
            border-radius: 16px;
            transition: var(--transition-smooth);
            position: relative;
        }

        .nav-link i {
            font-size: 1.15rem;
            transition: var(--transition-smooth);
        }

        /* ANIMASI MENAKJUBKAN SAAT MENU AKTIF/HOVER */
        .nav-item.active .nav-link,
        .nav-link:hover {
            color: #ffffff;
            text-shadow: 0 0 12px rgba(255, 255, 255, 0.9), 0 0 20px var(--accent-red);
        }

        .nav-item.active .nav-link i,
        .nav-link:hover i {
            color: var(--accent-yellow);
            transform: scale(1.3) rotate(6deg);
            filter: drop-shadow(0 0 12px var(--accent-orange)) drop-shadow(0 0 20px var(--accent-red));
            animation: iconJitter 0.2s infinite alternate;
        }

        @keyframes iconJitter {
            0% { transform: scale(1.28) rotate(4deg) translateY(0px); }
            100% { transform: scale(1.32) rotate(7deg) translateY(-2px); }
        }

        .sidebar-footer {
            position: relative;
            z-index: 2;
            padding: 1rem;
            background: rgba(255, 0, 60, 0.04);
            border-radius: 16px;
            border: 1px solid rgba(255, 0, 60, 0.18);
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 0.75rem;
            color: var(--text-muted);
        }

        .shield-icon {
            color: var(--accent-red);
            font-size: 1.2rem;
            animation: pulseGlow 2s infinite alternate;
        }

        @keyframes pulseGlow {
            from { opacity: 0.6; }
            to { opacity: 1; filter: drop-shadow(0 0 8px var(--accent-red)); }
        }

        /* --- MAIN CONTENT --- */
        main.main-content {
            padding: 2.5rem 3rem;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 2rem;
        }

        main.main-content::-webkit-scrollbar { width: 5px; }
        main.main-content::-webkit-scrollbar-thumb {
            background: rgba(255, 0, 60, 0.4);
            border-radius: 10px;
        }

        /* TOP BAR */
        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .page-title h2 {
            font-size: 1.6rem;
            font-weight: 800;
            letter-spacing: -0.5px;
            color: #fff;
            text-shadow: 0 0 12px rgba(255, 0, 60, 0.4);
        }

        .page-title p {
            font-size: 0.85rem;
            color: var(--text-muted);
            margin-top: 2px;
        }

        .user-profile {
            display: flex;
            align-items: center;
            gap: 14px;
            background: rgba(255, 0, 60, 0.05);
            padding: 6px 16px 6px 8px;
            border-radius: 30px;
            border: 1px solid rgba(255, 0, 60, 0.25);
        }

        .avatar {
            width: 38px; height: 38px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--accent-red), var(--accent-orange));
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 0.85rem;
            border: 2px solid var(--accent-red);
            box-shadow: 0 0 12px rgba(255, 0, 60, 0.6);
        }

        .user-info { line-height: 1.2; }
        .user-name { font-size: 0.85rem; font-weight: 700; }
        .user-status { font-size: 0.7rem; color: var(--accent-red); font-weight: 600; }

        /* FORM CARD */
        .form-card {
            background: rgba(20, 3, 7, 0.6);
            border: 1px solid rgba(255, 0, 60, 0.25);
            border-radius: 20px;
            padding: 1.8rem;
            box-shadow: 0 10px 30px rgba(0,0,0,0.6);
            position: relative;
        }

        .card-header-title {
            font-size: 1rem;
            font-weight: 700;
            margin-bottom: 1.2rem;
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--accent-red);
            text-shadow: 0 0 10px rgba(255, 0, 60, 0.5);
        }

        .form-grid {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr 180px;
            gap: 1rem;
            align-items: center;
        }

        .input-group { position: relative; }

        .input-group i {
            position: absolute;
            left: 14px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-muted);
            transition: var(--transition-smooth);
        }

        .input-group input {
            width: 100%;
            padding: 0.85rem 1rem 0.85rem 2.8rem;
            background: rgba(8, 0, 2, 0.8);
            border: 1px solid rgba(255, 0, 60, 0.18);
            border-radius: 12px;
            color: #fff;
            font-size: 0.88rem;
            transition: var(--transition-smooth);
        }

        .input-group input:focus {
            outline: none;
            border-color: var(--accent-red);
            box-shadow: 0 0 20px rgba(255, 0, 60, 0.4);
            background: rgba(15, 0, 4, 0.95);
        }

        .input-group input:focus + i { color: var(--accent-red); }

        .btn-glow {
            width: 100%;
            padding: 0.85rem;
            border: none;
            border-radius: 12px;
            background: linear-gradient(135deg, var(--accent-red), var(--accent-orange));
            color: #fff;
            font-weight: 800;
            font-size: 0.85rem;
            cursor: pointer;
            transition: var(--transition-smooth);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            box-shadow: 0 0 20px rgba(255, 0, 60, 0.5);
        }

        .btn-glow:hover {
            transform: translateY(-2px);
            box-shadow: 0 0 35px rgba(255, 0, 60, 0.85);
            background: linear-gradient(135deg, var(--accent-orange), var(--accent-pink));
        }

        /* VAULT LIST SECTION */
        .vault-section {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .vault-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .vault-header h3 { font-size: 1.1rem; font-weight: 700; }

        .search-box {
            position: relative;
            width: 240px;
        }

        .search-box input {
            width: 100%;
            padding: 0.55rem 1rem 0.55rem 2.2rem;
            background: rgba(255, 0, 60, 0.04);
            border: 1px solid rgba(255, 0, 60, 0.2);
            border-radius: 20px;
            color: #fff;
            font-size: 0.8rem;
            transition: var(--transition-smooth);
        }

        .search-box input:focus {
            outline: none;
            border-color: var(--accent-red);
            box-shadow: 0 0 15px rgba(255, 0, 60, 0.35);
        }

        .search-box i {
            position: absolute;
            left: 12px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 0.75rem;
            color: var(--text-muted);
        }

        .credential-list {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .credential-item {
            background: rgba(18, 2, 6, 0.6);
            border: 1px solid rgba(255, 0, 60, 0.15);
            border-radius: 16px;
            padding: 1rem 1.4rem;
            display: grid;
            grid-template-columns: 2fr 2fr 1.5fr 140px;
            align-items: center;
            transition: var(--transition-smooth);
        }

        .credential-item:hover {
            border-color: rgba(255, 0, 60, 0.6);
            background: rgba(28, 3, 9, 0.85);
            transform: scale(1.008) translateY(-2px);
            box-shadow: 0 10px 30px rgba(255, 0, 60, 0.25);
        }

        .platform-col {
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: 700;
        }

        .platform-icon {
            width: 40px; height: 40px;
            border-radius: 12px;
            background: rgba(255, 0, 60, 0.12);
            border: 1px solid rgba(255, 0, 60, 0.3);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--accent-red);
            font-size: 1.15rem;
            box-shadow: 0 0 12px rgba(255, 0, 60, 0.2);
        }

        .user-col { color: var(--text-muted); font-size: 0.88rem; word-break: break-all; }
        .pass-col { font-family: 'JetBrains Mono', monospace; letter-spacing: 2px; font-size: 0.9rem; }

        .action-col {
            display: flex;
            justify-content: flex-end;
            gap: 8px;
        }

        .action-btn {
            width: 36px; height: 36px;
            border-radius: 10px;
            border: 1px solid rgba(255, 0, 60, 0.2);
            background: rgba(255, 0, 60, 0.05);
            color: var(--text-muted);
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: var(--transition-smooth);
            font-size: 0.85rem;
        }

        .action-btn:hover {
            color: #fff;
            border-color: var(--accent-red);
            background: rgba(255, 0, 60, 0.35);
            box-shadow: 0 0 15px rgba(255, 0, 60, 0.5);
        }

        .action-btn.del:hover {
            border-color: var(--danger);
            background: rgba(255, 42, 42, 0.4);
            color: #fff;
            box-shadow: 0 0 18px rgba(255, 42, 42, 0.8);
        }

        @media (max-width: 1024px) {
            .fire-border-wrapper { height: auto; }
            .app-container { grid-template-columns: 220px 1fr; }
            .form-grid { grid-template-columns: 1fr 1fr; }
            .btn-glow { grid-column: span 2; }
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

    <!-- SPACE ANIMATED CANVAS -->
    <canvas id="spaceCanvas"></canvas>

    <!-- NEBULA BACKGROUND ORBS -->
    <div class="bg-glow-container">
        <div class="nebula-orb nebula-1"></div>
        <div class="nebula-orb nebula-2"></div>
    </div>

    <!-- FIRE BORDER CONTAINER WRAPPER -->
    <div class="fire-border-wrapper">
        <div class="app-container">

            <!-- SIDEBAR MENU WITH LIVING FIRE -->
            <aside class="sidebar" id="sidebarContainer">
                <canvas id="menuFireCanvas"></canvas>

                <div>
                    <div class="brand-logo">
                        <div class="logo-icon-wrapper">
                            <i class="fas fa-shield-halved"></i>
                        </div>
                        <div>
                            <div class="brand-name">PHOENIX</div>
                            <div class="brand-tag">RED VAULT</div>
                        </div>
                    </div>

                    <div class="nav-wrapper">
                        <div class="nav-indicator" id="navIndicator"></div>
                        <ul class="nav-menu" id="navMenu">
                            <li class="nav-item active">
                                <a href="#" class="nav-link">
                                    <i class="fas fa-chart-pie"></i>
                                    <span>Dashboard</span>
                                </a>
                            </li>
                            <li class="nav-item">
                                <a href="#" class="nav-link">
                                    <i class="fas fa-vault"></i>
                                    <span>Credentials Vault</span>
                                </a>
                            </li>
                        </ul>
                    </div>
                </div>

                <div class="sidebar-footer">
                    <i class="fas fa-lock shield-icon"></i>
                    <div>
                        <div style="font-weight:700; color:#fff;">AES-256 GCM</div>
                        <div>Cosmic Hardware Active</div>
                    </div>
                </div>
            </aside>

            <!-- MAIN CONTENT AREA -->
            <main class="main-content">

                <!-- TOP BAR -->
                <div class="top-bar">
                    <div class="page-title">
                        <h2>Vault Operations</h2>
                        <p>Encrypted Space Security Platform</p>
                    </div>
                    <div class="user-profile">
                        <div class="avatar">AR</div>
                        <div class="user-info">
                            <div class="user-name">Alexis Reed</div>
                            <div class="user-status"><i class="fas fa-circle" style="font-size:0.5rem;"></i> SECURED</div>
                        </div>
                    </div>
                </div>

                <!-- SEAL FORM CARD -->
                <div class="form-card">
                    <div class="card-header-title">
                        <i class="fas fa-plus-circle"></i>
                        Seal Asset Credential
                    </div>
                    <form id="vaultForm">
                        <div class="form-grid">
                            <div class="input-group">
                                <input type="text" id="platform" placeholder="Platform (e.g. Google, AWS)" required>
                                <i class="fas fa-globe"></i>
                            </div>
                            <div class="input-group">
                                <input type="text" id="email" placeholder="Username / Email" required>
                                <i class="fas fa-user-shield"></i>
                            </div>
                            <div class="input-group">
                                <input type="password" id="password" placeholder="Access Password" required>
                                <i class="fas fa-key"></i>
                            </div>
                            <button type="submit" class="btn-glow">
                                <i class="fas fa-lock"></i>
                                SEAL ASSET
                            </button>
                        </div>
                    </form>
                </div>

                <!-- CREDENTIAL LIST -->
                <div class="vault-section">
                    <div class="vault-header">
                        <h3>Secured Assets (<span id="assetCount">0</span>)</h3>
                        <div class="search-box">
                            <i class="fas fa-search"></i>
                            <input type="text" id="searchInput" placeholder="Search assets...">
                        </div>
                    </div>

                    <div class="credential-list" id="credentialList">
                        <!-- Dynamic rendering -->
                    </div>
                </div>

            </main>
        </div>
    </div>

    <script>
        // --- 1. ANIMASI PARTIKEL API MENU BERKOBAR (INTERACTIVE MENU FIRE) ---
        const fireCanvas = document.getElementById('menuFireCanvas');
        const fireCtx = fireCanvas.getContext('2d');
        const sidebar = document.getElementById('sidebarContainer');
        let fireParticles = [];
        let activeMenuY = 0;
        let isHoveringMenu = false;

        function resizeFireCanvas() {
            fireCanvas.width = sidebar.offsetWidth;
            fireCanvas.height = sidebar.offsetHeight;
        }
        window.addEventListener('resize', resizeFireCanvas);
        resizeFireCanvas();

        class FireEmber {
            constructor(yPos) {
                this.reset(yPos);
            }

            reset(yPos) {
                this.x = Math.random() * (sidebar.offsetWidth - 40) + 20;
                this.y = yPos + Math.random() * 20 - 10;
                this.size = Math.random() * 3 + 1.5;
                this.speedY = Math.random() * 1.5 + 0.8;
                this.speedX = (Math.random() - 0.5) * 1.2;
                this.alpha = Math.random() * 0.9 + 0.3;
                this.color = Math.random() > 0.4 ? '#ffcc00' : (Math.random() > 0.5 ? '#ff5400' : '#ff003c');
            }

            update(yPos) {
                this.y -= this.speedY;
                this.x += this.speedX;
                this.alpha -= 0.02;

                if (this.alpha <= 0 || this.y < yPos - 60) {
                    this.reset(yPos);
                }
            }

            draw() {
                fireCtx.beginPath();
                fireCtx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                fireCtx.fillStyle = this.color;
                fireCtx.globalAlpha = Math.max(0, this.alpha);
                fireCtx.shadowBlur = 10;
                fireCtx.shadowColor = this.color;
                fireCtx.fill();
                fireCtx.shadowBlur = 0;
            }
        }

        for (let i = 0; i < 40; i++) {
            fireParticles.push(new FireEmber(200));
        }

        function animateMenuFire() {
            fireCtx.clearRect(0, 0, fireCanvas.width, fireCanvas.height);
            
            if (activeMenuY > 0) {
                fireParticles.forEach(p => {
                    p.update(activeMenuY);
                    p.draw();
                });
            }
            requestAnimationFrame(animateMenuFire);
        }
        animateMenuFire();

        // --- 2. SIDEBAR MENU HOVER & SLIDER LOGIC ---
        const navMenu = document.getElementById('navMenu');
        const navItems = document.querySelectorAll('.nav-item');
        const indicator = document.getElementById('navIndicator');

        function updateMenuFirePosition(element) {
            if (!element) return;
            const rect = element.getBoundingClientRect();
            const sidebarRect = sidebar.getBoundingClientRect();
            activeMenuY = rect.bottom - sidebarRect.top;
        }

        function moveIndicator(element) {
            if (!element) return;
            const rect = element.getBoundingClientRect();
            const parentRect = navMenu.getBoundingClientRect();
            const topOffset = rect.top - parentRect.top;

            indicator.style.opacity = '1';
            indicator.style.transform = `translateY(${topOffset}px)`;
            indicator.style.height = `${rect.height}px`;

            updateMenuFirePosition(element);
        }

        const activeItem = document.querySelector('.nav-item.active');
        if (activeItem) {
            moveIndicator(activeItem);
        }

        navItems.forEach(item => {
            item.addEventListener('mouseenter', () => moveIndicator(item));
            item.addEventListener('click', (e) => {
                e.preventDefault();
                navItems.forEach(i => i.classList.remove('active'));
                item.classList.add('active');
                moveIndicator(item);
            });
        });

        navMenu.addEventListener('mouseleave', () => {
            const currentActive = document.querySelector('.nav-item.active');
            if (currentActive) moveIndicator(currentActive);
        });

        // --- 3. SPACE CANVAS ANIMATION ---
        const canvas = document.getElementById('spaceCanvas');
        const ctx = canvas.getContext('2d');
        let width, height;
        let stars = [], meteors = [];

        function resizeSpaceCanvas() {
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeSpaceCanvas);
        resizeSpaceCanvas();

        class Star {
            constructor() { this.reset(); }
            reset() {
                this.x = (Math.random() - 0.5) * width * 2;
                this.y = (Math.random() - 0.5) * height * 2;
                this.z = Math.random() * width;
                this.size = Math.random() * 1.5 + 0.5;
                this.color = Math.random() > 0.4 ? '#ff003c' : (Math.random() > 0.5 ? '#ff5400' : '#ffffff');
            }
            update() {
                this.z -= 1.8;
                if (this.z <= 0) { this.reset(); this.z = width; }
            }
            draw() {
                const k = 256 / this.z;
                const px = this.x * k + width / 2;
                const py = this.y * k + height / 2;
                if (px >= 0 && px <= width && py >= 0 && py <= height) {
                    const size = Math.max(0.1, (1 - this.z / width) * 2.5 * this.size);
                    const alpha = Math.min(1, (1 - this.z / width) * 1.2);
                    ctx.beginPath();
                    ctx.arc(px, py, size, 0, Math.PI * 2);
                    ctx.fillStyle = this.color;
                    ctx.globalAlpha = alpha;
                    ctx.shadowBlur = 8;
                    ctx.shadowColor = this.color;
                    ctx.fill();
                    ctx.shadowBlur = 0;
                }
            }
        }

        class Meteor {
            constructor() { this.reset(); }
            reset() {
                this.x = Math.random() * width + width * 0.3;
                this.y = Math.random() * -height * 0.5;
                this.length = Math.random() * 80 + 40;
                this.speed = Math.random() * 10 + 12;
                this.alpha = Math.random() * 0.8 + 0.2;
            }
            update() {
                this.x -= this.speed;
                this.y += this.speed * 0.6;
                if (this.x < -100 || this.y > height + 100) { this.reset(); }
            }
            draw() {
                ctx.beginPath();
                const grad = ctx.createLinearGradient(this.x, this.y, this.x + this.length, this.y - this.length * 0.6);
                grad.addColorStop(0, 'rgba(255, 0, 60, ' + this.alpha + ')');
                grad.addColorStop(0.5, 'rgba(255, 84, 0, ' + (this.alpha * 0.5) + ')');
                grad.addColorStop(1, 'rgba(255, 255, 255, 0)');
                ctx.strokeStyle = grad;
                ctx.lineWidth = 2;
                ctx.moveTo(this.x, this.y);
                ctx.lineTo(this.x + this.length, this.y - this.length * 0.6);
                ctx.stroke();
            }
        }

        for (let i = 0; i < 280; i++) stars.push(new Star());
        for (let i = 0; i < 4; i++) meteors.push(new Meteor());

        function animateSpace() {
            ctx.clearRect(0, 0, width, height);
            const bgGrad = ctx.createRadialGradient(width/2, height/2, 100, width/2, height/2, width*0.8);
            bgGrad.addColorStop(0, '#0a0104');
            bgGrad.addColorStop(1, '#020001');
            ctx.fillStyle = bgGrad;
            ctx.globalAlpha = 1;
            ctx.fillRect(0, 0, width, height);

            stars.forEach(star => { star.update(); star.draw(); });
            meteors.forEach(meteor => { meteor.update(); meteor.draw(); });

            requestAnimationFrame(animateSpace);
        }
        animateSpace();

        // --- 4. CREDENTIALS VAULT LOGIC ---
        function getPlatformIcon(platform) {
            const p = platform.toLowerCase();
            if (p.includes('google') || p.includes('gmail')) return 'fab fa-google';
            if (p.includes('aws') || p.includes('amazon')) return 'fab fa-amazon';
            if (p.includes('facebook')) return 'fab fa-facebook-f';
            if (p.includes('twitter') || p.includes('x')) return 'fab fa-x-twitter';
            if (p.includes('github')) return 'fab fa-github';
            if (p.includes('microsoft')) return 'fab fa-microsoft';
            if (p.includes('apple')) return 'fab fa-apple';
            return 'fas fa-shield-cat';
        }

        const vaultForm = document.getElementById('vaultForm');
        const credentialList = document.getElementById('credentialList');
        const assetCount = document.getElementById('assetCount');
        const searchInput = document.getElementById('searchInput');

        vaultForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const platform = document.getElementById('platform').value;
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;

            const newAsset = { id: Date.now(), platform, email, password };
            let assets = JSON.parse(localStorage.getItem('spaceVaultCrimson')) || [];
            assets.push(newAsset);
            localStorage.setItem('spaceVaultCrimson', JSON.stringify(assets));

            vaultForm.reset();
            renderAssets();
            showToast('Asset Sealed in Living Fire Vault!');
        });

        function renderAssets(filter = '') {
            let assets = JSON.parse(localStorage.getItem('spaceVaultCrimson')) || [];
            credentialList.innerHTML = '';

            const filteredAssets = assets.filter(a => 
                a.platform.toLowerCase().includes(filter.toLowerCase()) || 
                a.email.toLowerCase().includes(filter.toLowerCase())
            );

            assetCount.textContent = filteredAssets.length;

            if (filteredAssets.length === 0) {
                credentialList.innerHTML = `
                    <div style="text-align:center; padding: 3rem; color: var(--text-muted); background: rgba(255,0,60,0.02); border-radius: 16px; border: 1px dashed rgba(255,0,60,0.2);">
                        <i class="fas fa-box-open" style="font-size:2.2rem; margin-bottom:12px; color:var(--accent-red);"></i>
                        <div>Vault empty or no matching cosmic asset found.</div>
                    </div>`;
                return;
            }

            filteredAssets.forEach(item => {
                const iconClass = getPlatformIcon(item.platform);
                const el = document.createElement('div');
                el.className = 'credential-item';
                el.innerHTML = `
                    <div class="platform-col">
                        <div class="platform-icon"><i class="${iconClass}"></i></div>
                        <span>${item.platform}</span>
                    </div>
                    <div class="user-col">${item.email}</div>
                    <div class="pass-col" id="pass-${item.id}">••••••••••••</div>
                    <div class="action-col">
                        <button class="action-btn" onclick="togglePassword(${item.id}, '${item.password}')" title="Toggle Password">
                            <i class="fas fa-eye" id="eye-${item.id}"></i>
                        </button>
                        <button class="action-btn" onclick="copyToClipboard('${item.email}')" title="Copy Email">
                            <i class="fas fa-user"></i>
                        </button>
                        <button class="action-btn" onclick="copyToClipboard('${item.password}')" title="Copy Password">
                            <i class="fas fa-key"></i>
                        </button>
                        <button class="action-btn del" onclick="deleteAsset(${item.id})" title="Purge Asset">
                            <i class="fas fa-trash"></i>
                        </button>
                    </div>
                `;
                credentialList.appendChild(el);
            });
        }

        function togglePassword(id, realPass) {
            const passEl = document.getElementById(`pass-${id}`);
            const eyeEl = document.getElementById(`eye-${id}`);
            if (passEl.textContent === '••••••••••••') {
                passEl.textContent = realPass;
                passEl.style.color = 'var(--accent-red)';
                eyeEl.className = 'fas fa-eye-slash';
            } else {
                passEl.textContent = '••••••••••••';
                passEl.style.color = 'inherit';
                eyeEl.className = 'fas fa-eye';
            }
        }

        function copyToClipboard(text) {
            navigator.clipboard.writeText(text);
            showToast('Copied to Clipboard!');
        }

        function deleteAsset(id) {
            let assets = JSON.parse(localStorage.getItem('spaceVaultCrimson')) || [];
            assets = assets.filter(a => a.id !== id);
            localStorage.setItem('spaceVaultCrimson', JSON.stringify(assets));
            renderAssets(searchInput.value);
            showToast('Asset Purged Permanently!', '#ff2a2a');
        }

        searchInput.addEventListener('input', (e) => { renderAssets(e.target.value); });

        function showToast(msg, bg = 'var(--accent-red)') {
            const toast = document.createElement('div');
            toast.style.cssText = `
                position: fixed; bottom: 30px; right: 30px;
                background: ${bg}; color: #ffffff;
                padding: 12px 24px; border-radius: 12px; font-weight: 800;
                font-size: 0.85rem; box-shadow: 0 0 25px rgba(255, 0, 60, 0.6);
                z-index: 9999; transform: translateY(20px); opacity: 0;
                transition: all 0.3s ease;
            `;
            toast.textContent = msg;
            document.body.appendChild(toast);
            setTimeout(() => { toast.style.transform = 'translateY(0)'; toast.style.opacity = '1'; }, 50);
            setTimeout(() => {
                toast.style.transform = 'translateY(20px)'; toast.style.opacity = '0';
                setTimeout(() => document.body.removeChild(toast), 300);
            }, 2500);
        }

        // Init Sample Data
        if (!localStorage.getItem('spaceVaultCrimson')) {
            const samples = [
                { id: 1, platform: 'Google Cloud', email: 'alexis.reed@gmail.com', password: 'p@ssw0rd_Cyber2026!' },
                { id: 2, platform: 'AWS Security', email: 'aws.root@cube.io', password: 'SecretKey_#909012' }
            ];
            localStorage.setItem('spaceVaultCrimson', JSON.stringify(samples));
        }

        renderAssets();
    </script>
</body>
</html>
