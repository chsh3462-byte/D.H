<!DOCTYPE html>
<html lang="en" class="h-full bg-slate-950 text-cyan-400 font-mono">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>D.H // DATA MATRIX & NET SEARCH</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts for Sci-Fi typography -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800;900&family=Share+Tech+Mono&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        cyber: {
                            black: '#07080c',
                            dark: '#0d0f17',
                            panel: '#121522',
                            border: '#1a233a',
                            neonCyan: '#00f3ff',
                            neonMagenta: '#ff0055',
                            neonYellow: '#ffe600',
                            neonGreen: '#00ff66',
                            textMuted: '#5b6b8c'
                        }
                    },
                    fontFamily: {
                        orbitron: ['Orbitron', 'sans-serif'],
                        mono: ['Share Tech Mono', 'monospace']
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #050608;
            background-image: 
                radial-gradient(circle at 50% 50%, rgba(0, 243, 255, 0.05) 0%, transparent 60%),
                linear-gradient(rgba(0, 243, 255, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 243, 255, 0.03) 1px, transparent 1px);
            background-size: 100% 100%, 30px 30px, 30px 30px;
            text-shadow: 0 0 2px rgba(0, 243, 255, 0.4);
        }

        /* CRT Scanline effect */
        .scanline {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none;
            background: linear-gradient(
                rgba(18, 16, 16, 0) 50%, 
                rgba(0, 0, 0, 0.25) 50%
            );
            background-size: 100% 4px;
            z-index: 50;
            opacity: 0.6;
        }

        /* Glowing outlines */
        .glow-cyan {
            box-shadow: 0 0 12px rgba(0, 243, 255, 0.35), inset 0 0 10px rgba(0, 243, 255, 0.1);
        }
        .glow-magenta {
            box-shadow: 0 0 12px rgba(255, 0, 85, 0.35), inset 0 0 10px rgba(255, 0, 85, 0.1);
        }
        .text-glow-cyan {
            text-shadow: 0 0 8px rgba(0, 243, 255, 0.7);
        }
        .text-glow-magenta {
            text-shadow: 0 0 8px rgba(255, 0, 85, 0.7);
        }

        /* Clip path futuristic corners */
        .cyber-corner {
            clip-path: polygon(
                0 0, 
                calc(100% - 12px) 0, 
                100% 12px, 
                100% 100%, 
                12px 100%, 
                0 calc(100% - 12px)
            );
        }
        .cyber-btn {
            clip-path: polygon(
                10px 0, 
                100% 0, 
                100% calc(100% - 10px), 
                calc(100% - 10px) 100%, 
                0 100%, 
                0 10px
            );
            transition: all 0.2s ease;
        }
        .cyber-btn:hover {
            transform: translateY(-1px);
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #080a11;
        }
        ::-webkit-scrollbar-thumb {
            background: #1e293b;
            border: 1px solid #00f3ff;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00f3ff;
        }

        /* Matrix Canvas container */
        #matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            pointer-events: none;
            opacity: 0.12;
            z-index: 0;
        }
    </style>
</head>

<body class="h-screen flex flex-col overflow-hidden select-none">
    <!-- Matrix Animated Background -->
    <canvas id="matrix-bg"></canvas>
    
    <!-- CRT Overlay -->
    <div class="scanline"></div>

    <header class="relative z-10 bg-cyber-dark/90 border-b border-cyber-neonCyan/40 px-4 py-2 flex items-center justify-between backdrop-blur-md">
        <div class="flex items-center space-x-4">
            <!-- Brand Logo -->
            <div class="flex items-center space-x-2">
                <div class="w-10 h-10 bg-cyber-neonCyan/20 border-2 border-cyber-neonCyan flex items-center justify-center font-orbitron font-black text-2xl text-cyber-neonCyan shadow-[0_0_15px_rgba(0,243,255,0.5)] cyber-corner">
                    D.H
                </div>
                <div>
                    <h1 class="font-orbitron font-extrabold text-lg tracking-widest text-white flex items-center gap-2">
                        <span>D.H // DATA TERMINAL</span>
                        <span class="text-xs font-mono bg-cyber-neonMagenta/20 border border-cyber-neonMagenta text-cyber-neonMagenta px-1.5 py-0.5 rounded">v4.02</span>
                    </h1>
                    <p class="text-xs text-cyber-textMuted tracking-wider font-mono">ENCRYPTED MATRIX NODE // WORKBOOK & NET-SEARCH MATRIX</p>
                </div>
            </div>
        </div>

        <!-- System HUD Telemetry -->
        <div class="hidden md:flex items-center space-x-6 text-xs font-mono">
            <div class="flex items-center space-x-2">
                <span class="text-cyber-textMuted">NET STAT:</span>
                <span class="inline-flex items-center text-cyber-neonGreen">
                    <span class="w-2 h-2 rounded-full bg-cyber-neonGreen animate-ping mr-1.5"></span>
                    ONLINE
                </span>
            </div>
            <div class="flex items-center space-x-2">
                <span class="text-cyber-textMuted">LATENCY:</span>
                <span id="sys-latency" class="text-cyber-neonCyan">14ms</span>
            </div>
            <div class="flex items-center space-x-2">
                <span class="text-cyber-textMuted">SESSION:</span>
                <span id="sys-clock" class="text-cyber-neonYellow">00:00:00</span>
            </div>
            <!-- Audio Mute Toggle -->
            <button id="audio-toggle-btn" onclick="toggleAudio()" class="px-2 py-1 border border-cyber-neonCyan/40 bg-cyber-panel hover:bg-cyber-neonCyan/20 text-cyber-neonCyan text-xs flex items-center space-x-1 transition-all">
                <i class="fas fa-volume-up" id="audio-icon"></i>
                <span id="audio-status-text">AUDIO ON</span>
            </button>
        </div>
    </header>

    <nav class="relative z-10 bg-cyber-black/80 border-b border-cyber-border px-4 py-1.5 flex items-center space-x-2 overflow-x-auto">
        <button onclick="switchTab('workbook')" id="nav-btn-workbook" class="cyber-btn px-4 py-1.5 font-orbitron text-xs font-bold flex items-center space-x-2 bg-cyber-neonCyan text-black shadow-[0_0_10px_rgba(0,243,255,0.4)]">
            <i class="fas fa-table"></i>
            <span>WORKBOOK & WORKSHEETS</span>
        </button>
        <button onclick="switchTab('netsearch')" id="nav-btn-netsearch" class="cyber-btn px-4 py-1.5 font-orbitron text-xs font-bold flex items-center space-x-2 bg-cyber-panel text-cyber-textMuted hover:text-cyber-neonCyan hover:bg-cyber-neonCyan/10 border border-cyber-border">
            <i class="fas fa-globe"></i>
            <span>NET-SEARCH (DEEP MATRIX)</span>
        </button>
        <button onclick="switchTab('terminal')" id="nav-btn-terminal" class="cyber-btn px-4 py-1.5 font-orbitron text-xs font-bold flex items-center space-x-2 bg-cyber-panel text-cyber-textMuted hover:text-cyber-neonMagenta hover:bg-cyber-neonMagenta/10 border border-cyber-border">
            <i class="fas fa-terminal"></i>
            <span>SYSTEM LOGS & TERMINAL</span>
        </button>
    </nav>

    <main class="relative z-10 flex-1 overflow-hidden flex flex-col p-3 gap-3">

        <!-- ================= TAB 1: WORKBOOK & WORKSHEETS ================= -->
        <section id="tab-workbook" class="flex-1 flex flex-col gap-2 overflow-hidden">
            <!-- Workbook Toolbar -->
            <div class="bg-cyber-panel/90 border border-cyber-border p-2 rounded flex flex-wrap items-center justify-between gap-2 shadow-lg">
                <!-- Left tools: Worksheet Switcher & Add -->
                <div class="flex items-center space-x-2 overflow-x-auto py-1">
                    <span class="text-xs text-cyber-neonCyan font-bold tracking-widest flex items-center gap-1">
                        <i class="fas fa-layer-group"></i> SHEETS:
                    </span>
                    <div id="worksheet-tabs-container" class="flex items-center space-x-1">
                        <!-- Dynamic sheet tabs rendered via JS -->
                    </div>
                    <button onclick="createNewWorksheetPrompt()" class="px-2 py-1 text-xs border border-dashed border-cyber-neonCyan/60 text-cyber-neonCyan hover:bg-cyber-neonCyan/20 rounded transition-all flex items-center gap-1" title="Create New Worksheet">
                        <i class="fas fa-plus"></i> NEW SHEET
                    </button>
                </div>

                <!-- Right tools: Cell calculation metrics & Actions -->
                <div class="flex items-center space-x-3 text-xs">
                    <!-- Quick Metrics HUD -->
                    <div class="bg-cyber-black/70 border border-cyber-border px-3 py-1 flex items-center space-x-4 text-cyber-textMuted font-mono">
                        <div>SUM: <span id="stat-sum" class="text-cyber-neonGreen font-bold">0</span></div>
                        <div>AVG: <span id="stat-avg" class="text-cyber-neonCyan font-bold">0</span></div>
                        <div>COUNT: <span id="stat-count" class="text-cyber-neonYellow font-bold">0</span></div>
                    </div>

                    <!-- Row/Col Operations -->
                    <button onclick="addRowToCurrentSheet()" class="px-2.5 py-1 bg-cyber-dark border border-cyber-neonCyan/40 hover:border-cyber-neonCyan text-cyber-neonCyan rounded hover:bg-cyber-neonCyan/10 transition">
                        <i class="fas fa-plus-square mr-1"></i> ROW
                    </button>
                    <button onclick="addColumnToCurrentSheet()" class="px-2.5 py-1 bg-cyber-dark border border-cyber-neonCyan/40 hover:border-cyber-neonCyan text-cyber-neonCyan rounded hover:bg-cyber-neonCyan/10 transition">
                        <i class="fas fa-plus-circle mr-1"></i> COL
                    </button>
                    
                    <!-- CSV Export Button -->
                    <button onclick="exportCurrentSheetCSV()" class="cyber-btn px-3 py-1 bg-cyber-neonMagenta/20 border border-cyber-neonMagenta text-cyber-neonMagenta hover:bg-cyber-neonMagenta hover:text-black font-bold transition">
                        <i class="fas fa-file-export mr-1"></i> EXPORT CSV
                    </button>
                </div>
            </div>

            <!-- Formula Bar -->
            <div class="bg-cyber-dark/80 border border-cyber-border px-3 py-1.5 flex items-center space-x-2 text-xs">
                <span class="text-cyber-neonMagenta font-bold font-orbitron">FX //</span>
                <span id="selected-cell-id" class="px-2 py-0.5 bg-cyber-black border border-cyber-neonCyan/30 text-cyber-neonCyan font-mono">A1</span>
                <input type="text" id="formula-input" oninput="handleFormulaInput(this.value)" placeholder="Enter numeric value or formula (e.g. =SUM(C2:C5), text data)" class="flex-1 bg-cyber-black/90 border border-cyber-border focus:border-cyber-neonCyan text-white px-2 py-1 outline-none font-mono">
            </div>

            <!-- Interactive Spreadsheet Data Matrix -->
            <div class="flex-1 bg-cyber-dark/90 border border-cyber-neonCyan/30 rounded overflow-auto relative glow-cyan">
                <table id="spreadsheet-table" class="w-full border-collapse text-xs font-mono select-text">
                    <thead id="spreadsheet-head" class="sticky top-0 bg-cyber-panel border-b border-cyber-neonCyan/40 text-cyber-neonCyan z-10">
                        <!-- Headings dynamically populated -->
                    </thead>
                    <tbody id="spreadsheet-body" class="divide-y divide-cyber-border/40">
                        <!-- Rows dynamically populated -->
                    </tbody>
                </table>
            </div>
        </section>

        <!-- ================= TAB 2: NET-SEARCH (CYBERPUNK SEARCH ENGINE) ================= -->
        <section id="tab-netsearch" class="hidden flex-1 flex-col gap-4 overflow-y-auto">
            <!-- Search Header Box -->
            <div class="bg-cyber-panel/90 border border-cyber-neonCyan/50 p-6 rounded cyber-corner glow-cyan relative overflow-hidden">
                <div class="absolute -right-10 -bottom-10 opacity-10 text-cyber-neonCyan text-9xl pointer-events-none">
                    <i class="fas fa-search"></i>
                </div>

                <div class="max-w-3xl mx-auto space-y-4">
                    <div class="text-center space-y-1">
                        <h2 class="font-orbitron font-black text-2xl text-cyber-neonCyan tracking-widest text-glow-cyan">
                            NET-SEARCH // DEEP-NET QUERY MATRIX
                        </h2>
                        <p class="text-xs text-cyber-textMuted font-mono">
                            EXECUTE REAL-TIME SEARCH VIA EXTERNAL PROXIES OR INTERNAL D.H DATA NODES
                        </p>
                    </div>

                    <!-- Search Bar input -->
                    <form onsubmit="handleNetSearch(event)" class="flex items-center space-x-2">
                        <div class="relative flex-1">
                            <i class="fas fa-terminal absolute left-4 top-3.5 text-cyber-neonCyan"></i>
                            <input type="text" id="net-search-input" placeholder="Query Matrix or external Web (e.g., 'Cyberpunk Data', 'AI Models', 'Cybersecurity')..." 
                                class="w-full bg-cyber-black/90 border-2 border-cyber-neonCyan/60 focus:border-cyber-neonCyan text-white pl-11 pr-4 py-3 rounded text-sm font-mono outline-none shadow-[0_0_15px_rgba(0,243,255,0.2)]">
                        </div>
                        <button type="submit" class="cyber-btn px-6 py-3 bg-cyber-neonCyan text-black font-orbitron font-bold text-sm hover:bg-white transition-all shadow-[0_0_15px_rgba(0,243,255,0.5)]">
                            SEARCH
                        </button>
                    </form>

                    <!-- Search Engine Mode Radio Switcher -->
                    <div class="flex items-center justify-center space-x-6 text-xs font-mono">
                        <label class="flex items-center space-x-2 cursor-pointer text-cyber-neonCyan">
                            <input type="radio" name="search-engine" value="simulated" checked class="accent-cyber-neonCyan">
                            <span>INTERNAL D.H MATRIX QUERY</span>
                        </label>
                        <label class="flex items-center space-x-2 cursor-pointer text-cyber-textMuted hover:text-white">
                            <input type="radio" name="search-engine" value="google" class="accent-cyber-neonCyan">
                            <span>GOOGLE PROXY</span>
                        </label>
                        <label class="flex items-center space-x-2 cursor-pointer text-cyber-textMuted hover:text-white">
                            <input type="radio" name="search-engine" value="duckduckgo" class="accent-cyber-neonCyan">
                            <span>DUCKDUCKGO ENCRYPTED</span>
                        </label>
                    </div>
                </div>
            </div>

            <!-- Quick Matrix Shortcuts / Cyber Nodes -->
            <div class="grid grid-cols-2 md:grid-cols-4 gap-3">
                <a href="https://github.com" target="_blank" onclick="playBeep(800, 0.05)" class="bg-cyber-panel/60 border border-cyber-border hover:border-cyber-neonCyan p-3 rounded flex items-center space-x-3 transition group">
                    <div class="w-8 h-8 rounded bg-cyber-neonCyan/10 border border-cyber-neonCyan/30 flex items-center justify-center text-cyber-neonCyan group-hover:scale-110 transition-transform">
                        <i class="fab fa-github"></i>
                    </div>
                    <div>
                        <div class="text-xs font-bold text-white group-hover:text-cyber-neonCyan">GITHUB REPO</div>
                        <div class="text-[10px] text-cyber-textMuted">Source Code Matrix</div>
                    </div>
                </a>

                <a href="https://wikipedia.org" target="_blank" onclick="playBeep(800, 0.05)" class="bg-cyber-panel/60 border border-cyber-border hover:border-cyber-neonMagenta p-3 rounded flex items-center space-x-3 transition group">
                    <div class="w-8 h-8 rounded bg-cyber-neonMagenta/10 border border-cyber-neonMagenta/30 flex items-center justify-center text-cyber-neonMagenta group-hover:scale-110 transition-transform">
                        <i class="fas fa-database"></i>
                    </div>
                    <div>
                        <div class="text-xs font-bold text-white group-hover:text-cyber-neonMagenta">WIKIPEDIA NODE</div>
                        <div class="text-[10px] text-cyber-textMuted">Global Knowledge Archive</div>
                    </div>
                </a>

                <a href="https://news.ycombinator.com" target="_blank" onclick="playBeep(800, 0.05)" class="bg-cyber-panel/60 border border-cyber-border hover:border-cyber-neonYellow p-3 rounded flex items-center space-x-3 transition group">
                    <div class="w-8 h-8 rounded bg-cyber-neonYellow/10 border border-cyber-neonYellow/30 flex items-center justify-center text-cyber-neonYellow group-hover:scale-110 transition-transform">
                        <i class="fas fa-newspaper"></i>
                    </div>
                    <div>
                        <div class="text-xs font-bold text-white group-hover:text-cyber-neonYellow">HACKER NEWS</div>
                        <div class="text-[10px] text-cyber-textMuted">Net Cyber Feed</div>
                    </div>
                </a>

                <a href="https://arxiv.org" target="_blank" onclick="playBeep(800, 0.05)" class="bg-cyber-panel/60 border border-cyber-border hover:border-cyber-neonGreen p-3 rounded flex items-center space-x-3 transition group">
                    <div class="w-8 h-8 rounded bg-cyber-neonGreen/10 border border-cyber-neonGreen/30 flex items-center justify-center text-cyber-neonGreen group-hover:scale-110 transition-transform">
                        <i class="fas fa-atom"></i>
                    </div>
                    <div>
                        <div class="text-xs font-bold text-white group-hover:text-cyber-neonGreen">ARXIV RESEARCH</div>
                        <div class="text-[10px] text-cyber-textMuted">Quantum & Tech Papers</div>
                    </div>
                </a>
            </div>

            <!-- Net Search Results Container -->
            <div class="bg-cyber-dark/80 border border-cyber-border rounded p-4 flex-1 flex flex-col space-y-3">
                <div class="flex items-center justify-between border-b border-cyber-border pb-2">
                    <span class="text-xs font-orbitron font-bold text-cyber-neonCyan">SEARCH RESULTS MATRIX</span>
                    <span id="search-result-count" class="text-xs text-cyber-textMuted">0 NODES DISCOVERED</span>
                </div>

                <div id="search-results-list" class="space-y-3 overflow-y-auto max-h-[400px] pr-2">
                    <!-- Default initial status -->
                    <div class="text-center py-10 text-cyber-textMuted">
                        <i class="fas fa-satellite-dish text-4xl mb-3 text-cyber-neonCyan/40 animate-pulse"></i>
                        <p class="text-sm">AWAITING TARGET QUERY INPUT PARAMETERS...</p>
                    </div>
                </div>
            </div>
        </section>

        <!-- ================= TAB 3: SYSTEM LOGS & TERMINAL ================= -->
        <section id="tab-terminal" class="hidden flex-1 flex-col gap-2 overflow-hidden">
            <div class="bg-cyber-panel border border-cyber-neonMagenta/40 p-2 rounded flex items-center justify-between">
                <span class="text-xs font-orbitron font-bold text-cyber-neonMagenta flex items-center gap-2">
                    <i class="fas fa-terminal"></i> D.H CONSOLE TERMINAL
                </span>
                <button onclick="clearTerminalLogs()" class="px-2 py-0.5 border border-cyber-border hover:border-cyber-neonMagenta text-xs text-cyber-textMuted hover:text-white rounded">
                    CLEAR LOGS
                </button>
            </div>

            <div id="terminal-output" class="flex-1 bg-cyber-black/95 border border-cyber-border rounded p-4 font-mono text-xs overflow-y-auto space-y-1.5 text-slate-300 shadow-inner">
                <div class="text-cyber-neonCyan">[SYSTEM INITIALIZED] D.H Terminal Version 4.02. Ready.</div>
                <div class="text-cyber-textMuted">[SECURITY] Matrix Firewall Status: ACTIVE (1024-bit matrix).</div>
            </div>

            <!-- Custom Command Input -->
            <form onsubmit="handleTerminalCommand(event)" class="flex items-center space-x-2">
                <span class="text-cyber-neonMagenta font-bold text-sm font-mono">&gt;</span>
                <input type="text" id="terminal-input" placeholder="Type command (e.g. 'help', 'status', 'clear', 'sheets', 'matrix')..." class="flex-1 bg-cyber-dark border border-cyber-border focus:border-cyber-neonMagenta text-white px-3 py-2 rounded text-xs outline-none font-mono">
                <button type="submit" class="cyber-btn px-4 py-2 bg-cyber-neonMagenta/20 border border-cyber-neonMagenta text-cyber-neonMagenta hover:bg-cyber-neonMagenta hover:text-black text-xs font-bold">
                    EXEC
                </button>
            </form>
        </section>

    </main>

    <script>
        /* ==========================================================================
           AUDIO SYNTHESIZER (Web Audio API - Zero External Assets)
           ========================================================================== */
        let audioCtx = null;
        let soundEnabled = true;

        function initAudio() {
            if (!audioCtx) {
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            }
        }

        function playBeep(freq = 600, duration = 0.05, type = 'sine') {
            if (!soundEnabled) return;
            try {
                initAudio();
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                
                osc.type = type;
                osc.frequency.setValueAtTime(freq, audioCtx.currentTime);
                
                gain.gain.setValueAtTime(0.08, audioCtx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + duration);
                
                osc.connect(gain);
                gain.connect(audioCtx.destination);
                
                osc.start();
                osc.stop(audioCtx.currentTime + duration);
            } catch (e) {
                console.log('Audio playback constrained', e);
            }
        }

        function playSuccessSound() {
            if (!soundEnabled) return;
            playBeep(523.25, 0.08); // C5
            setTimeout(() => playBeep(659.25, 0.08), 80); // E5
            setTimeout(() => playBeep(783.99, 0.12), 160); // G5
        }

        function toggleAudio() {
            soundEnabled = !soundEnabled;
            const icon = document.getElementById('audio-icon');
            const status = document.getElementById('audio-status-text');
            if (soundEnabled) {
                icon.className = 'fas fa-volume-up';
                status.innerText = 'AUDIO ON';
                playBeep(800, 0.1);
            } else {
                icon.className = 'fas fa-volume-mute';
                status.innerText = 'AUDIO OFF';
            }
        }

        /* ==========================================================================
           ANIMATED MATRIX BACKGROUND
           ========================================================================== */
        function initMatrixBg() {
            const canvas = document.getElementById('matrix-bg');
            const ctx = canvas.getContext('2d');
            
            function resize() {
                canvas.width = window.innerWidth;
                canvas.height = window.innerHeight;
            }
            resize();
            window.addEventListener('resize', resize);

            const katakana = 'アァカサタナハマヤャラワガザダバパイィキシチニヒミリヰギジヂビピウゥクスツヌフムユュルグズブヅプエェケセテネヘメレヱゲゼデベペオォコソトノホモヨョロヲゴゾドボポヴッン';
            const latin = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789DH01';
            const alphabet = katakana + latin;

            const fontSize = 14;
            const columns = Math.floor(canvas.width / fontSize);
            const rainDrops = Array(columns).fill(1);

            function render() {
                ctx.fillStyle = 'rgba(5, 6, 8, 0.08)';
                ctx.fillRect(0, 0, canvas.width, canvas.height);

                ctx.fillStyle = '#00f3ff';
                ctx.font = fontSize + 'px monospace';

                for (let i = 0; i < rainDrops.length; i++) {
                    const text = alphabet.charAt(Math.floor(Math.random() * alphabet.length));
                    ctx.fillText(text, i * fontSize, rainDrops[i] * fontSize);

                    if (rainDrops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                        rainDrops[i] = 0;
                    }
                    rainDrops[i]++;
                }
            }

            setInterval(render, 40);
        }

        /* ==========================================================================
           WORKBOOK & WORKSHEETS CORE STATE AND OPERATIONS
           ========================================================================== */
        // Default Worksheets State
        let workbook = {
            activeSheetIndex: 0,
            sheets: [
                {
                    name: 'DATA_SHEET_01',
                    cols: ['A', 'B', 'C', 'D', 'E', 'F'],
                    rowsCount: 12,
                    data: {
                        'A1': 'NODE_ID', 'B1': 'TARGET_NAME', 'C1': 'UNIT_COST', 'D1': 'UNITS', 'E1': 'TOTAL_CREDITS',
                        'A2': 'NX-101',  'B2': 'Quantum Core',  'C2': '1200',      'D2': '4',     'E2': '=C2*D2',
                        'A3': 'NX-102',  'B3': 'Cyber Optics',  'C3': '350',       'D3': '10',    'E3': '=C3*D3',
                        'A4': 'NX-103',  'B4': 'Neural Link',   'C4': '2100',      'D4': '2',     'E4': '=C4*D4',
                        'A5': 'NX-104',  'B5': 'Plasma Deck',   'C5': '850',       'D5': '5',     'E5': '=C5*D5'
                    }
                },
                {
                    name: 'FINANCIAL_LOGS',
                    cols: ['A', 'B', 'C', 'D', 'E'],
                    rowsCount: 10,
                    data: {
                        'A1': 'QUARTER', 'B1': 'REVENUE', 'C1': 'EXPENSES', 'D1': 'NET_PROFIT',
                        'A2': 'Q1_2026', 'B2': '50000',   'C2': '22000',    'D2': '=B2-C2',
                        'A3': 'Q2_2026', 'B3': '68000',   'C3': '31000',    'D3': '=B3-C3',
                        'A4': 'Q4_2026', 'B4': '92000',   'C4': '40000',    'D4': '=B4-C4'
                    }
                }
            ]
        };

        let selectedCellId = 'A1';

        // Evaluate formula or numerical value
        function evaluateCellValue(sheet, cellKey, visited = new Set()) {
            const raw = sheet.data[cellKey];
            if (!raw) return '';
            
            // Handle Formula (starts with =)
            if (raw.startsWith('=')) {
                if (visited.has(cellKey)) return '#CIRCULAR!';
                visited.add(cellKey);

                try {
                    let expr = raw.substring(1).toUpperCase();

                    // Basic SUM function support: =SUM(C2:C5)
                    if (expr.startsWith('SUM(') && expr.endsWith(')')) {
                        const range = expr.substring(4, expr.length - 1);
                        const [startCell, endCell] = range.split(':');
                        if (startCell && endCell) {
                            const startCol = startCell.charAt(0);
                            const startRow = parseInt(startCell.substring(1));
                            const endCol = endCell.charAt(0);
                            const endRow = parseInt(endCell.substring(1));

                            let sum = 0;
                            for (let r = startRow; r <= endRow; r++) {
                                const k = `${startCol}${r}`;
                                const val = parseFloat(evaluateCellValue(sheet, k, new Set(visited))) || 0;
                                sum += val;
                            }
                            return sum;
                        }
                    }

                    // Replace cell references with actual values (e.g. C2*D2)
                    expr = expr.replace(/([A-Z]+[0-9]+)/g, (match) => {
                        const val = parseFloat(evaluateCellValue(sheet, match, new Set(visited)));
                        return isNaN(val) ? 0 : val;
                    });

                    // Evaluate basic math safely
                    const result = Function(`'use strict'; return (${expr})`)();
                    return isNaN(result) ? '#ERROR!' : result;
                } catch (err) {
                    return '#ERR!';
                }
            }

            return raw;
        }

        // Render Worksheet Tabs
        function renderWorksheetTabs() {
            const container = document.getElementById('worksheet-tabs-container');
            container.innerHTML = '';

            workbook.sheets.forEach((sheet, idx) => {
                const isActive = idx === workbook.activeSheetIndex;
                const btn = document.createElement('button');
                btn.className = `px-3 py-1 rounded text-xs font-bold font-mono transition flex items-center space-x-1 border ${
                    isActive 
                    ? 'bg-cyber-neonCyan/20 text-cyber-neonCyan border-cyber-neonCyan shadow-[0_0_8px_rgba(0,243,255,0.3)]' 
                    : 'bg-cyber-dark text-cyber-textMuted border-cyber-border hover:text-white'
                }`;
                btn.innerHTML = `
                    <span>${sheet.name}</span>
                    ${workbook.sheets.length > 1 ? `<i onclick="deleteSheet(${idx}, event)" class="fas fa-times text-[10px] ml-1 hover:text-cyber-neonMagenta"></i>` : ''}
                `;
                btn.onclick = () => {
                    playBeep(700, 0.04);
                    workbook.activeSheetIndex = idx;
                    renderSpreadsheet();
                    renderWorksheetTabs();
                    logTerminal(`Switched active worksheet to: ${sheet.name}`);
                };
                container.appendChild(btn);
            });
        }

        // Render Spreadsheet Table Grid
        function renderSpreadsheet() {
            const sheet = workbook.sheets[workbook.activeSheetIndex];
            const headEl = document.getElementById('spreadsheet-head');
            const bodyEl = document.getElementById('spreadsheet-body');

            // Render Header
            let headHTML = '<tr><th class="w-10 p-2 bg-cyber-panel border border-cyber-border text-center text-cyber-textMuted font-mono">#</th>';
            sheet.cols.forEach(col => {
                headHTML += `<th class="p-2 border border-cyber-border text-center font-bold tracking-wider">${col}</th>`;
            });
            headHTML += '</tr>';
            headEl.innerHTML = headHTML;

            // Render Body Rows
            let bodyHTML = '';
            for (let r = 1; r <= sheet.rowsCount; r++) {
                bodyHTML += `<tr><td class="bg-cyber-panel border border-cyber-border text-center text-cyber-textMuted font-mono select-none">${r}</td>`;
                
                sheet.cols.forEach(col => {
                    const cellId = `${col}${r}`;
                    const rawVal = sheet.data[cellId] || '';
                    const evalVal = evaluateCellValue(sheet, cellId);
                    const isSelected = selectedCellId === cellId;

                    bodyHTML += `
                        <td id="cell-${cellId}" 
                            onclick="selectCell('${cellId}')"
                            ondblclick="makeCellEditable('${cellId}')"
                            class="p-2 border border-cyber-border/60 transition-all font-mono min-w-[100px] h-8 relative cursor-pointer ${
                                isSelected ? 'bg-cyber-neonCyan/20 border-cyber-neonCyan outline outline-1 outline-cyber-neonCyan text-white font-bold' : 'hover:bg-cyber-panel/60 text-slate-200'
                            }">
                            ${evalVal}
                        </td>
                    `;
                });
                bodyHTML += '</tr>';
            }
            bodyEl.innerHTML = bodyHTML;

            calculateMetrics();
        }

        // Select Cell Handler
        function selectCell(cellId) {
            selectedCellId = cellId;
            document.getElementById('selected-cell-id').innerText = cellId;
            
            const sheet = workbook.sheets[workbook.activeSheetIndex];
            const val = sheet.data[cellId] || '';
            document.getElementById('formula-input').value = val;

            playBeep(900, 0.02);
            renderSpreadsheet();
        }

        // Make Cell Directly Editable on Double Click
        function makeCellEditable(cellId) {
            const sheet = workbook.sheets[workbook.activeSheetIndex];
            const cellEl = document.getElementById(`cell-${cellId}`);
            if (!cellEl) return;

            const currentRawVal = sheet.data[cellId] || '';
            cellEl.innerHTML = `<input type="text" id="active-cell-input" value="${currentRawVal}" class="w-full h-full bg-cyber-black text-cyber-neonCyan border border-cyber-neonCyan px-1 outline-none font-mono text-xs">`;
            
            const input = document.getElementById('active-cell-input');
            input.focus();

            input.onblur = () => {
                sheet.data[cellId] = input.value;
                renderSpreadsheet();
                logTerminal(`Cell [${cellId}] updated in ${sheet.name}: "${input.value}"`);
            };

            input.onkeydown = (e) => {
                if (e.key === 'Enter') {
                    input.blur();
                }
            };
        }

        // Handle Formula Bar Live Input
        function handleFormulaInput(val) {
            const sheet = workbook.sheets[workbook.activeSheetIndex];
            sheet.data[selectedCellId] = val;
            renderSpreadsheet();
        }

        // Add Row / Column
        function addRowToCurrentSheet() {
            const sheet = workbook.sheets[workbook.activeSheetIndex];
            sheet.rowsCount += 1;
            renderSpreadsheet();
            playSuccessSound();
            logTerminal(`Added new row (${sheet.rowsCount}) to ${sheet.name}`);
        }

        function addColumnToCurrentSheet() {
            const sheet = workbook.sheets[workbook.activeSheetIndex];
            const lastCol = sheet.cols[sheet.cols.length - 1];
            const nextColChar = String.fromCharCode(lastCol.charCodeAt(0) + 1);
            if (sheet.cols.length < 12) {
                sheet.cols.push(nextColChar);
                renderSpreadsheet();
                playSuccessSound();
                logTerminal(`Added new column [${nextColChar}] to ${sheet.name}`);
            } else {
                alert('Maximum sheet width reached for D.H Matrix demo.');
            }
        }

        // Add New Sheet
        function createNewWorksheetPrompt() {
            const name = prompt('Enter New Worksheet Cyber-Tag / Title:', `SHEET_0${workbook.sheets.length + 1}`);
            if (name) {
                workbook.sheets.push({
                    name: name.toUpperCase().replace(/\s+/g, '_'),
                    cols: ['A', 'B', 'C', 'D', 'E'],
                    rowsCount: 10,
                    data: {}
                });
                workbook.activeSheetIndex = workbook.sheets.length - 1;
                renderWorksheetTabs();
                renderSpreadsheet();
                playSuccessSound();
                logTerminal(`Created new worksheet: ${name}`);
            }
        }

        function deleteSheet(idx, event) {
            event.stopPropagation();
            if (confirm(`Delete worksheet '${workbook.sheets[idx].name}'?`)) {
                workbook.sheets.splice(idx, 1);
                workbook.activeSheetIndex = Math.max(0, idx - 1);
                renderWorksheetTabs();
                renderSpreadsheet();
                logTerminal(`Deleted worksheet index ${idx}`);
            }
        }

        // Calculate Dynamic Metrics (Sum, Avg, Count)
        function calculateMetrics() {
            const sheet = workbook.sheets[workbook.activeSheetIndex];
            let sum = 0;
            let count = 0;

            Object.keys(sheet.data).forEach(cellKey => {
                const val = parseFloat(evaluateCellValue(sheet, cellKey));
                if (!isNaN(val)) {
                    sum += val;
                    count++;
                }
            });

            document.getElementById('stat-sum').innerText = sum.toLocaleString();
            document.getElementById('stat-avg').innerText = count > 0 ? (sum / count).toFixed(2) : 0;
            document.getElementById('stat-count').innerText = count;
        }

        // Export CSV Functionality
        function exportCurrentSheetCSV() {
            const sheet = workbook.sheets[workbook.activeSheetIndex];
            let csvContent = "data:text/csv;charset=utf-8,";

            // Headers
            csvContent += sheet.cols.join(",") + "\n";

            // Rows
            for (let r = 1; r <= sheet.rowsCount; r++) {
                let rowArray = [];
                sheet.cols.forEach(col => {
                    const evalVal = evaluateCellValue(sheet, `${col}${r}`);
                    rowArray.push(`"${evalVal}"`);
                });
                csvContent += rowArray.join(",") + "\n";
            }

            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", `${sheet.name}_EXPORT.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);

            playSuccessSound();
            logTerminal(`Exported sheet ${sheet.name} as CSV file.`);
        }

        /* ==========================================================================
           NET-SEARCH ENGINE LOGIC
           ========================================================================== */
        function handleNetSearch(event) {
            event.preventDefault();
            const query = document.getElementById('net-search-input').value.trim();
            if (!query) return;

            playBeep(1000, 0.08);
            logTerminal(`Executed NET-SEARCH query: "${query}"`);

            const mode = document.querySelector('input[name="search-engine"]:checked').value;

            if (mode === 'google') {
                window.open(`https://www.google.com/search?q=${encodeURIComponent(query)}`, '_blank');
                return;
            } else if (mode === 'duckduckgo') {
                window.open(`https://duckduckgo.com/?q=${encodeURIComponent(query)}`, '_blank');
                return;
            }

            // Simulated Cyberpunk In-App Search Generator
            const resultsContainer = document.getElementById('search-results-list');
            resultsContainer.innerHTML = `
                <div class="text-center py-6 text-cyber-neonCyan">
                    <i class="fas fa-spinner fa-spin text-2xl mb-2"></i>
                    <p class="font-mono text-xs">DECRYPTING NET NODES FOR: "${query.toUpperCase()}"...</p>
                </div>
            `;

            setTimeout(() => {
                const simulatedNodes = [
                    {
                        title: `D.H NODE // ${query.toUpperCase()}_PROTOCOL_V1`,
                        url: `https://dh-matrix.net/nodes/${encodeURIComponent(query)}`,
                        desc: `Encrypted telemetry data block matching matrix signature '${query}'. Data sub-routing online.`
                    },
                    {
                        title: `QUANTUM ARCHIVE: ${query.toUpperCase()} RESEARCH`,
                        url: `https://arxiv.org/search/?query=${encodeURIComponent(query)}`,
                        desc: `High-density knowledge grid containing whitepapers and neural network models for ${query}.`
                    },
                    {
                        title: `GLOBAL DATA MATRIX: ${query.toUpperCase()}`,
                        url: `https://wikipedia.org/wiki/${encodeURIComponent(query)}`,
                        desc: `Public decrypt database record detailing origins, parameters, and specifications of ${query}.`
                    }
                ];

                let html = '';
                simulatedNodes.forEach(node => {
                    html += `
                        <div class="p-3 bg-cyber-panel/80 border border-cyber-border hover:border-cyber-neonCyan rounded transition group">
                            <div class="flex items-center justify-between">
                                <a href="${node.url}" target="_blank" onclick="playBeep(900, 0.04)" class="text-sm font-bold font-orbitron text-cyber-neonCyan group-hover:underline flex items-center gap-2">
                                    <i class="fas fa-network-wired text-xs"></i>
                                    ${node.title}
                                </a>
                                <span class="text-[10px] font-mono text-cyber-neonGreen border border-cyber-neonGreen/30 px-1.5 py-0.5 rounded">ONLINE</span>
                            </div>
                            <p class="text-xs text-slate-300 mt-1 font-mono">${node.desc}</p>
                            <div class="text-[10px] text-cyber-textMuted mt-1 font-mono">${node.url}</div>
                        </div>
                    `;
                });

                resultsContainer.innerHTML = html;
                document.getElementById('search-result-count').innerText = `${simulatedNodes.length} NODES DISCOVERED`;
                playSuccessSound();
            }, 600);
        }

        /* ==========================================================================
           TERMINAL AND UTILITIES
           ========================================================================== */
        function logTerminal(msg) {
            const out = document.getElementById('terminal-output');
            const time = new Date().toISOString().split('T')[1].slice(0, 8);
            const line = document.createElement('div');
            line.innerHTML = `<span class="text-cyber-textMuted">[${time}]</span> <span class="text-cyber-neonCyan">&gt;</span> ${msg}`;
            out.appendChild(line);
            out.scrollTop = out.scrollHeight;
        }

        function clearTerminalLogs() {
            document.getElementById('terminal-output').innerHTML = '';
            logTerminal('Terminal logs cleared.');
        }

        function handleTerminalCommand(e) {
            e.preventDefault();
            const input = document.getElementById('terminal-input');
            const cmd = input.value.trim().toLowerCase();
            input.value = '';

            if (!cmd) return;
            logTerminal(`COMMAND EXEC: ${cmd}`);

            switch (cmd) {
                case 'help':
                    logTerminal('AVAILABLE COMMANDS: help, status, clear, sheets, export, matrix, ping');
                    break;
                case 'status':
                    logTerminal(`SYS VER: 4.02 | ACTIVE SHEETS: ${workbook.sheets.length} | AUDIO: ${soundEnabled ? 'ON' : 'OFF'}`);
                    break;
                case 'clear':
                    clearTerminalLogs();
                    break;
                case 'sheets':
                    workbook.sheets.forEach((s, i) => logTerminal(`Sheet [${i}]: ${s.name} (${s.cols.length} Cols x ${s.rowsCount} Rows)`));
                    break;
                case 'export':
                    exportCurrentSheetCSV();
                    break;
                case 'ping':
                    logTerminal('PONG! Matrix node responsiveness 12ms.');
                    break;
                default:
                    logTerminal(`UNKNOWN COMMAND: '${cmd}'. Type 'help' for instructions.`);
                    break;
            }
        }

        // Tab Switcher
        function switchTab(tabId) {
            playBeep(750, 0.05);
            ['workbook', 'netsearch', 'terminal'].forEach(t => {
                const el = document.getElementById(`tab-${t}`);
                const btn = document.getElementById(`nav-btn-${t}`);
                
                if (t === tabId) {
                    el.classList.remove('hidden');
                    el.classList.add('flex');
                    btn.className = 'cyber-btn px-4 py-1.5 font-orbitron text-xs font-bold flex items-center space-x-2 bg-cyber-neonCyan text-black shadow-[0_0_10px_rgba(0,243,255,0.4)]';
                } else {
                    el.classList.add('hidden');
                    el.classList.remove('flex');
                    btn.className = 'cyber-btn px-4 py-1.5 font-orbitron text-xs font-bold flex items-center space-x-2 bg-cyber-panel text-cyber-textMuted hover:text-cyber-neonCyan hover:bg-cyber-neonCyan/10 border border-cyber-border';
                }
            });
            logTerminal(`UI View changed to: ${tabId.toUpperCase()}`);
        }

        // Clock & Latency simulation ticker
        function startSystemClock() {
            const clockEl = document.getElementById('sys-clock');
            const latencyEl = document.getElementById('sys-latency');
            let seconds = 0;

            setInterval(() => {
                seconds++;
                const hrs = String(Math.floor(seconds / 3600)).padStart(2, '0');
                const mins = String(Math.floor((seconds % 3600) / 60)).padStart(2, '0');
                const secs = String(seconds % 60).padStart(2, '0');
                clockEl.innerText = `${hrs}:${mins}:${secs}`;

                if (seconds % 5 === 0) {
                    const simLatency = Math.floor(Math.random() * 8) + 10;
                    latencyEl.innerText = `${simLatency}ms`;
                }
            }, 1000);
        }

        /* ==========================================================================
           INITIALIZATION
           ========================================================================== */
        window.onload = function() {
            initMatrixBg();
            renderWorksheetTabs();
            renderSpreadsheet();
            startSystemClock();
            logTerminal('D.H Data Terminal Ready. Workbook & Net-Search active.');
        };
    </script>
</body>
</html>
