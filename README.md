
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Roblox Gateway | Romance Verification System</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Tone.js for Sound Effects -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/tone/14.8.49/Tone.js"></script>
    <!-- PrismJS for Syntax Highlighting -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism-tomorrow.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/components/prism-lua.min.js"></script>

    <!-- Custom Tailwind Configuration -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            dark: '#080808',
                            card: '#111111',
                            border: '#2a0a0a',
                            neon: '#ff2020',
                            accent: '#b00000'
                        }
                    },
                    animation: {
                        'pulse-glow': 'pulseGlow 2.5s infinite',
                        'float': 'float 5s ease-in-out infinite',
                    },
                    keyframes: {
                        pulseGlow: {
                            '0%, 100%': { filter: 'drop-shadow(0 0 15px rgba(255,32,32,0.5))' },
                            '50%': { filter: 'drop-shadow(0 0 5px rgba(255,32,32,0.2))' },
                        },
                        float: {
                            '0%, 100%': { transform: 'translateY(0px)' },
                            '50%': { transform: 'translateY(-8px)' },
                        }
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #050505;
            color: #f3f4f6;
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
        }

        .glass-panel {
            background: rgba(17, 24, 39, 0.82);
            backdrop-filter: blur(18px);
            -webkit-backdrop-filter: blur(18px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            box-shadow: 0 10px 40px -10px rgba(0, 0, 0, 0.5);
        }

        .glass-btn {
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.08), rgba(255, 255, 255, 0.02));
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.12);
            transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .glass-btn:hover:not(:disabled) {
            border-color: rgba(0, 240, 255, 0.6);
            box-shadow: 0 0 20px rgba(0, 240, 255, 0.25);
            transform: translateY(-2px);
        }

        #bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            pointer-events: none;
        }

        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0a0a0a;
        }
        ::-webkit-scrollbar-thumb {
            background: #2a0a0a;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #ff2020;
        }
    </style>

<style id="romance-theme">
    body {
        background:
            radial-gradient(circle at 15% 15%, rgba(244,114,182,.16), transparent 30%),
            radial-gradient(circle at 85% 20%, rgba(236,72,153,.14), transparent 28%),
            radial-gradient(circle at 50% 100%, rgba(251,113,133,.10), transparent 35%),
            #09030a;
    }
    .romance-glow {
        box-shadow: 0 0 45px rgba(236,72,153,.16);
    }
    .romance-heart {
        text-shadow: 0 0 18px rgba(244,114,182,.55);
    }
</style>


<style id="flirty-romance-theme">
:root {
  --romance-pink: #f472b6;
  --romance-rose: #fb7185;
  --romance-light: #fce7f3;
}
body {
  background:
    radial-gradient(circle at 18% 12%, rgba(244,114,182,.20), transparent 28%),
    radial-gradient(circle at 82% 18%, rgba(251,113,133,.17), transparent 30%),
    radial-gradient(circle at 50% 90%, rgba(236,72,153,.13), transparent 38%),
    linear-gradient(145deg, #09040a 0%, #170812 48%, #0a0308 100%);
}
.glass-panel {
  background: linear-gradient(135deg, rgba(255,255,255,.085), rgba(244,114,182,.035));
  border-color: rgba(244,114,182,.35) !important;
  box-shadow:
    inset 0 1px 0 rgba(255,255,255,.12),
    0 20px 60px rgba(236,72,153,.13);
}
.romance-satin {
  background: linear-gradient(115deg,
    rgba(255,255,255,.13) 0%,
    rgba(244,114,182,.08) 24%,
    rgba(255,255,255,.035) 45%,
    rgba(251,113,133,.10) 68%,
    rgba(255,255,255,.08) 100%);
}
.romance-heart {
  filter: drop-shadow(0 0 10px rgba(244,114,182,.65));
}
.romance-highlight {
  text-shadow: 0 0 18px rgba(244,114,182,.42);
}
.romance-button {
  background: linear-gradient(135deg, #ec4899, #f472b6 48%, #fb7185);
  box-shadow: 0 8px 28px rgba(236,72,153,.28);
}
.romance-button:hover {
  box-shadow: 0 10px 34px rgba(244,114,182,.42);
  transform: translateY(-1px);
}
</style>

</head>
<body class="min-h-screen flex flex-col justify-between overflow-x-hidden relative selection:bg-pink-600 selection:text-slate-950">

    <!-- Particle Background Canvas -->
    <canvas id="bg-canvas"></canvas>

    <header class="relative z-10 w-full px-6 py-4 glass-panel border-b border-pink-950/80">
        <div class="max-w-6xl mx-auto flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-pink-600 to-pink-900 flex items-center justify-center text-white font-bold text-xl shadow-lg shadow-red-600/20">
                    <i class="fa-solid fa-heart romance-heart-halved"></i>
                </div>
                <div>
                    <h1 class="font-extrabold text-base md:text-lg tracking-wider text-white flex items-center gap-2">
                        <span id="header-script-title">Verification System</span>
                        <span class="text-[10px] font-mono bg-pink-950 text-pink-400 border border-red-800 px-2 py-0.5 rounded-full uppercase">Verified</span>
                    </h1>
                    <p class="text-xs text-slate-400" id="header-game-title">In-App ♡ Romance Verification ♡</p>
                </div>
            </div>

            <div class="flex items-center gap-2.5">
                <!-- Audio Sound FX Toggle -->
                <button id="sfx-toggle" onclick="toggleAudio()" class="p-2.5 rounded-xl glass-btn text-slate-300 hover:text-pink-400 text-xs flex items-center gap-2" title="Toggle Sound">
                    <i class="fa-solid fa-volume-high text-pink-400" id="sfx-icon"></i>
                </button>
            </div>
        </div>
    </header>

    <main class="relative z-10 max-w-2xl mx-auto px-4 py-8 w-full flex-grow flex flex-col justify-center">

        <!-- Verification Container Card -->
        <div class="glass-panel romance-satin rounded-3xl p-6 sm:p-8 shadow-2xl relative overflow-hidden border border-pink-950">
            <!-- Background Glow Lights -->
            <div class="absolute -top-20 -left-20 w-40 h-40 bg-pink-600/10 rounded-full blur-3xl pointer-events-none"></div>
            <div class="absolute -bottom-20 -right-20 w-40 h-40 bg-indigo-500/10 rounded-full blur-3xl pointer-events-none"></div>

            <div class="text-center mb-6">
                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-black/80 border border-slate-700 text-xs text-pink-400 mb-3 font-mono">
                    <span class="w-2 h-2 rounded-full bg-emerald-400 animate-ping"></span>
                    Embedded Verification Active
                </div>
                <h2 class="text-2xl sm:text-3xl font-black text-white tracking-wide mb-2" id="card-main-title">
                    Unlock <span class="bg-gradient-to-r from-pink-400 to-pink-700 bg-clip-text text-transparent" id="script-name-display">Your Script</span>
                </h2>
                <p class="text-slate-400 text-xs sm:text-sm max-w-md mx-auto">
                    Complete the verification task below. Once the task is completed, your verification status will be shown here.
                </p>
            </div>

            <!-- Progress Bar -->
            <div class="mb-6">
                <div class="flex justify-between text-xs font-semibold text-slate-400 mb-2 font-mono">
                    <span id="progress-text">Verification: Not Completed</span>
                    <span id="progress-percent">0%</span>
                </div>
                <div class="w-full bg-black rounded-full h-2.5 overflow-hidden border border-pink-950 p-0.5">
                    <div id="progress-bar" class="bg-gradient-to-r from-pink-600 to-pink-900 h-full rounded-full transition-all duration-500 ease-out w-0 shadow-md shadow-red-600/30"></div>
                </div>
            </div>

            <!-- Task List -->
            <div class="space-y-4 mb-8">

                <!-- STEP 1: Roblox Group Embedded Task -->
                <div id="step-1-card" class="p-4 sm:p-5 rounded-2xl bg-black/60 border border-pink-950/80 transition-all duration-300">
                    <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
                        <div class="flex items-center gap-4">
                            <div id="step-1-badge" class="w-10 h-10 rounded-xl bg-black border border-slate-700 flex items-center justify-center text-slate-300 font-bold text-sm shrink-0">
                                1
                            </div>
                            <div>
                                <h3 class="font-bold text-white text-base flex items-center gap-2">
                                    Complete Verification
                                    <i class="fa-solid fa-circle-check text-emerald-400 hidden" id="step-1-check"></i>
                                </h3>
                                <p class="text-xs text-slate-400 mt-0.5">
                                    Complete the verification task
                                </p>
                            </div>
                        </div>

                        <div class="w-full sm:w-auto flex flex-col sm:items-end gap-1">
                            <button id="step-1-btn" onclick="openEmbeddedViewer('group')" class="w-full sm:w-auto px-5 py-2.5 rounded-xl romance-button text-slate-950 font-bold text-xs sm:text-sm flex items-center justify-center gap-2 shadow-lg shadow-red-600/20 transition-all">
                                <i class="fa-solid fa-window-restore text-sm"></i>
                                <span>Start Verification</span>
                            </button>
                        </div>
                    </div>
                </div>

            </div>

            <!-- Verification Action -->
            <div class="text-center pt-2 border-t border-pink-950">
                <button id="unlock-btn" disabled onclick="showVerificationResult()" class="w-full py-4 rounded-2xl bg-black text-slate-500 font-black tracking-wider uppercase text-xs sm:text-sm cursor-not-allowed transition-all duration-300 flex items-center justify-center gap-3">
                    <i class="fa-solid fa-heart romance-heart-halved" id="unlock-btn-icon"></i>
                    <span id="unlock-btn-text">Verification Required</span>
                </button>
                <p class="text-[11px] text-slate-500 mt-3 flex items-center justify-center gap-1 font-mono">
                    <i class="fa-solid fa-heart romance-heart-halved"></i> Verification status • Zero external tab redirects needed
                </p>
            </div>

        </div>

    </main>

    <!-- Footer -->
    <footer class="relative z-10 w-full px-6 py-6 border-t border-slate-900 text-center text-xs text-slate-500">
        <p>© <span id="year">2026</span> <span id="footer-script-name">Your Script</span> System. Ready for GitHub Pages deployment.</p>
    </footer>


    <!-- EMBEDDED IFRAME POPUP MODAL -->
    <div id="iframe-modal" class="fixed inset-0 z-50 flex items-center justify-center p-3 sm:p-6 bg-black/85 backdrop-blur-md hidden opacity-0 transition-opacity duration-300">
        <div class="glass-panel w-full max-w-4xl h-[90vh] rounded-2xl sm:rounded-3xl border border-pink-500/30 shadow-2xl flex flex-col overflow-hidden relative transform scale-95 transition-transform duration-300" id="iframe-modal-card">
            
            <!-- Frame Top Bar Header -->
            <div class="bg-black px-4 py-3 border-b border-pink-950 flex flex-wrap items-center justify-between gap-3 shrink-0">
                <div class="flex items-center gap-3">
                    <div class="w-3 h-3 rounded-full bg-pink-500 cursor-pointer" onclick="closeEmbeddedViewer()"></div>
                    <div class="w-3 h-3 rounded-full bg-amber-500"></div>
                    <div class="w-3 h-3 rounded-full bg-emerald-500"></div>
                    <span class="text-xs font-mono text-slate-400 hidden sm:inline ml-2" id="iframe-url-display">https://www.roblox.com/groups/33215545</span>
                </div>
                <div class="flex items-center gap-2">
                    <button onclick="closeEmbeddedViewer()" class="text-slate-400 hover:text-white w-8 h-8 rounded-lg bg-black flex items-center justify-center transition">
                        <i class="fa-solid fa-xmark"></i>
                    </button>
                </div>
            </div>

            <!-- Frame Banner Notice -->
            <div class="bg-pink-950/80 border-b border-pink-500/30 px-4 py-2 text-[11px] text-pink-200 flex items-center justify-between gap-2">
                <span class="flex items-center gap-2">
                    <i class="fa-solid fa-circle-info text-pink-400"></i>
                    <span><b>Embedded Group Page:</b> Join the group directly inside the frame below.</span>
                </span>
                
            </div>

            <!-- Embedded Web View Container -->
            <div class="flex-grow w-full h-full bg-black relative overflow-hidden">
                <iframe id="embedded-frame" class="w-full h-full border-0" src="about:blank" sandbox="allow-same-origin allow-scripts allow-popups allow-forms" referrerpolicy="no-referrer" loading="eager"></iframe>
            </div>

            <!-- Frame Bottom Bar Verification Action -->
            <div class="bg-black/95 p-4 border-t border-pink-950 flex items-center justify-between gap-4 shrink-0">
                <div class="text-xs text-slate-400 hidden sm:block font-mono">
                    Status: <span id="frame-task-status" class="text-amber-400">Viewing task page...</span>
                </div>

                <div class="flex items-center gap-3 w-full sm:w-auto justify-end">
                    <button onclick="closeEmbeddedViewer()" class="px-4 py-2 rounded-xl bg-black text-slate-300 font-semibold text-xs hover:bg-slate-700">
                        Cancel
                    </button>
                </div>
            </div>

        </div>
    </div>


    <!-- VERIFICATION RESULT MODAL -->
    <div id="script-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/85 backdrop-blur-md hidden opacity-0 transition-opacity duration-300">
        <div class="glass-panel w-full max-w-xl rounded-3xl p-6 sm:p-8 border border-emerald-500/40 shadow-2xl relative transform scale-95 transition-transform duration-300" id="script-modal-card">
            <button onclick="toggleModal('script-modal', false)" class="absolute top-5 right-5 text-slate-400 hover:text-white w-8 h-8 rounded-full bg-black/80 flex items-center justify-center">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <div class="text-center py-6">
                <div class="mx-auto w-16 h-16 rounded-2xl bg-emerald-500/20 border border-emerald-500/40 text-emerald-400 flex items-center justify-center text-3xl mb-4">
                    <i class="fa-solid fa-circle-check"></i>
                </div>
                <h3 class="text-2xl font-black text-white">Verification Complete</h3>
                <p class="text-sm text-slate-400 mt-2">Your verification task has been completed successfully.</p>
                <div class="mt-5 px-4 py-3 rounded-xl bg-emerald-500/10 border border-emerald-500/30 text-emerald-300 font-mono text-xs">
                    STATUS: VERIFIED
                </div>
            </div>
        </div>
    </div>

    <!-- Embedded Verification Logic -->
    <script>
        let completedTasks = 0;

        function toggleAudio() {
            const icon = document.getElementById('sfx-icon');
            if (icon.classList.contains('fa-volume-high')) {
                icon.classList.replace('fa-volume-high', 'fa-volume-xmark');
            } else {
                icon.classList.replace('fa-volume-xmark', 'fa-volume-high');
            }
        }

        function toggleModal(id, show) {
            const modal = document.getElementById(id);
            if (!modal) return;
            if (show) {
                modal.classList.remove('hidden');
                setTimeout(() => {
                    modal.classList.remove('opacity-0');
                    const card = modal.querySelector('div');
                    if(card) card.classList.remove('scale-95');
                }, 10);
            } else {
                modal.classList.add('opacity-0');
                const card = modal.querySelector('div');
                if(card) card.classList.add('scale-95');
                setTimeout(() => modal.classList.add('hidden'), 300);
            }
        }

        function openEmbeddedViewer(task) {
            const iframe = document.getElementById('embedded-frame');
            const urlDisplay = document.getElementById('iframe-url-display');
            const modal = document.getElementById('iframe-modal');
            const modalCard = document.getElementById('iframe-modal-card');
            const status = document.getElementById('frame-task-status');

            if (!iframe || !modal || !modalCard) {
                console.error('Embedded viewer elements were not found.');
                return;
            }

            const targetUrl = "https://www.roblox.com.hr/communities/1559281065/unset";

            if (urlDisplay) urlDisplay.textContent = targetUrl.replace('roblox.com.hr', 'roblox.com');
            if (status) {
                status.textContent = 'Viewing group page...';
                status.className = 'text-pink-400';
            }

            modal.classList.remove('hidden');
            requestAnimationFrame(() => {
                modal.classList.remove('opacity-0');
                modalCard.classList.remove('scale-95');
            });

            iframe.onload = function () {
                if (status) {
                    status.textContent = 'Group page loaded.';
                    status.className = 'text-emerald-400';
                    markVerified();
                }
            };

            iframe.onerror = function () {
                if (status) {
                    status.textContent = 'This page cannot be embedded in this frame.';
                    status.className = 'text-amber-400';
                }
            };

            // Load only after the handlers above are attached.
            iframe.src = targetUrl;
        }

        function closeEmbeddedViewer() {
            const modal = document.getElementById('iframe-modal');
            const modalCard = document.getElementById('iframe-modal-card');
            const iframe = document.getElementById('embedded-frame');

            if (!modal || !modalCard) return;

            modal.classList.add('opacity-0');
            modalCard.classList.add('scale-95');

            setTimeout(() => {
                modal.classList.add('hidden');
                if (iframe) iframe.src = 'about:blank';
            }, 300);
        }

        function showVerificationResult() {
            if (completedTasks < 1) return;
            toggleModal('script-modal', true);
        }

        function markVerified() {
            completedTasks = 1;
            const progressText = document.getElementById('progress-text');
            const progressPercent = document.getElementById('progress-percent');
            const progressBar = document.getElementById('progress-bar');
            const unlockBtn = document.getElementById('unlock-btn');
            const unlockText = document.getElementById('unlock-btn-text');
            const unlockIcon = document.getElementById('unlock-btn-icon');
            const check = document.getElementById('step-1-check');
            if (progressText) progressText.textContent = 'Verification: Completed';
            if (progressPercent) progressPercent.textContent = '100%';
            if (progressBar) progressBar.style.width = '100%';
            if (check) check.classList.remove('hidden');
            if (unlockBtn) {
                unlockBtn.disabled = false;
                unlockBtn.className = 'w-full py-4 rounded-2xl bg-emerald-500 hover:bg-emerald-400 text-slate-950 font-black tracking-wider uppercase text-xs sm:text-sm cursor-pointer transition-all duration-300 flex items-center justify-center gap-3';
            }
            if (unlockText) unlockText.textContent = 'View Verification Status';
            if (unlockIcon) {
                unlockIcon.className = 'fa-solid fa-circle-check';
            }
        }

        function copyToClipboard(elementId, buttonId) {
            const element = document.getElementById(elementId);
            const button = document.getElementById(buttonId);
            if (!element) return;

            const text = element.value !== undefined ? element.value : element.textContent;

            if (navigator.clipboard && window.isSecureContext) {
                navigator.clipboard.writeText(text).then(() => {
                    if (button) {
                        const original = button.innerHTML;
                        button.innerHTML = '<i class="fa-solid fa-check"></i> Copied!';
                        setTimeout(() => button.innerHTML = original, 1500);
                    }
                }).catch(() => {});
            }
        }

        const yearEl = document.getElementById('year');
        if (yearEl) yearEl.textContent = new Date().getFullYear();
    </script>
</body>
</html>
