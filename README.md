<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogos Educativos 3.0 - Plataforma Completa</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            --secondary-gradient: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            --success-gradient: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            --warning-gradient: linear-gradient(135deg, #fa709a 0%, #fee140 100%);
            --dark-gradient: linear-gradient(135deg, #2c3e50 0%, #34495e 100%);
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: var(--primary-gradient);
            min-height: 100vh;
            color: #333;
            transition: all 0.5s ease;
            overflow-x: hidden;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        /* Header moderno */
        header {
            text-align: center;
            margin-bottom: 40px;
            background: rgba(255, 255, 255, 0.95);
            padding: 50px;
            border-radius: 30px;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.15);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            position: relative;
            overflow: hidden;
        }

        header::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            animation: shine 4s infinite;
        }

        @keyframes shine {
            0% { transform: translateX(-100%) translateY(-100%) rotate(45deg); }
            50% { transform: translateX(100%) translateY(100%) rotate(45deg); }
            100% { transform: translateX(-100%) translateY(-100%) rotate(45deg); }
        }

        h1 {
            font-size: 4rem;
            background: linear-gradient(135deg, #667eea, #764ba2, #f093fb, #f5576c);
            background-size: 300% 300%;
            background-clip: text;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 20px;
            animation: gradientShift 3s ease-in-out infinite alternate, titleFloat 2s ease-in-out infinite alternate;
            position: relative;
            z-index: 1;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            100% { background-position: 100% 50%; }
        }

        @keyframes titleFloat {
            0% { transform: translateY(0px) scale(1); }
            100% { transform: translateY(-10px) scale(1.02); }
        }

        .subtitle {
            font-size: 1.4rem;
            color: #4a5568;
            margin-bottom: 30px;
            position: relative;
            z-index: 1;
            font-weight: 600;
            animation: fadeInUp 1s ease-out;
        }

        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .version-badge {
            display: inline-block;
            background: linear-gradient(135deg, #ff6b6b, #ee5a24);
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: bold;
            margin-top: 15px;
            animation: pulse 2s infinite;
            position: relative;
            z-index: 1;
        }

        @keyframes pulse {
            0% { transform: scale(1); box-shadow: 0 0 0 0 rgba(255, 107, 107, 0.7); }
            70% { transform: scale(1.05); box-shadow: 0 0 0 10px rgba(255, 107, 107, 0); }
            100% { transform: scale(1); box-shadow: 0 0 0 0 rgba(255, 107, 107, 0); }
        }

        /* Sistema de Pontuação Global */
        .score-system {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 20px;
            border-radius: 20px;
            margin-bottom: 30px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
        }

        .score-title {
            font-size: 1.2rem;
            font-weight: bold;
            margin-bottom: 15px;
        }

        .score-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 15px;
        }

        .score-stat {
            background: rgba(255, 255, 255, 0.2);
            padding: 15px;
            border-radius: 15px;
            backdrop-filter: blur(10px);
        }

        .score-number {
            font-size: 2rem;
            font-weight: bold;
            margin-bottom: 5px;
        }

        .score-label {
            font-size: 0.9rem;
            opacity: 0.9;
        }

        /* Grid de jogos */
        .games-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(380px, 1fr));
            gap: 35px;
            margin-bottom: 50px;
        }

        .game-card {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 25px;
            padding: 35px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            cursor: pointer;
            position: relative;
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .game-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
            transition: left 0.5s ease;
        }

        .game-card:hover::before {
            left: 100%;
        }

        .game-card:hover {
            transform: translateY(-10px) scale(1.02);
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.2);
        }

        .game-icon {
            font-size: 5rem;
            text-align: center;
            margin-bottom: 25px;
            animation: iconFloat 3s ease-in-out infinite alternate;
        }

        @keyframes iconFloat {
            0% { transform: translateY(0px) rotate(0deg); }
            100% { transform: translateY(-5px) rotate(2deg); }
        }

        .game-title {
            font-size: 1.6rem;
            font-weight: bold;
            color: #2d3748;
            margin-bottom: 18px;
            text-align: center;
        }

        .game-description {
            color: #4a5568;
            text-align: center;
            margin-bottom: 25px;
            line-height: 1.7;
            font-size: 1rem;
        }

        .score-display {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 10px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
            margin-bottom: 20px;
            text-align: center;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.3);
        }

        .play-button {
            background: linear-gradient(135deg, #4facfe, #00f2fe);
            color: white;
            border: none;
            padding: 15px 35px;
            border-radius: 30px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
            transition: all 0.3s ease;
            box-shadow: 0 8px 25px rgba(79, 172, 254, 0.3);
            position: relative;
            overflow: hidden;
        }

        .play-button::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
            transition: left 0.5s ease;
        }

        .play-button:hover::before {
            left: 100%;
        }

        .play-button:hover {
            transform: scale(1.05);
            box-shadow: 0 12px 35px rgba(79, 172, 254, 0.4);
        }

        /* Modais */
        .game-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(10px);
            z-index: 2000;
            justify-content: center;
            align-items: center;
            animation: fadeIn 0.3s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .modal-content {
            background: rgba(255, 255, 255, 0.98);
            border-radius: 25px;
            padding: 45px;
            max-width: 700px;
            width: 90%;
            max-height: 85vh;
            overflow-y: auto;
            position: relative;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            animation: modalSlideIn 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        @keyframes modalSlideIn {
            from { opacity: 0; transform: scale(0.8) translateY(-50px); }
            to { opacity: 1; transform: scale(1) translateY(0); }
        }

        .close-button {
            position: absolute;
            top: 20px;
            right: 25px;
            background: linear-gradient(135deg, #ff6b6b, #ee5a24);
            color: white;
            border: none;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            font-size: 1.3rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(255, 107, 107, 0.3);
        }

        .close-button:hover {
            transform: scale(1.1) rotate(90deg);
            box-shadow: 0 8px 25px rgba(255, 107, 107, 0.4);
        }

        /* Estilos dos Jogos */
        .game-interface {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
        }

        .difficulty-selector {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }

        .difficulty-btn {
            padding: 15px 20px;
            border: none;
            border-radius: 15px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1rem;
        }

        .difficulty-btn.easy {
            background: linear-gradient(135deg, #48bb78, #38a169);
            color: white;
        }

        .difficulty-btn.medium {
            background: linear-gradient(135deg, #ed8936, #dd6b20);
            color: white;
        }

        .difficulty-btn.hard {
            background: linear-gradient(135deg, #e53e3e, #c53030);
            color: white;
        }

        .difficulty-btn.impossible {
            background: linear-gradient(135deg, #805ad5, #6b46c1);
            color: white;
        }

        .difficulty-btn.deadly {
            background: linear-gradient(135deg, #000000, #8b0000, #ff0000);
            color: white;
            animation: deadlyPulse 2s infinite;
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.5);
            border: 2px solid #ff0000;
            font-weight: 900;
            text-shadow: 0 0 10px rgba(255, 0, 0, 0.8);
        }

        @keyframes deadlyPulse {
            0% { 
                box-shadow: 0 0 20px rgba(255, 0, 0, 0.5);
                transform: scale(1);
            }
            50% { 
                box-shadow: 0 0 30px rgba(255, 0, 0, 0.8);
                transform: scale(1.02);
            }
            100% { 
                box-shadow: 0 0 20px rgba(255, 0, 0, 0.5);
                transform: scale(1);
            }
        }

        .difficulty-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
        }

        .difficulty-btn.active {
            transform: scale(1.1);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }

        .game-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }

        .stat-item {
            background: linear-gradient(135deg, #4facfe, #00f2fe);
            color: white;
            padding: 15px;
            border-radius: 15px;
            text-align: center;
            font-weight: bold;
        }

        .question-area {
            background: linear-gradient(135deg, #f7fafc, #edf2f7);
            padding: 30px;
            border-radius: 20px;
            margin-bottom: 25px;
            text-align: center;
            font-size: 1.5rem;
            font-weight: bold;
            color: #2d3748;
            min-height: 120px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .answer-input {
            width: 100%;
            padding: 20px;
            border: 3px solid #e2e8f0;
            border-radius: 15px;
            font-size: 1.3rem;
            text-align: center;
            margin-bottom: 20px;
            transition: all 0.3s ease;
        }

        .answer-input:focus {
            border-color: #4facfe;
            outline: none;
            box-shadow: 0 0 20px rgba(79, 172, 254, 0.3);
        }

        .options-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }

        .option-btn {
            padding: 20px;
            border: 3px solid #e2e8f0;
            border-radius: 15px;
            background: white;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1.1rem;
            font-weight: bold;
            color: #2d3748;
        }

        .option-btn:hover {
            border-color: #4facfe;
            background: #f7fafc;
            transform: scale(1.02);
        }

        .option-btn.correct {
            background: linear-gradient(135deg, #48bb78, #38a169);
            color: white;
            border-color: #48bb78;
        }

        .option-btn.incorrect {
            background: linear-gradient(135deg, #e53e3e, #c53030);
            color: white;
            border-color: #e53e3e;
        }

        .memory-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
            margin-bottom: 25px;
            max-width: 400px;
            margin: 0 auto 25px;
        }

        .memory-card {
            aspect-ratio: 1;
            background: linear-gradient(135deg, #4facfe, #00f2fe);
            border-radius: 15px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            color: white;
            font-weight: bold;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .memory-card.flipped {
            background: white;
            color: #2d3748;
            border: 3px solid #4facfe;
        }

        .memory-card.matched {
            background: linear-gradient(135deg, #48bb78, #38a169);
            color: white;
        }

        .memory-card:hover {
            transform: scale(1.05);
        }

        /* Responsividade */
        @media (max-width: 768px) {
            h1 {
                font-size: 2.5rem;
            }
            
            .games-grid {
                grid-template-columns: 1fr;
                gap: 25px;
            }

            .modal-content {
                padding: 30px;
                margin: 20px;
            }

            .memory-grid {
                grid-template-columns: repeat(3, 1fr);
            }

            .difficulty-selector {
                grid-template-columns: 1fr 1fr;
            }
        }

        /* Notificações */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 20px;
            border-radius: 15px;
            color: white;
            font-weight: bold;
            z-index: 3000;
            animation: slideInRight 0.5s ease-out;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }

        .notification.success {
            background: linear-gradient(135deg, #48bb78, #38a169);
        }

        .notification.error {
            background: linear-gradient(135deg, #e53e3e, #c53030);
        }

        @keyframes slideInRight {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        @keyframes slideOutRight {
            from { transform: translateX(0); opacity: 1; }
            to { transform: translateX(100%); opacity: 0; }
        }

        /* Conquistas */
        .achievement-perfect {
            background: linear-gradient(135deg, #ffd700, #ffed4e) !important;
            color: #2d3748 !important;
            padding: 15px;
            border-radius: 15px;
            margin: 15px 0;
            font-weight: bold;
            animation: pulse 2s infinite;
            text-align: center;
            box-shadow: 0 10px 30px rgba(255, 215, 0, 0.3);
        }

        /* Botões de controle */
        .control-btn {
            background: linear-gradient(135deg, #48bb78, #38a169);
            color: white;
            border: none;
            padding: 15px 25px;
            border-radius: 15px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            margin: 5px;
        }

        .control-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 25px rgba(72, 187, 120, 0.3);
        }

        .control-btn.secondary {
            background: linear-gradient(135deg, #4facfe, #00f2fe);
        }

        .control-btn.secondary:hover {
            box-shadow: 0 8px 25px rgba(79, 172, 254, 0.3);
        }

        /* Experimentos do laboratório */
        .experiment-card {
            background: linear-gradient(135deg, #f7fafc, #edf2f7);
            padding: 25px;
            border-radius: 20px;
            margin-bottom: 20px;
            border: 2px solid #e2e8f0;
            transition: all 0.3s ease;
        }

        .experiment-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
        }

        .experiment-title {
            font-size: 1.3rem;
            font-weight: bold;
            color: #2d3748;
            margin-bottom: 15px;
        }

        .experiment-description {
            color: #4a5568;
            margin-bottom: 20px;
            line-height: 1.6;
        }

        .experiment-btn {
            background: linear-gradient(135deg, #805ad5, #6b46c1);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 10px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .experiment-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 25px rgba(128, 90, 213, 0.3);
        }

        .experiment-result {
            background: linear-gradient(135deg, #48bb78, #38a169);
            color: white;
            padding: 20px;
            border-radius: 15px;
            margin-top: 20px;
            text-align: center;
            font-weight: bold;
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🎮 Jogos Educativos 3.0</h1>
            <p class="subtitle">A mais avançada plataforma educativa interativa do Brasil!</p>
            <div style="font-size: 2.5rem; margin-top: 20px;">🌟📚🎯🧠✨🚀🏆🎊</div>
            <div class="version-badge">VERSÃO 3.0 - TOTALMENTE FUNCIONAL!</div>
        </header>

        <!-- Sistema de Pontuação Global -->
        <div class="score-system">
            <div class="score-title">📊 Seu Progresso Global</div>
            <div class="score-stats">
                <div class="score-stat">
                    <div class="score-number" id="total-points">0</div>
                    <div class="score-label">Pontos Totais</div>
                </div>
                <div class="score-stat">
                    <div class="score-number" id="games-played">0</div>
                    <div class="score-label">Jogos Jogados</div>
                </div>
                <div class="score-stat">
                    <div class="score-number" id="achievements">0</div>
                    <div class="score-label">Conquistas</div>
                </div>
                <div class="score-stat">
                    <div class="score-number" id="streak">0</div>
                    <div class="score-label">Sequência</div>
                </div>
            </div>
        </div>

        <div class="games-grid">
            <!-- Desafio Matemático -->
            <div class="game-card">
                <div class="game-icon">🔢</div>
                <h3 class="game-title">Desafio Matemático</h3>
                <p class="game-description">Resolva operações matemáticas com diferentes níveis de dificuldade e cronômetro!</p>
                <div class="score-display">⭐ Melhor: <span id="math-best">0</span> | 🏆 Nível: <span id="math-level">Fácil</span></div>
                <button class="play-button" onclick="abrirJogo('math')">🚀 Jogar Agora</button>
            </div>

            <!-- Quiz de Português -->
            <div class="game-card">
                <div class="game-icon">📚</div>
                <h3 class="game-title">Quiz de Português</h3>
                <p class="game-description">Teste seus conhecimentos de gramática, ortografia e literatura brasileira!</p>
                <div class="score-display">⭐ Melhor: <span id="portuguese-best">0</span> | 🏆 Nível: <span id="portuguese-level">Fácil</span></div>
                <button class="play-button" onclick="abrirJogo('portuguese')">🚀 Jogar Agora</button>
            </div>

            <!-- Jogo da Memória -->
            <div class="game-card">
                <div class="game-icon">🧠</div>
                <h3 class="game-title">Jogo da Memória</h3>
                <p class="game-description">Exercite sua memória encontrando pares de cartas com temas educativos!</p>
                <div class="score-display">⭐ Melhor: <span id="memory-best">0</span> | 🏆 Nível: <span id="memory-level">Fácil</span></div>
                <button class="play-button" onclick="abrirJogo('memory')">🚀 Jogar Agora</button>
            </div>

            <!-- Quiz de Geografia -->
            <div class="game-card">
                <div class="game-icon">🌍</div>
                <h3 class="game-title">Quiz de Geografia</h3>
                <p class="game-description">Explore o mundo através de perguntas sobre países, capitais e curiosidades!</p>
                <div class="score-display">⭐ Melhor: <span id="geography-best">0</span> | 🏆 Nível: <span id="geography-level">Fácil</span></div>
                <button class="play-button" onclick="abrirJogo('geography')">🚀 Jogar Agora</button>
            </div>

            <!-- Laboratório Virtual -->
            <div class="game-card">
                <div class="game-icon">🔬</div>
                <h3 class="game-title">Laboratório Virtual</h3>
                <p class="game-description">Realize experimentos científicos seguros em um ambiente virtual interativo!</p>
                <div class="score-display">⭐ Experimentos: <span id="lab-count">0</span> | 🏆 Nível: <span id="lab-level">Básico</span></div>
                <button class="play-button" onclick="abrirJogo('lab')">🚀 Experimentar</button>
            </div>

            <!-- Quiz de História -->
            <div class="game-card">
                <div class="game-icon">🏛️</div>
                <h3 class="game-title">Quiz de História</h3>
                <p class="game-description">Viaje no tempo e teste seus conhecimentos sobre eventos históricos!</p>
                <div class="score-display">⭐ Melhor: <span id="history-best">0</span> | 🏆 Nível: <span id="history-level">Fácil</span></div>
                <button class="play-button" onclick="abrirJogo('history')">🚀 Jogar Agora</button>
            </div>
        </div>
    </div>

    <!-- Modal do Desafio Matemático -->
    <div id="math-modal" class="game-modal">
        <div class="modal-content" style="max-width: 800px;">
            <button class="close-button" onclick="fecharModal()">&times;</button>
            <h2 style="text-align: center; margin-bottom: 30px; color: #4a5568;">🔢 Desafio Matemático</h2>
            
            <div class="game-interface">
                <div class="difficulty-selector">
                    <button class="difficulty-btn easy active" onclick="selecionarDificuldade('math', 'easy')">😊 Fácil</button>
                    <button class="difficulty-btn medium" onclick="selecionarDificuldade('math', 'medium')">🤔 Médio</button>
                    <button class="difficulty-btn hard" onclick="selecionarDificuldade('math', 'hard')">😰 Difícil</button>
                    <button class="difficulty-btn impossible" onclick="selecionarDificuldade('math', 'impossible')">🤯 Impossível</button>
                    <button class="difficulty-btn deadly" onclick="selecionarDificuldade('math', 'deadly')">💀 MORTAL</button>
                </div>

                <div class="game-stats">
                    <div class="stat-item">
                        <div>Pontos: <span id="math-points">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Tempo: <span id="math-timer">30</span>s</div>
                    </div>
                    <div class="stat-item">
                        <div>Acertos: <span id="math-correct">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Sequência: <span id="math-streak">0</span></div>
                    </div>
                </div>

                <div class="question-area" id="math-question">
                    Clique em "Iniciar Jogo" para começar!
                </div>

                <input type="number" class="answer-input" id="math-answer" placeholder="Digite sua resposta" style="display: none;">

                <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                    <button onclick="iniciarJogoMatematico()" id="math-start-btn" class="control-btn">
                        🚀 Iniciar Jogo
                    </button>
                    <button onclick="verificarRespostaMatematica()" id="math-submit-btn" class="control-btn secondary" style="display: none;">
                        ✅ Confirmar
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal do Quiz de Português -->
    <div id="portuguese-modal" class="game-modal">
        <div class="modal-content" style="max-width: 800px;">
            <button class="close-button" onclick="fecharModal()">&times;</button>
            <h2 style="text-align: center; margin-bottom: 30px; color: #4a5568;">📚 Quiz de Português</h2>
            
            <div class="game-interface">
                <div class="difficulty-selector">
                    <button class="difficulty-btn easy active" onclick="selecionarDificuldade('portuguese', 'easy')">😊 Fácil</button>
                    <button class="difficulty-btn medium" onclick="selecionarDificuldade('portuguese', 'medium')">🤔 Médio</button>
                    <button class="difficulty-btn hard" onclick="selecionarDificuldade('portuguese', 'hard')">😰 Difícil</button>
                    <button class="difficulty-btn impossible" onclick="selecionarDificuldade('portuguese', 'impossible')">🤯 Impossível</button>
                    <button class="difficulty-btn deadly" onclick="selecionarDificuldade('portuguese', 'deadly')">💀 MORTAL</button>
                </div>

                <div class="game-stats">
                    <div class="stat-item">
                        <div>Pontos: <span id="portuguese-points">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Pergunta: <span id="portuguese-current">0</span>/10</div>
                    </div>
                    <div class="stat-item">
                        <div>Acertos: <span id="portuguese-correct">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Precisão: <span id="portuguese-accuracy">0</span>%</div>
                    </div>
                </div>

                <div class="question-area" id="portuguese-question">
                    Clique em "Iniciar Quiz" para começar!
                </div>

                <div class="options-grid" id="portuguese-options" style="display: none;">
                </div>

                <button onclick="iniciarQuizPortugues()" id="portuguese-start-btn" class="control-btn" style="width: 100%;">
                    🚀 Iniciar Quiz
                </button>
            </div>
        </div>
    </div>

    <!-- Modal do Jogo da Memória -->
    <div id="memory-modal" class="game-modal">
        <div class="modal-content" style="max-width: 600px;">
            <button class="close-button" onclick="fecharModal()">&times;</button>
            <h2 style="text-align: center; margin-bottom: 30px; color: #4a5568;">🧠 Jogo da Memória</h2>
            
            <div class="game-interface">
                <div class="difficulty-selector">
                    <button class="difficulty-btn easy active" onclick="selecionarDificuldade('memory', 'easy')">😊 Fácil (3x4)</button>
                    <button class="difficulty-btn medium" onclick="selecionarDificuldade('memory', 'medium')">🤔 Médio (4x4)</button>
                    <button class="difficulty-btn hard" onclick="selecionarDificuldade('memory', 'hard')">😰 Difícil (4x5)</button>
                    <button class="difficulty-btn impossible" onclick="selecionarDificuldade('memory', 'impossible')">🤯 Impossível (5x6)</button>
                    <button class="difficulty-btn deadly" onclick="selecionarDificuldade('memory', 'deadly')">💀 MORTAL (6x8)</button>
                </div>

                <div class="game-stats">
                    <div class="stat-item">
                        <div>Pontos: <span id="memory-points">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Tempo: <span id="memory-timer">0</span>s</div>
                    </div>
                    <div class="stat-item">
                        <div>Pares: <span id="memory-pairs">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Tentativas: <span id="memory-attempts">0</span></div>
                    </div>
                </div>

                <div class="memory-grid" id="memory-grid">
                </div>

                <button onclick="iniciarJogoMemoria()" id="memory-start-btn" class="control-btn" style="width: 100%;">
                    🚀 Iniciar Jogo
                </button>
            </div>
        </div>
    </div>

    <!-- Modal do Quiz de Geografia -->
    <div id="geography-modal" class="game-modal">
        <div class="modal-content" style="max-width: 800px;">
            <button class="close-button" onclick="fecharModal()">&times;</button>
            <h2 style="text-align: center; margin-bottom: 30px; color: #4a5568;">🌍 Quiz de Geografia</h2>
            
            <div class="game-interface">
                <div class="difficulty-selector">
                    <button class="difficulty-btn easy active" onclick="selecionarDificuldade('geography', 'easy')">😊 Fácil</button>
                    <button class="difficulty-btn medium" onclick="selecionarDificuldade('geography', 'medium')">🤔 Médio</button>
                    <button class="difficulty-btn hard" onclick="selecionarDificuldade('geography', 'hard')">😰 Difícil</button>
                    <button class="difficulty-btn impossible" onclick="selecionarDificuldade('geography', 'impossible')">🤯 Impossível</button>
                    <button class="difficulty-btn deadly" onclick="selecionarDificuldade('geography', 'deadly')">💀 MORTAL</button>
                </div>

                <div class="game-stats">
                    <div class="stat-item">
                        <div>Pontos: <span id="geography-points">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Pergunta: <span id="geography-current">0</span>/10</div>
                    </div>
                    <div class="stat-item">
                        <div>Acertos: <span id="geography-correct">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Precisão: <span id="geography-accuracy">0</span>%</div>
                    </div>
                </div>

                <div class="question-area" id="geography-question">
                    Clique em "Iniciar Quiz" para começar!
                </div>

                <div class="options-grid" id="geography-options" style="display: none;">
                </div>

                <button onclick="iniciarQuizGeografia()" id="geography-start-btn" class="control-btn" style="width: 100%;">
                    🚀 Iniciar Quiz
                </button>
            </div>
        </div>
    </div>

    <!-- Modal do Laboratório Virtual -->
    <div id="lab-modal" class="game-modal">
        <div class="modal-content" style="max-width: 800px;">
            <button class="close-button" onclick="fecharModal()">&times;</button>
            <h2 style="text-align: center; margin-bottom: 30px; color: #4a5568;">🔬 Laboratório Virtual</h2>
            
            <div class="game-interface">
                <div class="difficulty-selector">
                    <button class="difficulty-btn easy active" onclick="selecionarDificuldade('lab', 'easy')">😊 Básico</button>
                    <button class="difficulty-btn medium" onclick="selecionarDificuldade('lab', 'medium')">🤔 Intermediário</button>
                    <button class="difficulty-btn hard" onclick="selecionarDificuldade('lab', 'hard')">😰 Avançado</button>
                    <button class="difficulty-btn impossible" onclick="selecionarDificuldade('lab', 'impossible')">🤯 Especialista</button>
                    <button class="difficulty-btn deadly" onclick="selecionarDificuldade('lab', 'deadly')">💀 MORTAL</button>
                </div>

                <div class="game-stats">
                    <div class="stat-item">
                        <div>Pontos: <span id="lab-points">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Experimentos: <span id="lab-experiments">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Sucessos: <span id="lab-success">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Nível: <span id="lab-current-level">Básico</span></div>
                    </div>
                </div>

                <div id="lab-experiments-list">
                    <!-- Experimentos serão carregados aqui -->
                </div>
            </div>
        </div>
    </div>

    <!-- Modal do Quiz de História -->
    <div id="history-modal" class="game-modal">
        <div class="modal-content" style="max-width: 800px;">
            <button class="close-button" onclick="fecharModal()">&times;</button>
            <h2 style="text-align: center; margin-bottom: 30px; color: #4a5568;">🏛️ Quiz de História</h2>
            
            <div class="game-interface">
                <div class="difficulty-selector">
                    <button class="difficulty-btn easy active" onclick="selecionarDificuldade('history', 'easy')">😊 Fácil</button>
                    <button class="difficulty-btn medium" onclick="selecionarDificuldade('history', 'medium')">🤔 Médio</button>
                    <button class="difficulty-btn hard" onclick="selecionarDificuldade('history', 'hard')">😰 Difícil</button>
                    <button class="difficulty-btn impossible" onclick="selecionarDificuldade('history', 'impossible')">🤯 Impossível</button>
                    <button class="difficulty-btn deadly" onclick="selecionarDificuldade('history', 'deadly')">💀 MORTAL</button>
                </div>

                <div class="game-stats">
                    <div class="stat-item">
                        <div>Pontos: <span id="history-points">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Pergunta: <span id="history-current">0</span>/10</div>
                    </div>
                    <div class="stat-item">
                        <div>Acertos: <span id="history-correct">0</span></div>
                    </div>
                    <div class="stat-item">
                        <div>Precisão: <span id="history-accuracy">0</span>%</div>
                    </div>
                </div>

                <div class="question-area" id="history-question">
                    Clique em "Iniciar Quiz" para começar!
                </div>

                <div class="options-grid" id="history-options" style="display: none;">
                </div>

                <button onclick="iniciarQuizHistoria()" id="history-start-btn" class="control-btn" style="width: 100%;">
                    🚀 Iniciar Quiz
                </button>
            </div>
        </div>
    </div>

    <script>
        // Sistema de Pontuação Global
        class SistemaPontuacao {
            constructor() {
                this.pontos = parseInt(localStorage.getItem('totalPoints') || '0');
                this.jogosJogados = parseInt(localStorage.getItem('gamesPlayed') || '0');
                this.conquistas = parseInt(localStorage.getItem('achievements') || '0');
                this.sequencia = parseInt(localStorage.getItem('streak') || '0');
                this.atualizarDisplay();
                this.carregarMelhoresPontuacoes();
            }

            adicionarPontos(pontos, jogo) {
                this.pontos += pontos;
                this.jogosJogados++;
                this.sequencia++;
                
                if (this.pontos >= 100 && this.conquistas < 1) this.conquistas = 1;
                if (this.pontos >= 500 && this.conquistas < 2) this.conquistas = 2;
                if (this.sequencia >= 10 && this.conquistas < 3) this.conquistas = 3;

                this.salvar();
                this.atualizarDisplay();
                this.mostrarConquista(pontos, jogo);
            }

            salvar() {
                localStorage.setItem('totalPoints', this.pontos.toString());
                localStorage.setItem('gamesPlayed', this.jogosJogados.toString());
                localStorage.setItem('achievements', this.conquistas.toString());
                localStorage.setItem('streak', this.sequencia.toString());
            }

            atualizarDisplay() {
                document.getElementById('total-points').textContent = this.pontos;
                document.getElementById('games-played').textContent = this.jogosJogados;
                document.getElementById('achievements').textContent = this.conquistas;
                document.getElementById('streak').textContent = this.sequencia;
            }

            mostrarConquista(pontos, jogo) {
                if (pontos > 0) {
                    this.criarNotificacao(`🎉 +${pontos} pontos em ${jogo}!`, 'success');
                }
            }

            criarNotificacao(mensagem, tipo) {
                const notificacao = document.createElement('div');
                notificacao.className = `notification ${tipo}`;
                notificacao.textContent = mensagem;
                document.body.appendChild(notificacao);

                setTimeout(() => {
                    notificacao.style.animation = 'slideOutRight 0.5s ease-out';
                    setTimeout(() => notificacao.remove(), 500);
                }, 3000);
            }

            carregarMelhoresPontuacoes() {
                const jogos = ['math', 'portuguese', 'memory', 'geography', 'history'];
                jogos.forEach(jogo => {
                    const melhor = localStorage.getItem(`${jogo}-best`) || '0';
                    const elemento = document.getElementById(`${jogo}-best`);
                    if (elemento) elemento.textContent = melhor;
                });

                const labCount = localStorage.getItem('lab-count') || '0';
                const labElement = document.getElementById('lab-count');
                if (labElement) labElement.textContent = labCount;
            }
        }

        // Desafio Matemático
        class DesafioMatematico {
            constructor() {
                this.dificuldade = 'easy';
                this.pontos = 0;
                this.acertos = 0;
                this.sequencia = 0;
                this.tempo = 30;
                this.timer = null;
                this.perguntaAtual = null;
                this.respostaCorreta = null;
                this.ativo = false;
                this.erros = 0;
            }

            gerarPergunta() {
                let num1, num2, operacao, pergunta, resposta;
                
                switch(this.dificuldade) {
                    case 'easy':
                        num1 = Math.floor(Math.random() * 10) + 1;
                        num2 = Math.floor(Math.random() * 10) + 1;
                        operacao = Math.random() > 0.5 ? '+' : '-';
                        if (operacao === '-' && num1 < num2) [num1, num2] = [num2, num1];
                        pergunta = `${num1} ${operacao} ${num2}`;
                        resposta = operacao === '+' ? num1 + num2 : num1 - num2;
                        break;
                    case 'medium':
                        num1 = Math.floor(Math.random() * 50) + 1;
                        num2 = Math.floor(Math.random() * 20) + 1;
                        operacao = ['+', '-', '×'][Math.floor(Math.random() * 3)];
                        if (operacao === '-' && num1 < num2) [num1, num2] = [num2, num1];
                        pergunta = `${num1} ${operacao} ${num2}`;
                        resposta = operacao === '+' ? num1 + num2 : operacao === '-' ? num1 - num2 : num1 * num2;
                        break;
                    case 'hard':
                        num1 = Math.floor(Math.random() * 100) + 1;
                        num2 = Math.floor(Math.random() * 50) + 1;
                        operacao = ['+', '-', '×', '÷'][Math.floor(Math.random() * 4)];
                        if (operacao === '÷') {
                            num1 = num2 * (Math.floor(Math.random() * 10) + 1);
                        }
                        if (operacao === '-' && num1 < num2) [num1, num2] = [num2, num1];
                        pergunta = `${num1} ${operacao} ${num2}`;
                        resposta = operacao === '+' ? num1 + num2 : operacao === '-' ? num1 - num2 : operacao === '×' ? num1 * num2 : num1 / num2;
                        break;
                    case 'impossible':
                        num1 = Math.floor(Math.random() * 500) + 1;
                        num2 = Math.floor(Math.random() * 100) + 1;
                        const num3 = Math.floor(Math.random() * 50) + 1;
                        pergunta = `(${num1} + ${num2}) × ${num3}`;
                        resposta = (num1 + num2) * num3;
                        break;
                    case 'deadly':
                        num1 = Math.floor(Math.random() * 999) + 1;
                        num2 = Math.floor(Math.random() * 999) + 1;
                        const num3_deadly = Math.floor(Math.random() * 99) + 1;
                        const num4 = Math.floor(Math.random() * 99) + 1;
                        const operacoes = ['+', '-', '×'];
                        const op1 = operacoes[Math.floor(Math.random() * 3)];
                        const op2 = operacoes[Math.floor(Math.random() * 3)];
                        const op3 = operacoes[Math.floor(Math.random() * 3)];
                        
                        pergunta = `((${num1} ${op1} ${num2}) ${op2} ${num3_deadly}) ${op3} ${num4}`;
                        
                        let resultado1 = op1 === '+' ? num1 + num2 : op1 === '-' ? num1 - num2 : num1 * num2;
                        let resultado2 = op2 === '+' ? resultado1 + num3_deadly : op2 === '-' ? resultado1 - num3_deadly : resultado1 * num3_deadly;
                        resposta = op3 === '+' ? resultado2 + num4 : op3 === '-' ? resultado2 - num4 : resultado2 * num4;
                        break;
                }
                
                this.perguntaAtual = pergunta;
                this.respostaCorreta = resposta;
                document.getElementById('math-question').textContent = pergunta + ' = ?';
            }

            iniciar() {
                this.pontos = 0;
                this.acertos = 0;
                this.sequencia = 0;
                this.erros = 0;
                this.tempo = this.dificuldade === 'deadly' ? 15 : 30;
                this.ativo = true;
                
                document.getElementById('math-start-btn').style.display = 'none';
                document.getElementById('math-submit-btn').style.display = 'block';
                document.getElementById('math-answer').style.display = 'block';
                document.getElementById('math-answer').focus();
                
                this.gerarPergunta();
                this.iniciarTimer();
                this.atualizarDisplay();
            }

            iniciarTimer() {
                this.timer = setInterval(() => {
                    this.tempo--;
                    document.getElementById('math-timer').textContent = this.tempo;
                    
                    if (this.tempo <= 0) {
                        this.finalizarJogo();
                    }
                }, 1000);
            }

            verificarResposta() {
                if (!this.ativo) return;
                
                const resposta = parseFloat(document.getElementById('math-answer').value);
                
                if (Math.abs(resposta - this.respostaCorreta) < 0.01) {
                    this.acertos++;
                    this.sequencia++;
                    const pontosGanhos = this.dificuldade === 'easy' ? 10 : this.dificuldade === 'medium' ? 20 : this.dificuldade === 'hard' ? 30 : this.dificuldade === 'impossible' ? 50 : 100;
                    this.pontos += pontosGanhos + (this.sequencia * 2);
                    
                    sistemaPontuacao.criarNotificacao('✅ Correto!', 'success');
                } else {
                    this.erros++;
                    this.sequencia = 0;
                    sistemaPontuacao.criarNotificacao(`❌ Errado! Era ${this.respostaCorreta}`, 'error');
                }
                
                document.getElementById('math-answer').value = '';
                this.gerarPergunta();
                this.atualizarDisplay();
            }

            finalizarJogo() {
                this.ativo = false;
                clearInterval(this.timer);
                
                document.getElementById('math-start-btn').style.display = 'block';
                document.getElementById('math-submit-btn').style.display = 'none';
                document.getElementById('math-answer').style.display = 'none';
                
                // Verificar conquista de jogo perfeito (10+ acertos sem erros)
                let conquistaTexto = '';
                if (this.acertos >= 10 && this.erros === 0) {
                    const bonusPerfeito = this.dificuldade === 'easy' ? 50 : this.dificuldade === 'medium' ? 100 : this.dificuldade === 'hard' ? 200 : this.dificuldade === 'impossible' ? 500 : 1000;
                    this.pontos += bonusPerfeito;
                    conquistaTexto = `<div class="achievement-perfect">🏆 JOGO PERFEITO! +${bonusPerfeito} bônus! 🏆</div>`;
                    sistemaPontuacao.criarNotificacao(`🏆 JOGO PERFEITO em ${this.dificuldade.toUpperCase()}! +${bonusPerfeito} bônus!`, 'success');
                }
                
                document.getElementById('math-question').innerHTML = `
                    <div style="text-align: center;">
                        <h3>🎉 Jogo Finalizado!</h3>
                        <p>Pontos: ${this.pontos}</p>
                        <p>Acertos: ${this.acertos}</p>
                        <p>Erros: ${this.erros}</p>
                        ${conquistaTexto}
                    </div>
                `;
                
                sistemaPontuacao.adicionarPontos(this.pontos, 'Matemática');
                
                const melhorAnterior = parseInt(localStorage.getItem('math-best') || '0');
                if (this.pontos > melhorAnterior) {
                    localStorage.setItem('math-best', this.pontos.toString());
                    document.getElementById('math-best').textContent = this.pontos;
                }
            }

            atualizarDisplay() {
                document.getElementById('math-points').textContent = this.pontos;
                document.getElementById('math-correct').textContent = this.acertos;
                document.getElementById('math-streak').textContent = this.sequencia;
            }

            selecionarDificuldade(dificuldade) {
                this.dificuldade = dificuldade;
                document.getElementById('math-level').textContent = 
                    dificuldade === 'easy' ? 'Fácil' : 
                    dificuldade === 'medium' ? 'Médio' : 
                    dificuldade === 'hard' ? 'Difícil' : 
                    dificuldade === 'impossible' ? 'Impossível' : 'MORTAL';
            }
        }

        // Quiz de Português
        class QuizPortugues {
            constructor() {
                this.dificuldade = 'easy';
                this.pontos = 0;
                this.acertos = 0;
                this.perguntaAtual = 0;
                this.totalPerguntas = 10;
                this.perguntas = [];
                this.ativo = false;
                this.inicializarPerguntas();
            }

            inicializarPerguntas() {
                this.perguntasBase = {
                    easy: [
                        {
                            pergunta: "Qual é o plural de 'animal'?",
                            opcoes: ["animais", "animals", "animales", "animaes"],
                            correta: 0
                        },
                        {
                            pergunta: "Complete: 'Eu _____ na escola ontem.'",
                            opcoes: ["foi", "fui", "fomos", "foram"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual palavra está escrita corretamente?",
                            opcoes: ["excessão", "exceção", "exeção", "excesão"],
                            correta: 1
                        },
                        {
                            pergunta: "O que é um substantivo?",
                            opcoes: ["Palavra que indica ação", "Palavra que nomeia seres", "Palavra que qualifica", "Palavra que liga"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual é o feminino de 'galo'?",
                            opcoes: ["gala", "galinha", "galia", "galona"],
                            correta: 1
                        }
                    ],
                    medium: [
                        {
                            pergunta: "Qual figura de linguagem está presente em 'Seus olhos são duas estrelas'?",
                            opcoes: ["Metáfora", "Comparação", "Personificação", "Hipérbole"],
                            correta: 0
                        },
                        {
                            pergunta: "Complete com a forma correta: 'Se eu _____ rico, viajaria o mundo.'",
                            opcoes: ["fosse", "for", "seria", "sou"],
                            correta: 0
                        },
                        {
                            pergunta: "Qual é a função sintática de 'livro' em 'João comprou um livro'?",
                            opcoes: ["Sujeito", "Predicado", "Objeto direto", "Objeto indireto"],
                            correta: 2
                        },
                        {
                            pergunta: "Identifique a oração subordinada: 'Espero que você venha.'",
                            opcoes: ["Espero", "que você venha", "você venha", "Espero que"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual é o processo de formação da palavra 'infeliz'?",
                            opcoes: ["Composição", "Derivação", "Hibridismo", "Onomatopeia"],
                            correta: 1
                        }
                    ],
                    hard: [
                        {
                            pergunta: "Em 'Machado de Assis', qual escola literária o autor representa?",
                            opcoes: ["Romantismo", "Realismo", "Parnasianismo", "Simbolismo"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual é a diferença entre 'onde' e 'aonde'?",
                            opcoes: ["Não há diferença", "Onde = lugar, Aonde = movimento", "Aonde = lugar, Onde = movimento", "Ambos indicam tempo"],
                            correta: 1
                        },
                        {
                            pergunta: "Identifique a figura de linguagem em 'A vida é uma viagem':",
                            opcoes: ["Metonímia", "Sinestesia", "Metáfora", "Antítese"],
                            correta: 2
                        },
                        {
                            pergunta: "Qual é o sujeito em 'Choveu muito ontem'?",
                            opcoes: ["Muito", "Ontem", "Choveu", "Sujeito inexistente"],
                            correta: 3
                        },
                        {
                            pergunta: "Complete: 'Haja _____ o que houver, não desistirei.'",
                            opcoes: ["vista", "visto", "vistas", "vistos"],
                            correta: 1
                        }
                    ],
                    impossible: [
                        {
                            pergunta: "Qual é a classificação morfológica de 'que' em 'O livro que li era interessante'?",
                            opcoes: ["Conjunção", "Pronome relativo", "Advérbio", "Preposição"],
                            correta: 1
                        },
                        {
                            pergunta: "Identifique o período composto por coordenação:",
                            opcoes: ["Quando chegou, todos saíram", "Estudou muito, mas não passou", "Disse que viria cedo", "Espero que entenda"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual é a função da palavra 'se' em 'Não sei se ele virá'?",
                            opcoes: ["Pronome reflexivo", "Conjunção integrante", "Partícula apassivadora", "Índice de indeterminação"],
                            correta: 1
                        },
                        {
                            pergunta: "Em qual obra Machado de Assis criou o narrador Brás Cubas?",
                            opcoes: ["Dom Casmurro", "O Cortiço", "Memórias Póstumas de Brás Cubas", "Quincas Borba"],
                            correta: 2
                        },
                        {
                            pergunta: "Qual é a diferença entre 'cessão', 'sessão' e 'seção'?",
                            opcoes: ["São sinônimos", "Cessão=ato de ceder, Sessão=reunião, Seção=divisão", "Todas indicam tempo", "Não há diferença"],
                            correta: 1
                        }
                    ],
                    deadly: [
                        {
                            pergunta: "Qual é a diferença semântica entre 'iminente' e 'eminente'?",
                            opcoes: ["Não há diferença", "Iminente=prestes a acontecer, Eminente=elevado/ilustre", "Eminente=prestes a acontecer, Iminente=elevado", "Ambos significam urgente"],
                            correta: 1
                        },
                        {
                            pergunta: "Identifique a função sintática de 'lhe' em 'Eu lhe disse a verdade':",
                            opcoes: ["Objeto direto", "Objeto indireto", "Sujeito", "Predicativo"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual é o processo de formação da palavra 'planalto'?",
                            opcoes: ["Composição por justaposição", "Derivação prefixal", "Composição por aglutinação", "Derivação sufixal"],
                            correta: 2
                        },
                        {
                            pergunta: "Em 'Quem casa quer casa', qual é a classificação da primeira oração?",
                            opcoes: ["Subordinada substantiva subjetiva", "Subordinada adjetiva restritiva", "Principal", "Coordenada sindética"],
                            correta: 2
                        },
                        {
                            pergunta: "Qual é a diferença entre 'ratificar' e 'retificar'?",
                            opcoes: ["São sinônimos", "Ratificar=confirmar, Retificar=corrigir", "Retificar=confirmar, Ratificar=corrigir", "Ambos significam anular"],
                            correta: 1
                        }
                    ]
                };
            }

            iniciar() {
                this.pontos = 0;
                this.acertos = 0;
                this.perguntaAtual = 0;
                this.ativo = true;
                
                this.perguntas = [...this.perguntasBase[this.dificuldade]].sort(() => Math.random() - 0.5);
                
                document.getElementById('portuguese-start-btn').style.display = 'none';
                document.getElementById('portuguese-options').style.display = 'grid';
                
                this.mostrarPergunta();
                this.atualizarDisplay();
            }

            mostrarPergunta() {
                if (this.perguntaAtual >= this.perguntas.length) {
                    this.finalizarJogo();
                    return;
                }

                const pergunta = this.perguntas[this.perguntaAtual];
                document.getElementById('portuguese-question').textContent = pergunta.pergunta;
                
                const optionsContainer = document.getElementById('portuguese-options');
                optionsContainer.innerHTML = '';
                
                pergunta.opcoes.forEach((opcao, index) => {
                    const button = document.createElement('button');
                    button.className = 'option-btn';
                    button.textContent = opcao;
                    button.onclick = () => this.verificarResposta(index);
                    optionsContainer.appendChild(button);
                });
            }

            verificarResposta(opcaoSelecionada) {
                if (!this.ativo) return;
                
                const pergunta = this.perguntas[this.perguntaAtual];
                const buttons = document.querySelectorAll('#portuguese-options .option-btn');
                
                buttons.forEach((btn, index) => {
                    if (index === pergunta.correta) {
                        btn.classList.add('correct');
                    } else if (index === opcaoSelecionada && index !== pergunta.correta) {
                        btn.classList.add('incorrect');
                    }
                    btn.disabled = true;
                });
                
                if (opcaoSelecionada === pergunta.correta) {
                    this.acertos++;
                    const pontosGanhos = this.dificuldade === 'easy' ? 10 : this.dificuldade === 'medium' ? 20 : this.dificuldade === 'hard' ? 30 : this.dificuldade === 'impossible' ? 50 : 100;
                    this.pontos += pontosGanhos;
                    sistemaPontuacao.criarNotificacao('✅ Correto!', 'success');
                } else {
                    sistemaPontuacao.criarNotificacao('❌ Incorreto!', 'error');
                }
                
                setTimeout(() => {
                    this.perguntaAtual++;
                    this.mostrarPergunta();
                    this.atualizarDisplay();
                }, 2000);
            }

            finalizarJogo() {
                this.ativo = false;
                const precisao = Math.round((this.acertos / this.perguntas.length) * 100);
                
                document.getElementById('portuguese-start-btn').style.display = 'block';
                document.getElementById('portuguese-options').style.display = 'none';
                
                // Verificar conquista de quiz perfeito (todas corretas)
                let conquistaTexto = '';
                if (this.acertos === this.perguntas.length) {
                    const bonusPerfeito = this.dificuldade === 'easy' ? 50 : this.dificuldade === 'medium' ? 100 : this.dificuldade === 'hard' ? 200 : this.dificuldade === 'impossible' ? 500 : 1000;
                    this.pontos += bonusPerfeito;
                    conquistaTexto = `<div class="achievement-perfect">🏆 QUIZ PERFEITO! +${bonusPerfeito} bônus! 🏆</div>`;
                    sistemaPontuacao.criarNotificacao(`🏆 QUIZ PERFEITO em ${this.dificuldade.toUpperCase()}! +${bonusPerfeito} bônus!`, 'success');
                }
                
                document.getElementById('portuguese-question').innerHTML = `
                    <div style="text-align: center;">
                        <h3>🎉 Quiz Finalizado!</h3>
                        <p>Pontos: ${this.pontos}</p>
                        <p>Acertos: ${this.acertos}/${this.perguntas.length}</p>
                        <p>Precisão: ${precisao}%</p>
                        ${conquistaTexto}
                    </div>
                `;
                
                sistemaPontuacao.adicionarPontos(this.pontos, 'Português');
                
                const melhorAnterior = parseInt(localStorage.getItem('portuguese-best') || '0');
                if (this.pontos > melhorAnterior) {
                    localStorage.setItem('portuguese-best', this.pontos.toString());
                    document.getElementById('portuguese-best').textContent = this.pontos;
                }
            }

            atualizarDisplay() {
                document.getElementById('portuguese-points').textContent = this.pontos;
                document.getElementById('portuguese-current').textContent = this.perguntaAtual + 1;
                document.getElementById('portuguese-correct').textContent = this.acertos;
                const precisao = this.perguntaAtual > 0 ? Math.round((this.acertos / this.perguntaAtual) * 100) : 0;
                document.getElementById('portuguese-accuracy').textContent = precisao;
            }

            selecionarDificuldade(dificuldade) {
                this.dificuldade = dificuldade;
                document.getElementById('portuguese-level').textContent = 
                    dificuldade === 'easy' ? 'Fácil' : 
                    dificuldade === 'medium' ? 'Médio' : 
                    dificuldade === 'hard' ? 'Difícil' : 
                    dificuldade === 'impossible' ? 'Impossível' : 'MORTAL';
            }
        }

        // Jogo da Memória
        class JogoMemoria {
            constructor() {
                this.dificuldade = 'easy';
                this.pontos = 0;
                this.pares = 0;
                this.tentativas = 0;
                this.tempo = 0;
                this.timer = null;
                this.cartasViradas = [];
                this.cartasEncontradas = [];
                this.cartas = [];
                this.ativo = false;
                this.emojis = ['🐶', '🐱', '🐭', '🐹', '🐰', '🦊', '🐻', '🐼', '🐨', '🐯', '🦁', '🐮', '🐷', '🐸', '🐵', '🐔', '🐧', '🐦', '🐤', '🦆', '🦅', '🦉', '🦇', '🐺', '🐗'];
            }

            gerarCartas() {
                const tamanhos = {
                    easy: { cols: 3, rows: 4 },
                    medium: { cols: 4, rows: 4 },
                    hard: { cols: 4, rows: 5 },
                    impossible: { cols: 5, rows: 6 },
                    deadly: { cols: 6, rows: 8 }
                };
                
                const { cols, rows } = tamanhos[this.dificuldade];
                const totalCartas = cols * rows;
                const pares = totalCartas / 2;
                
                this.cartas = [];
                const emojisUsados = this.emojis.slice(0, pares);
                
                emojisUsados.forEach(emoji => {
                    this.cartas.push(emoji, emoji);
                });
                
                this.cartas.sort(() => Math.random() - 0.5);
                
                const grid = document.getElementById('memory-grid');
                grid.style.gridTemplateColumns = `repeat(${cols}, 1fr)`;
                grid.innerHTML = '';
                
                this.cartas.forEach((emoji, index) => {
                    const carta = document.createElement('div');
                    carta.className = 'memory-card';
                    carta.dataset.index = index;
                    carta.dataset.emoji = emoji;
                    carta.textContent = '?';
                    carta.onclick = () => this.virarCarta(index);
                    grid.appendChild(carta);
                });
            }

            iniciar() {
                this.pontos = 0;
                this.pares = 0;
                this.tentativas = 0;
                this.tempo = 0;
                this.cartasViradas = [];
                this.cartasEncontradas = [];
                this.ativo = true;
                
                document.getElementById('memory-start-btn').style.display = 'none';
                
                this.gerarCartas();
                this.iniciarTimer();
                this.atualizarDisplay();
            }

            iniciarTimer() {
                this.timer = setInterval(() => {
                    this.tempo++;
                    document.getElementById('memory-timer').textContent = this.tempo;
                }, 1000);
            }

            virarCarta(index) {
                if (!this.ativo || this.cartasViradas.length >= 2 || this.cartasViradas.includes(index) || this.cartasEncontradas.includes(index)) {
                    return;
                }
                
                const carta = document.querySelector(`[data-index="${index}"]`);
                carta.textContent = carta.dataset.emoji;
                carta.classList.add('flipped');
                this.cartasViradas.push(index);
                
                if (this.cartasViradas.length === 2) {
                    this.tentativas++;
                    setTimeout(() => this.verificarPar(), 1000);
                }
            }

            verificarPar() {
                const [index1, index2] = this.cartasViradas;
                const carta1 = document.querySelector(`[data-index="${index1}"]`);
                const carta2 = document.querySelector(`[data-index="${index2}"]`);
                
                if (carta1.dataset.emoji === carta2.dataset.emoji) {
                    carta1.classList.add('matched');
                    carta2.classList.add('matched');
                    this.cartasEncontradas.push(index1, index2);
                    this.pares++;
                    
                    const pontosGanhos = this.dificuldade === 'easy' ? 20 : this.dificuldade === 'medium' ? 30 : this.dificuldade === 'hard' ? 40 : this.dificuldade === 'impossible' ? 60 : 120;
                    this.pontos += pontosGanhos;
                    
                    sistemaPontuacao.criarNotificacao('✅ Par encontrado!', 'success');
                    
                    if (this.cartasEncontradas.length === this.cartas.length) {
                        this.finalizarJogo();
                    }
                } else {
                    carta1.textContent = '?';
                    carta2.textContent = '?';
                    carta1.classList.remove('flipped');
                    carta2.classList.remove('flipped');
                }
                
                this.cartasViradas = [];
                this.atualizarDisplay();
            }

            finalizarJogo() {
                this.ativo = false;
                clearInterval(this.timer);
                
                document.getElementById('memory-start-btn').style.display = 'block';
                
                const bonusTempo = Math.max(0, 300 - this.tempo) * 2;
                this.pontos += bonusTempo;
                
                // Verificar conquista de memória perfeita (sem erros)
                const totalPares = this.cartas.length / 2;
                let conquistaTexto = '';
                if (this.tentativas === totalPares) {
                    const bonusPerfeito = this.dificuldade === 'easy' ? 100 : this.dificuldade === 'medium' ? 200 : this.dificuldade === 'hard' ? 300 : this.dificuldade === 'impossible' ? 500 : 1000;
                    this.pontos += bonusPerfeito;
                    conquistaTexto = `<div class="achievement-perfect">🏆 MEMÓRIA PERFEITA! +${bonusPerfeito} bônus! 🏆</div>`;
                    sistemaPontuacao.criarNotificacao(`🏆 MEMÓRIA PERFEITA em ${this.dificuldade.toUpperCase()}! +${bonusPerfeito} bônus!`, 'success');
                }
                
                const grid = document.getElementById('memory-grid');
                grid.innerHTML = `
                    <div style="grid-column: 1 / -1; text-align: center; padding: 20px;">
                        <h3>🎉 Jogo Completo!</h3>
                        <p>Pontos: ${this.pontos}</p>
                        <p>Tempo: ${this.tempo}s</p>
                        <p>Tentativas: ${this.tentativas}</p>
                        <p>Bônus tempo: +${bonusTempo}</p>
                        ${conquistaTexto}
                    </div>
                `;
                
                sistemaPontuacao.criarNotificacao(`🎉 Jogo completo! +${bonusTempo} bônus de tempo!`, 'success');
                sistemaPontuacao.adicionarPontos(this.pontos, 'Memória');
                
                const melhorAnterior = parseInt(localStorage.getItem('memory-best') || '0');
                if (this.pontos > melhorAnterior) {
                    localStorage.setItem('memory-best', this.pontos.toString());
                    document.getElementById('memory-best').textContent = this.pontos;
                }
            }

            atualizarDisplay() {
                document.getElementById('memory-points').textContent = this.pontos;
                document.getElementById('memory-pairs').textContent = this.pares;
                document.getElementById('memory-attempts').textContent = this.tentativas;
            }

            selecionarDificuldade(dificuldade) {
                this.dificuldade = dificuldade;
                document.getElementById('memory-level').textContent = 
                    dificuldade === 'easy' ? 'Fácil' : 
                    dificuldade === 'medium' ? 'Médio' : 
                    dificuldade === 'hard' ? 'Difícil' : 
                    dificuldade === 'impossible' ? 'Impossível' : 'MORTAL';
            }
        }

        // Quiz de Geografia
        class QuizGeografia {
            constructor() {
                this.dificuldade = 'easy';
                this.pontos = 0;
                this.acertos = 0;
                this.perguntaAtual = 0;
                this.totalPerguntas = 10;
                this.perguntas = [];
                this.ativo = false;
                this.inicializarPerguntas();
            }

            inicializarPerguntas() {
                this.perguntasBase = {
                    easy: [
                        {
                            pergunta: "Qual é a capital do Brasil?",
                            opcoes: ["São Paulo", "Rio de Janeiro", "Brasília", "Salvador"],
                            correta: 2
                        },
                        {
                            pergunta: "Qual é o maior país do mundo?",
                            opcoes: ["China", "Estados Unidos", "Canadá", "Rússia"],
                            correta: 3
                        },
                        {
                            pergunta: "Em que continente fica o Egito?",
                            opcoes: ["Ásia", "África", "Europa", "América"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual é o rio mais longo do mundo?",
                            opcoes: ["Amazonas", "Nilo", "Mississippi", "Yangtzé"],
                            correta: 1
                        },
                        {
                            pergunta: "Quantos continentes existem?",
                            opcoes: ["5", "6", "7", "8"],
                            correta: 2
                        }
                    ],
                    medium: [
                        {
                            pergunta: "Qual é a capital da Austrália?",
                            opcoes: ["Sydney", "Melbourne", "Canberra", "Perth"],
                            correta: 2
                        },
                        {
                            pergunta: "Qual país tem a maior população do mundo?",
                            opcoes: ["Índia", "China", "Estados Unidos", "Indonésia"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual cordilheira separa a Europa da Ásia?",
                            opcoes: ["Alpes", "Andes", "Urais", "Himalaia"],
                            correta: 2
                        },
                        {
                            pergunta: "Qual é o ponto mais alto da Terra?",
                            opcoes: ["K2", "Monte Everest", "Kangchenjunga", "Lhotse"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual é a capital do Canadá?",
                            opcoes: ["Toronto", "Vancouver", "Montreal", "Ottawa"],
                            correta: 3
                        }
                    ],
                    hard: [
                        {
                            pergunta: "Qual é a capital do Cazaquistão?",
                            opcoes: ["Almaty", "Astana", "Shymkent", "Aktobe"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual país tem mais fusos horários?",
                            opcoes: ["Rússia", "Estados Unidos", "China", "França"],
                            correta: 3
                        },
                        {
                            pergunta: "Qual é o lago mais profundo do mundo?",
                            opcoes: ["Lago Superior", "Lago Baikal", "Lago Tanganica", "Mar Cáspio"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual país é conhecido como 'Terra do Sol Nascente'?",
                            opcoes: ["China", "Coreia do Sul", "Japão", "Tailândia"],
                            correta: 2
                        },
                        {
                            pergunta: "Qual é o deserto mais seco do mundo?",
                            opcoes: ["Saara", "Atacama", "Gobi", "Kalahari"],
                            correta: 1
                        }
                    ],
                    impossible: [
                        {
                            pergunta: "Qual é a capital de Burkina Faso?",
                            opcoes: ["Ouagadougou", "Bobo-Dioulasso", "Koudougou", "Banfora"],
                            correta: 0
                        },
                        {
                            pergunta: "Qual país tem o código ISO 'BH'?",
                            opcoes: ["Butão", "Bahrain", "Belize", "Benin"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual é a moeda oficial de Vanuatu?",
                            opcoes: ["Dólar de Vanuatu", "Vatu", "Franco do Pacífico", "Kina"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual arquipélago pertence ao Equador?",
                            opcoes: ["Açores", "Galápagos", "Maldivas", "Seychelles"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual é o ponto mais baixo da Terra?",
                            opcoes: ["Vale da Morte", "Mar Morto", "Depressão de Qattara", "Lago Assal"],
                            correta: 1
                        }
                    ],
                    deadly: [
                        {
                            pergunta: "Qual é a capital de São Tomé e Príncipe?",
                            opcoes: ["São Tomé", "Príncipe", "Santo António", "Trindade"],
                            correta: 0
                        },
                        {
                            pergunta: "Qual país tem o código telefônico internacional +298?",
                            opcoes: ["Ilhas Faroé", "Groenlândia", "Islândia", "Andorra"],
                            correta: 0
                        },
                        {
                            pergunta: "Qual é a moeda oficial de Bhutan?",
                            opcoes: ["Rupiah", "Ngultrum", "Taka", "Kyat"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual é o ponto mais alto da Antártida?",
                            opcoes: ["Monte Erebus", "Monte Sidley", "Vinson Massif", "Monte Terror"],
                            correta: 2
                        },
                        {
                            pergunta: "Qual país possui o enclave de Cabinda?",
                            opcoes: ["República Democrática do Congo", "Angola", "Gabão", "Camarões"],
                            correta: 1
                        }
                    ]
                };
            }

            iniciar() {
                this.pontos = 0;
                this.acertos = 0;
                this.perguntaAtual = 0;
                this.ativo = true;
                
                this.perguntas = [...this.perguntasBase[this.dificuldade]].sort(() => Math.random() - 0.5);
                
                document.getElementById('geography-start-btn').style.display = 'none';
                document.getElementById('geography-options').style.display = 'grid';
                
                this.mostrarPergunta();
                this.atualizarDisplay();
            }

            mostrarPergunta() {
                if (this.perguntaAtual >= this.perguntas.length) {
                    this.finalizarJogo();
                    return;
                }

                const pergunta = this.perguntas[this.perguntaAtual];
                document.getElementById('geography-question').textContent = pergunta.pergunta;
                
                const optionsContainer = document.getElementById('geography-options');
                optionsContainer.innerHTML = '';
                
                pergunta.opcoes.forEach((opcao, index) => {
                    const button = document.createElement('button');
                    button.className = 'option-btn';
                    button.textContent = opcao;
                    button.onclick = () => this.verificarResposta(index);
                    optionsContainer.appendChild(button);
                });
            }

            verificarResposta(opcaoSelecionada) {
                if (!this.ativo) return;
                
                const pergunta = this.perguntas[this.perguntaAtual];
                const buttons = document.querySelectorAll('#geography-options .option-btn');
                
                buttons.forEach((btn, index) => {
                    if (index === pergunta.correta) {
                        btn.classList.add('correct');
                    } else if (index === opcaoSelecionada && index !== pergunta.correta) {
                        btn.classList.add('incorrect');
                    }
                    btn.disabled = true;
                });
                
                if (opcaoSelecionada === pergunta.correta) {
                    this.acertos++;
                    const pontosGanhos = this.dificuldade === 'easy' ? 10 : this.dificuldade === 'medium' ? 20 : this.dificuldade === 'hard' ? 30 : this.dificuldade === 'impossible' ? 50 : 100;
                    this.pontos += pontosGanhos;
                    sistemaPontuacao.criarNotificacao('✅ Correto!', 'success');
                } else {
                    sistemaPontuacao.criarNotificacao('❌ Incorreto!', 'error');
                }
                
                setTimeout(() => {
                    this.perguntaAtual++;
                    this.mostrarPergunta();
                    this.atualizarDisplay();
                }, 2000);
            }

            finalizarJogo() {
                this.ativo = false;
                const precisao = Math.round((this.acertos / this.perguntas.length) * 100);
                
                document.getElementById('geography-start-btn').style.display = 'block';
                document.getElementById('geography-options').style.display = 'none';
                
                // Verificar conquista de geografia perfeita (todas corretas)
                let conquistaTexto = '';
                if (this.acertos === this.perguntas.length) {
                    const bonusPerfeito = this.dificuldade === 'easy' ? 50 : this.dificuldade === 'medium' ? 100 : this.dificuldade === 'hard' ? 200 : this.dificuldade === 'impossible' ? 500 : 1000;
                    this.pontos += bonusPerfeito;
                    conquistaTexto = `<div class="achievement-perfect">🏆 GEOGRAFIA PERFEITA! +${bonusPerfeito} bônus! 🏆</div>`;
                    sistemaPontuacao.criarNotificacao(`🏆 GEOGRAFIA PERFEITA em ${this.dificuldade.toUpperCase()}! +${bonusPerfeito} bônus!`, 'success');
                }
                
                document.getElementById('geography-question').innerHTML = `
                    <div style="text-align: center;">
                        <h3>🎉 Quiz Finalizado!</h3>
                        <p>Pontos: ${this.pontos}</p>
                        <p>Acertos: ${this.acertos}/${this.perguntas.length}</p>
                        <p>Precisão: ${precisao}%</p>
                        ${conquistaTexto}
                    </div>
                `;
                
                sistemaPontuacao.adicionarPontos(this.pontos, 'Geografia');
                
                const melhorAnterior = parseInt(localStorage.getItem('geography-best') || '0');
                if (this.pontos > melhorAnterior) {
                    localStorage.setItem('geography-best', this.pontos.toString());
                    document.getElementById('geography-best').textContent = this.pontos;
                }
            }

            atualizarDisplay() {
                document.getElementById('geography-points').textContent = this.pontos;
                document.getElementById('geography-current').textContent = this.perguntaAtual + 1;
                document.getElementById('geography-correct').textContent = this.acertos;
                const precisao = this.perguntaAtual > 0 ? Math.round((this.acertos / this.perguntaAtual) * 100) : 0;
                document.getElementById('geography-accuracy').textContent = precisao;
            }

            selecionarDificuldade(dificuldade) {
                this.dificuldade = dificuldade;
                document.getElementById('geography-level').textContent = 
                    dificuldade === 'easy' ? 'Fácil' : 
                    dificuldade === 'medium' ? 'Médio' : 
                    dificuldade === 'hard' ? 'Difícil' : 
                    dificuldade === 'impossible' ? 'Impossível' : 'MORTAL';
            }
        }

        // Laboratório Virtual
        class LaboratorioVirtual {
            constructor() {
                this.dificuldade = 'easy';
                this.pontos = 0;
                this.experimentos = 0;
                this.sucessos = 0;
                this.experimentosRealizados = [];
                this.inicializarExperimentos();
            }

            inicializarExperimentos() {
                this.experimentosBase = {
                    easy: [
                        {
                            titulo: "🌱 Germinação de Sementes",
                            descricao: "Observe como as sementes germinam com água e luz.",
                            resultado: "As sementes germinaram após 3 dias! Você observou o crescimento das raízes e folhas.",
                            pontos: 15
                        },
                        {
                            titulo: "🔥 Combustão da Vela",
                            descricao: "Estude a reação de combustão e os produtos formados.",
                            resultado: "A vela queimou consumindo oxigênio e produzindo CO₂ e vapor d'água!",
                            pontos: 20
                        },
                        {
                            titulo: "🧲 Magnetismo",
                            descricao: "Teste quais materiais são atraídos por ímãs.",
                            resultado: "Ferro, níquel e cobalto foram atraídos! Plástico e madeira não foram afetados.",
                            pontos: 18
                        }
                    ],
                    medium: [
                        {
                            titulo: "⚗️ Reação Ácido-Base",
                            descricao: "Misture vinagre (ácido) com bicarbonato (base) e observe.",
                            resultado: "Houve efervescência! Formou-se CO₂, água e acetato de sódio. pH neutralizado!",
                            pontos: 25
                        },
                        {
                            titulo: "🔬 Osmose em Células",
                            descricao: "Observe o movimento da água através de membranas celulares.",
                            resultado: "A água moveu-se do meio hipotônico para o hipertônico! Células murcharam.",
                            pontos: 30
                        },
                        {
                            titulo: "⚡ Condutividade Elétrica",
                            descricao: "Teste quais soluções conduzem eletricidade.",
                            resultado: "Água salgada conduziu bem! Água pura e açúcar não conduziram.",
                            pontos: 28
                        }
                    ],
                    hard: [
                        {
                            titulo: "🧬 Extração de DNA",
                            descricao: "Extraia DNA de frutas usando detergente e álcool.",
                            resultado: "DNA extraído com sucesso! Observou-se a estrutura fibrilar característica.",
                            pontos: 40
                        },
                        {
                            titulo: "🌡️ Cristalização",
                            descricao: "Forme cristais controlando temperatura e concentração.",
                            resultado: "Cristais perfeitos formados! Estrutura hexagonal observada no microscópio.",
                            pontos: 35
                        },
                        {
                            titulo: "🔋 Pilha de Batata",
                            descricao: "Crie eletricidade usando batatas e metais diferentes.",
                            resultado: "Gerou 1.2V! A diferença de potencial entre zinco e cobre funcionou!",
                            pontos: 38
                        }
                    ],
                    impossible: [
                        {
                            titulo: "⚛️ Espectroscopia",
                            descricao: "Analise a composição de elementos através da luz emitida.",
                            resultado: "Identificou hidrogênio, hélio e sódio! Cada elemento tem assinatura única.",
                            pontos: 60
                        },
                        {
                            titulo: "🧪 Síntese Orgânica",
                            descricao: "Sintetize aspirina a partir de ácido salicílico.",
                            resultado: "Aspirina sintetizada com 85% de pureza! Reação de acetilação bem-sucedida.",
                            pontos: 55
                        },
                        {
                            titulo: "🔬 Microscopia Eletrônica",
                            descricao: "Observe estruturas celulares em nível nanométrico.",
                            resultado: "Visualizou mitocôndrias e ribossomos! Resolução de 0.1 nanômetros alcançada.",
                            pontos: 65
                        }
                    ],
                    deadly: [
                        {
                            titulo: "🧬 Engenharia Genética CRISPR",
                            descricao: "Edite genes usando a tecnologia CRISPR-Cas9 para corrigir mutações.",
                            resultado: "Gene editado com 99.7% de precisão! Mutação corrigida sem efeitos colaterais. Revolução na medicina!",
                            pontos: 150
                        },
                        {
                            titulo: "⚛️ Fusão Nuclear Controlada",
                            descricao: "Realize fusão nuclear em reator tokamak para energia limpa.",
                            resultado: "Fusão sustentada por 17 minutos! Temperatura de 100 milhões °C alcançada. Energia infinita desbloqueada!",
                            pontos: 200
                        },
                        {
                            titulo: "🌌 Simulação de Buraco Negro",
                            descricao: "Crie um micro buraco negro em acelerador de partículas.",
                            resultado: "Buraco negro microscópico criado! Hawking radiation detectada. Física quântica confirmada!",
                            pontos: 180
                        }
                    ]
                };
            }

            carregarExperimentos() {
                const container = document.getElementById('lab-experiments-list');
                container.innerHTML = '';
                
                this.experimentosBase[this.dificuldade].forEach((exp, index) => {
                    const expDiv = document.createElement('div');
                    expDiv.className = 'experiment-card';
                    
                    expDiv.innerHTML = `
                        <h3 class="experiment-title">${exp.titulo}</h3>
                        <p class="experiment-description">${exp.descricao}</p>
                        <button onclick="realizarExperimento(${index})" class="experiment-btn">
                            🧪 Realizar Experimento (+${exp.pontos} pts)
                        </button>
                        <div id="result-${index}" class="experiment-result"></div>
                    `;
                    
                    container.appendChild(expDiv);
                });
            }

            realizarExperimento(index) {
                const exp = this.experimentosBase[this.dificuldade][index];
                const resultDiv = document.getElementById(`result-${index}`);
                
                this.experimentos++;
                this.sucessos++;
                this.pontos += exp.pontos;
                
                resultDiv.textContent = exp.resultado;
                resultDiv.style.display = 'block';
                
                // Verificar se completou todos os experimentos do nível
                if (this.sucessos >= this.experimentosBase[this.dificuldade].length) {
                    const bonusCompleto = this.dificuldade === 'easy' ? 50 : this.dificuldade === 'medium' ? 100 : this.dificuldade === 'hard' ? 200 : this.dificuldade === 'impossible' ? 500 : 1000;
                    this.pontos += bonusCompleto;
                    sistemaPontuacao.criarNotificacao(`🏆 LABORATÓRIO COMPLETO! +${bonusCompleto} bônus!`, 'success');
                }
                
                sistemaPontuacao.criarNotificacao(`🧪 Experimento realizado! +${exp.pontos} pontos!`, 'success');
                sistemaPontuacao.adicionarPontos(exp.pontos, 'Laboratório');
                
                // Salvar progresso
                const labCount = parseInt(localStorage.getItem('lab-count') || '0') + 1;
                localStorage.setItem('lab-count', labCount.toString());
                document.getElementById('lab-count').textContent = labCount;
                
                this.atualizarDisplay();
            }

            selecionarDificuldade(dificuldade) {
                this.dificuldade = dificuldade;
                document.getElementById('lab-current-level').textContent = 
                    dificuldade === 'easy' ? 'Básico' : 
                    dificuldade === 'medium' ? 'Intermediário' : 
                    dificuldade === 'hard' ? 'Avançado' : 
                    dificuldade === 'impossible' ? 'Especialista' : 'MORTAL';
                document.getElementById('lab-level').textContent = 
                    dificuldade === 'easy' ? 'Básico' : 
                    dificuldade === 'medium' ? 'Intermediário' : 
                    dificuldade === 'hard' ? 'Avançado' : 
                    dificuldade === 'impossible' ? 'Especialista' : 'MORTAL';
                this.carregarExperimentos();
            }

            atualizarDisplay() {
                document.getElementById('lab-points').textContent = this.pontos;
                document.getElementById('lab-experiments').textContent = this.experimentos;
                document.getElementById('lab-success').textContent = this.sucessos;
            }
        }

        // Quiz de História
        class QuizHistoria {
            constructor() {
                this.dificuldade = 'easy';
                this.pontos = 0;
                this.acertos = 0;
                this.perguntaAtual = 0;
                this.totalPerguntas = 10;
                this.perguntas = [];
                this.ativo = false;
                this.inicializarPerguntas();
            }

            inicializarPerguntas() {
                this.perguntasBase = {
                    easy: [
                        {
                            pergunta: "Em que ano o Brasil foi descoberto?",
                            opcoes: ["1500", "1498", "1502", "1499"],
                            correta: 0
                        },
                        {
                            pergunta: "Quem foi o primeiro presidente do Brasil?",
                            opcoes: ["Getúlio Vargas", "Deodoro da Fonseca", "Juscelino Kubitschek", "Prudente de Morais"],
                            correta: 1
                        },
                        {
                            pergunta: "Quando foi proclamada a Independência do Brasil?",
                            opcoes: ["7 de setembro de 1822", "15 de novembro de 1889", "21 de abril de 1792", "12 de outubro de 1492"],
                            correta: 0
                        },
                        {
                            pergunta: "Qual foi a primeira capital do Brasil?",
                            opcoes: ["Rio de Janeiro", "São Paulo", "Salvador", "Brasília"],
                            correta: 2
                        },
                        {
                            pergunta: "Em que século ocorreu a Revolução Industrial?",
                            opcoes: ["Século XVII", "Século XVIII", "Século XIX", "Século XX"],
                            correta: 1
                        }
                    ],
                    medium: [
                        {
                            pergunta: "Qual foi o período da Era Vargas?",
                            opcoes: ["1930-1945", "1920-1935", "1940-1955", "1935-1950"],
                            correta: 0
                        },
                        {
                            pergunta: "Quando começou a Segunda Guerra Mundial?",
                            opcoes: ["1938", "1939", "1940", "1941"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual foi o nome da operação de desembarque na Normandia?",
                            opcoes: ["Operação Overlord", "Operação Barbarossa", "Operação Market Garden", "Operação Torch"],
                            correta: 0
                        },
                        {
                            pergunta: "Em que ano caiu o Muro de Berlim?",
                            opcoes: ["1987", "1988", "1989", "1990"],
                            correta: 2
                        },
                        {
                            pergunta: "Quem foi o líder da Revolução Russa de 1917?",
                            opcoes: ["Stalin", "Trotsky", "Lenin", "Kerensky"],
                            correta: 2
                        }
                    ],
                    hard: [
                        {
                            pergunta: "Qual tratado encerrou a Primeira Guerra Mundial?",
                            opcoes: ["Tratado de Versalhes", "Tratado de Tordesilhas", "Tratado de Utrecht", "Tratado de Westfália"],
                            correta: 0
                        },
                        {
                            pergunta: "Em que ano ocorreu a Conjuração Mineira?",
                            opcoes: ["1789", "1792", "1798", "1801"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual imperador romano legalizou o cristianismo?",
                            opcoes: ["Nero", "Constantino", "Augusto", "Trajano"],
                            correta: 1
                        },
                        {
                            pergunta: "Quando foi assinada a Lei Áurea?",
                            opcoes: ["13 de maio de 1888", "15 de novembro de 1889", "7 de setembro de 1822", "21 de abril de 1792"],
                            correta: 0
                        },
                        {
                            pergunta: "Qual foi a duração da Guerra dos Cem Anos?",
                            opcoes: ["100 anos", "116 anos", "98 anos", "120 anos"],
                            correta: 1
                        }
                    ],
                    impossible: [
                        {
                            pergunta: "Em que ano foi fundada a cidade de Ouro Preto?",
                            opcoes: ["1698", "1711", "1720", "1729"],
                            correta: 0
                        },
                        {
                            pergunta: "Qual foi o nome original de Istambul?",
                            opcoes: ["Bizâncio", "Constantinopla", "Ambas estão corretas", "Nenhuma das anteriores"],
                            correta: 2
                        },
                        {
                            pergunta: "Quem foi o último imperador romano do Ocidente?",
                            opcoes: ["Rômulo Augusto", "Odoacro", "Teodósio", "Honório"],
                            correta: 0
                        },
                        {
                            pergunta: "Em que batalha Napoleão foi definitivamente derrotado?",
                            opcoes: ["Waterloo", "Leipzig", "Austerlitz", "Borodino"],
                            correta: 0
                        },
                        {
                            pergunta: "Qual dinastia chinesa construiu a Cidade Proibida?",
                            opcoes: ["Tang", "Song", "Ming", "Qing"],
                            correta: 2
                        }
                    ],
                    deadly: [
                        {
                            pergunta: "Em que data exata foi assinado o Tratado de Methuen?",
                            opcoes: ["27 de dezembro de 1703", "16 de maio de 1703", "3 de setembro de 1703", "12 de janeiro de 1704"],
                            correta: 0
                        },
                        {
                            pergunta: "Qual foi o nome do plano econômico que precedeu o Plano Real?",
                            opcoes: ["Plano Collor II", "Plano Bresser", "Plano Verão", "Plano Cruzado"],
                            correta: 0
                        },
                        {
                            pergunta: "Quem foi o arquiteto da Catedral de Brasília?",
                            opcoes: ["Oscar Niemeyer", "Lúcio Costa", "Vilanova Artigas", "Paulo Mendes da Rocha"],
                            correta: 0
                        },
                        {
                            pergunta: "Em que ano foi criada a Organização das Nações Unidas?",
                            opcoes: ["1944", "1945", "1946", "1947"],
                            correta: 1
                        },
                        {
                            pergunta: "Qual foi o primeiro país a conceder direito de voto às mulheres?",
                            opcoes: ["Nova Zelândia", "Austrália", "Finlândia", "Noruega"],
                            correta: 0
                        }
                    ]
                };
            }

            iniciar() {
                this.pontos = 0;
                this.acertos = 0;
                this.perguntaAtual = 0;
                this.ativo = true;
                
                this.perguntas = [...this.perguntasBase[this.dificuldade]].sort(() => Math.random() - 0.5);
                
                document.getElementById('history-start-btn').style.display = 'none';
                document.getElementById('history-options').style.display = 'grid';
                
                this.mostrarPergunta();
                this.atualizarDisplay();
            }

            mostrarPergunta() {
                if (this.perguntaAtual >= this.perguntas.length) {
                    this.finalizarJogo();
                    return;
                }

                const pergunta = this.perguntas[this.perguntaAtual];
                document.getElementById('history-question').textContent = pergunta.pergunta;
                
                const optionsContainer = document.getElementById('history-options');
                optionsContainer.innerHTML = '';
                
                pergunta.opcoes.forEach((opcao, index) => {
                    const button = document.createElement('button');
                    button.className = 'option-btn';
                    button.textContent = opcao;
                    button.onclick = () => this.verificarResposta(index);
                    optionsContainer.appendChild(button);
                });
            }

            verificarResposta(opcaoSelecionada) {
                if (!this.ativo) return;
                
                const pergunta = this.perguntas[this.perguntaAtual];
                const buttons = document.querySelectorAll('#history-options .option-btn');
                
                buttons.forEach((btn, index) => {
                    if (index === pergunta.correta) {
                        btn.classList.add('correct');
                    } else if (index === opcaoSelecionada && index !== pergunta.correta) {
                        btn.classList.add('incorrect');
                    }
                    btn.disabled = true;
                });
                
                if (opcaoSelecionada === pergunta.correta) {
                    this.acertos++;
                    const pontosGanhos = this.dificuldade === 'easy' ? 10 : this.dificuldade === 'medium' ? 20 : this.dificuldade === 'hard' ? 30 : this.dificuldade === 'impossible' ? 50 : 100;
                    this.pontos += pontosGanhos;
                    sistemaPontuacao.criarNotificacao('✅ Correto!', 'success');
                } else {
                    sistemaPontuacao.criarNotificacao('❌ Incorreto!', 'error');
                }
                
                setTimeout(() => {
                    this.perguntaAtual++;
                    this.mostrarPergunta();
                    this.atualizarDisplay();
                }, 2000);
            }

            finalizarJogo() {
                this.ativo = false;
                const precisao = Math.round((this.acertos / this.perguntas.length) * 100);
                
                document.<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'97c6e42c613cda2e',t:'MTc1NzQyMzA2NS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script>
