<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rationatsu's Fantasy Realm | Interactive Portfolio</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts for Pixel/RPG feel -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=VT323&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --pixel-border-color: #8b5cf6;
            --pixel-bg-dark: rgba(15, 23, 42, 0.88);
            --pixel-gold: #fbbf24;
        }

        body {
            font-family: 'VT323', monospace;
            background-color: #0d0e15;
            color: #e2e8f0;
            overflow-x: hidden;
            letter-spacing: 1px;
        }

        .font-pixel {
            font-family: 'Press Start 2P', cursive;
        }

        /* Pixel art border utility */
        .pixel-box {
            background: var(--pixel-bg-dark);
            border: 4px solid #4c1d95;
            box-shadow: 
                inset -4px -4px 0px 0px #2e1065,
                inset 4px 4px 0px 0px #a78bfa,
                0px 0px 15px rgba(139, 92, 246, 0.4);
            image-rendering: pixelated;
        }

        .pixel-button {
            transition: all 0.1s ease;
            box-shadow: 0 4px 0 #3b0764;
            position: relative;
            top: 0;
        }

        .pixel-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 0 #3b0764, 0 0 10px rgba(251, 191, 36, 0.5);
            background-color: #7c3aed;
        }

        .pixel-button:active {
            transform: translateY(4px);
            box-shadow: 0 0 0 #3b0764;
        }

        /* Background Animated Container */
        .bg-gif-container {
            background-image: url('https://i.pinimg.com/originals/be/b1/fe/beb1fe077b35b3e85be70712dc81d6ae.gif');
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
        }

        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #1e1b4b;
        }
        ::-webkit-scrollbar-thumb {
            background: #7c3aed;
            border-radius: 4px;
        }

        /* Glow effects */
        .glow-gold {
            text-shadow: 0 0 8px rgba(251, 191, 36, 0.8);
        }
        .glow-purple {
            text-shadow: 0 0 8px rgba(168, 85, 247, 0.8);
        }

        /* Floating Animation */
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-8px); }
            100% { transform: translateY(0px); }
        }
        .animate-float {
            animation: float 4s ease-in-out infinite;
        }

        /* Canvas particles */
        #magic-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            pointer-events: none;
            z-index: 10;
        }
    </style>
</head>
<body class="bg-gif-container min-h-screen relative flex flex-col justify-between items-center p-2 md:p-6">

    <!-- Magic Particle Canvas -->
    <canvas id="magic-canvas"></canvas>

    <!-- Top Floating Audio/SFX Control HUD -->
    <header class="w-full max-w-4xl z-20 flex justify-between items-center mb-4 px-2">
        <div class="pixel-box px-3 py-1 text-sm flex items-center space-x-2 text-yellow-400 font-pixel">
            <i class="fa-solid fa-shield-halved animate-pulse"></i>
            <span>LVL. 99 ARTIST & DEV</span>
        </div>
        <div class="flex space-x-2">
            <button id="sfx-toggle" onclick="toggleSFX()" class="pixel-box px-3 py-2 text-xs bg-purple-900 hover:bg-purple-800 text-white font-pixel flex items-center space-x-1">
                <i class="fa-solid fa-volume-high" id="sfx-icon"></i>
                <span class="hidden sm:inline">SFX</span>
            </button>
            <button id="bgm-toggle" onclick="toggleBGM()" class="pixel-box px-3 py-2 text-xs bg-purple-900 hover:bg-purple-800 text-yellow-300 font-pixel flex items-center space-x-1">
                <i class="fa-solid fa-music" id="bgm-icon"></i>
                <span class="hidden sm:inline">MUSIC</span>
            </button>
        </div>
    </header>

    <!-- Main RPG UI Window -->
    <main class="w-full max-w-4xl z-20 my-auto">
        <div class="pixel-box p-4 md:p-8 rounded-lg relative overflow-hidden backdrop-blur-sm">
            
            <!-- Character Header Banner -->
            <div class="text-center mb-6 border-b-4 border-purple-800 pb-4 relative">
                <div class="inline-block relative">
                    <!-- Animated Avatar/Icon -->
                    <div class="w-24 h-24 md:w-32 md:h-32 mx-auto mb-2 rounded-full border-4 border-amber-400 overflow-hidden shadow-2xl animate-float bg-purple-950">
                        <img src="https://cdn.dbimg.app/PFeCSDG1.jpg" alt="Rationatsu" class="w-full h-full object-cover" onerror="this.src='https://placehold.co/150x150/4c1d95/fbbf24?text=Rationatsu'">
                    </div>
                    <span class="absolute bottom-1 right-2 bg-emerald-500 text-black text-xs font-bold px-2 py-0.5 rounded-full font-pixel border border-black">ONLINE</span>
                </div>
                
                <h1 class="text-3xl md:text-5xl font-bold font-pixel text-amber-300 glow-gold tracking-wide mt-2">RATIONATSU</h1>
                <p class="text-xl md:text-2xl text-purple-200 mt-1 glow-purple">⚔️ Digital Artist & Junior Developer 🎨</p>
                
                <!-- Status Bars (RPG HUD) -->
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 max-w-md mx-auto mt-4 text-xs font-pixel">
                    <div>
                        <div class="flex justify-between mb-1 text-red-400"><span>HP (Creative Energy)</span><span>100/100</span></div>
                        <div class="w-full bg-gray-900 h-3 border border-red-500 p-0.5">
                            <div class="bg-red-500 h-full w-full"></div>
                        </div>
                    </div>
                    <div>
                        <div class="flex justify-between mb-1 text-blue-400"><span>MP (Logic & Code)</span><span>95/100</span></div>
                        <div class="w-full bg-gray-900 h-3 border border-blue-500 p-0.5">
                            <div class="bg-blue-400 h-full w-[95%]"></div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Navigation Tabs (Dropdown/Interactive Quest Log) -->
            <div class="grid grid-cols-2 sm:grid-cols-4 gap-2 mb-6 font-pixel text-xs">
                <button onclick="switchTab('profile')" id="btn-profile" class="tab-btn pixel-button bg-purple-700 text-white py-3 px-2 rounded border-2 border-amber-300 flex flex-col items-center justify-center space-y-1">
                    <i class="fa-solid fa-scroll text-base text-amber-300"></i>
                    <span>BIO & PROFILE</span>
                </button>
                <button onclick="switchTab('tech')" id="btn-tech" class="tab-btn pixel-button bg-purple-900 text-gray-300 py-3 px-2 rounded border-2 border-purple-500 flex flex-col items-center justify-center space-y-1">
                    <i class="fa-solid fa-wand-magic-sparkles text-base text-cyan-300"></i>
                    <span>TECH STACK</span>
                </button>
                <button onclick="switchTab('partners')" id="btn-partners" class="tab-btn pixel-button bg-purple-900 text-gray-300 py-3 px-2 rounded border-2 border-purple-500 flex flex-col items-center justify-center space-y-1">
                    <i class="fa-solid fa-handshake text-base text-emerald-300"></i>
                    <span>PARTNERS</span>
                </button>
                <button onclick="switchTab('quests')" id="btn-quests" class="tab-btn pixel-button bg-purple-900 text-gray-300 py-3 px-2 rounded border-2 border-purple-500 flex flex-col items-center justify-center space-y-1">
                    <i class="fa-solid fa-compass text-base text-rose-400"></i>
                    <span>SOCIAL QUESTS</span>
                </button>
            </div>

            <!-- TAB CONTENTS -->

            <!-- 1. Profile / Bio Tab -->
            <div id="tab-profile" class="tab-content space-y-4">
                <div class="bg-purple-950/70 p-4 border-2 border-purple-600 rounded text-lg md:text-xl">
                    <h2 class="text-2xl text-amber-300 font-pixel mb-2 flex items-center space-x-2">
                        <i class="fa-solid fa-feather-pointed"></i>
                        <span>TRAVELER'S BIOGRAPHY</span>
                    </h2>
                    <p class="leading-relaxed">
                        Halo! Saya <strong class="text-amber-300">Rationatsu</strong>, seorang Digital Artist & Developer. Selamat datang di markas digital saya! 🏰
                    </p>
                    <p class="mt-2 text-purple-200">
                        Saya membuat berbagai project visual dan pemrograman. Saya berharap project-project saya bisa dijadikan referensi dan inspirasi untuk karya-karya hebatmu! ✨
                    </p>
                    
                    <!-- Collapsible Dropdown Detail -->
                    <div class="mt-4 border-t border-purple-700 pt-3">
                        <button onclick="toggleAccordion('bio-extra')" class="w-full text-left font-pixel text-xs text-cyan-300 hover:text-cyan-100 flex justify-between items-center bg-purple-900/60 p-2 rounded border border-purple-500">
                            <span><i class="fa-solid fa-circle-info mr-1"></i> VIEW CHARACTER STATS & LOCATION</span>
                            <i id="bio-extra-arrow" class="fa-solid fa-chevron-down"></i>
                        </button>
                        <div id="bio-extra" class="hidden mt-3 space-y-2 text-base bg-black/40 p-3 rounded border border-purple-800">
                            <p>📍 <strong>Base Guild:</strong> Manado, North Sulawesi, Indonesia</p>
                            <p>🎨 <strong>Specialty:</strong> Character Illustration, Concept Art, Web Dev</p>
                            <p>🐉 <strong>Current Quest:</strong> Building interactive web experiences & art references.</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 2. Tech Stack Tab -->
            <div id="tab-tech" class="tab-content hidden space-y-4">
                <div class="bg-purple-950/70 p-4 border-2 border-purple-600 rounded">
                    <h2 class="text-2xl text-amber-300 font-pixel mb-4 flex items-center space-x-2">
                        <i class="fa-solid fa-toolbox"></i>
                        <span>SPELLBOOK & EQUIPMENT</span>
                    </h2>
                    <div class="grid grid-cols-2 sm:grid-cols-4 gap-3 text-center">
                        <div class="pixel-box p-3 bg-red-950/60 border-red-500">
                            <i class="fa-brands fa-html5 text-4xl text-red-500 mb-2"></i>
                            <div class="font-pixel text-xs text-white">HTML5</div>
                            <div class="text-xs text-gray-400">Structure</div>
                        </div>
                        <div class="pixel-box p-3 bg-blue-950/60 border-blue-500">
                            <i class="fa-brands fa-css3-alt text-4xl text-blue-400 mb-2"></i>
                            <div class="font-pixel text-xs text-white">CSS3</div>
                            <div class="text-xs text-gray-400">Styling & Magic</div>
                        </div>
                        <div class="pixel-box p-3 bg-yellow-950/60 border-yellow-500">
                            <i class="fa-brands fa-js text-4xl text-yellow-400 mb-2"></i>
                            <div class="font-pixel text-xs text-white">JAVASCRIPT</div>
                            <div class="text-xs text-gray-400">Interactivity</div>
                        </div>
                        <div class="pixel-box p-3 bg-amber-950/60 border-amber-500">
                            <i class="fa-brands fa-linux text-4xl text-amber-300 mb-2"></i>
                            <div class="font-pixel text-xs text-white">LINUX</div>
                            <div class="text-xs text-gray-400">OS Terminal</div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 3. Partners & Hosts Tab -->
            <div id="tab-partners" class="tab-content hidden space-y-4">
                <div class="bg-purple-950/70 p-4 border-2 border-purple-600 rounded">
                    <h2 class="text-2xl text-amber-300 font-pixel mb-4 flex items-center space-x-2">
                        <i class="fa-solid fa-handshake"></i>
                        <span>ALLIES & HOSTING PARTNERS</span>
                    </h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <!-- Partner 1 -->
                        <div class="pixel-box p-4 bg-purple-900/40 flex items-center space-x-4 border-purple-400">
                            <div class="bg-purple-950 p-3 rounded border border-purple-400">
                                <i class="fa-solid fa-sparkles text-3xl text-purple-300"></i>
                            </div>
                            <div>
                                <h3 class="font-pixel text-sm text-purple-200">Google Gemini</h3>
                                <p class="text-sm text-gray-300">AI Companion & Reference Assistant</p>
                            </div>
                        </div>
                        <!-- Partner 2 -->
                        <div class="pixel-box p-4 bg-purple-900/40 flex items-center space-x-4 border-purple-400">
                            <div class="bg-purple-950 p-2 rounded border border-purple-400 w-16 h-12 flex items-center justify-center">
                                <img src="https://cdn.prod.website-files.com/5e6aa3e3f001fad873b8e1f5/68cd7c3a47288bc0a652b8ee_znegppeohzlm0sjlvlil.png" alt="Base44" class="max-h-full object-contain">
                            </div>
                            <div>
                                <h3 class="font-pixel text-sm text-purple-200">Base44</h3>
                                <p class="text-sm text-gray-300">Hosting & Platform Deployment</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 4. Social Quests Tab -->
            <div id="tab-quests" class="tab-content hidden space-y-4">
                <div class="bg-purple-950/70 p-4 border-2 border-purple-600 rounded">
                    <h2 class="text-2xl text-amber-300 font-pixel mb-4 flex items-center space-x-2">
                        <i class="fa-solid fa-map-location-dot"></i>
                        <span>SOCIAL QUEST GUILD</span>
                    </h2>
                    <div class="space-y-3">
                        <a href="https://instagram.com/hikarurationatsu" target="_blank" onclick="playClickSound()" class="pixel-button block p-3 bg-rose-900/80 hover:bg-rose-800 text-white rounded border-2 border-rose-400 flex items-center justify-between">
                            <div class="flex items-center space-x-3">
                                <i class="fa-brands fa-instagram text-2xl text-pink-400"></i>
                                <span class="font-pixel text-xs">INSTAGRAM</span>
                            </div>
                            <span class="text-sm text-rose-200">@hikarurationatsu <i class="fa-solid fa-arrow-right ml-1"></i></span>
                        </a>

                        <a href="https://discord.com/users/arskhy" target="_blank" onclick="playClickSound()" class="pixel-button block p-3 bg-indigo-900/80 hover:bg-indigo-800 text-white rounded border-2 border-indigo-400 flex items-center justify-between">
                            <div class="flex items-center space-x-3">
                                <i class="fa-brands fa-discord text-2xl text-indigo-300"></i>
                                <span class="font-pixel text-xs">DISCORD</span>
                            </div>
                            <span class="text-sm text-indigo-200">arskhy <i class="fa-solid fa-arrow-right ml-1"></i></span>
                        </a>

                        <a href="mailto:hikarurationatsu@proton.me" onclick="playClickSound()" class="pixel-button block p-3 bg-emerald-900/80 hover:bg-emerald-800 text-white rounded border-2 border-emerald-400 flex items-center justify-between">
                            <div class="flex items-center space-x-3">
                                <i class="fa-solid fa-envelope text-2xl text-emerald-300"></i>
                                <span class="font-pixel text-xs">EMAIL</span>
                            </div>
                            <span class="text-sm text-emerald-200">hikarurationatsu@proton.me <i class="fa-solid fa-arrow-right ml-1"></i></span>
                        </a>
                    </div>
                </div>
            </div>

            <!-- Visitor Counter Badge HUD -->
            <div class="mt-6 pt-4 border-t-2 border-purple-800 flex flex-col sm:flex-row items-center justify-between text-sm text-purple-300 font-pixel gap-2">
                <div class="flex items-center space-x-2">
                    <i class="fa-solid fa-eye text-amber-300"></i>
                    <span>TRAVELER VISITS:</span>
                    <span class="bg-purple-900 px-2 py-0.5 rounded border border-purple-500 text-amber-300" id="visit-counter">0002098</span>
                </div>
                <div class="text-xs text-gray-400">
                    Press <span class="text-yellow-400">[TAB]</span> To Explore
                </div>
            </div>

        </div>
    </main>

    <!-- Footer -->
    <footer class="w-full max-w-4xl z-20 text-center text-xs font-pixel text-purple-300 mt-4 mb-2">
        <p>© 2026 RATIONATSU • CRAFTED WITH MAGICAL PIXELS & CODE</p>
    </footer>

    <!-- Tone.js for Retro Sound Effects -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/tone/14.8.49/Tone.js"></script>

    <script>
        // Sound System State
        let sfxEnabled = true;
        let bgmEnabled = false;
        let synth, bgmLoop;

        // Initialize Audio Synths
        function initAudio() {
            if (!synth) {
                synth = new Tone.Synth({
                    oscillator: { type: "square" },
                    envelope: { attack: 0.01, decay: 0.1, sustain: 0.1, release: 0.1 }
                }).toDestination();
                synth.volume.value = -12;
            }
        }

        function playClickSound() {
            if (!sfxEnabled) return;
            try {
                initAudio();
                Tone.start();
                synth.triggerAttackRelease("C6", "16n");
            } catch (e) { console.log(e); }
        }

        function playTabSound() {
            if (!sfxEnabled) return;
            try {
                initAudio();
                Tone.start();
                synth.triggerAttackRelease("E6", "16n");
            } catch (e) { console.log(e); }
        }

        function toggleSFX() {
            sfxEnabled = !sfxEnabled;
            const icon = document.getElementById('sfx-icon');
            icon.className = sfxEnabled ? "fa-solid fa-volume-high" : "fa-solid fa-volume-xmark";
            if (sfxEnabled) playClickSound();
        }

        function toggleBGM() {
            bgmEnabled = !bgmEnabled;
            const icon = document.getElementById('bgm-icon');
            icon.className = bgmEnabled ? "fa-solid fa-music animate-spin" : "fa-solid fa-music";

            if (bgmEnabled) {
                initAudio();
                Tone.start();
                if (!bgmLoop) {
                    const notes = ["C4", "E4", "G4", "B4", "A4", "G4", "E4", "D4"];
                    let index = 0;
                    bgmLoop = new Tone.Loop(time => {
                        synth.triggerAttackRelease(notes[index % notes.length], "8n", time);
                        index++;
                    }, "4n");
                }
                Tone.Transport.bpm.value = 90;
                Tone.Transport.start();
                bgmLoop.start(0);
            } else {
                if (bgmLoop) bgmLoop.stop();
            }
        }

        // Tab Switching Logic
        function switchTab(tabName) {
            playTabSound();
            
            // Hide all tabs
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            
            // Reset button styles
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('bg-purple-700', 'border-amber-300', 'text-white');
                btn.classList.add('bg-purple-900', 'border-purple-500', 'text-gray-300');
            });

            // Show target tab
            document.getElementById(`tab-${tabName}`).classList.remove('hidden');

            // Active button style
            const activeBtn = document.getElementById(`btn-${tabName}`);
            activeBtn.classList.remove('bg-purple-900', 'border-purple-500', 'text-gray-300');
            activeBtn.classList.add('bg-purple-700', 'border-amber-300', 'text-white');
        }

        // Accordion Toggle Logic
        function toggleAccordion(id) {
            playClickSound();
            const content = document.getElementById(id);
            const arrow = document.getElementById(`${id}-arrow`);
            if (content.classList.contains('hidden')) {
                content.classList.remove('hidden');
                arrow.className = "fa-solid fa-chevron-up";
            } else {
                content.classList.add('hidden');
                arrow.className = "fa-solid fa-chevron-down";
            }
        }

        // Magic Particle Canvas
        const canvas = document.getElementById('magic-canvas');
        const ctx = canvas.getContext('2d');
        let particles = [];

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        class Particle {
            constructor() {
                this.reset();
            }
            reset() {
                this.x = Math.random() * canvas.width;
                this.y = canvas.height + 10;
                this.size = Math.random() * 3 + 1;
                this.speedY = Math.random() * 1.5 + 0.5;
                this.speedX = (Math.random() - 0.5) * 0.8;
                this.opacity = Math.random() * 0.8 + 0.2;
                this.color = ['#fbbf24', '#a855f7', '#60a5fa', '#f43f5e'][Math.floor(Math.random() * 4)];
            }
            update() {
                this.y -= this.speedY;
                this.x += this.speedX;
                if (this.y < -10) this.reset();
            }
            draw() {
                ctx.fillStyle = this.color;
                ctx.globalAlpha = this.opacity;
                ctx.fillRect(Math.floor(this.x), Math.floor(this.y), this.size, this.size); // Pixel rendering
            }
        }

        for (let i = 0; i < 40; i++) {
            particles.push(new Particle());
        }

        function animateParticles() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach(p => {
                p.update();
                p.draw();
            });
            requestAnimationFrame(animateParticles);
        }
        animateParticles();
    </script>
</body>
</html>
