<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PHOENIX VAULT | Ultra-Premium Cyber Armor</title>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- FontAwesome Pro / Free Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --bg-dark: #030712;
            --accent-cyan: #00f2fe;
            --accent-blue: #4facfe;
            --accent-purple: #9d4edd;
            --accent-magenta: #f72585;
            --card-glass: rgba(15, 23, 42, 0.65);
            --card-border: rgba(0, 242, 254, 0.22);
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --danger: #ff4757;
            --transition-smooth: all 0.35s cubic-bezier(0.4, 0, 0.2, 1);
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

        /* --- ANIMATED BACKGROUND GLOW ORBS --- */
        .bg-glow-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: 0;
            overflow: hidden;
            pointer-events: none;
        }

        .glow-orb {
            position: absolute;
            border-radius: 50%;
            filter: blur(100px);
            opacity: 0.45;
            animation: floatGlow 18s ease-in-out infinite alternate;
        }

        .glow-orb-1 {
            width: 500px;
            height: 500px;
            background: radial-gradient(circle, var(--accent-cyan), var(--accent-blue));
            top: -100px;
            left: -100px;
            animation-duration: 16s;
        }

        .glow-orb-2 {
            width: 600px;
            height: 600px;
            background: radial-gradient(circle, var(--accent-magenta), var(--accent-purple));
            bottom: -150px;
            right: -150px;
            animation-duration: 22s;
            animation-delay: -5s;
        }

        .glow-orb-3 {
            width: 400px;
            height: 400px;
            background: radial-gradient(circle, #3a0ca3, var(--accent-cyan));
            top: 40%;
            left: 50%;
            transform: translate(-50%, -50%);
            animation-duration: 20s;
            animation-delay: -10s;
        }

        @keyframes floatGlow {
            0% { transform: translate(0, 0) scale(1) rotate(0deg); }
            33% { transform: translate(80px, -60px) scale(1.15) rotate(120deg); }
            66% { transform: translate(-50px, 70px) scale(0.9) rotate(240deg); }
            100% { transform: translate(40px, 50px) scale(1.1) rotate(360deg); }
        }

        /* Ambient Animated Grid Overlay */
        .grid-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-image: 
                linear-gradient(rgba(0, 242, 254, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 242, 254, 0.03) 1px, transparent 1px);
            background-size: 50px 50px;
            z-index: 1;
            pointer-events: none;
        }

        /* --- DASHBOARD CONTAINER WRAPPER --- */
        .app-container {
            position: relative;
            z-index: 2;
            width: 100%;
            max-width: 1280px;
            height: 820px;
            background: var(--card-glass);
            backdrop-filter: blur(25px);
            -webkit-backdrop-filter: blur(25px);
            border-radius: 24px;
            border: 1px solid var(--card-border);
            box-shadow: 
                0 30px 60px rgba(0, 0, 0, 0.6),
                0 0 40px rgba(0, 242, 254, 0.15),
                inset 0 0 20px rgba(255, 255, 255, 0.05);
            display: grid;
            grid-template-columns: 280px 1fr;
            overflow: hidden;
            animation: containerAppear 0.8s ease-out;
        }

        @keyframes containerAppear {
            from { opacity: 0; transform: scale(0.96) translateY(20px); }
            to { opacity: 1; transform: scale(1) translateY(0); }
        }

        /* --- SIDEBAR MENU (ULTRA-PREMIUM UPGRADE) --- */
        aside.sidebar {
            background: rgba(6, 10, 20, 0.85);
            border-right: 1px solid rgba(0, 242, 254, 0.12);
            padding: 2.2rem 1.2rem;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            position: relative;
            z-index: 5;
        }

        .brand-logo {
            display: flex;
            align-items: center;
            gap: 14px;
            padding-left: 0.5rem;
            margin-bottom: 2.5rem;
        }

        .logo-icon-wrapper {
            width: 46px;
            height: 46px;
            border-radius: 14px;
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-magenta));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.4rem;
            color: #030712;
            box-shadow: 0 0 20px rgba(0, 242, 254, 0.6);
            animation: logoPulse 3s infinite alternate;
        }

        @keyframes logoPulse {
            0% { box-shadow: 0 0 15px rgba(0, 242, 254, 0.4); }
            100% { box-shadow: 0 0 30px rgba(247, 37, 133, 0.8); }
        }

        .brand-name {
            font-size: 1.3rem;
            font-weight: 800;
            letter-spacing: -0.5px;
            background: linear-gradient(to right, #fff, var(--accent-cyan));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .brand-tag {
            font-size: 0.65rem;
            color: var(--accent-cyan);
            letter-spacing: 2.5px;
            text-transform: uppercase;
            font-weight: 800;
        }

        .nav-menu {
            list-style: none;
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .nav-item {
            position: relative;
            border-radius: 16px;
        }

        /* NAV LINK EFEK PREMIUM GLASS & GRADIENT BORDER */
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
            position: relative;
            overflow: hidden;
            z-index: 1;
            background: rgba(255, 255, 255, 0.02);
            border: 1px solid rgba(255, 255, 255, 0.04);
            transition: var(--transition-smooth);
        }

        /* EFEK HOVER: GRADIENT BORDER & GLOW MOVING BACKGROUND */
        .nav-link::before {
            content: '';
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(135deg, rgba(0, 242, 254, 0.2), rgba(247, 37, 133, 0.2), rgba(157, 78, 221, 0.2));
            background-size: 200% 200%;
            opacity: 0;
            z-index: -1;
            transition: opacity 0.35s ease;
            animation: rainbowMove 4s ease infinite;
        }

        @keyframes rainbowMove {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .nav-link:hover::before, .nav-item.active .nav-link::before {
            opacity: 1;
        }

        .nav-link:hover, .nav-item.active .nav-link {
            color: #ffffff;
            border-color: rgba(0, 242, 254, 0.4);
            box-shadow: 0 8px 25px rgba(0, 242, 254, 0.2);
            text-shadow: 0 0 12px rgba(255, 255, 255, 0.8);
            transform: translateX(4px) scale(1.02);
        }

        .nav-link i {
            font-size: 1.15rem;
            transition: var(--transition-smooth);
        }

        .nav-link:hover i, .nav-item.active .nav-link i {
            color: var(--accent-cyan);
            transform: scale(1.2) rotate(6deg);
            filter: drop-shadow(0 0 8px var(--accent-cyan));
        }

        /* INDIKATOR AKTIF KIRI */
        .nav-item.active::after {
            content: '';
            position: absolute;
            left: -4px; top: 15%; height: 70%; width: 5px;
            background: linear-gradient(to bottom, var(--accent-cyan), var(--accent-magenta));
            border-radius: 4px;
            box-shadow: 0 0 15px var(--accent-cyan);
        }

        /* PARTIKEL WARNA-WARNI UNTUK MENU */
        .menu-particle {
            position: absolute;
            pointer-events: none;
            border-radius: 50%;
            animation: floatParticle 0.7s cubic-bezier(0.1, 0.8, 0.3, 1) forwards;
            z-index: 20;
        }

        @keyframes floatParticle {
            0% {
                opacity: 1;
                transform: translate(0, 0) scale(1);
            }
            100% {
                opacity: 0;
                transform: translate(var(--dx), var(--dy)) scale(0);
            }
        }

        .sidebar-footer {
            padding: 1rem;
            background: rgba(255, 255, 255, 0.03);
            border-radius: 16px;
            border: 1px solid rgba(0, 242, 254, 0.15);
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 0.75rem;
            color: var(--text-muted);
            box-shadow: inset 0 0 15px rgba(0, 0, 0, 0.5);
        }

        .shield-icon {
            color: #4ade80;
            font-size: 1.1rem;
            animation: pulseGlow 2s infinite alternate;
        }

        @keyframes pulseGlow {
            from { opacity: 0.5; }
            to { opacity: 1; text-shadow: 0 0 12px #4ade80; }
        }

        /* --- MAIN CONTENT AREA --- */
        main.main-content {
            padding: 2.2rem 3rem;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 2rem;
        }

        /* Custom Scrollbar */
        main.main-content::-webkit-scrollbar {
            width: 6px;
        }
        main.main-content::-webkit-scrollbar-thumb {
            background: rgba(0, 242, 254, 0.2);
            border-radius: 10px;
        }

        /* TOP HEADER BAR */
        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .page-title h2 {
            font-size: 1.6rem;
            font-weight: 700;
            color: #fff;
        }

        .page-title p {
            font-size: 0.85rem;
            color: var(--text-muted);
        }

        .user-profile {
            display: flex;
            align-items: center;
            gap: 14px;
            background: rgba(255,255,255,0.03);
            padding: 6px 14px 6px 8px;
            border-radius: 30px;
            border: 1px solid rgba(255,255,255,0.08);
        }

        .avatar {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--accent-magenta), var(--accent-purple));
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 0.85rem;
            border: 2px solid var(--accent-cyan);
        }

        .user-info { line-height: 1.2; }
        .user-name { font-size: 0.85rem; font-weight: 700; }
        .user-status { font-size: 0.7rem; color: #4ade80; }

        /* FORM ASSET CARD */
        .form-card {
            background: rgba(15, 23, 42, 0.4);
            border: 1px solid rgba(0, 242, 254, 0.15);
            border-radius: 18px;
            padding: 1.8rem;
            position: relative;
            overflow: hidden;
        }

        .card-header-title {
            font-size: 1rem;
            font-weight: 700;
            margin-bottom: 1.2rem;
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--accent-cyan);
        }

        .form-grid {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr 180px;
            gap: 1rem;
            align-items: center;
        }

        .input-group {
            position: relative;
        }

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
            background: rgba(3, 7, 18, 0.6);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            color: #fff;
            font-size: 0.88rem;
            transition: var(--transition-smooth);
        }

        .input-group input:focus {
            outline: none;
            border-color: var(--accent-cyan);
            box-shadow: 0 0 15px rgba(0, 242, 254, 0.25);
            background: rgba(3, 7, 18, 0.9);
        }

        .input-group input:focus + i {
            color: var(--accent-cyan);
        }

        /* GLOWING SUBMIT BUTTON */
        .btn-glow {
            width: 100%;
            padding: 0.85rem;
            border: none;
            border-radius: 12px;
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-blue));
            color: #030712;
            font-weight: 800;
            font-size: 0.85rem;
            cursor: pointer;
            transition: var(--transition-smooth);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            box-shadow: 0 0 15px rgba(0, 242, 254, 0.3);
        }

        .btn-glow:hover {
            transform: translateY(-2px);
            box-shadow: 0 0 30px rgba(0, 242, 254, 0.6);
            background: linear-gradient(135deg, #00f2fe, #f72585);
            color: #fff;
        }

        /* CREDENTIALS ASSETS GRID */
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
            padding: 0.5rem 1rem 0.5rem 2.2rem;
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 20px;
            color: #fff;
            font-size: 0.8rem;
        }

        .search-box i {
            position: absolute;
            left: 10px;
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
            background: rgba(15, 23, 42, 0.4);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 14px;
            padding: 1rem 1.4rem;
            display: grid;
            grid-template-columns: 2fr 2fr 1.5fr 140px;
            align-items: center;
            transition: var(--transition-smooth);
        }

        .credential-item:hover {
            border-color: rgba(0, 242, 254, 0.3);
            background: rgba(15, 23, 42, 0.7);
            transform: scale(1.01);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
        }

        .platform-col {
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: 700;
        }

        .platform-icon {
            width: 38px;
            height: 38px;
            border-radius: 10px;
            background: rgba(0, 242, 254, 0.1);
            border: 1px solid rgba(0, 242, 254, 0.2);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--accent-cyan);
            font-size: 1.1rem;
        }

        .user-col { color: var(--text-muted); font-size: 0.88rem; word-break: break-all; }
        .pass-col { font-family: monospace; letter-spacing: 2px; font-size: 0.95rem; }

        .action-col {
            display: flex;
            justify-content: flex-end;
            gap: 8px;
        }

        .action-btn {
            width: 34px;
            height: 34px;
            border-radius: 8px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            background: rgba(255, 255, 255, 0.03);
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
            border-color: var(--accent-cyan);
            background: rgba(0, 242, 254, 0.15);
            box-shadow: 0 0 10px rgba(0, 242, 254, 0.3);
        }

        .action-btn.del:hover {
            border-color: var(--danger);
            background: rgba(255, 71, 87, 0.15);
            color: var(--danger);
            box-shadow: 0 0 10px rgba(255, 71, 87, 0.3);
        }

        /* RESPONSIVE DESIGN */
        @media (max-width: 1024px) {
            .app-container { grid-template-columns: 220px 1fr; }
            .form-grid { grid-template-columns: 1fr 1fr; }
            .btn-glow { grid-column: span 2; }
        }

        @media (max-width: 768px) {
            .app-container { grid-template-columns: 1fr; height: auto; }
            aside.sidebar { display: none; }
            .credential-item { grid-template-columns: 1fr; gap: 10px; }
            .action-col { justify-content: flex-start; }
            .form-grid { grid-template-columns: 1fr; }
            .btn-glow { grid-column: span 1; }
        }
    </style>
</head>
<body>

    <!-- ANIMATED BACKGROUND GLOW ORBS -->
    <div class="bg-glow-container">
        <div class="glow-orb glow-orb-1"></div>
        <div class="glow-orb glow-orb-2"></div>
        <div class="glow-orb glow-orb-3"></div>
    </div>

    <!-- GRID OVERLAY -->
    <div class="grid-overlay"></div>

    <!-- MAIN DASHBOARD WRAPPER -->
    <div class="app-container">

        <!-- ANIMATED SIDEBAR -->
        <aside class="sidebar">
            <div>
                <div class="brand-logo">
                    <div class="logo-icon-wrapper">
                        <i class="fas fa-shield-halved"></i>
                    </div>
                    <div>
                        <div class="brand-name">PHOENIX</div>
                        <div class="brand-tag">ULTRA VAULT</div>
                    </div>
                </div>

                <ul class="nav-menu">
                    <li class="nav-item active">
                        <a href="#" class="nav-link">
                            <i class="fas fa-chart-pie"></i>
                            <span>Dashboard</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a href="#" class="nav-link">
                            <i class="fas fa-key"></i>
                            <span>Credentials</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a href="#" class="nav-link">
                            <i class="fas fa-file-contract"></i>
                            <span>Secure Notes</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a href="#" class="nav-link">
                            <i class="fas fa-bell"></i>
                            <span>Alerts</span>
                        </a>
                    </li>
                    <li class="nav-item">
                        <a href="#" class="nav-link">
                            <i class="fas fa-sliders"></i>
                            <span>Settings</span>
                        </a>
                    </li>
                </ul>
            </div>

            <div class="sidebar-footer">
                <i class="fas fa-lock shield-icon"></i>
                <div>
                    <div style="font-weight:700; color:#fff;">AES-256 AES-GCM</div>
                    <div>Hardware-backed Armor</div>
                </div>
            </div>
        </aside>

        <!-- MAIN CONTENT -->
        <main class="main-content">

            <!-- TOP BAR -->
            <div class="top-bar">
                <div class="page-title">
                    <h2>Credentials Armor</h2>
                    <p>Encrypted Data Vault & Identity Protection</p>
                </div>
                <div class="user-profile">
                    <div class="avatar">AR</div>
                    <div class="user-info">
                        <div class="user-name">Alexis Reed</div>
                        <div class="user-status"><i class="fas fa-circle" style="font-size:0.5rem;"></i> SECURED SESSION</div>
                    </div>
                </div>
            </div>

            <!-- FORM CARD -->
            <div class="form-card">
                <div class="card-header-title">
                    <i class="fas fa-plus-circle"></i>
                    Seal New Credential Asset
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

            <!-- CREDENTIALS LIST -->
            <div class="vault-section">
                <div class="vault-header">
                    <h3>Secured Assets (<span id="assetCount">0</span>)</h3>
                    <div class="search-box">
                        <i class="fas fa-search"></i>
                        <input type="text" id="searchInput" placeholder="Search assets...">
                    </div>
                </div>

                <div class="credential-list" id="credentialList">
                    <!-- Dynamic List Items will be rendered here -->
                </div>
            </div>

        </main>
    </div>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        // --- EFEK PARTIKEL WARNA-WARNI UNTUK MENU SIDEBAR ---
        const navLinks = document.querySelectorAll('.nav-link');
        const particleColors = ['#00f2fe', '#f72585', '#9d4edd', '#4facfe', '#00ff87', '#ffe600'];

        navLinks.forEach(link => {
            link.addEventListener('mousemove', (e) => {
                createMenuParticle(e, link);
            });
        });

        function createMenuParticle(e, element) {
            // Kontrol frekuensi agar efek halus
            if (Math.random() > 0.35) return;

            const particle = document.createElement('span');
            particle.classList.add('menu-particle');

            const rect = element.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;

            const size = Math.random() * 6 + 4; // Ukuran 4px - 10px
            particle.style.width = `${size}px`;
            particle.style.height = `${size}px`;

            particle.style.left = `${x}px`;
            particle.style.top = `${y}px`;

            const color = particleColors[Math.floor(Math.random() * particleColors.length)];
            particle.style.backgroundColor = color;
            particle.style.boxShadow = `0 0 10px ${color}`;

            // Arah percikan acak
            const dx = (Math.random() - 0.5) * 45 + 'px';
            const dy = (Math.random() - 0.5) * 45 + 'px';
            particle.style.setProperty('--dx', dx);
            particle.style.setProperty('--dy', dy);

            element.appendChild(particle);

            setTimeout(() => {
                particle.remove();
            }, 700);
        }

        // --- SISTEM MANAGEMENT ASSET ---
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
            let assets = JSON.parse(localStorage.getItem('ultraVaultAssets')) || [];
            assets.push(newAsset);
            localStorage.setItem('ultraVaultAssets', JSON.stringify(assets));

            vaultForm.reset();
            renderAssets();
            showToast('Asset Sealed & Encrypted!');
        });

        function renderAssets(filter = '') {
            let assets = JSON.parse(localStorage.getItem('ultraVaultAssets')) || [];
            credentialList.innerHTML = '';

            const filteredAssets = assets.filter(a => 
                a.platform.toLowerCase().includes(filter.toLowerCase()) || 
                a.email.toLowerCase().includes(filter.toLowerCase())
            );

            assetCount.textContent = filteredAssets.length;

            if (filteredAssets.length === 0) {
                credentialList.innerHTML = `
                    <div style="text-align:center; padding: 2.5rem; color: var(--text-muted); background: rgba(255,255,255,0.01); border-radius: 14px;">
                        <i class="fas fa-box-open" style="font-size:2rem; margin-bottom:10px; color:var(--accent-cyan);"></i>
                        <div>No encrypted assets found in vault.</div>
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
                        <button class="action-btn" onclick="togglePassword(${item.id}, '${item.password}')" title="Toggle Visibility">
                            <i class="fas fa-eye" id="eye-${item.id}"></i>
                        </button>
                        <button class="action-btn" onclick="copyToClipboard('${item.email}')" title="Copy Username">
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
                passEl.style.color = 'var(--accent-cyan)';
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
            let assets = JSON.parse(localStorage.getItem('ultraVaultAssets')) || [];
            assets = assets.filter(a => a.id !== id);
            localStorage.setItem('ultraVaultAssets', JSON.stringify(assets));
            renderAssets(searchInput.value);
            showToast('Asset Purged permanently!', '#ff4757');
        }

        searchInput.addEventListener('input', (e) => {
            renderAssets(e.target.value);
        });

        function showToast(msg, bg = 'var(--accent-cyan)') {
            const toast = document.createElement('div');
            toast.style.cssText = `
                position: fixed; bottom: 30px; right: 30px;
                background: ${bg}; color: #030712;
                padding: 12px 24px; border-radius: 12px; font-weight: 800;
                font-size: 0.85rem; box-shadow: 0 0 20px rgba(0,0,0,0.5);
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

        // Initialize Sample Data
        if (!localStorage.getItem('ultraVaultAssets')) {
            const samples = [
                { id: 1, platform: 'Google Cloud', email: 'alexis.reed@gmail.com', password: 'p@ssw0rd_Cyber2026!' },
                { id: 2, platform: 'AWS Architecture', email: 'aws.root@cube.io', password: 'SecretKey_#909012' }
            ];
            localStorage.setItem('ultraVaultAssets', JSON.stringify(samples));
        }

        renderAssets();
    </script>
</body>
</html>
