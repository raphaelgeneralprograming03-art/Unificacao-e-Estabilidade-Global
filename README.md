
<html lang="pt-BR" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cooperação Internacional & O Grande Filtro - Simulador de Governança Global</title>
    
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Fonts Google: Orbitron & Rajdhani -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800;900&family=Rajdhani:wght@400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- FontAwesome para Ícones Sci-Fi -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            bg: '#060913',
                            panel: 'rgba(12, 20, 39, 0.75)',
                            border: '#1a2c4e',
                            cyan: '#00f3ff',
                            magenta: '#ff0055',
                            green: '#00ff88',
                            amber: '#ffaa00',
                            purple: '#9d00ff'
                        }
                    },
                    fontFamily: {
                        orbitron: ['Orbitron', 'sans-serif'],
                        rajdhani: ['Rajdhani', 'sans-serif']
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #040711;
            color: #d1e4ff;
            font-family: 'Rajdhani', sans-serif;
            overflow-x: hidden;
            background-image: 
                radial-gradient(circle at 50% 50%, rgba(0, 243, 255, 0.03) 0%, transparent 70%),
                linear-gradient(to bottom, #040711, #080d1a);
        }

        /* Glassmorphism futurista */
        .glass-panel {
            background: rgba(10, 18, 36, 0.7);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(0, 243, 255, 0.15);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.5), inset 0 0 15px rgba(0, 243, 255, 0.03);
        }

        .glass-panel-danger {
            background: rgba(30, 8, 18, 0.75);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 0, 85, 0.3);
            box-shadow: 0 8px 32px 0 rgba(255, 0, 85, 0.15);
        }

        .glass-panel-success {
            background: rgba(6, 28, 20, 0.75);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(0, 255, 136, 0.3);
            box-shadow: 0 8px 32px 0 rgba(0, 255, 136, 0.15);
        }

        /* Neon Glows */
        .glow-cyan {
            text-shadow: 0 0 10px rgba(0, 243, 255, 0.7), 0 0 20px rgba(0, 243, 255, 0.4);
        }

        .glow-magenta {
            text-shadow: 0 0 10px rgba(255, 0, 85, 0.7), 0 0 20px rgba(255, 0, 85, 0.4);
        }

        .glow-green {
            text-shadow: 0 0 10px rgba(0, 255, 136, 0.7), 0 0 20px rgba(0, 255, 136, 0.4);
        }

        .box-glow-cyan {
            box-shadow: 0 0 15px rgba(0, 243, 255, 0.3), inset 0 0 10px rgba(0, 243, 255, 0.1);
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(5, 10, 20, 0.8);
        }
        ::-webkit-scrollbar-thumb {
            background: #1a2c4e;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00f3ff;
        }

        /* Custom Range Input */
        input[type=range] {
            -webkit-appearance: none;
            background: transparent;
            width: 100%;
        }
        input[type=range]:focus {
            outline: none;
        }
        input[type=range]::-webkit-slider-runnable-track {
            width: 100%;
            height: 8px;
            cursor: pointer;
            background: #0c182e;
            border-radius: 4px;
            border: 1px solid rgba(0, 243, 255, 0.2);
        }
        input[type=range]::-webkit-slider-thumb {
            height: 18px;
            width: 18px;
            border-radius: 50%;
            background: #00f3ff;
            cursor: pointer;
            -webkit-appearance: none;
            margin-top: -5px;
            box-shadow: 0 0 10px #00f3ff;
            transition: transform 0.1s, background-color 0.2s;
        }
        input[type=range]::-webkit-slider-thumb:hover {
            transform: scale(1.2);
            background: #ffffff;
        }

        /* Pulse Animations */
        @keyframes scanline {
            0% { transform: translateY(-100%); }
            100% { transform: translateY(1000%); }
        }
        .scanline-overlay {
            position: absolute;
            top: 0; left: 0; right: 0; bottom: 0;
            background: linear-gradient(to bottom, transparent 50%, rgba(0, 243, 255, 0.02) 51%);
            background-size: 100% 4px;
            pointer-events: none;
        }

        @keyframes radar-sweep {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between p-2 md:p-4 selection:bg-cyan-500 selection:text-black">

    <!-- Header Principal -->
    <header class="glass-panel rounded-xl p-3 mb-3 flex flex-wrap justify-between items-center relative overflow-hidden border-b-2 border-cyan-500/40">
        <div class="scanline-overlay"></div>
        
        <div class="flex items-center space-x-3 z-10">
            <div class="w-10 h-10 rounded-lg bg-cyan-950/80 border border-cyan-400 flex items-center justify-center text-cyan-400 text-xl shadow-[0_0_15px_rgba(0,243,255,0.4)]">
                <i class="fa-solid font-bold fa-globe"></i>
            </div>
            <div>
                <h1 class="font-orbitron font-extrabold text-lg md:text-xl tracking-wider text-white flex items-center gap-2">
                    GOVERNANÇA PLANETÁRIA <span class="text-xs px-2 py-0.5 rounded bg-cyan-900/60 text-cyan-300 border border-cyan-500/50 font-mono">SIM-CORE v2.7</span>
                </h1>
                <p class="text-xs text-cyan-300/70 font-mono tracking-widest">SISTEMA DE PREVENÇÃO DO GRANDE FILTRO & COOPERAÇÃO GLOBAL</p>
            </div>
        </div>

        <!-- Indicadores rápidos superiores -->
        <div class="flex items-center space-x-2 md:space-x-6 my-2 md:my-0 z-10 text-xs md:text-sm font-mono">
            <div class="bg-slate-900/80 px-3 py-1.5 rounded-lg border border-slate-700/60 flex items-center gap-2">
                <span class="text-slate-400">STATUS:</span>
                <span id="sim-status-text" class="text-emerald-400 font-bold flex items-center gap-1.5">
                    <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span> EM ESTABILIDADE
                </span>
            </div>
            
            <div class="bg-slate-900/80 px-3 py-1.5 rounded-lg border border-slate-700/60 flex items-center gap-2">
                <span class="text-slate-400">ANO DA SIMULAÇÃO:</span>
                <span id="sim-year" class="text-cyan-400 font-bold font-orbitron">2050.0</span>
            </div>
        </div>

        <!-- Botões de Controle de Áudio e Dossiê -->
        <div class="flex items-center space-x-2 z-10">
            <button id="btn-audio-toggle" title="Alternar Som" class="px-3 py-1.5 rounded-lg bg-slate-800 hover:bg-slate-700 text-cyan-400 border border-cyan-500/30 transition flex items-center gap-2 text-xs font-semibold">
                <i id="audio-icon" class="fa-solid fa-volume-high"></i> <span class="hidden sm:inline">SOM</span>
            </button>
            <button id="btn-dossier" class="px-3 py-1.5 rounded-lg bg-cyan-950 hover:bg-cyan-900 text-cyan-300 border border-cyan-400/50 transition flex items-center gap-2 text-xs font-semibold shadow-[0_0_10px_rgba(0,243,255,0.2)]">
                <i class="fa-solid fa-book-bookmark"></i> <span>DOSSIÊ TEÓRICO</span>
            </button>
            <button id="btn-reset" class="px-3 py-1.5 rounded-lg bg-red-950 hover:bg-red-900 text-red-300 border border-red-500/40 transition flex items-center gap-2 text-xs font-semibold">
                <i class="fa-solid fa-rotate-right"></i> <span class="hidden sm:inline">REINICIAR</span>
            </button>
        </div>
    </header>

    <!-- Conteúdo Principal - Grid 3 Colunas -->
    <main class="grid grid-cols-1 lg:grid-cols-12 gap-3 flex-1 mb-3">

        <!-- PAINEL ESQUERDO: Métricas de Sobrevivência & Kardashev (3 cols) -->
        <section class="lg:col-span-3 flex flex-col gap-3">
            
            <!-- Relógio do Grande Filtro (Meter Principal) -->
            <div class="glass-panel rounded-xl p-4 flex flex-col items-center justify-center relative overflow-hidden">
                <div class="text-xs font-mono text-cyan-300/80 uppercase tracking-widest mb-1 flex items-center gap-2">
                    <i class="fa-solid fa-radiation text-rose-500"></i> Relógio do Grande Filtro
                </div>
                
                <!-- Display Numérico e Meter -->
                <div class="relative my-2 flex items-center justify-center">
                    <div class="w-36 h-36 rounded-full border-4 border-slate-800 flex items-center justify-center relative shadow-inner">
                        <svg class="w-full h-full transform -rotate-90" viewBox="0 0 100 100">
                            <circle cx="50" cy="50" r="42" stroke="currentColor" stroke-width="8" class="text-slate-800" fill="transparent"/>
                            <circle id="filter-gauge-circle" cx="50" cy="50" r="42" stroke="currentColor" stroke-width="8" 
                                    class="text-rose-500 transition-all duration-500" 
                                    stroke-dasharray="263.89" 
                                    stroke-dashoffset="180" 
                                    stroke-linecap="round" 
                                    fill="transparent"/>
                        </svg>
                        <div class="absolute text-center">
                            <span id="filter-threat-val" class="font-orbitron text-3xl font-black text-rose-500 glow-magenta">32%</span>
                            <span class="block text-[10px] text-slate-400 font-mono uppercase tracking-tighter">Ameaça Colapso</span>
                        </div>
                    </div>
                </div>

                <p id="filter-warning-msg" class="text-xs text-center text-slate-300 font-mono mt-1 bg-slate-950/60 px-3 py-1 rounded border border-slate-800 w-full">
                    Risco de extinção sob controle nominal.
                </p>
            </div>

            <!-- Progresso Kardashev Tipo I -->
            <div class="glass-panel rounded-xl p-4">
                <div class="flex justify-between items-center mb-2">
                    <span class="text-xs font-mono text-cyan-300 uppercase tracking-wider flex items-center gap-1.5">
                        <i class="fa-solid fa-bolt text-amber-400"></i> Escala Kardashev (Tipo I)
                    </span>
                    <span id="kardashev-val" class="font-orbitron font-bold text-amber-400 text-sm">0.728</span>
                </div>
                
                <div class="w-full bg-slate-900 rounded-full h-3 border border-slate-700/80 overflow-hidden p-0.5">
                    <div id="kardashev-bar" class="bg-gradient-to-r from-amber-500 via-yellow-400 to-emerald-400 h-full rounded-full transition-all duration-300" style="width: 28%"></div>
                </div>
                <div class="flex justify-between text-[10px] font-mono text-slate-400 mt-1">
                    <span>Tipo 0.70 (Atual)</span>
                    <span>Tipo 1.00 (Domínio Planetário)</span>
                </div>
            </div>

            <!-- Indicadores Chave de Desempenho (Unidade, Recursos, Guerra) -->
            <div class="glass-panel rounded-xl p-4 flex-1 flex flex-col justify-between space-y-3">
                
                <!-- Unidade Global -->
                <div>
                    <div class="flex justify-between text-xs font-mono mb-1">
                        <span class="text-cyan-400 flex items-center gap-1.5">
                            <i class="fa-solid fa-handshake"></i> Coesão Global
                        </span>
                        <span id="unity-val" class="font-bold text-cyan-300">55%</span>
                    </div>
                    <div class="w-full bg-slate-900 rounded-full h-2.5 border border-slate-700 overflow-hidden">
                        <div id="unity-bar" class="bg-cyan-400 h-full transition-all duration-300" style="width: 55%"></div>
                    </div>
                </div>

                <!-- Reservas de Recursos Críticos -->
                <div>
                    <div class="flex justify-between text-xs font-mono mb-1">
                        <span class="text-emerald-400 flex items-center gap-1.5">
                            <i class="fa-solid fa-boxes-stacked"></i> Reservas de Recursos
                        </span>
                        <span id="resources-val" class="font-bold text-emerald-300">68%</span>
                    </div>
                    <div class="w-full bg-slate-900 rounded-full h-2.5 border border-slate-700 overflow-hidden">
                        <div id="resources-bar" class="bg-emerald-400 h-full transition-all duration-300" style="width: 68%"></div>
                    </div>
                </div>

                <!-- Taxa de Economia Circular -->
                <div>
                    <div class="flex justify-between text-xs font-mono mb-1">
                        <span class="text-purple-400 flex items-center gap-1.5">
                            <i class="fa-solid fa-recycle"></i> Taxa de Reciclagem
                        </span>
                        <span id="recycling-val" class="font-bold text-purple-300">42%</span>
                    </div>
                    <div class="w-full bg-slate-900 rounded-full h-2.5 border border-slate-700 overflow-hidden">
                        <div id="recycling-bar" class="bg-purple-400 h-full transition-all duration-300" style="width: 42%"></div>
                    </div>
                </div>

                <!-- Risco de Guerra / Colapso -->
                <div>
                    <div class="flex justify-between text-xs font-mono mb-1">
                        <span class="text-rose-400 flex items-center gap-1.5">
                            <i class="fa-solid fa-burst"></i> Risco de Guerra Sistêmica
                        </span>
                        <span id="war-val" class="font-bold text-rose-400">22%</span>
                    </div>
                    <div class="w-full bg-slate-900 rounded-full h-2.5 border border-slate-700 overflow-hidden">
                        <div id="war-bar" class="bg-rose-500 h-full transition-all duration-300" style="width: 22%"></div>
                    </div>
                </div>

            </div>
        </section>

        <!-- PAINEL CENTRAL: Globo 3D em Canvas 2D + Gráfico Histórico (6 cols) -->
        <section class="lg:col-span-6 flex flex-col gap-3">
            
            <!-- Canvas do Globo Planetário -->
            <div class="glass-panel rounded-xl p-2 relative flex-1 flex flex-col items-center justify-center min-h-[380px] overflow-hidden">
                
                <!-- Overlay de Informações de Interação -->
                <div class="absolute top-3 left-3 z-10 text-[11px] font-mono bg-slate-950/70 p-2 rounded border border-cyan-500/20 text-cyan-300/80 pointer-events-none">
                    <p><i class="fa-solid fa-arrows-spin text-cyan-400 mr-1"></i> Arraste para rotacionar o Globo</p>
                    <p><i class="fa-solid fa-circle-dot text-emerald-400 mr-1"></i> Arcos: Redes de Cooperação</p>
                    <p><i class="fa-solid fa-triangle-exclamation text-rose-500 mr-1"></i> Pulso Vermelho: Tensão geopolítica</p>
                </div>

                <!-- Canvas da Terra 3D -->
                <canvas id="globe-canvas" class="w-full h-full cursor-grab active:cursor-grabbing rounded-lg"></canvas>

                <!-- Status de Bloco selecionado/hover -->
                <div id="bloc-tooltip" class="absolute bottom-3 left-3 right-3 z-10 glass-panel p-2 rounded-lg text-xs font-mono hidden flex justify-between items-center border border-cyan-400/40">
                    <div>
                        <span class="text-slate-400">BLOCO ATIVO:</span>
                        <span id="bloc-name" class="font-bold text-cyan-300 ml-1">União Euro-Atlântica</span>
                    </div>
                    <div>
                        <span class="text-slate-400">ESTABILIDADE:</span>
                        <span id="bloc-stab" class="font-bold text-emerald-400 ml-1">85%</span>
                    </div>
                </div>
            </div>

            <!-- Canvas de Gráfico Histórico Dinâmico -->
            <div class="glass-panel rounded-xl p-3 h-44 flex flex-col">
                <div class="flex justify-between items-center mb-1 text-xs font-mono">
                    <span class="text-cyan-300 flex items-center gap-1.5">
                        <i class="fa-solid fa-chart-line"></i> Histórico em Tempo Real: Relógio vs Unidade
                    </span>
                    <div class="flex gap-3 text-[10px]">
                        <span class="text-rose-400 flex items-center gap-1"><span class="w-2 h-2 rounded-full bg-rose-500 inline-block"></span> Ameça Filtro</span>
                        <span class="text-cyan-400 flex items-center gap-1"><span class="w-2 h-2 rounded-full bg-cyan-400 inline-block"></span> Coesão Global</span>
                        <span class="text-emerald-400 flex items-center gap-1"><span class="w-2 h-2 rounded-full bg-emerald-400 inline-block"></span> Kardashev</span>
                    </div>
                </div>
                <div class="flex-1 w-full relative">
                    <canvas id="chart-canvas" class="w-full h-full"></canvas>
                </div>
            </div>

        </section>

        <!-- PAINEL DIREITO: Diretrizes Políticas, Ações & Ticker de Eventos (3 cols) -->
        <section class="lg:col-span-3 flex flex-col gap-3">
            
            <!-- Sliders de Diretrizes Políticas Globais -->
            <div class="glass-panel rounded-xl p-4 flex flex-col gap-3">
                <h2 class="font-orbitron text-xs font-bold text-cyan-300 uppercase tracking-wider flex items-center gap-1.5 pb-2 border-b border-cyan-500/20">
                    <i class="fa-solid fa-sliders text-cyan-400"></i> Diretrizes Políticas Globais
                </h2>

                <!-- Slider 1: Partilha de Recursos -->
                <div>
                    <div class="flex justify-between text-xs font-mono mb-1">
                        <span class="text-slate-300">Partilha de Recursos</span>
                        <span id="slider-sharing-val" class="text-cyan-400 font-bold">50%</span>
                    </div>
                    <input type="range" id="slider-sharing" min="0" max="100" value="50">
                </div>

                <!-- Slider 2: Diretiva de Desarmamento -->
                <div>
                    <div class="flex justify-between text-xs font-mono mb-1">
                        <span class="text-slate-300">Diretiva de Desarmamento</span>
                        <span id="slider-disarm-val" class="text-cyan-400 font-bold">40%</span>
                    </div>
                    <input type="range" id="slider-disarm" min="0" max="100" value="40">
                </div>

                <!-- Slider 3: Financiamento Ecológico -->
                <div>
                    <div class="flex justify-between text-xs font-mono mb-1">
                        <span class="text-slate-300">Financiamento Ecológico</span>
                        <span id="slider-eco-val" class="text-cyan-400 font-bold">60%</span>
                    </div>
                    <input type="range" id="slider-eco" min="0" max="100" value="60">
                </div>

                <!-- Slider 4: Integração Diplomática -->
                <div>
                    <div class="flex justify-between text-xs font-mono mb-1">
                        <span class="text-slate-300">Integração Diplomática</span>
                        <span id="slider-diplo-val" class="text-cyan-400 font-bold">55%</span>
                    </div>
                    <input type="range" id="slider-diplo" min="0" max="100" value="55">
                </div>
            </div>

            <!-- Botões de Ação Tática de Emergência -->
            <div class="glass-panel rounded-xl p-4 space-y-2">
                <h2 class="font-orbitron text-xs font-bold text-cyan-300 uppercase tracking-wider mb-2 flex items-center gap-1.5">
                    <i class="fa-solid fa-crosshairs text-rose-400"></i> Intervenções Táticas
                </h2>

                <button id="btn-action-accord" class="w-full py-2 px-3 rounded-lg bg-cyan-950/80 hover:bg-cyan-900 border border-cyan-400/50 text-cyan-200 text-xs font-mono font-semibold flex items-center justify-between transition active:scale-95">
                    <span><i class="fa-solid fa-file-contract mr-1.5 text-cyan-400"></i> Acordo de Unificação</span>
                    <span class="text-[10px] bg-cyan-900/60 px-1.5 py-0.5 rounded text-cyan-300">+Unidade</span>
                </button>

                <button id="btn-action-grid" class="w-full py-2 px-3 rounded-lg bg-emerald-950/80 hover:bg-emerald-900 border border-emerald-400/50 text-emerald-200 text-xs font-mono font-semibold flex items-center justify-between transition active:scale-95">
                    <span><i class="fa-solid fa-network-wired mr-1.5 text-emerald-400"></i> Malha de Recursos</span>
                    <span class="text-[10px] bg-emerald-900/60 px-1.5 py-0.5 rounded text-emerald-300">+Recursos</span>
                </button>

                <button id="btn-action-suppress" class="w-full py-2 px-3 rounded-lg bg-rose-950/80 hover:bg-rose-900 border border-rose-400/50 text-rose-200 text-xs font-mono font-semibold flex items-center justify-between transition active:scale-95">
                    <span><i class="fa-solid fa-shield-halved mr-1.5 text-rose-400"></i> Suprimir Conflito</span>
                    <span class="text-[10px] bg-rose-900/60 px-1.5 py-0.5 rounded text-rose-300">-Risco Guerra</span>
                </button>

                <button id="btn-action-aid" class="w-full py-2 px-3 rounded-lg bg-purple-950/80 hover:bg-purple-900 border border-purple-400/50 text-purple-200 text-xs font-mono font-semibold flex items-center justify-between transition active:scale-95">
                    <span><i class="fa-solid fa-kit-medical mr-1.5 text-purple-400"></i> Socorro de Emergência</span>
                    <span class="text-[10px] bg-purple-900/60 px-1.5 py-0.5 rounded text-purple-300">-Ameaça Filtro</span>
                </button>
            </div>

            <!-- Feed de Eventos Globais Sci-Fi -->
            <div class="glass-panel rounded-xl p-3 flex-1 flex flex-col min-h-[160px]">
                <div class="text-xs font-mono text-cyan-300 uppercase tracking-wider mb-2 flex items-center justify-between border-b border-slate-800 pb-1">
                    <span><i class="fa-solid fa-satellite-dish text-cyan-400 mr-1"></i> Feed Geopolítico</span>
                    <span class="w-2 h-2 rounded-full bg-cyan-400 animate-ping"></span>
                </div>
                <div id="event-log" class="flex-1 overflow-y-auto space-y-2 text-xs font-mono pr-1 max-h-48">
                    <!-- Registros dinâmicos via JS -->
                </div>
            </div>

        </section>

    </main>

    <!-- Modal: Dossiê Teórico e Manual Técnico -->
    <div id="dossier-modal" class="fixed inset-0 bg-slate-950/85 backdrop-blur-md z-50 hidden flex items-center justify-center p-4">
        <div class="glass-panel rounded-2xl max-w-3xl w-full max-h-[85vh] flex flex-col border border-cyan-400/40 shadow-[0_0_50px_rgba(0,243,255,0.2)]">
            
            <div class="p-4 border-b border-cyan-500/30 flex justify-between items-center bg-cyan-950/40">
                <div class="flex items-center space-x-2">
                    <i class="fa-solid fa-atom text-cyan-400 text-xl"></i>
                    <h2 class="font-orbitron font-bold text-lg text-white">DOSSIÊ TEÓRICO: O GRANDE FILTRO & TEORIA DOS JOGOS</h2>
                </div>
                <button id="btn-close-dossier" class="text-slate-400 hover:text-white transition text-xl px-2">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div class="p-6 overflow-y-auto space-y-6 text-slate-300 text-sm font-sans leading-relaxed">
                
                <!-- Seção 1 -->
                <section>
                    <h3 class="font-orbitron text-cyan-400 font-bold text-base mb-2 flex items-center gap-2">
                        <i class="fa-solid fa-[#00f3ff] fa-brain"></i> 1. O Paradoxo de Fermi e a Hipótese do Grande Filtro
                    </h3>
                    <p class="mb-2">
                        O <strong>Paradoxo de Fermi</strong> questiona por que, em um universo com bilhões de estrelas antigas, não encontramos evidências claras de civilizações extraterrestres.
                    </p>
                    <p>
                        A resposta formulada por Robin Hanson é a <strong>Hipótese do Grande Filtro</strong>: existe uma barreira teórica extremamente difícil no desenvolvimento evolutivo ou tecnológico de uma espécie. Se o Filtro está no nosso futuro, a transição para uma civilização de <em>Tipo I na Escala de Kardashev</em> exige superar a autodestruição pré-planetária (guerra nuclear, colapso climático, escassez fatal de recursos ou IA descontrolada).
                    </p>
                </section>

                <!-- Seção 2 -->
                <section>
                    <h3 class="font-orbitron text-cyan-400 font-bold text-base mb-2 flex items-center gap-2">
                        <i class="fa-solid fa-chess text-amber-400"></i> 2. Teoria dos Jogos Geopolíticos & A Tragédia dos Comuns
                    </h3>
                    <p class="mb-2">
                        A sobrevivência planetária é um problema clássico de <strong>Dilema dos Prisioneiros Repetido</strong> e <strong>Tragédia dos Comuns</strong>. Bloco geopolíticos isolados tendem à competição de equilíbrio de Nash desfavorável: acumulação militar e exploração de recursos exauríveis.
                    </p>
                    <p>
                        Para ultrapassar o Grande Filtro, a sociedade global precisa migrar para uma estratégia de <em>Cooperação Global Coordenada</em>, transformando a matriz energética em economia circular e mitigando riscos de conflito sistêmico.
                    </p>
                </section>

                <!-- Seção 3 -->
                <section class="bg-slate-900/80 p-4 rounded-xl border border-cyan-500/20 font-mono text-xs">
                    <h3 class="font-orbitron text-emerald-400 font-bold mb-2">3. Equações Diferenciais da Governança (Modelo Dinâmico)</h3>
                    <p class="mb-1 text-slate-400">// Taxa de Ameaça do Grande Filtro (F):</p>
                    <p class="text-cyan-300 mb-3">dF/dt = α · (RiscoGuerra) + β · (100 - Reciclagem) - γ · (UnidadeGlobal)</p>
                    
                    <p class="text-slate-400">// Progresso para Kardashev Tipo I (K):</p>
                    <p class="text-emerald-300 mb-3">dK/dt = δ · (Recursos) · (Unidade) · (1 + FinanciamentoEcológico)</p>

                    <p class="text-slate-400">// Dinâmica de Recursos Planetários (R):</p>
                    <p class="text-amber-300">dR/dt = (TaxaReciclagem) - ConsumoGlobal · (1 - PartilhaRecursos)</p>
                </section>

            </div>

            <div class="p-4 border-t border-cyan-500/30 flex justify-end bg-cyan-950/20">
                <button id="btn-close-dossier-2" class="px-5 py-2 rounded-lg bg-cyan-500 hover:bg-cyan-400 text-black font-orbitron font-bold text-xs transition">
                    ENTENDIDO / RETORNAR AO SIMULADOR
                </button>
            </div>

        </div>
    </div>

    <script>
        // =========================================================================
        // SINTETIZADOR DE ÁUDIO WEB AUDIO API
        // =========================================================================
        class SoundEngine {
            constructor() {
                this.ctx = null;
                this.enabled = true;
            }

            init() {
                if (!this.ctx) {
                    const AudioContext = window.AudioContext || window.webkitAudioContext;
                    this.ctx = new AudioContext();
                }
                if (this.ctx.state === 'suspended') {
                    this.ctx.resume();
                }
            }

            playBeep(freq = 440, type = 'sine', duration = 0.08, vol = 0.15) {
                if (!this.enabled) return;
                this.init();
                try {
                    const osc = this.ctx.createOscillator();
                    const gain = this.ctx.createGain();
                    osc.type = type;
                    osc.frequency.setValueAtTime(freq, this.ctx.currentTime);
                    gain.gain.setValueAtTime(vol, this.ctx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.001, this.ctx.currentTime + duration);
                    osc.connect(gain);
                    gain.connect(this.ctx.destination);
                    osc.start();
                    osc.stop(this.ctx.currentTime + duration);
                } catch(e) {}
            }

            playActionSuccess() {
                if (!this.enabled) return;
                this.init();
                const now = this.ctx.currentTime;
                [523.25, 659.25, 783.99, 1046.50].forEach((freq, idx) => {
                    setTimeout(() => this.playBeep(freq, 'triangle', 0.12, 0.12), idx * 60);
                });
            }

            playAlarm() {
                if (!this.enabled) return;
                this.init();
                [220, 180, 220, 180].forEach((freq, idx) => {
                    setTimeout(() => this.playBeep(freq, 'sawtooth', 0.15, 0.2), idx * 100);
                });
            }

            playConflictPulse() {
                if (!this.enabled) return;
                this.playBeep(110, 'sawtooth', 0.3, 0.25);
            }
        }

        const audio = new SoundEngine();

        // =========================================================================
        // ESTADO GLOBAL DA SIMULAÇÃO
        // =========================================================================
        const state = {
            year: 2050.0,
            filterClock: 32.0,      // % Ameaça de extinção (0-100)
            kardashev: 0.728,       // Escala 0.70 a 1.00
            unity: 55.0,            // % Coesão global (0-100)
            resources: 68.0,        // % Reservas globais (0-100)
            recycling: 42.0,        // % Economia circular (0-100)
            warRisk: 22.0,          // % Risco de Guerra (0-100)

            // Políticas
            sharing: 50,
            disarm: 40,
            ecoFunding: 60,
            diplo: 55,

            // Histórico para o gráfico (Array de amostras)
            history: [],
            maxHistory: 60,

            // Status do Jogo
            gameOver: false,
            victory: false,

            // Dados dos 6 Blocos Geopolíticos no Globo
            blocs: [
                { id: 1, name: "União Euro-Atlântica", lat: 50, lon: 10, stability: 85, color: "#00f3ff" },
                { id: 2, name: "Bloco Pan-Americano", lat: 38, lon: -95, stability: 80, color: "#00ff88" },
                { id: 3, name: "Aliança Indo-Pacífico", lat: 20, lon: 78, stability: 72, color: "#ffaa00" },
                { id: 4, name: "Federação Leste-Asiática", lat: 35, lon: 105, stability: 78, color: "#9d00ff" },
                { id: 5, name: "Bloco Afro-Sustentável", lat: 0, lon: 20, stability: 65, color: "#00e5ff" },
                { id: 6, name: "Coletivo Sul-Americano", lat: -15, lon: -60, stability: 75, color: "#ff0088" }
            ],

            // Rotas Ativas e Conflitos
            coopRoutes: [
                { from: 0, to: 1 }, { from: 1, to: 5 }, { from: 2, to: 3 },
                { from: 0, to: 4 }, { from: 3, to: 4 }
            ],
            activeConflicts: []
        };

        // =========================================================================
        // GLOBO PLANETÁRIO ORTOGRÁFICO EM CANVAS 2D
        // =========================================================================
        const globeCanvas = document.getElementById('globe-canvas');
        const gCtx = globeCanvas.getContext('2d');

        let rotationX = 0.3;
        let rotationY = 0.0;
        let isDragging = false;
        let lastMouseX = 0;
        let lastMouseY = 0;

        function resizeGlobeCanvas() {
            const rect = globeCanvas.parentElement.getBoundingClientRect();
            globeCanvas.width = rect.width * window.devicePixelRatio;
            globeCanvas.height = rect.height * window.devicePixelRatio;
        }
        window.addEventListener('resize', resizeGlobeCanvas);
        resizeGlobeCanvas();

        // Contornos resumidos de continentes (Pontos Lat/Lon) para visual estilo Holo-HUD
        const continentDots = [
            // América do Norte
            {lat: 60, lon: -100}, {lat: 50, lon: -110}, {lat: 40, lon: -120}, {lat: 30, lon: -100}, {lat: 25, lon: -80}, {lat: 45, lon: -70},
            // América do Sul
            {lat: 5, lon: -75}, {lat: -10, lon: -60}, {lat: -20, lon: -45}, {lat: -35, lon: -65}, {lat: -50, lon: -70},
            // Europa
            {lat: 60, lon: 15}, {lat: 50, lon: 10}, {lat: 45, lon: 2.5}, {lat: 40, lon: -3}, {lat: 55, lon: 37},
            // África
            {lat: 30, lon: 30}, {lat: 15, lon: 40}, {lat: 0, lon: 40}, {lat: -25, lon: 30}, {lat: -30, lon: 20}, {lat: 5, lon: 10}, {lat: 15, lon: -15},
            // Ásia
            {lat: 60, lon: 70}, {lat: 50, lon: 85}, {lat: 60, lon: 100}, {lat: 65, lon: 140}, {lat: 35, lon: 105}, {lat: 22, lon: 114}, {lat: 28, lon: 77},
            // Oceania
            {lat: -25, lon: 135}, {lat: -30, lon: 115}, {lat: -35, lon: 145}, {lat: -40, lon: 175}
        ];

        // Converte Lat/Lon para Posição 3D Ortográfica na Esfera
        function project3D(lat, lon, radius) {
            const phi = (90 - lat) * (Math.PI / 180);
            const theta = (lon + 180) * (Math.PI / 180);

            let x = -(radius * Math.sin(phi) * Math.cos(theta));
            let z = radius * Math.sin(phi) * Math.sin(theta);
            let y = radius * Math.cos(phi);

            // Rotacionar em Y
            let x1 = x * Math.cos(rotationY) + z * Math.sin(rotationY);
            let z1 = -x * Math.sin(rotationY) + z * Math.cos(rotationY);

            // Rotacionar em X
            let y2 = y * Math.cos(rotationX) - z1 * Math.sin(rotationX);
            let z2 = y * Math.sin(rotationX) + z1 * Math.cos(rotationX);

            return { x: x1, y: y2, z: z2 };
        }

        function renderGlobe() {
            const dpr = window.devicePixelRatio || 1;
            const width = globeCanvas.width;
            const height = globeCanvas.height;
            const cx = width / 2;
            const cy = height / 2;
            const radius = Math.min(width, height) * 0.35;

            gCtx.clearRect(0, 0, width, height);

            // Auto-rotação se não estiver arrastando
            if (!isDragging) {
                rotationY += 0.003;
            }

            // 1. Desenhar Atmo-Glow Esférico
            const bgGlow = gCtx.createRadialGradient(cx, cy, radius * 0.8, cx, cy, radius * 1.25);
            bgGlow.addColorStop(0, 'rgba(0, 243, 255, 0.08)');
            bgGlow.addColorStop(0.8, 'rgba(0, 243, 255, 0.02)');
            bgGlow.addColorStop(1, 'rgba(0, 0, 0, 0)');
            gCtx.fillStyle = bgGlow;
            gCtx.beginPath();
            gCtx.arc(cx, cy, radius * 1.3, 0, Math.PI * 2);
            gCtx.fill();

            // 2. Base da Esfera
            gCtx.strokeStyle = 'rgba(0, 243, 255, 0.25)';
            gCtx.lineWidth = 1.5 * dpr;
            gCtx.beginPath();
            gCtx.arc(cx, cy, radius, 0, Math.PI * 2);
            gCtx.stroke();

            // Grid de Paralelos e Meridianos
            gCtx.strokeStyle = 'rgba(0, 243, 255, 0.06)';
            gCtx.lineWidth = 1 * dpr;
            for (let lat = -60; lat <= 60; lat += 30) {
                gCtx.beginPath();
                for (let lon = -180; lon <= 180; lon += 10) {
                    const p = project3D(lat, lon, radius);
                    if (p.z > 0) {
                        if (lon === -180) gCtx.moveTo(cx + p.x, cy + p.y);
                        else gCtx.lineTo(cx + p.x, cy + p.y);
                    }
                }
                gCtx.stroke();
            }

            // 3. Desenhar Pontos de Continentes
            continentDots.forEach(dot => {
                const p = project3D(dot.lat, dot.lon, radius);
                if (p.z > 0) {
                    const alpha = Math.max(0.1, p.z / radius);
                    gCtx.fillStyle = `rgba(0, 243, 255, ${alpha * 0.7})`;
                    gCtx.beginPath();
                    gCtx.arc(cx + p.x, cy + p.y, 2.5 * dpr, 0, Math.PI * 2);
                    gCtx.fill();
                }
            });

            // 4. Rotas de Cooperação (Arcos Cyan/Verde Cintilantes)
            const time = Date.now() * 0.003;
            state.coopRoutes.forEach(route => {
                const b1 = state.blocs[route.from];
                const b2 = state.blocs[route.to];
                const p1 = project3D(b1.lat, b1.lon, radius);
                const p2 = project3D(b2.lat, b2.lon, radius);

                if (p1.z > 0 || p2.z > 0) {
                    gCtx.strokeStyle = 'rgba(0, 255, 136, 0.4)';
                    gCtx.lineWidth = 1.5 * dpr;
                    gCtx.setLineDash([4 * dpr, 4 * dpr]);
                    gCtx.lineDashOffset = -time * 10;
                    gCtx.beginPath();
                    
                    // Curva elevando o arco no centro
                    const midX = (p1.x + p2.x) / 2 * 1.25;
                    const midY = (p1.y + p2.y) / 2 * 1.25;

                    gCtx.moveTo(cx + p1.x, cy + p1.y);
                    gCtx.quadraticCurveTo(cx + midX, cy + midY, cx + p2.x, cy + p2.y);
                    gCtx.stroke();
                    gCtx.setLineDash([]);
                }
            });

            // 5. Blocos Geopolíticos (Nós Globais)
            state.blocs.forEach((bloc, idx) => {
                const p = project3D(bloc.lat, bloc.lon, radius);
                if (p.z > 0) {
                    const px = cx + p.x;
                    const py = cy + p.y;

                    // Halo Pulsante do Bloco
                    const pulse = Math.sin(time * 2 + idx) * 3 + 6;
                    gCtx.fillStyle = bloc.color + '33';
                    gCtx.beginPath();
                    gCtx.arc(px, py, (pulse + 4) * dpr, 0, Math.PI * 2);
                    gCtx.fill();

                    // Ponto Central
                    gCtx.fillStyle = bloc.color;
                    gCtx.beginPath();
                    gCtx.arc(px, py, 4 * dpr, 0, Math.PI * 2);
                    gCtx.fill();

                    // Rótulo do Bloco
                    gCtx.fillStyle = '#ffffff';
                    gCtx.font = `${9 * dpr}px Orbitron`;
                    gCtx.fillText(bloc.name, px + 8 * dpr, py + 3 * dpr);
                }
            });

            // 6. Vetores de Conflito Ativos (Pulsos Vermelhos)
            if (state.warRisk > 25) {
                state.activeConflicts.forEach(conf => {
                    const p = project3D(conf.lat, conf.lon, radius);
                    if (p.z > 0) {
                        const px = cx + p.x;
                        const py = cy + p.y;
                        const pulse = (Date.now() % 1000) / 1000;
                        
                        gCtx.strokeStyle = `rgba(255, 0, 85, ${1 - pulse})`;
                        gCtx.lineWidth = 2 * dpr;
                        gCtx.beginPath();
                        gCtx.arc(px, py, pulse * 25 * dpr, 0, Math.PI * 2);
                        gCtx.stroke();

                        gCtx.fillStyle = '#ff0055';
                        gCtx.beginPath();
                        gCtx.arc(px, py, 3 * dpr, 0, Math.PI * 2);
                        gCtx.fill();
                    }
                });
            }

            requestAnimationFrame(renderGlobe);
        }

        // Interatividade de Rotação Manual
        globeCanvas.addEventListener('mousedown', (e) => {
            isDragging = true;
            lastMouseX = e.clientX;
            lastMouseY = e.clientY;
        });
        window.addEventListener('mouseup', () => isDragging = false);
        window.addEventListener('mousemove', (e) => {
            if (!isDragging) return;
            const dx = e.clientX - lastMouseX;
            const dy = e.clientY - lastMouseY;
            rotationY += dx * 0.005;
            rotationX += dy * 0.005;
            lastMouseX = e.clientX;
            lastMouseY = e.clientY;
        });

        // Suporte para Touch (Mobile)
        globeCanvas.addEventListener('touchstart', (e) => {
            if (e.touches.length === 1) {
                isDragging = true;
                lastMouseX = e.touches[0].clientX;
                lastMouseY = e.touches[0].clientY;
            }
        });
        window.addEventListener('touchend', () => isDragging = false);
        window.addEventListener('touchmove', (e) => {
            if (!isDragging || e.touches.length !== 1) return;
            const dx = e.touches[0].clientX - lastMouseX;
            const dy = e.touches[0].clientY - lastMouseY;
            rotationY += dx * 0.005;
            rotationX += dy * 0.005;
            lastMouseX = e.touches[0].clientX;
            lastMouseY = e.touches[0].clientY;
        });

        // =========================================================================
        // GRÁFICO HISTÓRICO DINÂMICO NO CANVAS
        // =========================================================================
        const chartCanvas = document.getElementById('chart-canvas');
        const cCtx = chartCanvas.getContext('2d');

        function resizeChartCanvas() {
            const rect = chartCanvas.parentElement.getBoundingClientRect();
            chartCanvas.width = rect.width * window.devicePixelRatio;
            chartCanvas.height = rect.height * window.devicePixelRatio;
        }
        window.addEventListener('resize', resizeChartCanvas);
        resizeChartCanvas();

        function renderChart() {
            const width = chartCanvas.width;
            const height = chartCanvas.height;
            const dpr = window.devicePixelRatio || 1;

            cCtx.clearRect(0, 0, width, height);

            if (state.history.length < 2) return;

            // Desenhar Linhas Guia e Grid
            cCtx.strokeStyle = 'rgba(255, 255, 255, 0.05)';
            cCtx.lineWidth = 1 * dpr;
            for (let y = 0; y <= height; y += height / 4) {
                cCtx.beginPath();
                cCtx.moveTo(0, y);
                cCtx.lineTo(width, y);
                cCtx.stroke();
            }

            const stepX = width / (state.maxHistory - 1);

            // Helper para desenhar uma linha do gráfico
            function drawMetricLine(key, color, lineWidth = 2) {
                cCtx.strokeStyle = color;
                cCtx.lineWidth = lineWidth * dpr;
                cCtx.beginPath();

                state.history.forEach((sample, idx) => {
                    const x = idx * stepX;
                    const val = sample[key]; // 0 a 100 ou Kardashev mapeado
                    const y = height - (val / 100) * height;

                    if (idx === 0) cCtx.moveTo(x, y);
                    else cCtx.lineTo(x, y);
                });
                cCtx.stroke();
            }

            // Mapear Kardashev (0.70 - 1.00) para escala 0-100 para renderização
            const historyMapped = state.history.map(h => ({
                filter: h.filter,
                unity: h.unity,
                kardashevMap: (h.kardashev - 0.70) * 333.33 // 0.70 -> 0, 1.00 -> 100
            }));

            // Desenhar Relógio do Filtro (Vermelho/Rosa)
            drawMetricLine('filter', '#ff0055', 2.5);
            // Desenhar Unidade (Cyan)
            drawMetricLine('unity', '#00f3ff', 2);
            // Desenhar Kardashev (Verde)
            drawMetricLine('kardashevMap', '#00ff88', 1.5);
        }

        // =========================================================================
        // MOTOR DA SIMULAÇÃO PLANETÁRIA & SISTEMA DINÂMICO
        // =========================================================================
        function updateSimulation() {
            if (state.gameOver || state.victory) return;

            // Avanço do tempo
            state.year += 0.1;

            // 1. Atualizar Taxa de Reciclagem com base na Política Ecológica
            state.recycling += (state.ecoFunding - state.recycling) * 0.05;

            // 2. Dinâmica de Reservas de Recursos
            const consumption = (100 - state.sharing * 0.5) * 0.08;
            const recovery = state.recycling * 0.07;
            state.resources = Math.max(0, Math.min(100, state.resources + (recovery - consumption) * 0.1));

            // 3. Dinâmica de Coesão / Unidade Global
            const unityTarget = (state.sharing * 0.3) + (state.diplo * 0.5) + (state.disarm * 0.2);
            state.unity += (unityTarget - state.unity) * 0.04;

            // 4. Dinâmica do Risco de Guerra Sistêmica
            let warTension = 0;
            if (state.resources < 35) warTension += (35 - state.resources) * 0.8;
            if (state.unity < 40) warTension += (40 - state.unity) * 0.6;
            
            const disarmEffect = state.disarm * 0.4;
            const targetWarRisk = Math.max(0, warTension + 10 - disarmEffect);
            state.warRisk += (targetWarRisk - state.warRisk) * 0.05;

            // Atualizar locais de conflito ativo
            if (state.warRisk > 30 && Math.random() < 0.2) {
                const randomBloc = state.blocs[Math.floor(Math.random() * state.blocs.length)];
                state.activeConflicts = [{ lat: randomBloc.lat, lon: randomBloc.lon }];
            } else if (state.warRisk <= 30) {
                state.activeConflicts = [];
            }

            // 5. Relógio do Grande Filtro (% Ameaça de Extinção)
            const threatFactor = (state.warRisk * 0.4) + ((100 - state.resources) * 0.3) + ((100 - state.unity) * 0.3);
            state.filterClock += (threatFactor - state.filterClock) * 0.03;

            // 6. Progresso da Escala de Kardashev (Tipo I)
            if (state.filterClock < 60 && state.unity > 45) {
                const kGrowth = (state.unity / 100) * (state.resources / 100) * (1 + state.ecoFunding / 100) * 0.0008;
                state.kardashev = Math.min(1.000, state.kardashev + kGrowth);
            }

            // 7. Salvar histórico para gráfico
            state.history.push({
                filter: state.filterClock,
                unity: state.unity,
                kardashev: state.kardashev
            });
            if (state.history.length > state.maxHistory) state.history.shift();

            // 8. Checar Condições de Fim de Jogo ou Vitória
            checkGameConditions();

            // 9. Atualizar Interface do Usuário (UI)
            updateUI();

            // Renderizar Gráfico
            renderChart();
        }

        function addLogEntry(msg, type = 'info') {
            const logEl = document.getElementById('event-log');
            const entry = document.createElement('div');
            entry.className = 'p-1.5 rounded border text-[11px] font-mono animate-fade-in flex items-start gap-1.5';
            
            if (type === 'danger') {
                entry.className += ' bg-rose-950/60 border-rose-500/40 text-rose-300';
                entry.innerHTML = `<i class="fa-solid fa-circle-exclamation text-rose-400 mt-0.5"></i> <span>${msg}</span>`;
            } else if (type === 'success') {
                entry.className += ' bg-emerald-950/60 border-emerald-500/40 text-emerald-300';
                entry.innerHTML = `<i class="fa-solid fa-circle-check text-emerald-400 mt-0.5"></i> <span>${msg}</span>`;
            } else {
                entry.className += ' bg-slate-900/60 border-cyan-500/30 text-cyan-200';
                entry.innerHTML = `<i class="fa-solid fa-satellite text-cyan-400 mt-0.5"></i> <span>${msg}</span>`;
            }

            logEl.prepend(entry);
            if (logEl.children.length > 20) logEl.removeChild(logEl.lastChild);
        }

        function checkGameConditions() {
            // Condição de Derrota (Colapso Civilizacional)
            if (state.filterClock >= 100 || state.resources <= 0) {
                state.gameOver = true;
                state.filterClock = 100;
                document.getElementById('sim-status-text').innerHTML = `<span class="text-rose-500 font-bold"><i class="fa-solid fa-skull"></i> COLAPSO CIVILIZACIONAL</span>`;
                addLogEntry('CRÍTICO: O Grande Filtro não foi superado. Extinção da governança global.', 'danger');
                audio.playAlarm();
            }

            // Condição de Vitória (Conquista de Tipo I na Escala de Kardashev)
            if (state.kardashev >= 1.000 && !state.victory) {
                state.victory = true;
                document.getElementById('sim-status-text').innerHTML = `<span class="text-emerald-400 font-bold"><i class="fa-solid fa-crown"></i> CIVILIZAÇÃO TIPO I</span>`;
                addLogEntry('VITÓRIA PLANETÁRIA: Humanidade atingiu o Tipo I na Escala Kardashev e superou o Grande Filtro!', 'success');
                audio.playActionSuccess();
            }

            // Gerar eventos aleatórios esporádicos
            if (Math.random() < 0.05 && !state.gameOver) {
                triggerRandomEvent();
            }
        }

        function triggerRandomEvent() {
            const rand = Math.random();
            if (rand < 0.3 && state.warRisk > 40) {
                addLogEntry('ALERTA: Tensão fronteiriça escalada na Aliança Indo-Pacífico!', 'danger');
                audio.playConflictPulse();
            } else if (rand < 0.6) {
                addLogEntry('AVANÇO: Nova fusão nuclear limpa reduz demanda por recursos críticos.', 'success');
                state.resources = Math.min(100, state.resources + 4);
            } else if (rand < 0.8) {
                addLogEntry('CIMEIRA GLOBAL: Bloco Afro-Sustentável propõe nova meta de reciclagem.', 'info');
            }
        }

        function updateUI() {
            // Atualizar Textos
            document.getElementById('sim-year').innerText = state.year.toFixed(1);
            
            // Meter do Grande Filtro
            const filterValEl = document.getElementById('filter-threat-val');
            filterValEl.innerText = `${Math.round(state.filterClock)}%`;
            const circle = document.getElementById('filter-gauge-circle');
            const circumference = 2 * Math.PI * 42;
            const offset = circumference - (state.filterClock / 100) * circumference;
            circle.style.strokeDashoffset = offset;

            // Kardashev
            document.getElementById('kardashev-val').innerText = state.kardashev.toFixed(3);
            const kPercent = Math.max(0, Math.min(100, (state.kardashev - 0.70) * 333.33));
            document.getElementById('kardashev-bar').style.width = `${kPercent}%`;

            // Barras Secundárias
            document.getElementById('unity-val').innerText = `${Math.round(state.unity)}%`;
            document.getElementById('unity-bar').style.width = `${state.unity}%`;

            document.getElementById('resources-val').innerText = `${Math.round(state.resources)}%`;
            document.getElementById('resources-bar').style.width = `${state.resources}%`;

            document.getElementById('recycling-val').innerText = `${Math.round(state.recycling)}%`;
            document.getElementById('recycling-bar').style.width = `${state.recycling}%`;

            document.getElementById('war-val').innerText = `${Math.round(state.warRisk)}%`;
            document.getElementById('war-bar').style.width = `${state.warRisk}%`;

            // Mensagem de Aviso Dinâmica
            const msgEl = document.getElementById('filter-warning-msg');
            if (state.filterClock > 75) {
                msgEl.innerText = 'PERIGO EXTREMO: Colapso existencial iminente!';
                msgEl.className = 'text-xs text-center text-rose-400 font-mono mt-1 bg-rose-950/80 px-3 py-1 rounded border border-rose-500/50 animate-pulse';
            } else if (state.filterClock > 50) {
                msgEl.innerText = 'ALERTA: Instabilidade sistêmica elevada.';
                msgEl.className = 'text-xs text-center text-amber-400 font-mono mt-1 bg-amber-950/60 px-3 py-1 rounded border border-amber-500/40';
            } else {
                msgEl.innerText = 'Risco de extinção sob controle nominal.';
                msgEl.className = 'text-xs text-center text-cyan-300 font-mono mt-1 bg-slate-950/60 px-3 py-1 rounded border border-slate-800';
            }
        }

        // =========================================================================
        // EVENT LISTENERS DE CONTROLE E POLÍTICAS
        // =========================================================================
        
        // Vínculo dos Sliders
        const sliderMap = [
            { id: 'slider-sharing', valId: 'slider-sharing-val', key: 'sharing' },
            { id: 'slider-disarm', valId: 'slider-disarm-val', key: 'disarm' },
            { id: 'slider-eco', valId: 'slider-eco-val', key: 'ecoFunding' },
            { id: 'slider-diplo', valId: 'slider-diplo-val', key: 'diplo' }
        ];

        sliderMap.forEach(s => {
            const input = document.getElementById(s.id);
            const display = document.getElementById(s.valId);
            input.addEventListener('input', (e) => {
                const val = parseInt(e.target.value);
                state[s.key] = val;
                display.innerText = `${val}%`;
                audio.playBeep(300 + val * 4, 'sine', 0.03, 0.05);
            });
        });

        // Botões de Intervenções Táticas
        document.getElementById('btn-action-accord').addEventListener('click', () => {
            if (state.gameOver) return;
            state.unity = Math.min(100, state.unity + 12);
            state.filterClock = Math.max(0, state.filterClock - 4);
            addLogEntry('AÇÃO TÁTICA: Tratado Unificado assinado por 5 blocos.', 'success');
            audio.playActionSuccess();
        });

        document.getElementById('btn-action-grid').addEventListener('click', () => {
            if (state.gameOver) return;
            state.resources = Math.min(100, state.resources + 15);
            addLogEntry('AÇÃO TÁTICA: Malha de Recursos Redundantes ativada.', 'success');
            audio.playActionSuccess();
        });

        document.getElementById('btn-action-suppress').addEventListener('click', () => {
            if (state.gameOver) return;
            state.warRisk = Math.max(0, state.warRisk - 20);
            state.activeConflicts = [];
            addLogEntry('AÇÃO TÁTICA: Missão de Manutenção da Paz desescalou tensões.', 'success');
            audio.playActionSuccess();
        });

        document.getElementById('btn-action-aid').addEventListener('click', () => {
            if (state.gameOver) return;
            state.filterClock = Math.max(0, state.filterClock - 10);
            addLogEntry('AÇÃO TÁTICA: Socorro de Emergência mitiga ameaça iminente.', 'success');
            audio.playActionSuccess();
        });

        // Modal do Dossiê Teórico
        const dossierModal = document.getElementById('dossier-modal');
        document.getElementById('btn-dossier').addEventListener('click', () => {
            dossierModal.classList.remove('hidden');
            audio.playBeep(600, 'sine', 0.1, 0.1);
        });

        const closeDossier = () => dossierModal.classList.add('hidden');
        document.getElementById('btn-close-dossier').addEventListener('click', closeDossier);
        document.getElementById('btn-close-dossier-2').addEventListener('click', closeDossier);

        // Resetar Simulação
        document.getElementById('btn-reset').addEventListener('click', () => {
            state.year = 2050.0;
            state.filterClock = 32.0;
            state.kardashev = 0.728;
            state.unity = 55.0;
            state.resources = 68.0;
            state.recycling = 42.0;
            state.warRisk = 22.0;
            state.history = [];
            state.gameOver = false;
            state.victory = false;
            document.getElementById('sim-status-text').innerHTML = `<span class="text-emerald-400 font-bold flex items-center gap-1.5"><span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span> EM ESTABILIDADE</span>`;
            addLogEntry('SISTEMA: Simulação reiniciada para os parâmetros de 2050.', 'info');
            audio.playBeep(800, 'triangle', 0.2, 0.15);
        });

        // Alternar Áudio
        let audioMuted = false;
        document.getElementById('btn-audio-toggle').addEventListener('click', () => {
            audioMuted = !audioMuted;
            audio.enabled = !audioMuted;
            const icon = document.getElementById('audio-icon');
            icon.className = audioMuted ? 'fa-solid fa-volume-xmark text-rose-400' : 'fa-solid fa-volume-high text-cyan-400';
        });

        // =========================================================================
        // INICIALIZAÇÃO DO SIMULADOR
        // =========================================================================
        window.onload = () => {
            // Log de Boas-Vindas
            addLogEntry('INICIALIZADO: Terminal de Governança Planetária ativado.', 'info');
            addLogEntry('OBJETIVO: Mantenha o Relógio do Filtro < 100% e alcance Kardashev Tipo I.', 'info');

            // Iniciar renderização do Globo
            renderGlobe();

            // Loop de Simulação Dinâmica (A cada 300ms)
            setInterval(updateSimulation, 300);
        };
    </script>
</body>
</html>
