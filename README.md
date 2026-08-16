<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Phoenix Cyber Vault - Password Manager Pro</title>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800&family=Rajdhani:wght@400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-primary: #0a0b10;
            --bg-secondary: #121520;
            --card-bg: rgba(20, 24, 38, 0.7);
            --accent-cyan: #00f0ff;
            --accent-purple: #7000ff;
            --accent-pink: #ff0055;
            --text-main: #e2e8f0;
            --text-muted: #94a3b8;
            --border-neon: rgba(0, 240, 255, 0.2);
            --border-glow: 0 0 15px rgba(0, 240, 255, 0.3);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Rajdhani', sans-serif;
        }

        body {
            background-color: var(--bg-primary);
            color: var(--text-main);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }

        #spaceCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
        }

        /* --- LOCK SCREEN MODAL --- */
        #lockScreen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(10, 11, 16, 0.95);
            backdrop-filter: blur(15px);
            z-index: 10000;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            transition: opacity 0.5s ease;
        }

        .lock-card {
            background: var(--card-bg);
            border: 1px solid var(--accent-cyan);
            box-shadow: var(--border-glow);
            padding: 40px;
            border-radius: 16px;
            text-align: center;
            max-width: 380px;
            width: 90%;
        }

        .lock-title {
            font-family: 'Orbitron', sans-serif;
            color: var(--accent-cyan);
            margin-bottom: 20px;
            letter-spacing: 2px;
        }

        .pin-dots {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 20px 0;
        }

        .pin-dot {
            width: 16px;
            height: 16px;
            border-radius: 50%;
            border: 2px solid var(--accent-cyan);
            transition: 0.2s;
        }

        .pin-dot.filled {
            background: var(--accent-cyan);
            box-shadow: 0 0 10px var(--accent-cyan);
        }

        .numpad {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            margin-top: 20px;
        }

        .num-btn {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid var(--border-neon);
            color: var(--text-main);
            padding: 15px;
            font-size: 1.2rem;
            border-radius: 8px;
            cursor: pointer;
            transition: 0.2s;
            font-weight: 600;
        }

        .num-btn:hover {
            background: var(--accent-cyan);
            color: #000;
            box-shadow: 0 0 10px var(--accent-cyan);
        }

        /* --- LAYOUT UTAMA --- */
        .container {
            max-width: 1100px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px 0;
            border-bottom: 1px solid var(--border-neon);
            margin-bottom: 30px;
        }

        .logo {
            font-family: 'Orbitron', sans-serif;
            font-size: 1.8rem;
            color: var(--accent-cyan);
            text-transform: uppercase;
            letter-spacing: 2px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .header-actions {
            display: flex;
            gap: 12px;
            align-items: center;
        }

        .sync-status {
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 0.85rem;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .sync-status.online { background: rgba(0, 255, 136, 0.1); color: #00ff88; border: 1px solid #00ff88; }
        .sync-status.offline { background: rgba(255, 0, 85, 0.1); color: var(--accent-pink); border: 1px solid var(--accent-pink); }

        .btn {
            background: rgba(0, 240, 255, 0.1);
            border: 1px solid var(--accent-cyan);
            color: var(--accent-cyan);
            padding: 10px 18px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn:hover {
            background: var(--accent-cyan);
            color: #000;
            box-shadow: 0 0 15px var(--accent-cyan);
        }

        .btn-danger {
            border-color: var(--accent-pink);
            color: var(--accent-pink);
            background: rgba(255, 0, 85, 0.1);
        }

        .btn-danger:hover {
            background: var(--accent-pink);
            color: #fff;
            box-shadow: 0 0 15px var(--accent-pink);
        }

        /* --- DASHBOARD GRID --- */
        .dashboard-grid {
            display: grid;
            grid-template-columns: 320px 1fr;
            gap: 25px;
        }

        @media (max-width: 850px) {
            .dashboard-grid { grid-template-columns: 1fr; }
        }

        .card {
            background: var(--card-bg);
            border: 1px solid var(--border-neon);
            border-radius: 12px;
            padding: 20px;
            backdrop-filter: blur(10px);
        }

        .card-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 1.1rem;
            color: var(--accent-cyan);
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        /* --- FORM STYLES --- */
        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            color: var(--text-muted);
            font-size: 0.9rem;
        }

        .form-control {
            width: 100%;
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid var(--border-neon);
            padding: 12px;
            border-radius: 6px;
            color: #fff;
            outline: none;
            transition: 0.3s;
        }

        .form-control:focus {
            border-color: var(--accent-cyan);
            box-shadow: 0 0 8px rgba(0, 240, 255, 0.4);
        }

        .input-group {
            position: relative;
        }

        .input-btn-inside {
            position: absolute;
            right: 8px;
            top: 50%;
            transform: translateY(-50%);
            background: none;
            border: none;
            color: var(--accent-cyan);
            cursor: pointer;
            padding: 5px;
        }

        /* --- VAULT ITEMS LIST --- */
        .search-bar {
            margin-bottom: 20px;
        }

        .credential-list {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .credential-item {
            display: grid;
            grid-template-columns: 1.5fr 2fr 1.5fr auto;
            align-items: center;
            padding: 15px;
            background: rgba(255, 255, 255, 0.02);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 8px;
            gap: 10px;
            transition: 0.3s;
        }

        @media (max-width: 650px) {
            .credential-item {
                grid-template-columns: 1fr;
                gap: 8px;
            }
        }

        .credential-item:hover {
            border-color: var(--accent-cyan);
            box-shadow: 0 0 10px rgba(0, 240, 255, 0.1);
            background: rgba(0, 240, 255, 0.03);
        }

        .platform-col {
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: 600;
        }

        .platform-icon-wrapper {
            width: 36px;
            height: 36px;
            border-radius: 8px;
            background: rgba(0, 240, 255, 0.1);
            border: 1px solid var(--accent-cyan);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--accent-cyan);
        }

        .user-col {
            color: var(--text-muted);
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .pass-col {
            font-family: monospace;
            letter-spacing: 2px;
            color: var(--accent-cyan);
        }

        .action-col {
            display: flex;
            gap: 8px;
        }

        .action-btn {
            background: none;
            border: 1px solid var(--border-neon);
            color: var(--text-main);
            width: 32px;
            height: 32px;
            border-radius: 6px;
            cursor: pointer;
            transition: 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .action-btn:hover {
            background: var(--accent-cyan);
            color: #000;
        }

        .action-btn.del:hover {
            background: var(--accent-pink);
            border-color: var(--accent-pink);
            color: #fff;
        }

        /* --- TOAST NOTIFICATION --- */
        #toast {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--bg-secondary);
            border: 1px solid var(--accent-cyan);
            padding: 15px 20px;
            border-radius: 8px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.5);
            display: flex;
            align-items: center;
            gap: 12px;
            transform: translateY(100px);
            opacity: 0;
            transition: 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            z-index: 1000;
        }

        #toast.show {
            transform: translateY(0);
            opacity: 1;
        }
    </style>
</head>
<body>
    <canvas id="spaceCanvas"></canvas>

    <!-- LOCK SCREEN AUTH -->
    <div id="lockScreen">
        <div class="lock-card">
            <i class="fas fa-shield-halved" style="font-size: 3rem; color: var(--accent-cyan); margin-bottom: 10px;"></i>
            <h2 class="lock-title">VAULT TERKUNCI</h2>
            <p style="color: var(--text-muted); font-size: 0.9rem;">Masukkan PIN Keamanan (Default: 1234)</p>
            <div class="pin-dots">
                <div class="pin-dot"></div>
                <div class="pin-dot"></div>
                <div class="pin-dot"></div>
                <div class="pin-dot"></div>
            </div>
            <div class="numpad">
                <button class="num-btn" onclick="pressPin('1')">1</button>
                <button class="num-btn" onclick="pressPin('2')">2</button>
                <button class="num-btn" onclick="pressPin('3')">3</button>
                <button class="num-btn" onclick="pressPin('4')">4</button>
                <button class="num-btn" onclick="pressPin('5')">5</button>
                <button class="num-btn" onclick="pressPin('6')">6</button>
                <button class="num-btn" onclick="pressPin('7')">7</button>
                <button class="num-btn" onclick="pressPin('8')">8</button>
                <button class="num-btn" onclick="pressPin('9')">9</button>
                <button class="num-btn" onclick="clearPin()"><i class="fas fa-undo"></i></button>
                <button class="num-btn" onclick="pressPin('0')">0</button>
                <button class="num-btn" onclick="checkPin()"><i class="fas fa-arrow-right"></i></button>
            </div>
        </div>
    </div>

    <!-- UTAMA CONTAINER -->
    <div class="container">
        <header>
            <div class="logo">
                <i class="fas fa-fire-alt"></i> Phoenix Cyber Vault
            </div>
            <div class="header-actions">
                <div id="syncStatus" class="sync-status online">
                    <i class="fas fa-wifi"></i> <span id="syncText">Online</span>
                </div>
                <button class="btn" onclick="lockVault()"><i class="fas fa-lock"></i> Kunci</button>
            </div>
        </header>

        <div class="dashboard-grid">
            <!-- SIDEBAR: ADD FORM -->
            <div class="card">
                <h3 class="card-title"><i class="fas fa-plus-circle"></i> Tambah Kredensial</h3>
                <form id="vaultForm">
                    <div class="form-group">
                        <label>Platform / Layanan</label>
                        <input type="text" id="platformInput" class="form-control" placeholder="cth: Google, Steam" required>
                    </div>
                    <div class="form-group">
                        <label>Username / Email</label>
                        <input type="text" id="userInput" class="form-control" placeholder="user@domain.com" required>
                    </div>
                    <div class="form-group">
                        <label>Password</label>
                        <div class="input-group">
                            <input type="password" id="passInput" class="form-control" placeholder="••••••••" required>
                            <button type="button" class="input-btn-inside" onclick="generatePassword()" title="Generate Password Auto"><i class="fas fa-dice"></i></button>
                        </div>
                    </div>
                    <button type="submit" class="btn" style="width: 100%; justify-content: center; margin-top: 10px;">
                        <i class="fas fa-save"></i> Simpan Ke Vault
                    </button>
                </form>

                <hr style="border: none; border-top: 1px solid var(--border-neon); margin: 25px 0;">

                <h3 class="card-title" style="font-size: 0.95rem;"><i class="fas fa-database"></i> Manajemen Data</h3>
                <div style="display: flex; flex-direction: column; gap: 8px;">
                    <button class="btn" onclick="exportData()"><i class="fas fa-download"></i> Backup Data (JSON)</button>
                    <button class="btn" onclick="importData()"><i class="fas fa-upload"></i> Restore Data</button>
                    <input type="file" id="fileInput" style="display: none;" onchange="handleImport(event)">
                    <button class="btn btn-danger" onclick="clearAllData()"><i class="fas fa-trash-alt"></i> Kosongkan Vault</button>
                </div>
            </div>

            <!-- MAIN CONTENT: VAULT DISPLAY -->
            <div class="card">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                    <h3 class="card-title" style="margin-bottom: 0;">
                        <i class="fas fa-vault"></i> Terpenjara Data (<span id="totalCount">0</span>)
                    </h3>
                </div>

                <div class="search-bar">
                    <input type="text" id="searchInput" class="form-control" placeholder="Cari platform atau username..." oninput="filterCredentials()">
                </div>

                <div class="credential-list" id="credentialList">
                    <!-- Iterasi data vault akan dirender di sini via JS -->
                </div>
            </div>
        </div>
    </div>

    <!-- TOAST ALERT -->
    <div id="toast">
        <i class="fas fa-check-circle" id="toastIcon" style="color: var(--accent-cyan); font-size: 1.2rem;"></i>
        <div>
            <div id="toastTitle" style="font-weight: 600;">Notifikasi</div>
            <div id="toastMessage" style="font-size: 0.85rem; color: var(--text-muted);">Pesan sukses</div>
        </div>
    </div>

    <script>
        /* --- SECURITY PIN & LOCK SYSTEM --- */
        const MASTER_PIN = "1234";
        let currentPin = "";

        function pressPin(num) {
            if (currentPin.length < 4) {
                currentPin += num;
                updatePinDots();
                if (currentPin.length === 4) {
                    setTimeout(checkPin, 100);
                }
            }
        }

        function clearPin() {
            currentPin = "";
            updatePinDots();
        }

        function updatePinDots() {
            const dots = document.querySelectorAll('.pin-dot');
            dots.forEach((dot, index) => {
                if (index < currentPin.length) {
                    dot.classList.add('filled');
                } else {
                    dot.classList.remove('filled');
                }
            });
        }

        function checkPin() {
            if (currentPin === MASTER_PIN) {
                document.getElementById('lockScreen').style.opacity = '0';
                setTimeout(() => {
                    document.getElementById('lockScreen').style.display = 'none';
                }, 500);
                showToast("Berhasil Akses", "Vault Keamanan Terbuka!");
                clearPin();
            } else {
                showToast("Akses Ditolak", "PIN yang Anda masukkan salah!", true);
                setTimeout(() => { clearPin(); }, 400);
            }
        }

        function lockVault() {
            document.getElementById('lockScreen').style.display = 'flex';
            setTimeout(() => {
                document.getElementById('lockScreen').style.opacity = '1';
            }, 10);
            clearPin();
            showToast("Terkunci", "Vault berhasil dikunci.");
        }

        /* --- TOAST NOTIFICATIONS --- */
        function showToast(title, message, isError = false) {
            const toast = document.getElementById('toast');
            const icon = document.getElementById('toastIcon');
            document.getElementById('toastTitle').innerText = title;
            document.getElementById('toastMessage').innerText = message;

            if (isError) {
                toast.style.borderColor = 'var(--accent-pink)';
                icon.className = 'fas fa-exclamation-circle';
                icon.style.color = 'var(--accent-pink)';
            } else {
                toast.style.borderColor = 'var(--accent-cyan)';
                icon.className = 'fas fa-check-circle';
                icon.style.color = 'var(--accent-cyan)';
            }

            toast.classList.add('show');
            setTimeout(() => { toast.classList.remove('show'); }, 3000);
        }

        /* --- DATA MANAGEMENT (localStorage) --- */
        const STORAGE_KEY = 'phoenix_vault_credentials';

        function loadCredentials() {
            try {
                const data = localStorage.getItem(STORAGE_KEY);
                return data ? JSON.parse(data) : getInitialDefaultData();
            } catch (e) {
                console.error("Gagal memuat data", e);
                return getInitialDefaultData();
            }
        }

        function getInitialDefaultData() {
            return [
                { id: 1, platform: 'Google', user: 'user@gmail.com', pass: 'p@ssw0rd123' },
                { id: 2, platform: 'Github', user: 'octocat', pass: 'git_hub_secret' }
            ];
        }

        function saveCredentials(credentials) {
            try {
                localStorage.setItem(STORAGE_KEY, JSON.stringify(credentials));
                updateStats();
            } catch (e) {
                showToast("Kesalahan Simpan", "Tidak dapat menyimpan data ke penyimpanan lokal.", true);
            }
        }

        let credentials = loadCredentials();

        function updateStats() {
            document.getElementById('totalCount').innerText = credentials.length;
        }

        /* --- GENERATOR PASSWORD --- */
        function generatePassword() {
            const chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()";
            let pass = "";
            for (let i = 0; i < 14; i++) {
                pass += chars.charAt(Math.floor(Math.random() * chars.length));
            }
            document.getElementById('passInput').value = pass;
            showToast("Password Generated", "Password kuat acak berhasil dibuat.");
        }

        /* --- ICON MAPPING --- */
        function getPlatformIcon(platform) {
            const p = platform.toLowerCase().trim();
            if (p.includes('google') || p.includes('gmail')) return 'fab fa-google';
            if (p.includes('github')) return 'fab fa-github';
            if (p.includes('facebook')) return 'fab fa-facebook-f';
            if (p.includes('instagram')) return 'fab fa-instagram';
            if (p.includes('twitter') || p.includes('x')) return 'fab fa-x-twitter';
            if (p.includes('discord')) return 'fab fa-discord';
            if (p.includes('steam')) return 'fab fa-steam';
            if (p.includes('spotify')) return 'fab fa-spotify';
            if (p.includes('linkedin')) return 'fab fa-linkedin-in';
            if (p.includes('netflix')) return 'fas fa-film';
            if (p.includes('amazon')) return 'fab fa-amazon';
            return 'fas fa-globe';
        }

        /* --- RENDER VAULT --- */
        function renderCredentials(dataToRender = credentials) {
            const listEl = document.getElementById('credentialList');
            listEl.innerHTML = '';

            if (dataToRender.length === 0) {
                listEl.innerHTML = `
                    <div style="text-align: center; color: var(--text-muted); padding: 40px 0;">
                        <i class="fas fa-folder-open" style="font-size: 2.5rem; margin-bottom: 10px; opacity: 0.5;"></i>
                        <p>Tidak ada kredensial ditemukan.</p>
                    </div>`;
                return;
            }

            dataToRender.forEach(item => {
                const iconClass = getPlatformIcon(item.platform);
                const itemEl = document.createElement('div');
                itemEl.className = 'credential-item';
                itemEl.innerHTML = `
                    <div class="platform-col">
                        <div class="platform-icon-wrapper">
                            <i class="${iconClass}"></i>
                        </div>
                        <span class="platform-name">${escapeHtml(item.platform)}</span>
                    </div>

                    <div class="user-col">
                        <span title="${escapeHtml(item.user)}">${escapeHtml(item.user)}</span>
                        <button class="action-btn" style="width: 24px; height: 24px;" onclick="copyToClipboard('${escapeJs(item.user)}', 'Username/Email')" title="Salin Email">
                            <i class="fas fa-copy" style="font-size: 0.75rem;"></i>
                        </button>
                    </div>

                    <div class="pass-col" id="pass-${item.id}">••••••••</div>

                    <div class="action-col">
                        <button class="action-btn" onclick="togglePasswordVisibility(${item.id}, '${escapeJs(item.pass)}')" title="Lihat/Sembunyikan">
                            <i class="fas fa-eye" id="eye-${item.id}"></i>
                        </button>
                        <button class="action-btn" onclick="copyToClipboard('${escapeJs(item.pass)}', 'Password')" title="Salin Password">
                            <i class="fas fa-key"></i>
                        </button>
                        <button class="action-btn del" onclick="deleteCredential(${item.id})" title="Hapus">
                            <i class="fas fa-trash"></i>
                        </button>
                    </div>
                `;
                listEl.appendChild(itemEl);
            });

            updateStats();
        }

        function escapeHtml(str) {
            return String(str)
                .replace(/&/g, "&amp;")
                .replace(/</g, "&lt;")
                .replace(/>/g, "&gt;")
                .replace(/"/g, "&quot;")
                .replace(/'/g, "&#039;");
        }

        function escapeJs(str) {
            return String(str).replace(/\\/g, '\\\\').replace(/'/g, "\\'");
        }

        /* --- FORM EVENT LISTENER --- */
        document.getElementById('vaultForm').addEventListener('submit', function(e) {
            e.preventDefault();
            const platform = document.getElementById('platformInput').value.trim();
            const user = document.getElementById('userInput').value.trim();
            const pass = document.getElementById('passInput').value.trim();

            if (platform && user && pass) {
                const newItem = {
                    id: Date.now(),
                    platform,
                    user,
                    pass
                };
                credentials.unshift(newItem);
                saveCredentials(credentials);
                renderCredentials();

                this.reset();
                showToast("Tersimpan", `Kredensial ${platform} berhasil ditambahkan!`);
            }
        });

        function togglePasswordVisibility(id, realPass) {
            const passEl = document.getElementById(`pass-${id}`);
            const eyeEl = document.getElementById(`eye-${id}`);

            if (passEl.innerText === '••••••••') {
                passEl.innerText = realPass;
                eyeEl.className = 'fas fa-eye-slash';
            } else {
                passEl.innerText = '••••••••';
                eyeEl.className = 'fas fa-eye';
            }
        }

        function copyToClipboard(text, label) {
            navigator.clipboard.writeText(text).then(() => {
                showToast("Tersalin", `${label} berhasil disalin ke clipboard!`);
            }).catch(() => {
                showToast("Gagal", `Gagal menyalin ${label}`, true);
            });
        }

        function deleteCredential(id) {
            if (confirm("Apakah Anda yakin ingin menghapus kredensial ini?")) {
                credentials = credentials.filter(item => item.id !== id);
                saveCredentials(credentials);
                renderCredentials();
                showToast("Dihapus", "Kredensial berhasil dihapus.");
            }
        }

        function filterCredentials() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = credentials.filter(item =>
                item.platform.toLowerCase().includes(query) ||
                item.user.toLowerCase().includes(query)
            );
            renderCredentials(filtered);
        }

        /* --- BACKUP & RESTORE --- */
        function exportData() {
            const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(credentials, null, 2));
            const downloadAnchor = document.createElement('a');
            downloadAnchor.setAttribute("href", dataStr);
            downloadAnchor.setAttribute("download", `phoenix_vault_backup_${new Date().toISOString().slice(0,10)}.json`);
            document.body.appendChild(downloadAnchor);
            downloadAnchor.click();
            downloadAnchor.remove();
            showToast("Backup Selesai", "Data kredensial berhasil diunduh.");
        }

        function importData() {
            document.getElementById('fileInput').click();
        }

        function handleImport(event) {
            const file = event.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const importedData = JSON.parse(e.target.result);
                    if (Array.isArray(importedData)) {
                        credentials = importedData;
                        saveCredentials(credentials);
                        renderCredentials();
                        showToast("Restore Berhasil", `${credentials.length} kredensial berhasil dimuat!`);
                    } else {
                        throw new Error("Format JSON tidak valid");
                    }
                } catch (err) {
                    showToast("Format Gagal", "File backup tidak valid!", true);
                }
            };
            reader.readAsText(file);
            event.target.value = '';
        }

        function clearAllData() {
            if (confirm("PERINGATAN: Semua data kredensial akan dihapus secara permanen. Lanjutkan?")) {
                credentials = [];
                saveCredentials(credentials);
                renderCredentials();
                showToast("Semua Data Dihapus", "Vault Anda sekarang kosong.", true);
            }
        }

        /* --- ONLINE / OFFLINE DETECTOR --- */
        function updateNetworkStatus() {
            const syncStatus = document.getElementById('syncStatus');
            const syncText = document.getElementById('syncText');
            if (navigator.onLine) {
                syncStatus.className = 'sync-status online';
                syncText.innerText = 'Online';
            } else {
                syncStatus.className = 'sync-status offline';
                syncText.innerText = 'Offline (Lokal)';
            }
        }

        window.addEventListener('online', updateNetworkStatus);
        window.addEventListener('offline', updateNetworkStatus);

        /* --- BACKGROUND SPACE ANIMATION --- */
        const canvas = document.getElementById('spaceCanvas');
        const ctx = canvas.getContext('2d');
        let stars = [];

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            initStars();
        }

        function initStars() {
            stars = [];
            const count = Math.floor((canvas.width * canvas.height) / 3000);
            for (let i = 0; i < count; i++) {
                stars.push({
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height,
                    size: Math.random() * 1.5,
                    alpha: Math.random(),
                    speed: Math.random() * 0.02 + 0.005
                });
            }
        }

        function drawStars() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            stars.forEach(star => {
                star.alpha += star.speed;
                if (star.alpha > 1 || star.alpha < 0) star.speed = -star.speed;
                ctx.fillStyle = `rgba(0, 240, 255, ${Math.abs(star.alpha)})`;
                ctx.beginPath();
                ctx.arc(star.x, star.y, star.size, 0, Math.PI * 2);
                ctx.fill();
            });
            requestAnimationFrame(drawStars);
        }

        window.addEventListener('resize', resizeCanvas);

        /* --- INITIALIZATION --- */
        window.onload = function() {
            resizeCanvas();
            drawStars();
            updateNetworkStatus();
            renderCredentials();
        };
    </script>
</body>
</html>
