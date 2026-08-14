<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PHOENIX VAULT | Ultra Crimson Armor</title>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            --bg-dark: #050002;
            --accent-red: #ff003c;
            --accent-crimson: #d90429;
            --accent-orange: #ff5400;
            --accent-pink: #ff0077;
            --card-glass: rgba(18, 2, 6, 0.78);
            --card-border: rgba(255, 0, 60, 0.35);
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

        /* --- ANIMATED BACKGROUND ORBS --- */
        .bg-glow-container {
            position: fixed;
            top: 0; left: 0;
            width: 100vw; height: 100vh;
            z-index: 0;
            overflow: hidden;
            pointer-events: none;
        }

        .glow-orb {
            position: absolute;
            border-radius: 50%;
            filter: blur(120px);
            opacity: 0.5;
            animation: floatGlow 15s ease-in-out infinite alternate;
        }

        .glow-orb-1 {
            width: 600px; height: 600px;
            background: radial-gradient(circle, var(--accent-red), var(--accent-orange));
            top: -150px; left: -150px;
            animation-duration: 12s;
        }

        .glow-orb-2 {
            width: 700px; height: 700px;
            background: radial-gradient(circle, var(--accent-crimson), #4a000e);
            bottom: -180px; right: -180px;
            animation-duration: 18s;
            animation-delay: -4s;
        }

        @keyframes floatGlow {
            0% { transform: translate(0, 0) scale(1) rotate(0deg); }
            50% { transform: translate(80px, -60px) scale(1.15) rotate(180deg); }
            100% { transform: translate(-40px, 50px) scale(0.9) rotate(360deg); }
        }

        /* GRID BACKGROUND EFFECT */
        .grid-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-image: 
                linear-gradient(rgba(255, 0, 60, 0.04) 1px, transparent 1px),
                linear-gradient(90deg, rgba(255, 0, 60, 0.04) 1px, transparent 1px);
            background-size: 32px 32px;
            z-index: 1;
            pointer-events: none;
            animation: gridPulse 6s ease-in-out infinite alternate;
        }

        @keyframes gridPulse {
            0% { opacity: 0.2; }
            100% { opacity: 0.7; }
        }

        /* --- DASHBOARD WRAPPER --- */
        .app-container {
            position: relative;
            z-index: 2;
            width: 100%;
            max-width: 1240px;
            height: 800px;
            background: var(--card-glass);
            backdrop-filter: blur(35px);
            -webkit-backdrop-filter: blur(35px);
            border-radius: 28px;
            border: 1px solid var(--card-border);
            box-shadow: 
                0 30px 80px rgba(0, 0, 0, 0.95),
                0 0 60px rgba(255, 0, 60, 0.2),
                inset 0 0 20px rgba(255, 0, 60, 0.08);
            display: grid;
            grid-template-columns: 280px 1fr;
            overflow: hidden;
            animation: containerAppear 0.8s cubic-bezier(0.16, 1, 0.3, 1);
        }

        @keyframes containerAppear {
            from { opacity: 0; transform: scale(0.96) translateY(20px); }
            to { opacity: 1; transform: scale(1) translateY(0); }
        }

        /* --- SIDEBAR MENU --- */
        aside.sidebar {
            background: rgba(10, 1, 3, 0.92);
            border-right: 1px solid rgba(255, 0, 60, 0.2);
            padding: 2.2rem 1.4rem;
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
            padding-left: 0.4rem;
            margin-bottom: 3rem;
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

        /* MENU NAVIGASI DENGAN GLOW SLIDER */
        .nav-wrapper {
            position: relative;
        }

        .nav-menu {
            list-style: none;
            display: flex;
            flex-direction: column;
            gap: 12px;
            position: relative;
            z-index: 2;
        }

        /* BACKDROP HOVER SLIDER INTERAKTIF */
        .nav-indicator {
            position: absolute;
            left: 0;
            width: 100%;
            height: 52px;
            background: linear-gradient(90deg, rgba(255, 0, 60, 0.25), rgba(255, 84, 0, 0.1));
            border: 1px solid var(--accent-red);
            border-radius: 16px;
            box-shadow: 0 0 20px rgba(255, 0, 60, 0.4);
            pointer-events: none;
            transition: all 0.3s cubic-bezier(0.25, 1, 0.5, 1);
            opacity: 0;
            z-index: 1;
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
        }

        .nav-link i {
            font-size: 1.15rem;
            transition: var(--transition-smooth);
        }

        .nav-item.active .nav-link,
        .nav-link:hover {
            color: #ffffff;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
        }

        .nav-item.active .nav-link i,
        .nav-link:hover i {
            color: var(--accent-red);
            transform: scale(1.2) rotate(4deg);
            filter: drop-shadow(0 0 8px var(--accent-red));
        }

        .sidebar-footer {
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

        .input-group input:focus + i {
            color: var(--accent-red);
        }

        /* GLOW BUTTON */
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

        /* RESPONSIVE */
        @media (max-width: 1024px) {
            .app-container { grid-template-columns: 220px 1fr; }
            .form-grid { grid-template-columns: 1fr 1fr; }
            .btn-glow { grid-column: span 2; }
        }

        @media (max-width: 768px) {
            .app-container { grid-template-columns: 1fr; height: auto; }
            aside.sidebar { display: none; }
            .credential-item { grid-template-columns: 1fr; gap: 12px; }
            .action-col { justify-content: flex-start; }
            .form-grid { grid-template-columns: 1fr; }
            .btn-glow { grid-column: span 1; }
        }
    </style>
</head>
<body>

    <!-- ANIMATED BACKGROUND -->
    <div class="bg-glow-container">
        <div class="glow-orb glow-orb-1"></div>
        <div class="glow-orb glow-orb-2"></div>
    </div>
    <div class="grid-overlay"></div>

    <!-- MAIN DASHBOARD -->
    <div class="app-container">

        <!-- CLEAN SIDEBAR WITH ANIMATED INDICATOR -->
        <aside class="sidebar">
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
                    <!-- ANIMATED HOVER INDICATOR SLIDER -->
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
                    <div>Hardware Armor Active</div>
                </div>
            </div>
        </aside>

        <!-- MAIN CONTENT AREA -->
        <main class="main-content">

            <!-- TOP BAR -->
            <div class="top-bar">
                <div class="page-title">
                    <h2>Vault Operations</h2>
                    <p>Encrypted Identity & Access Management</p>
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

    <script>
        // --- ANIMASI MENU SLIDER INTERAKTIF ---
        const navMenu = document.getElementById('navMenu');
        const navItems = document.querySelectorAll('.nav-item');
        const indicator = document.getElementById('navIndicator');

        function moveIndicator(element) {
            if (!element) return;
            const rect = element.getBoundingClientRect();
            const parentRect = navMenu.getBoundingClientRect();
            const topOffset = rect.top - parentRect.top;

            indicator.style.opacity = '1';
            indicator.style.transform = `translateY(${topOffset}px)`;
            indicator.style.height = `${rect.height}px`;
        }

        // Set indikator ke item aktif saat pertama kali load
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


        // --- MANAJEMEN VAULT (LOCAL STORAGE) ---
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
            let assets = JSON.parse(localStorage.getItem('ultraRedVaultV2')) || [];
            assets.push(newAsset);
            localStorage.setItem('ultraRedVaultV2', JSON.stringify(assets));

            vaultForm.reset();
            renderAssets();
            showToast('Asset Sealed & Encrypted!');
        });

        function renderAssets(filter = '') {
            let assets = JSON.parse(localStorage.getItem('ultraRedVaultV2')) || [];
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
                        <div>Vault empty or no matching asset found.</div>
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
                        <button class="action-btn" onclick="copyToClipboard('${item.email}')" title="Copy Email/User">
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
            let assets = JSON.parse(localStorage.getItem('ultraRedVaultV2')) || [];
            assets = assets.filter(a => a.id !== id);
            localStorage.setItem('ultraRedVaultV2', JSON.stringify(assets));
            renderAssets(searchInput.value);
            showToast('Asset Purged Permanently!', '#ff2a2a');
        }

        searchInput.addEventListener('input', (e) => {
            renderAssets(e.target.value);
        });

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

        // Initialize Sample Data
        if (!localStorage.getItem('ultraRedVaultV2')) {
            const samples = [
                { id: 1, platform: 'Google Cloud', email: 'alexis.reed@gmail.com', password: 'p@ssw0rd_Cyber2026!' },
                { id: 2, platform: 'AWS Security', email: 'aws.root@cube.io', password: 'SecretKey_#909012' }
            ];
            localStorage.setItem('ultraRedVaultV2', JSON.stringify(samples));
        }

        renderAssets();
    </script>
</body>
</html>
