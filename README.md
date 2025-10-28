<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EduPlay - Jogos Educativos</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        body { font-family: 'Poppins', sans-serif; }
        
        .game-card {
            transition: all 0.3s ease;
        }
        
        .game-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
        }
        
        .login-form {
            backdrop-filter: blur(10px);
            background: rgba(255, 255, 255, 0.95);
        }
        
        .demo-badge {
            position: fixed;
            top: 10px;
            right: 10px;
            background: #ff6b6b;
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            z-index: 1000;
        }
        
        .error-message {
            color: #e53e3e;
            font-size: 14px;
            margin-top: 5px;
            display: none;
        }
        
        .success-message {
            color: #38a169;
            font-size: 14px;
            margin-top: 5px;
            display: none;
        }
        
        .loading-spinner {
            display: none;
            width: 20px;
            height: 20px;
            border: 2px solid #f3f3f3;
            border-top: 2px solid #805ad5;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 0 auto;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .game-screen {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: white;
            z-index: 1000;
            overflow-y: auto;
        }

        .question {
            background: white;
            border-radius: 12px;
            padding: 20px;
            margin: 10px 0;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }

        .option {
            background: #f7fafc;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            padding: 12px;
            margin: 8px 0;
            cursor: pointer;
            transition: all 0.3s;
        }

        .option:hover {
            background: #edf2f7;
            border-color: #cbd5e0;
        }

        .option.correct {
            background: #c6f6d5;
            border-color: #48bb78;
        }

        .option.incorrect {
            background: #fed7d7;
            border-color: #f56565;
        }

        .crossword-grid {
            display: grid;
            gap: 2px;
            margin: 20px auto;
            justify-content: center;
        }

        .crossword-cell {
            width: 40px;
            height: 40px;
            border: 2px solid #4a5568;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            background: white;
        }

        .crossword-cell input {
            width: 100%;
            height: 100%;
            border: none;
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            text-transform: uppercase;
        }

        .crossword-cell.black {
            background: #2d3748;
        }
    </style>
</head>
<body class="bg-gradient-to-br from-purple-400 via-pink-500 to-red-500 min-h-screen">
    <div class="demo-badge">SISTEMA DE LOGIN REAL</div>
    
    <!-- Tela de Login -->
    <div id="loginScreen" class="min-h-screen flex items-center justify-center p-4">
        <div class="login-form rounded-2xl p-8 w-full max-w-md shadow-2xl">
            <div class="text-center mb-8">
                <h1 class="text-4xl font-bold text-purple-600 mb-2">🎮 EduPlay</h1>
                <p class="text-gray-600">Jogos educativos divertidos para aprender!</p>
            </div>
            
            <form id="loginForm" class="space-y-6">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Nome de usuário</label>
                    <input type="text" id="username" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="Digite seu nome de usuário" required>
                    <div id="usernameError" class="error-message"></div>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Senha</label>
                    <input type="password" id="password" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="Digite sua senha" required>
                    <div id="passwordError" class="error-message"></div>
                </div>
                
                <div class="flex items-center justify-between">
                    <div class="flex items-center">
                        <input type="checkbox" id="rememberMe" class="h-4 w-4 text-purple-600 focus:ring-purple-500 border-gray-300 rounded">
                        <label for="rememberMe" class="ml-2 block text-sm text-gray-700">Lembrar-me</label>
                    </div>
                    <button type="button" id="forgotPassword" class="text-sm text-purple-600 hover:text-purple-800">Esqueceu a senha?</button>
                </div>
                
                <button type="submit" id="loginButton" class="w-full bg-purple-600 hover:bg-purple-700 text-white font-semibold py-3 px-4 rounded-lg transition duration-300 transform hover:scale-105 flex justify-center items-center">
                    <span id="loginText">Entrar</span>
                    <div id="loginSpinner" class="loading-spinner ml-2"></div>
                </button>
            </form>
            
            <div class="mt-6 text-center">
                <p class="text-sm text-gray-600">Não tem conta? 
                    <button id="registerBtn" class="text-purple-600 hover:text-purple-800 font-medium">Cadastre-se</button>
                </p>
            </div>
            
            <div class="mt-4 p-3 bg-blue-50 rounded-lg">
                <p class="text-xs text-blue-600 text-center">
                    💡 <strong>Conta do proprietário:</strong><br>
                    • vitor202 / admin (👑 Dono Verificado)
                </p>
            </div>
        </div>
    </div>
    
    <!-- Tela de Registro -->
    <div id="registerScreen" class="hidden min-h-screen flex items-center justify-center p-4">
        <!-- ... (código anterior igual) ... -->
    </div>
    
    <!-- Tela Principal de Jogos -->
    <div id="gameScreen" class="hidden min-h-screen">
        <!-- ... (código anterior igual) ... -->
    </div>
    
    <!-- Modal de Seleção de Jogo -->
    <div id="gameModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
        <!-- ... (código anterior igual) ... -->
    </div>

    <!-- Tela do Quiz de Matemática -->
    <div id="mathGame" class="game-screen">
        <div class="min-h-screen bg-gradient-to-br from-blue-400 to-purple-600 p-4">
            <div class="max-w-4xl mx-auto">
                <div class="bg-white rounded-2xl p-6 shadow-lg">
                    <div class="flex justify-between items-center mb-6">
                        <h1 class="text-3xl font-bold text-gray-800">🔢 Quiz de Matemática</h1>
                        <button onclick="closeGame('mathGame')" class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg">
                            Voltar
                        </button>
                    </div>
                    
                    <div id="mathProgress" class="mb-4">
                        <div class="flex justify-between text-sm text-gray-600 mb-2">
                            <span>Pergunta <span id="mathCurrent">1</span>/5</span>
                            <span>Pontuação: <span id="mathScore">0</span></span>
                        </div>
                        <div class="w-full bg-gray-200 rounded-full h-2">
                            <div id="mathProgressBar" class="bg-green-500 h-2 rounded-full" style="width: 0%"></div>
                        </div>
                    </div>
                    
                    <div id="mathQuestions" class="space-y-4">
                        <!-- As perguntas serão inseridas aqui via JavaScript -->
                    </div>
                    
                    <div id="mathResults" class="hidden text-center py-8">
                        <div class="text-6xl mb-4">🎉</div>
                        <h2 class="text-2xl font-bold text-gray-800 mb-2">Quiz Concluído!</h2>
                        <p class="text-gray-600 mb-4">Sua pontuação final: <span id="mathFinalScore" class="font-bold text-2xl">0</span>/5</p>
                        <button onclick="restartMathGame()" class="bg-green-500 hover:bg-green-600 text-white px-6 py-3 rounded-lg mr-4">
                            Jogar Novamente
                        </button>
                        <button onclick="closeGame('mathGame')" class="bg-gray-500 hover:bg-gray-600 text-white px-6 py-3 rounded-lg">
                            Voltar ao Menu
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Tela de Palavras Cruzadas -->
    <div id="wordsGame" class="game-screen">
        <div class="min-h-screen bg-gradient-to-br from-green-400 to-blue-500 p-4">
            <div class="max-w-4xl mx-auto">
                <div class="bg-white rounded-2xl p-6 shadow-lg">
                    <div class="flex justify-between items-center mb-6">
                        <h1 class="text-3xl font-bold text-gray-800">📝 Palavras Cruzadas</h1>
                        <button onclick="closeGame('wordsGame')" class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg">
                            Voltar
                        </button>
                    </div>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                        <div>
                            <h3 class="text-xl font-bold mb-4">Dicas Horizontais:</h3>
                            <ul class="space-y-2 text-gray-700">
                                <li>1. Capital do Brasil</li>
                                <li>3. Maior planeta do sistema solar</li>
                                <li>5. Animal que mia</li>
                            </ul>
                            
                            <h3 class="text-xl font-bold mt-6 mb-4">Dicas Verticais:</h3>
                            <ul class="space-y-2 text-gray-700">
                                <li>2. Cor do céu</li>
                                <li>4. Fruta vermelha</li>
                            </ul>
                        </div>
                        
                        <div class="flex justify-center">
                            <div id="crosswordGrid" class="crossword-grid grid-cols-5">
                                <!-- Grade será gerada via JavaScript -->
                            </div>
                        </div>
                    </div>
                    
                    <div class="mt-6 text-center">
                        <button onclick="checkCrossword()" class="bg-green-500 hover:bg-green-600 text-white px-6 py-3 rounded-lg mr-4">
                            Verificar Respostas
                        </button>
                        <button onclick="resetCrossword()" class="bg-yellow-500 hover:bg-yellow-600 text-white px-6 py-3 rounded-lg">
                            Reiniciar
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Tela do Quiz de Ciências -->
    <div id="scienceGame" class="game-screen">
        <div class="min-h-screen bg-gradient-to-br from-orange-400 to-red-500 p-4">
            <div class="max-w-4xl mx-auto">
                <div class="bg-white rounded-2xl p-6 shadow-lg">
                    <div class="flex justify-between items-center mb-6">
                        <h1 class="text-3xl font-bold text-gray-800">🔬 Quiz de Ciências</h1>
                        <button onclick="closeGame('scienceGame')" class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg">
                            Voltar
                        </button>
                    </div>
                    
                    <div id="scienceQuestions">
                        <!-- Perguntas de ciências serão inseridas aqui -->
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Tela de Geografia -->
    <div id="geographyGame" class="game-screen">
        <div class="min-h-screen bg-gradient-to-br from-teal-400 to-blue-500 p-4">
            <div class="max-w-4xl mx-auto">
                <div class="bg-white rounded-2xl p-6 shadow-lg">
                    <div class="flex justify-between items-center mb-6">
                        <h1 class="text-3xl font-bold text-gray-800">🌍 Geografia Mundial</h1>
                        <button onclick="closeGame('geographyGame')" class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg">
                            Voltar
                        </button>
                    </div>
                    
                    <div id="geographyContent">
                        <!-- Conteúdo de geografia será inserido aqui -->
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Tela de História -->
    <div id="historyGame" class="game-screen">
        <div class="min-h-screen bg-gradient-to-br from-amber-400 to-orange-500 p-4">
            <div class="max-w-4xl mx-auto">
                <div class="bg-white rounded-2xl p-6 shadow-lg">
                    <div class="flex justify-between items-center mb-6">
                        <h1 class="text-3xl font-bold text-gray-800">📚 História do Brasil</h1>
                        <button onclick="closeGame('historyGame')" class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg">
                            Voltar
                        </button>
                    </div>
                    
                    <div id="historyContent">
                        <!-- Conteúdo de história será inserido aqui -->
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Tela de Inglês -->
    <div id="englishGame" class="game-screen">
        <div class="min-h-screen bg-gradient-to-br from-indigo-400 to-purple-500 p-4">
            <div class="max-w-4xl mx-auto">
                <div class="bg-white rounded-2xl p-6 shadow-lg">
                    <div class="flex justify-between items-center mb-6">
                        <h1 class="text-3xl font-bold text-gray-800">🇺🇸 Inglês Básico</h1>
                        <button onclick="closeGame('englishGame')" class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg">
                            Voltar
                        </button>
                    </div>
                    
                    <div id="englishContent">
                        <!-- Conteúdo de inglês será inserido aqui -->
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Sistema de Autenticação (mantido igual)
        class AuthSystem {
            constructor() {
                this.users = this.loadUsers();
                this.currentUser = null;
                this.currentSession = null;
            }
            
            loadUsers() {
                const storedUsers = localStorage.getItem('eduplay_users');
                if (storedUsers) {
                    return JSON.parse(storedUsers);
                } else {
                    const defaultUsers = {
                        'vitor202': {
                            id: this.generateId(),
                            username: 'vitor202',
                            password: this.hashPassword('admin'),
                            fullName: 'Vitor',
                            email: 'vitor@eduplay.com',
                            role: 'owner',
                            verified: true,
                            createdAt: new Date().toISOString(),
                            lastLogin: null
                        }
                    };
                    this.saveUsers(defaultUsers);
                    return defaultUsers;
                }
            }
            
            saveUsers(users) {
                localStorage.setItem('eduplay_users', JSON.stringify(users));
            }
            
            generateId() {
                return 'user_' + Math.random().toString(36).substr(2, 9) + Date.now().toString(36);
            }
            
            hashPassword(password) {
                let hash = 0;
                for (let i = 0; i < password.length; i++) {
                    const char = password.charCodeAt(i);
                    hash = ((hash << 5) - hash) + char;
                    hash = hash & hash;
                }
                return hash.toString();
            }
            
            verifyPassword(password, hashedPassword) {
                return this.hashPassword(password) === hashedPassword;
            }
            
            register(userData) {
                return new Promise((resolve, reject) => {
                    if (this.users[userData.username]) {
                        reject('Nome de usuário já existe');
                        return;
                    }
                    
                    if (userData.password !== userData.confirmPassword) {
                        reject('As senhas não coincidem');
                        return;
                    }
                    
                    if (userData.password.length < 6) {
                        reject('A senha deve ter pelo menos 6 caracteres');
                        return;
                    }
                    
                    const newUser = {
                        id: this.generateId(),
                        username: userData.username,
                        password: this.hashPassword(userData.password),
                        fullName: userData.fullName,
                        email: userData.email,
                        role: 'user',
                        verified: false,
                        createdAt: new Date().toISOString(),
                        lastLogin: null
                    };
                    
                    this.users[userData.username] = newUser;
                    this.saveUsers(this.users);
                    
                    resolve(newUser);
                });
            }
            
            login(username, password, rememberMe = false) {
                return new Promise((resolve, reject) => {
                    setTimeout(() => {
                        const user = this.users[username];
                        
                        if (!user) {
                            reject('Usuário não encontrado');
                            return;
                        }
                        
                        if (!this.verifyPassword(password, user.password)) {
                            reject('Senha incorreta');
                            return;
                        }
                        
                        user.lastLogin = new Date().toISOString();
                        this.saveUsers(this.users);
                        
                        this.currentUser = user;
                        this.currentSession = {
                            token: this.generateToken(),
                            expiresAt: new Date(Date.now() + (rememberMe ? 30 * 24 * 60 * 60 * 1000 : 24 * 60 * 60 * 1000))
                        };
                        
                        if (rememberMe) {
                            localStorage.setItem('eduplay_session', JSON.stringify({
                                username: user.username,
                                token: this.currentSession.token,
                                expiresAt: this.currentSession.expiresAt.toISOString()
                            }));
                        }
                        
                        resolve(user);
                    }, 1000);
                });
            }
            
            logout() {
                this.currentUser = null;
                this.currentSession = null;
                localStorage.removeItem('eduplay_session');
            }
            
            checkActiveSession() {
                const storedSession = localStorage.getItem('eduplay_session');
                if (storedSession) {
                    const session = JSON.parse(storedSession);
                    const expiresAt = new Date(session.expiresAt);
                    
                    if (expiresAt > new Date()) {
                        const user = this.users[session.username];
                        if (user) {
                            this.currentUser = user;
                            this.currentSession = {
                                token: session.token,
                                expiresAt: expiresAt
                            };
                            return user;
                        }
                    } else {
                        localStorage.removeItem('eduplay_session');
                    }
                }
                return null;
            }
            
            generateToken() {
                return 'token_' + Math.random().toString(36).substr(2) + Date.now().toString(36);
            }
        }

        // Inicializar sistema de autenticação
        const authSystem = new AuthSystem();
        
        // Dados dos Jogos
        const games = {
            math: {
                icon: '🔢',
                title: 'Quiz de Matemática',
                description: 'Resolva problemas matemáticos e teste suas habilidades!'
            },
            words: {
                icon: '📝',
                title: 'Palavras Cruzadas',
                description: 'Complete as palavras cruzadas e expanda seu vocabulário!'
            },
            science: {
                icon: '🔬',
                title: 'Quiz de Ciências',
                description: 'Explore o mundo da ciência com perguntas desafiadoras!'
            },
            geography: {
                icon: '🌍',
                title: 'Geografia Mundial',
                description: 'Teste seus conhecimentos sobre países e capitais!'
            },
            history: {
                icon: '📚',
                title: 'História do Brasil',
                description: 'Aprenda sobre os eventos históricos do Brasil!'
            },
            english: {
                icon: '🇺🇸',
                title: 'Inglês Básico',
                description: 'Pratique vocabulário e gramática em inglês!'
            }
        };

        // Perguntas para os quizzes
        const mathQuestions = [
            {
                question: "Quanto é 15 + 27?",
                options: ["40", "42", "45", "52"],
                correct: 1
            },
            {
                question: "Qual é o resultado de 8 × 7?",
                options: ["54", "56", "58", "60"],
                correct: 1
            },
            {
                question: "Se um quadrado tem lado 5cm, qual é sua área?",
                options: ["20cm²", "25cm²", "30cm²", "35cm²"],
                correct: 1
            },
            {
                question: "Quanto é 144 ÷ 12?",
                options: ["10", "11", "12", "13"],
                correct: 2
            },
            {
                question: "Qual é o dobro de 3/4?",
                options: ["3/8", "1/2", "3/2", "6/4"],
                correct: 2
            }
        ];

        const scienceQuestions = [
            {
                question: "Qual é o planeta mais próximo do Sol?",
                options: ["Vênus", "Mercúrio", "Terra", "Marte"],
                correct: 1
            },
            {
                question: "Quantos ossos tem o corpo humano adulto?",
                options: ["196", "206", "216", "226"],
                correct: 1
            },
            {
                question: "Qual é o elemento químico mais abundante na Terra?",
                options: ["Oxigênio", "Silício", "Ferro", "Alumínio"],
                correct: 0
            }
        ];

        // Estado dos jogos
        let currentMathQuestion = 0;
        let mathScore = 0;

        // Inicializar a aplicação
        document.addEventListener('DOMContentLoaded', function() {
            const activeUser = authSystem.checkActiveSession();
            if (activeUser) {
                showGameScreen(activeUser);
            }
            
            document.getElementById('loginForm').addEventListener('submit', handleLogin);
            document.getElementById('registerForm').addEventListener('submit', handleRegister);
            document.getElementById('registerBtn').addEventListener('click', showRegisterScreen);
            document.getElementById('backToLogin').addEventListener('click', showLoginScreen);
            document.getElementById('logoutBtn').addEventListener('click', handleLogout);
            document.getElementById('forgotPassword').addEventListener('click', handleForgotPassword);

            // Inicializar palavras cruzadas
            initializeCrossword();
        });

        // Funções de Autenticação (mantidas iguais)
        async function handleLogin(e) {
            e.preventDefault();
            
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const rememberMe = document.getElementById('rememberMe').checked;
            
            clearErrors();
            
            if (!username || !password) {
                showError('usernameError', 'Por favor, preencha todos os campos');
                return;
            }
            
            showLoading('login');
            
            try {
                const user = await authSystem.login(username, password, rememberMe);
                showGameScreen(user);
            } catch (error) {
                showError('passwordError', error);
            } finally {
                hideLoading('login');
            }
        }
        
        async function handleRegister(e) {
            e.preventDefault();
            
            const fullName = document.getElementById('fullName').value;
            const username = document.getElementById('newUsername').value;
            const email = document.getElementById('email').value;
            const password = document.getElementById('newPassword').value;
            const confirmPassword = document.getElementById('confirmPassword').value;
            const terms = document.getElementById('terms').checked;
            
            clearErrors();
            
            if (!fullName || !username || !email || !password || !confirmPassword) {
                showError('newUsernameError', 'Por favor, preencha todos os campos');
                return;
            }
            
            if (!terms) {
                showError('termsError', 'Você deve aceitar os termos de uso');
                return;
            }
            
            showLoading('register');
            
            try {
                const userData = {
                    fullName,
                    username,
                    email,
                    password,
                    confirmPassword
                };
                
                const newUser = await authSystem.register(userData);
                showSuccess('Conta criada com sucesso! Faça login para continuar.');
                showLoginScreen();
            } catch (error) {
                showError('newUsernameError', error);
            } finally {
                hideLoading('register');
            }
        }
        
        function handleLogout() {
            authSystem.logout();
            showLoginScreen();
        }
        
        function handleForgotPassword() {
            alert('Funcionalidade de recuperação de senha seria implementada aqui!');
        }
        
        function showGameScreen(user) {
            let welcomeText = `Olá, ${user.username}!`;
            if (user.verified) {
                if (user.role === 'owner') {
                    welcomeText += ' ✅👑 (Dono Verificado)';
                } else if (user.role === 'admin') {
                    welcomeText += ' ✅🛡️ (Admin Verificado)';
                } else {
                    welcomeText += ' ✅';
                }
            }
            
            document.getElementById('welcomeUser').textContent = welcomeText;
            document.getElementById('loginScreen').classList.add('hidden');
            document.getElementById('registerScreen').classList.add('hidden');
            document.getElementById('gameScreen').classList.remove('hidden');
            
            if (user.role === 'admin' || user.role === 'owner') {
                document.getElementById('adminPanel').classList.remove('hidden');
            }
            
            if (user.username === 'vitor202') {
                setTimeout(() => {
                    alert('🎉 Bem-vindo de volta, Vitor!\n\n👑 Você é o dono verificado do site!\nAcesso total ao painel administrativo liberado.');
                }, 500);
            } else if (user.role === 'admin') {
                setTimeout(() => {
                    alert('🛡️ Bem-vindo, Administrador!\n\nVocê tem acesso ao painel administrativo.');
                }, 500);
            }
        }
        
        function showLoginScreen() {
            document.getElementById('loginScreen').classList.remove('hidden');
            document.getElementById('registerScreen').classList.add('hidden');
            document.getElementById('gameScreen').classList.add('hidden');
            clearForm('loginForm');
            clearErrors();
        }
        
        function showRegisterScreen() {
            document.getElementById('loginScreen').classList.add('hidden');
            document.getElementById('registerScreen').classList.remove('hidden');
            document.getElementById('gameScreen').classList.add('hidden');
            clearForm('registerForm');
            clearErrors();
        }
        
        function clearForm(formId) {
            document.getElementById(formId).reset();
        }
        
        function clearErrors() {
            const errorElements = document.querySelectorAll('.error-message');
            errorElements.forEach(el => {
                el.style.display = 'none';
                el.textContent = '';
            });
        }
        
        function showError(elementId, message) {
            const element = document.getElementById(elementId);
            element.textContent = message;
            element.style.display = 'block';
        }
        
        function showSuccess(message) {
            alert(message);
        }
        
        function showLoading(type) {
            document.getElementById(`${type}Text`).style.display = 'none';
            document.getElementById(`${type}Spinner`).style.display = 'block';
            document.getElementById(`${type}Button`).disabled = true;
        }
        
        function hideLoading(type) {
            document.getElementById(`${type}Text`).style.display = 'block';
            document.getElementById(`${type}Spinner`).style.display = 'none';
            document.getElementById(`${type}Button`).disabled = false;
        }

        // Funções dos Jogos
        function startGame(gameType) {
            closeGameModal();
            
            switch(gameType) {
                case 'math':
                    startMathGame();
                    break;
                case 'words':
                    startWordsGame();
                    break;
                case 'science':
                    startScienceGame();
                    break;
                case 'geography':
                    startGeographyGame();
                    break;
                case 'history':
                    startHistoryGame();
                    break;
                case 'english':
                    startEnglishGame();
                    break;
            }
        }

        function playGame() {
            startGame(currentGame);
        }

        function closeGameModal() {
            document.getElementById('gameModal').classList.add('hidden');
        }

        // Quiz de Matemática
        function startMathGame() {
            document.getElementById('mathGame').style.display = 'block';
            currentMathQuestion = 0;
            mathScore = 0;
            updateMathProgress();
            showMathQuestion();
        }

        function showMathQuestion() {
            const questionsContainer = document.getElementById('mathQuestions');
            const question = mathQuestions[currentMathQuestion];
            
            questionsContainer.innerHTML = `
                <div class="question">
                    <h3 class="text-xl font-bold mb-4">${question.question}</h3>
                    <div class="space-y-3">
                        ${question.options.map((option, index) => `
                            <div class="option" onclick="selectMathAnswer(${index})">
                                ${option}
                            </div>
                        `).join('')}
                    </div>
                </div>
            `;
        }

        function selectMathAnswer(selectedIndex) {
            const question = mathQuestions[currentMathQuestion];
            const options = document.querySelectorAll('#mathQuestions .option');
            
            options.forEach((option, index) => {
                if (index === question.correct) {
                    option.classList.add('correct');
                } else if (index === selectedIndex && index !== question.correct) {
                    option.classList.add('incorrect');
                }
                option.style.pointerEvents = 'none';
            });
            
            if (selectedIndex === question.correct) {
                mathScore++;
            }
            
            document.getElementById('mathScore').textContent = mathScore;
            
            setTimeout(() => {
                currentMathQuestion++;
                if (currentMathQuestion < mathQuestions.length) {
                    updateMathProgress();
                    showMathQuestion();
                } else {
                    showMathResults();
                }
            }, 1500);
        }

        function updateMathProgress() {
            const progress = ((currentMathQuestion) / mathQuestions.length) * 100;
            document.getElementById('mathProgressBar').style.width = `${progress}%`;
            document.getElementById('mathCurrent').textContent = currentMathQuestion + 1;
        }

        function showMathResults() {
            document.getElementById('mathQuestions').classList.add('hidden');
            document.getElementById('mathResults').classList.remove('hidden');
            document.getElementById('mathFinalScore').textContent = mathScore;
        }

        function restartMathGame() {
            document.getElementById('mathQuestions').classList.remove('hidden');
            document.getElementById('mathResults').classList.add('hidden');
            startMathGame();
        }

        // Palavras Cruzadas
        function initializeCrossword() {
            const grid = document.getElementById('crosswordGrid');
            const crossword = [
                ['B', 'R', 'A', 'S', 'I', 'L', 'I', 'A'],
                ['', '', '', '', 'Z', '', '', ''],
                ['', '', '', '', 'U', '', '', ''],
                ['', '', '', '', 'R', '', '', ''],
                ['', '', '', '', 'T', '', '', ''],
                ['G', 'A', 'T', 'O', '', 'M', 'O', 'R'],
                ['', '', '', '', '', 'A', '', ''],
                ['', '', '', '', '', 'R', '', ''],
                ['', '', '', '', '', 'T', '', ''],
                ['', '', '', '', '', 'E', '', '']
            ];
            
            grid.innerHTML = '';
            crossword.forEach((row, rowIndex) => {
                row.forEach((cell, colIndex) => {
                    const cellDiv = document.createElement('div');
                    cellDiv.className = 'crossword-cell';
                    
                    if (cell === '') {
                        cellDiv.classList.add('black');
                    } else {
                        const input = document.createElement('input');
                        input.type = 'text';
                        input.maxLength = 1;
                        input.dataset.row = rowIndex;
                        input.dataset.col = colIndex;
                        cellDiv.appendChild(input);
                    }
                    
                    grid.appendChild(cellDiv);
                });
            });
        }

        function startWordsGame() {
            document.getElementById('wordsGame').style.display = 'block';
        }

        function checkCrossword() {
            alert('Em desenvolvimento! Esta função verificará todas as respostas.');
        }

        function resetCrossword() {
            const inputs = document.querySelectorAll('#crosswordGrid input');
            inputs.forEach(input => {
                input.value = '';
            });
        }

        // Quiz de Ciências
        function startScienceGame() {
            document.getElementById('scienceGame').style.display = 'block';
            const container = document.getElementById('scienceQuestions');
            
            container.innerHTML = `
                <div class="text-center py-8">
                    <div class="text-6xl mb-4">🔬</div>
                    <h2 class="text-2xl font-bold mb-4">Quiz de Ciências</h2>
                    <p class="text-gray-600 mb-6">Teste seus conhecimentos científicos!</p>
                    <div class="space-y-4">
                        ${scienceQuestions.map((q, index) => `
                            <div class="question">
                                <h3 class="text-lg font-bold mb-3">${q.question}</h3>
                                <div class="grid grid-cols-2 gap-2">
                                    ${q.options.map((opt, optIndex) => `
                                        <button class="bg-blue-500 hover:bg-blue-600 text-white p-3 rounded" 
                                                onclick="alert('${optIndex === q.correct ? '✅ Correto!' : '❌ Incorreto!'}')">
                                            ${opt}
                                        </button>
                                    `).join('')}
                                </div>
                            </div>
                        `).join('')}
                    </div>
                </div>
            `;
        }

        // Geografia
        function startGeographyGame() {
            document.getElementById('geographyGame').style.display = 'block';
            const container = document.getElementById('geographyContent');
            
            container.innerHTML = `
                <div class="text-center">
                    <div class="text-6xl mb-4">🌍</div>
                    <h2 class="text-2xl font-bold mb-4">Geografia Mundial</h2>
                    <p class="text-gray-600 mb-6">Aprenda sobre países e capitais!</p>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
                        <div class="bg-blue-50 p-4 rounded-lg">
                            <h3 class="font-bold mb-2">Países e Capitais</h3>
                            <ul class="text-left space-y-1">
                                <li>🇧🇷 Brasil - Brasília</li>
                                <li>🇺🇸 EUA - Washington</li>
                                <li>🇫🇷 França - Paris</li>
                                <li>🇯🇵 Japão - Tóquio</li>
                            </ul>
                        </div>
                        
                        <div class="bg-green-50 p-4 rounded-lg">
                            <h3 class="font-bold mb-2">Quiz Rápido</h3>
                            <button class="bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded w-full mb-2"
                                    onclick="alert('🌎 Resposta: Paris')">
                                Qual a capital da França?
                            </button>
                            <button class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded w-full"
                                    onclick="alert('🌎 Resposta: Egito')">
                                Em qual país fica a pirâmide de Gizé?
                            </button>
                        </div>
                    </div>
                </div>
            `;
        }

        // História
        function startHistoryGame() {
            document.getElementById('historyGame').style.display = 'block';
            const container = document.getElementById('historyContent');
            
            container.innerHTML = `
                <div class="text-center">
                    <div class="text-6xl mb-4">📚</div>
                    <h2 class="text-2xl font-bold mb-4">História do Brasil</h2>
                    <p class="text-gray-600 mb-6">Conheça nossa história!</p>
                    
                    <div class="space-y-6">
                        <div class="bg-yellow-50 p-4 rounded-lg">
                            <h3 class="font-bold mb-2">Linha do Tempo</h3>
                            <ul class="text-left space-y-2">
                                <li>🏹 1500 - Descobrimento do Brasil</li>
                                <li>👑 1822 - Independência do Brasil</li>
                                <li>📜 1888 - Abolição da Escravatura</li>
                                <li>🇧🇷 1889 - Proclamação da República</li>
                            </ul>
                        </div>
                        
                        <div class="bg-red-50 p-4 rounded-lg">
                            <h3 class="font-bold mb-2">Personagens Históricos</h3>
                            <div class="grid grid-cols-2 gap-4">
                                <div class="text-center">
                                    <div class="text-4xl">👸</div>
                                    <div>Princesa Isabel</div>
                                </div>
                                <div class="text-center">
                                    <div class="text-4xl">👑</div>
                                    <div>Dom Pedro I</div>
                                </div>
                                <div class="text-center">
                                    <div class="text-4xl">⚔️</div>
                                    <div>Tiradentes</div>
                                </div>
                                <div class="text-center">
                                    <div class="text-4xl">📖</div>
                                    <div>José Bonifácio</div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            `;
        }

        // Inglês
        function startEnglishGame() {
            document.getElementById('englishGame').style.display = 'block';
            const container = document.getElementById('englishContent');
            
            container.innerHTML = `
                <div class="text-center">
                    <div class="text-6xl mb-4">🇺🇸</div>
                    <h2 class="text-2xl font-bold mb-4">Inglês Básico</h2>
                    <p class="text-gray-600 mb-6">Pratique vocabulário e gramática!</p>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div class="bg-purple-50 p-4 rounded-lg">
                            <h3 class="font-bold mb-3">Vocabulário</h3>
                            <div class="space-y-2 text-left">
                                <div>🐶 Dog - Cachorro</div>
                                <div>🐱 Cat - Gato</div>
                                <div>🏠 House - Casa</div>
                                <div>📚 Book - Livro</div>
                                <div>👋 Hello - Olá</div>
                            </div>
                        </div>
                        
                        <div class="bg-indigo-50 p-4 rounded-lg">
                            <h3 class="font-bold mb-3">Frases Úteis</h3>
                            <div class="space-y-2 text-left">
                                <div>"How are you?" - Como você está?</div>
                                <div>"What is your name?" - Qual é seu nome?</div>
                                <div>"I like..." - Eu gosto de...</div>
                                <div>"Thank you" - Obrigado</div>
                                <div>"Goodbye" - Tchau</div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="mt-6 bg-white p-4 rounded-lg border-2 border-dashed border-gray-300">
                        <h3 class="font-bold mb-3">Prática Interativa</h3>
                        <button class="bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded mr-2"
                                onclick="alert('✅ Correto! Good morning = Bom dia')">
                            Good morning = ?
                        </button>
                        <button class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded"
                                onclick="alert('✅ Correto! Water = Água')">
                            Water = ?
                        </button>
                    </div>
                </div>
            `;
        }

        function closeGame(gameId) {
            document.getElementById(gameId).style.display = 'none';
        }

        // Fechar modal clicando fora
        document.getElementById('gameModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeGameModal();
            }
        });

        // Funções do Painel Administrativo (mantidas iguais)
        function manageUsers() {
            if (authSystem.currentUser.role === 'owner' || authSystem.currentUser.role === 'admin') {
                alert('👥 Gerenciamento de Usuários\n\n• Total de usuários: ' + Object.keys(authSystem.users).length);
            } else {
                alert('❌ Acesso negado! Apenas administradores podem acessar esta função.');
            }
        }
        
        function manageGames() {
            if (authSystem.currentUser.role === 'owner' || authSystem.currentUser.role === 'admin') {
                alert('🎮 Gerenciamento de Jogos\n\n• Total de jogos: 6');
            } else {
                alert('❌ Acesso negado! Apenas administradores podem acessar esta função.');
            }
        }
        
        function viewReports() {
            if (authSystem.currentUser.role === 'owner' || authSystem.currentUser.role === 'admin') {
                alert('📊 Relatórios do Sistema\n\n• Uptime: 99.2%');
            } else {
                alert('❌ Acesso negado! Apenas administradores podem acessar esta função.');
            }
        }

        // Funções Disponíveis para Todos os Usuários (mantidas iguais)
        function viewProfile() {
            const user = authSystem.currentUser;
            const roleText = user.role === 'owner' ? '👑 Dono do Site' : 
                               user.role === 'admin' ? '🛡️ Administrador' : '👤 Usuário';
            
            alert(`👤 Perfil de ${user.username}\n\n` +
                  `🎯 Cargo: ${roleText}\n` +
                  `📧 E-mail: ${user.email}`);
        }
        
        function viewRanking() {
            alert('🏆 Ranking Global - Top 10\n\n' +
                  '1. 👑 MathMaster - 15,420 pts\n' +
                  `Sua posição: #47 com 2,450 pts`);
        }
        
        function viewAchievements() {
            alert('🏅 Suas Conquistas\n\n' +
                  '✅ Primeiro Jogo - Completou seu primeiro jogo\n' +
                  '✅ Matemático Iniciante - 5 jogos de matemática');
        }
        
        function viewHistory() {
            alert('📈 Histórico de Jogos\n\n' +
                  '🔢 Quiz de Matemática - 85% - 8 min (Hoje)');
        }
        
        function changeTheme() {
            alert('🎨 Tema alterado!');
        }
        
        function downloadProgress() {
            alert('💾 Preparando download do seu progresso...');
        }
        
        function shareProfile() {
            alert('📤 Compartilhar Perfil\n\nFuncionalidade em desenvolvimento!');
        }
        
        function resetStats() {
            if (confirm('🔄 Tem certeza que deseja resetar suas estatísticas?')) {
                document.getElementById('gamesCompleted').textContent = '0';
                document.getElementById('successRate').textContent = '0%';
                document.getElementById('totalTime').textContent = '0h 0m';
                alert('Suas estatísticas foram resetadas com sucesso!');
            }
        }
    </script>
</body>
</html>
