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
    </style>
</head>
<body class="bg-gradient-to-br from-purple-400 via-pink-500 to-red-500 min-h-screen">
    <div class="demo-badge">SISTEMA DE LOGIN REAL</div>
    
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
    
    <div id="registerScreen" class="hidden min-h-screen flex items-center justify-center p-4">
        <div class="login-form rounded-2xl p-8 w-full max-w-md shadow-2xl">
            <div class="text-center mb-8">
                <h1 class="text-4xl font-bold text-purple-600 mb-2">🎮 EduPlay</h1>
                <p class="text-gray-600">Criar nova conta</p>
            </div>
            
            <form id="registerForm" class="space-y-6">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Nome completo</label>
                    <input type="text" id="fullName" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="Digite seu nome completo" required>
                    <div id="fullNameError" class="error-message"></div>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Nome de usuário</label>
                    <input type="text" id="newUsername" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="Escolha um nome de usuário" required>
                    <div id="newUsernameError" class="error-message"></div>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">E-mail</label>
                    <input type="email" id="email" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="Digite seu e-mail" required>
                    <div id="emailError" class="error-message"></div>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Senha</label>
                    <input type="password" id="newPassword" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="Crie uma senha" required>
                    <div id="newPasswordError" class="error-message"></div>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Confirmar senha</label>
                    <input type="password" id="confirmPassword" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="Digite a senha novamente" required>
                    <div id="confirmPasswordError" class="error-message"></div>
                </div>
                
                <div class="flex items-center">
                    <input type="checkbox" id="terms" class="h-4 w-4 text-purple-600 focus:ring-purple-500 border-gray-300 rounded" required>
                    <label for="terms" class="ml-2 block text-sm text-gray-700">Aceito os <a href="#" class="text-purple-600 hover:text-purple-800">termos de uso</a> e <a href="#" class="text-purple-600 hover:text-purple-800">política de privacidade</a></label>
                </div>
                <div id="termsError" class="error-message"></div>
                
                <button type="submit" id="registerButton" class="w-full bg-purple-600 hover:bg-purple-700 text-white font-semibold py-3 px-4 rounded-lg transition duration-300 transform hover:scale-105 flex justify-center items-center">
                    <span id="registerText">Criar conta</span>
                    <div id="registerSpinner" class="loading-spinner ml-2"></div>
                </button>
            </form>
            
            <div class="mt-6 text-center">
                <p class="text-sm text-gray-600">Já tem conta? 
                    <button id="backToLogin" class="text-purple-600 hover:text-purple-800 font-medium">Fazer login</button>
                </p>
            </div>
        </div>
    </div>
    
    <div id="gameScreen" class="hidden min-h-screen">
        <header class="bg-white shadow-lg">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between items-center py-4">
                    <div class="flex items-center">
                        <h1 class="text-2xl font-bold text-purple-600">🎮 EduPlay</h1>
                    </div>
                    <div class="flex items-center space-x-4">
                        <span id="welcomeUser" class="text-gray-700 font-medium"></span>
                        <button id="logoutBtn" class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg transition duration-300">
                            Sair
                        </button>
                    </div>
                </div>
            </div>
        </header>
        
        <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <div class="text-center mb-12">
                <h2 class="text-4xl font-bold text-white mb-4">Escolha seu Jogo Educativo!</h2>
                <p class="text-xl text-white opacity-90">Aprenda brincando com nossos jogos interativos</p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <div class="game-card bg-white rounded-2xl p-6 shadow-lg cursor-pointer" onclick="startGame('math')">
                    <div class="text-center">
                        <div class="text-6xl mb-4">🔢</div>
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">Quiz de Matemática</h3>
                        <p class="text-gray-600 mb-4">Teste seus conhecimentos em matemática com problemas divertidos!</p>
                        <div class="flex justify-center items-center space-x-2 text-sm text-gray-500">
                            <span>⭐ Nível: Iniciante</span>
                            <span>•</span>
                            <span>⏱️ 10 min</span>
                        </div>
                    </div>
                </div>
                
                <div class="game-card bg-white rounded-2xl p-6 shadow-lg cursor-pointer" onclick="startGame('words')">
                    <div class="text-center">
                        <div class="text-6xl mb-4">📝</div>
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">Palavras Cruzadas</h3>
                        <p class="text-gray-600 mb-4">Expanda seu vocabulário com palavras cruzadas educativas!</p>
                        <div class="flex justify-center items-center space-x-2 text-sm text-gray-500">
                            <span>⭐ Nível: Intermediário</span>
                            <span>•</span>
                            <span>⏱️ 15 min</span>
                        </div>
                    </div>
                </div>
                
                <div class="game-card bg-white rounded-2xl p-6 shadow-lg cursor-pointer" onclick="startGame('science')">
                    <div class="text-center">
                        <div class="text-6xl mb-4">🔬</div>
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">Quiz de Ciências</h3>
                        <p class="text-gray-600 mb-4">Descubra os mistérios da ciência de forma divertida!</p>
                        <div class="flex justify-center items-center space-x-2 text-sm text-gray-500">
                            <span>⭐ Nível: Avançado</span>
                            <span>•</span>
                            <span>⏱️ 12 min</span>
                        </div>
                    </div>
                </div>
                
                <div class="game-card bg-white rounded-2xl p-6 shadow-lg cursor-pointer" onclick="startGame('geography')">
                    <div class="text-center">
                        <div class="text-6xl mb-4">🌍</div>
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">Geografia Mundial</h3>
                        <p class="text-gray-600 mb-4">Explore países, capitais e culturas ao redor do mundo!</p>
                        <div class="flex justify-center items-center space-x-2 text-sm text-gray-500">
                            <span>⭐ Nível: Intermediário</span>
                            <span>•</span>
                            <span>⏱️ 20 min</span>
                        </div>
                    </div>
                </div>
                
                <div class="game-card bg-white rounded-2xl p-6 shadow-lg cursor-pointer" onclick="startGame('history')">
                    <div class="text-center">
                        <div class="text-6xl mb-4">📚</div>
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">História do Brasil</h3>
                        <p class="text-gray-600 mb-4">Viaje no tempo e aprenda sobre a história brasileira!</p>
                        <div class="flex justify-center items-center space-x-2 text-sm text-gray-500">
                            <span>⭐ Nível: Avançado</span>
                            <span>•</span>
                            <span>⏱️ 18 min</span>
                        </div>
                    </div>
                </div>
                
                <div class="game-card bg-white rounded-2xl p-6 shadow-lg cursor-pointer" onclick="startGame('english')">
                    <div class="text-center">
                        <div class="text-6xl mb-4">🇺🇸</div>
                        <h3 class="text-2xl font-bold text-gray-800 mb-2">Inglês Básico</h3>
                        <p class="text-gray-600 mb-4">Aprenda inglês de forma interativa e divertida!</p>
                        <div class="flex justify-center items-center space-x-2 text-sm text-gray-500">
                            <span>⭐ Nível: Iniciante</span>
                            <span>•</span>
                            <span>⏱️ 15 min</span>
                        </div>
                    </div>
                </div>
            </div>
            
            <div id="adminPanel" class="hidden mt-12 bg-gradient-to-r from-red-500 to-purple-600 rounded-2xl p-8 shadow-lg text-white">
                <h3 class="text-3xl font-bold mb-6 text-center">🛡️ Painel Administrativo</h3>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
                    <div class="bg-white bg-opacity-20 rounded-xl p-4 text-center">
                        <div class="text-3xl font-bold">1,247</div>
                        <p class="text-sm opacity-90">Usuários Totais</p>
                    </div>
                    <div class="bg-white bg-opacity-20 rounded-xl p-4 text-center">
                        <div class="text-3xl font-bold">8,932</div>
                        <p class="text-sm opacity-90">Jogos Jogados</p>
                    </div>
                    <div class="bg-white bg-opacity-20 rounded-xl p-4 text-center">
                        <div class="text-3xl font-bold">156</div>
                        <p class="text-sm opacity-90">Usuários Online</p>
                    </div>
                    <div class="bg-white bg-opacity-20 rounded-xl p-4 text-center">
                        <div class="text-3xl font-bold">99.2%</div>
                        <p class="text-sm opacity-90">Uptime</p>
                    </div>
                </div>
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <button onclick="manageUsers()" class="bg-white bg-opacity-20 hover:bg-opacity-30 rounded-xl p-4 transition duration-300">
                        <div class="text-2xl mb-2">👥</div>
                        <div class="font-semibold">Gerenciar Usuários</div>
                        <div class="text-sm opacity-90">Visualizar e editar contas</div>
                    </button>
                    
                    <button onclick="manageGames()" class="bg-white bg-opacity-20 hover:bg-opacity-30 rounded-xl p-4 transition duration-300">
                        <div class="text-2xl mb-2">🎮</div>
                        <div class="font-semibold">Gerenciar Jogos</div>
                        <div class="text-sm opacity-90">Adicionar/editar jogos</div>
                    </button>
                    
                    <button onclick="viewReports()" class="bg-white bg-opacity-20 hover:bg-opacity-30 rounded-xl p-4 transition duration-300">
                        <div class="text-2xl mb-2">📊</div>
                        <div class="font-semibold">Relatórios</div>
                        <div class="text-sm opacity-90">Estatísticas detalhadas</div>
                    </button>
                </div>
            </div>

            <div class="mt-12 bg-white rounded-2xl p-8 shadow-lg">
                <h3 class="text-2xl font-bold text-gray-800 mb-6 text-center">🎯 Funcionalidades Disponíveis</h3>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 mb-8">
                    <button onclick="viewProfile()" class="bg-blue-500 hover:bg-blue-600 text-white p-4 rounded-xl transition duration-300 transform hover:scale-105">
                        <div class="text-2xl mb-2">👤</div>
                        <div class="font-semibold">Meu Perfil</div>
                        <div class="text-sm opacity-90">Ver informações</div>
                    </button>
                    
                    <button onclick="viewRanking()" class="bg-green-500 hover:bg-green-600 text-white p-4 rounded-xl transition duration-300 transform hover:scale-105">
                        <div class="text-2xl mb-2">🏆</div>
                        <div class="font-semibold">Ranking</div>
                        <div class="text-sm opacity-90">Top jogadores</div>
                    </button>
                    
                    <button onclick="viewAchievements()" class="bg-yellow-500 hover:bg-yellow-600 text-white p-4 rounded-xl transition duration-300 transform hover:scale-105">
                        <div class="text-2xl mb-2">🏅</div>
                        <div class="font-semibold">Conquistas</div>
                        <div class="text-sm opacity-90">Suas medalhas</div>
                    </button>
                    
                    <button onclick="viewHistory()" class="bg-purple-500 hover:bg-purple-600 text-white p-4 rounded-xl transition duration-300 transform hover:scale-105">
                        <div class="text-2xl mb-2">📈</div>
                        <div class="font-semibold">Histórico</div>
                        <div class="text-sm opacity-90">Jogos anteriores</div>
                    </button>
                </div>
                
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
                    <button onclick="changeTheme()" class="bg-indigo-500 hover:bg-indigo-600 text-white p-4 rounded-xl transition duration-300">
                        <div class="text-xl mb-2">🎨</div>
                        <div class="font-semibold">Mudar Tema</div>
                    </button>
                    
                    <button onclick="downloadProgress()" class="bg-teal-500 hover:bg-teal-600 text-white p-4 rounded-xl transition duration-300">
                        <div class="text-xl mb-2">💾</div>
                        <div class="font-semibold">Baixar Progresso</div>
                    </button>
                    
                    <button onclick="shareProfile()" class="bg-pink-500 hover:bg-pink-600 text-white p-4 rounded-xl transition duration-300">
                        <div class="text-xl mb-2">📤</div>
                        <div class="font-semibold">Compartilhar</div>
                    </button>
                </div>
            </div>

            <div class="mt-8 bg-white rounded-2xl p-8 shadow-lg">
                <h3 class="text-2xl font-bold text-gray-800 mb-6 text-center">Suas Estatísticas</h3>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div class="text-center">
                        <div id="gamesCompleted" class="text-4xl font-bold text-purple-600">12</div>
                        <p class="text-gray-600">Jogos Completados</p>
                    </div>
                    <div class="text-center">
                        <div id="successRate" class="text-4xl font-bold text-green-600">85%</div>
                        <p class="text-gray-600">Taxa de Acerto</p>
                    </div>
                    <div class="text-center">
                        <div id="totalTime" class="text-4xl font-bold text-blue-600">2h 30m</div>
                        <p class="text-gray-600">Tempo Total</p>
                    </div>
                </div>
                
                <div class="mt-6 text-center">
                    <button onclick="resetStats()" class="bg-red-500 hover:bg-red-600 text-white px-6 py-2 rounded-lg transition duration-300">
                        🔄 Resetar Estatísticas
                    </button>
                </div>
            </div>
        </main>
    </div>
    
    <div id="gameModal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
        <div class="bg-white rounded-2xl p-8 max-w-md w-full">
            <div class="text-center">
                <div id="gameIcon" class="text-6xl mb-4"></div>
                <h3 id="gameTitle" class="text-2xl font-bold text-gray-800 mb-4"></h3>
                <p id="gameDescription" class="text-gray-600 mb-6"></p>
                <div class="space-y-3">
                    <button onclick="playGame()" class="w-full bg-green-500 hover:bg-green-600 text-white font-semibold py-3 px-4 rounded-lg transition duration-300">
                        🎮 Jogar Agora
                    </button>
                    <button onclick="closeGameModal()" class="w-full bg-gray-500 hover:bg-gray-600 text-white font-semibold py-3 px-4 rounded-lg transition duration-300">
                        Voltar
                    </button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Sistema de Autenticação Real
        class AuthSystem {
            constructor() {
                this.users = this.loadUsers();
                this.currentUser = null;
                this.currentSession = null;
            }
            
            // Carregar usuários do localStorage
            loadUsers() {
                const storedUsers = localStorage.getItem('eduplay_users');
                if (storedUsers) {
                    return JSON.parse(storedUsers);
                } else {
                    // Usuário padrão (vitor202)
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
            
            // Salvar usuários no localStorage
            saveUsers(users) {
                localStorage.setItem('eduplay_users', JSON.stringify(users));
            }
            
            // Gerar ID único
            generateId() {
                return 'user_' + Math.random().toString(36).substr(2, 9) + Date.now().toString(36);
            }
            
            // Hash simples de senha (em um sistema real, use bcrypt)
            hashPassword(password) {
                // Simulação de hash - em produção use uma biblioteca adequada
                let hash = 0;
                for (let i = 0; i < password.length; i++) {
                    const char = password.charCodeAt(i);
                    hash = ((hash << 5) - hash) + char;
                    hash = hash & hash; // Convert to 32bit integer
                }
                return hash.toString();
            }
            
            // Verificar senha
            verifyPassword(password, hashedPassword) {
                return this.hashPassword(password) === hashedPassword;
            }
            
            // Registrar novo usuário
            register(userData) {
                return new Promise((resolve, reject) => {
                    // Validações
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
                    
                    // Criar novo usuário
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
                    
                    // Adicionar ao sistema
                    this.users[userData.username] = newUser;
                    this.saveUsers(this.users);
                    
                    resolve(newUser);
                });
            }
            
            // Login
            login(username, password, rememberMe = false) {
                return new Promise((resolve, reject) => {
                    // Simular delay de rede
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
                        
                        // Atualizar último login
                        user.lastLogin = new Date().toISOString();
                        this.saveUsers(this.users);
                        
                        // Criar sessão
                        this.currentUser = user;
                        this.currentSession = {
                            token: this.generateToken(),
                            expiresAt: new Date(Date.now() + (rememberMe ? 30 * 24 * 60 * 60 * 1000 : 24 * 60 * 60 * 1000)) // 30 dias ou 1 dia
                        };
                        
                        // Salvar sessão no localStorage se "lembrar-me" estiver ativo
                        if (rememberMe) {
                            localStorage.setItem('eduplay_session', JSON.stringify({
                                username: user.username,
                                token: this.currentSession.token,
                                expiresAt: this.currentSession.expiresAt.toISOString()
                            }));
                        }
                        
                        resolve(user);
                    }, 1000); // Simular delay de rede
                });
            }
            
            // Logout
            logout() {
                this.currentUser = null;
                this.currentSession = null;
                localStorage.removeItem('eduplay_session');
            }
            
            // Verificar se há sessão ativa
            checkActiveSession() {
                const storedSession = localStorage.getItem('eduplay_session');
                if (storedSession) {
                    const session = JSON.parse(storedSession);
                    const expiresAt = new Date(session.expiresAt);
                    
                    if (expiresAt > new Date()) {
                        // Sessão ainda é válida
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
                        // Sessão expirada
                        localStorage.removeItem('eduplay_session');
                    }
                }
                return null;
            }
            
            // Gerar token de sessão
            generateToken() {
                return 'token_' + Math.random().toString(36).substr(2) + Date.now().toString(36);
            }
        }

        // Inicializar sistema de autenticação
        const authSystem = new AuthSystem();
        
        // Elementos da UI
        let currentGame = '';
        
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
        
        // Inicializar a aplicação
        document.addEventListener('DOMContentLoaded', function() {
            // Verificar se há uma sessão ativa
            const activeUser = authSystem.checkActiveSession();
            if (activeUser) {
                showGameScreen(activeUser);
            }
            
            // Event Listeners
            document.getElementById('loginForm').addEventListener('submit', handleLogin);
            document.getElementById('registerForm').addEventListener('submit', handleRegister);
            document.getElementById('registerBtn').addEventListener('click', showRegisterScreen);
            document.getElementById('backToLogin').addEventListener('click', showLoginScreen);
            document.getElementById('logoutBtn').addEventListener('click', handleLogout);
            document.getElementById('forgotPassword').addEventListener('click', handleForgotPassword);
        });
        
        // Função de login
        async function handleLogin(e) {
            e.preventDefault();
            
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const rememberMe = document.getElementById('rememberMe').checked;
            
            // Limpar erros anteriores
            clearErrors();
            
            // Validação básica
            if (!username || !password) {
                showError('usernameError', 'Por favor, preencha todos os campos');
                return;
            }
            
            // Mostrar loading
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
        
        // Função de registro
        async function handleRegister(e) {
            e.preventDefault();
            
            const fullName = document.getElementById('fullName').value;
            const username = document.getElementById('newUsername').value;
            const email = document.getElementById('email').value;
            const password = document.getElementById('newPassword').value;
            const confirmPassword = document.getElementById('confirmPassword').value;
            const terms = document.getElementById('terms').checked;
            
            // Limpar erros anteriores
            clearErrors();
            
            // Validações
            if (!fullName || !username || !email || !password || !confirmPassword) {
                showError('newUsernameError', 'Por favor, preencha todos os campos');
                return;
            }
            
            if (!terms) {
                showError('termsError', 'Você deve aceitar os termos de uso');
                return;
            }
            
            // Mostrar loading
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
        
        // Função de logout
        function handleLogout() {
            authSystem.logout();
            showLoginScreen();
        }
        
        // Função de esqueci a senha
        function handleForgotPassword() {
            alert('Funcionalidade de recuperação de senha seria implementada aqui!\n\nEm um sistema real, enviaríamos um e-mail com um link para redefinir sua senha.');
        }
        
        // Mostrar tela de jogos
        function showGameScreen(user) {
            // Criar texto de boas-vindas com verificação
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
            
            // Mostrar painel admin se for admin ou owner
            if (user.role === 'admin' || user.role === 'owner') {
                document.getElementById('adminPanel').classList.remove('hidden');
            }
            
            // Mostrar mensagem de boas-vindas personalizada
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
        
        // Mostrar tela de login
        function showLoginScreen() {
            document.getElementById('loginScreen').classList.remove('hidden');
            document.getElementById('registerScreen').classList.add('hidden');
            document.getElementById('gameScreen').classList.add('hidden');
            clearForm('loginForm');
            clearErrors();
        }
        
        // Mostrar tela de registro
        function showRegisterScreen() {
            document.getElementById('loginScreen').classList.add('hidden');
            document.getElementById('registerScreen').classList.remove('hidden');
            document.getElementById('gameScreen').classList.add('hidden');
            clearForm('registerForm');
            clearErrors();
        }
        
        // Limpar formulário
        function clearForm(formId) {
            document.getElementById(formId).reset();
        }
        
        // Limpar mensagens de erro
        function clearErrors() {
            const errorElements = document.querySelectorAll('.error-message');
            errorElements.forEach(el => {
                el.style.display = 'none';
                el.textContent = '';
            });
        }
        
        // Mostrar erro
        function showError(elementId, message) {
            const element = document.getElementById(elementId);
            element.textContent = message;
            element.style.display = 'block';
        }
        
        // Mostrar sucesso
        function showSuccess(message) {
            alert(message);
        }
        
        // Mostrar loading
        function showLoading(type) {
            document.getElementById(`${type}Text`).style.display = 'none';
            document.getElementById(`${type}Spinner`).style.display = 'block';
            document.getElementById(`${type}Button`).disabled = true;
        }
        
        // Esconder loading
        function hideLoading(type) {
            document.getElementById(`${type}Text`).style.display = 'block';
            document.getElementById(`${type}Spinner`).style.display = 'none';
            document.getElementById(`${type}Button`).disabled = false;
        }
        
        // Iniciar Jogo
        function startGame(gameType) {
            currentGame = gameType;
            const game = games[gameType];
            
            document.getElementById('gameIcon').textContent = game.icon;
            document.getElementById('gameTitle').textContent = game.title;
            document.getElementById('gameDescription').textContent = game.description;
            document.getElementById('gameModal').classList.remove('hidden');
        }
        
        // Jogar
        function playGame() {
            alert(`🎮 Iniciando ${games[currentGame].title}!\n\nEm um sistema real, o jogo seria carregado aqui com todas as funcionalidades interativas.`);
            closeGameModal();
        }
        
        // Fechar Modal
        function closeGameModal() {
            document.getElementById('gameModal').classList.add('hidden');
        }
        
        // Fechar modal clicando fora
        document.getElementById('gameModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeGameModal();
            }
        });
        
        // Funções do Painel Administrativo
        function manageUsers() {
            if (authSystem.currentUser.role === 'owner' || authSystem.currentUser.role === 'admin') {
                alert('👥 Gerenciamento de Usuários\n\n• Total de usuários: ' + Object.keys(authSystem.users).length + '\n• Usuários ativos hoje: 156\n• Novos cadastros esta semana: 23\n\nEm um sistema real, aqui você poderia:\n- Ver lista completa de usuários\n- Editar permissões\n- Banir/desbanir usuários\n- Ver histórico de atividades');
            } else {
                alert('❌ Acesso negado! Apenas administradores podem acessar esta função.');
            }
        }
        
        function manageGames() {
            if (authSystem.currentUser.role === 'owner' || authSystem.currentUser.role === 'admin') {
                alert('🎮 Gerenciamento de Jogos\n\n• Total de jogos: 6\n• Jogos mais populares: Quiz de Matemática\n• Média de tempo por sessão: 12 min\n\nEm um sistema real, aqui você poderia:\n- Adicionar novos jogos\n- Editar jogos existentes\n- Ver estatísticas de cada jogo\n- Configurar níveis de dificuldade');
            } else {
                alert('❌ Acesso negado! Apenas administradores podem acessar esta função.');
            }
        }
        
        function viewReports() {
            if (authSystem.currentUser.role === 'owner' || authSystem.currentUser.role === 'admin') {
                alert('📊 Relatórios do Sistema\n\n• Uptime: 99.2%\n• Jogos jogados hoje: 342\n• Taxa de conclusão: 78%\n• Usuários mais ativos: 45\n\nEm um sistema real, aqui você teria:\n- Gráficos detalhados\n- Relatórios exportáveis\n- Análise de performance\n- Métricas de engajamento');
            } else {
                alert('❌ Acesso negado! Apenas administradores podem acessar esta função.');
            }
        }
        
        // Funções Disponíveis para Todos os Usuários
        function viewProfile() {
            const user = authSystem.currentUser;
            const roleText = user.role === 'owner' ? '👑 Dono do Site' : 
                               user.role === 'admin' ? '🛡️ Administrador' : '👤 Usuário';
            const verifiedText = user.verified ? '✅ Verificado' : '❌ Não Verificado';
            
            alert(`👤 Perfil de ${user.username}\n\n` +
                  `🎯 Cargo: ${roleText}\n` +
                  `${verifiedText}\n` +
                  `📧 E-mail: ${user.email}\n` +
                  `📅 Membro desde: ${new Date(user.createdAt).toLocaleDateString('pt-BR')}\n` +
                  `🎮 Jogos favoritos: Matemática, Ciências\n` +
                  `🏆 Nível atual: Intermediário\n` +
                  `⭐ Pontos totais: 2,450`);
        }
        
        function viewRanking() {
            alert('🏆 Ranking Global - Top 10\n\n' +
                  '1. 👑 MathMaster - 15,420 pts\n' +
                  '2. 🧠 ScienceGuru - 14,890 pts\n' +
                  '3. 📚 HistoryBuff - 13,750 pts\n' +
                  '4. 🌍 GeoExplorer - 12,980 pts\n' +
                  '5. 📝 WordWizard - 11,650 pts\n' +
                  '6. 🇺🇸 EnglishPro - 10,420 pts\n' +
                  '7. 🎯 QuizChamp - 9,870 pts\n' +
                  '8. 🔢 NumberNinja - 8,950 pts\n' +
                  '9. 🎮 GameMaster - 7,680 pts\n' +
                  '10. 🌟 StarPlayer - 6,420 pts\n\n' +
                  `Sua posição: #47 com 2,450 pts`);
        }
        
        function viewAchievements() {
            alert('🏅 Suas Conquistas\n\n' +
                  '✅ Primeiro Jogo - Completou seu primeiro jogo\n' +
                  '✅ Matemático Iniciante - 5 jogos de matemática\n' +
                  '✅ Cientista Curioso - 3 jogos de ciências\n' +
                  '✅ Explorador - Jogou todos os tipos de jogo\n' +
                  '✅ Persistente - 10 jogos completados\n\n' +
                  '🔒 Conquistas Bloqueadas:\n' +
                  '❌ Matemático Expert - 20 jogos de matemática\n' +
                  '❌ Velocista - Complete um jogo em menos de 5 min\n' +
                  '❌ Perfecionista - 100% de acerto em 5 jogos\n' +
                  '❌ Maratonista - 50 jogos completados');
        }
        
        function viewHistory() {
            alert('📈 Histórico de Jogos\n\n' +
                  '🔢 Quiz de Matemática - 85% - 8 min (Hoje)\n' +
                  '🔬 Quiz de Ciências - 92% - 12 min (Ontem)\n' +
                  '🌍 Geografia Mundial - 78% - 15 min (2 dias)\n' +
                  '📝 Palavras Cruzadas - 88% - 10 min (3 dias)\n' +
                  '📚 História do Brasil - 95% - 18 min (4 dias)\n' +
                  '🇺🇸 Inglês Básico - 82% - 14 min (5 dias)\n\n' +
                  '📊 Estatísticas da Semana:\n' +
                  '• Jogos jogados: 12\n' +
                  '• Média de acerto: 85%\n' +
                  '• Tempo total: 2h 30m');
        }
        
        function changeTheme() {
            const themes = ['Roxo Gradiente', 'Azul Oceano', 'Verde Natureza', 'Rosa Sunset'];
            const currentTheme = themes[Math.floor(Math.random() * themes.length)];
            alert(`🎨 Tema alterado para: ${currentTheme}\n\n` +
                  'Em um sistema real, o tema seria aplicado imediatamente!\n\n' +
                  'Temas disponíveis:\n' +
                  '• Roxo Gradiente (atual)\n' +
                  '• Azul Oceano\n' +
                  '• Verde Natureza\n' +
                  '• Rosa Sunset\n' +
                  '• Modo Escuro\n' +
                  '• Modo Claro');
        }
        
        function downloadProgress() {
            alert('💾 Preparando download do seu progresso...\n\n' +
                  'Arquivo: eduplay_progresso_' + authSystem.currentUser.username + '.json\n' +
                  'Tamanho: 2.4 KB\n\n' +
                  'Conteúdo incluído:\n' +
                  '• Estatísticas completas\n' +
                  '• Histórico de jogos\n' +
                  '• Conquistas desbloqueadas\n' +
                  '• Configurações pessoais\n\n' +
                  'Em um sistema real, o arquivo seria baixado automaticamente!');
        }
        
        function shareProfile() {
            const shareText = `🎮 Confira meu perfil no EduPlay!\n\n` +
                              `👤 ${authSystem.currentUser.username}\n` +
                              `🎯 12 jogos completados\n` +
                              `⭐ 85% de taxa de acerto\n` +
                              `🏆 2,450 pontos totais\n\n` +
                              `Venha jogar comigo!`;
            
            if (navigator.share) {
                navigator.share({
                    title: 'Meu Perfil EduPlay',
                    text: shareText,
                    url: window.location.href
                });
            } else {
                // Fallback para navegadores que não suportam Web Share API
                navigator.clipboard.writeText(shareText).then(() => {
                    alert('📤 Perfil copiado para a área de transferência!\n\n' + shareText);
                }).catch(() => {
                    alert('📤 Compartilhar Perfil\n\n' + shareText + '\n\n(Copie manualmente o texto acima)');
                });
            }
        }
        
        function resetStats() {
            if (confirm('🔄 Tem certeza que deseja resetar suas estatísticas?\n\nEsta ação não pode ser desfeita!')) {
                // Lógica para resetar as estatísticas na tela
                document.getElementById('gamesCompleted').textContent = '0';
                document.getElementById('successRate').textContent = '0%';
                document.getElementById('totalTime').textContent = '0h 0m';
                alert('Suas estatísticas foram resetadas com sucesso!');
            } else {
                alert('Ação cancelada. Suas estatísticas não foram alteradas.');
            }
        }
    </script>

</body>
</html>