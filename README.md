<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Rifas - Panel de Administración</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
        }
        
        .sidebar-transition {
            transition: transform 0.3s ease-in-out;
        }
        
        .fade-in {
            animation: fadeIn 0.5s ease-in;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .winner-animation {
            animation: winnerPulse 2s infinite;
        }
        
        @keyframes winnerPulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }
        
        .chart-bar {
            transition: height 0.5s ease-in-out;
        }
        
        .notification {
            animation: slideIn 0.3s ease-out;
        }
        
        @keyframes slideIn {
            from { transform: translateX(100%); }
            to { transform: translateX(0); }
        }
    </style>
</head>
<body class="bg-gray-50">
    <!-- Navigation -->
    <nav class="bg-white shadow-sm border-b border-gray-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16">
                <div class="flex items-center">
                    <div class="flex-shrink-0">
                        <h1 class="text-2xl font-bold text-gray-900">🎟️ RifaAdmin Pro</h1>
                    </div>
                </div>
                <div class="flex items-center space-x-4">
                    <div class="text-sm text-gray-500">
                        <span id="currentDateTime"></span>
                    </div>
                    <div class="relative">
                        <button class="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors">
                            👤 Administrador
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </nav>

    <div class="flex">
        <!-- Sidebar -->
        <div class="w-64 bg-white shadow-lg h-screen sticky top-0">
            <div class="p-6">
                <nav class="space-y-2">
                    <button onclick="showSection('dashboard')" class="nav-item w-full text-left px-4 py-3 rounded-lg hover:bg-gray-100 transition-colors flex items-center gap-3">
                        📊 Dashboard
                    </button>
                    <button onclick="showSection('rifas')" class="nav-item w-full text-left px-4 py-3 rounded-lg hover:bg-gray-100 transition-colors flex items-center gap-3">
                        🎯 Gestionar Rifas
                    </button>
                    <button onclick="showSection('participants')" class="nav-item w-full text-left px-4 py-3 rounded-lg hover:bg-gray-100 transition-colors flex items-center gap-3">
                        👥 Participantes
                    </button>
                    <button onclick="showSection('winners')" class="nav-item w-full text-left px-4 py-3 rounded-lg hover:bg-gray-100 transition-colors flex items-center gap-3">
                        🏆 Ganadores
                    </button>
                    <button onclick="showSection('reports')" class="nav-item w-full text-left px-4 py-3 rounded-lg hover:bg-gray-100 transition-colors flex items-center gap-3">
                        📈 Reportes
                    </button>
                    <button onclick="showSection('settings')" class="nav-item w-full text-left px-4 py-3 rounded-lg hover:bg-gray-100 transition-colors flex items-center gap-3">
                        ⚙️ Configuración
                    </button>
                </nav>
            </div>
        </div>

        <!-- Main Content -->
        <div class="flex-1 p-8">
            <!-- Dashboard Section -->
            <div id="dashboard" class="section">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-gray-900 mb-2">Dashboard</h2>
                    <p class="text-gray-600">Resumen general del sistema de rifas</p>
                </div>

                <!-- Stats Cards -->
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
                    <div class="bg-white rounded-xl shadow-sm p-6 border border-gray-200">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-600">Rifas Activas</p>
                                <p class="text-3xl font-bold text-gray-900" id="activeRifas">0</p>
                            </div>
                            <div class="bg-blue-100 p-3 rounded-full">
                                <span class="text-2xl">🎯</span>
                            </div>
                        </div>
                    </div>

                    <div class="bg-white rounded-xl shadow-sm p-6 border border-gray-200">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-600">Total Participantes</p>
                                <p class="text-3xl font-bold text-gray-900" id="totalParticipants">0</p>
                            </div>
                            <div class="bg-green-100 p-3 rounded-full">
                                <span class="text-2xl">👥</span>
                            </div>
                        </div>
                    </div>

                    <div class="bg-white rounded-xl shadow-sm p-6 border border-gray-200">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-600">Ganadores</p>
                                <p class="text-3xl font-bold text-gray-900" id="totalWinners">0</p>
                            </div>
                            <div class="bg-yellow-100 p-3 rounded-full">
                                <span class="text-2xl">🏆</span>
                            </div>
                        </div>
                    </div>

                    <div class="bg-white rounded-xl shadow-sm p-6 border border-gray-200">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-600">Ingresos Totales</p>
                                <p class="text-3xl font-bold text-gray-900" id="totalRevenue">$0</p>
                            </div>
                            <div class="bg-purple-100 p-3 rounded-full">
                                <span class="text-2xl">💰</span>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Recent Activity -->
                <div class="grid lg:grid-cols-2 gap-8">
                    <div class="bg-white rounded-xl shadow-sm p-6 border border-gray-200">
                        <h3 class="text-lg font-semibold text-gray-900 mb-4">Actividad Reciente</h3>
                        <div id="recentActivity" class="space-y-3">
                            <div class="text-gray-500 text-center py-8">No hay actividad reciente</div>
                        </div>
                    </div>

                    <div class="bg-white rounded-xl shadow-sm p-6 border border-gray-200">
                        <h3 class="text-lg font-semibold text-gray-900 mb-4">Rifas por Estado</h3>
                        <div id="rifaChart" class="space-y-3">
                            <!-- Chart will be generated here -->
                        </div>
                    </div>
                </div>
            </div>

            <!-- Rifas Section -->
            <div id="rifas" class="section hidden">
                <div class="mb-8">
                    <div class="flex justify-between items-center">
                        <div>
                            <h2 class="text-3xl font-bold text-gray-900 mb-2">Gestionar Rifas</h2>
                            <p class="text-gray-600">Crear y administrar rifas</p>
                        </div>
                        <button onclick="showCreateRifaModal()" class="bg-blue-600 text-white px-6 py-3 rounded-lg hover:bg-blue-700 transition-colors flex items-center gap-2">
                            ➕ Nueva Rifa
                        </button>
                    </div>
                </div>

                <!-- Rifas List -->
                <div class="bg-white rounded-xl shadow-sm border border-gray-200">
                    <div class="p-6">
                        <div class="overflow-x-auto">
                            <table class="w-full">
                                <thead>
                                    <tr class="border-b border-gray-200">
                                        <th class="text-left py-3 px-4 font-semibold text-gray-900">Nombre</th>
                                        <th class="text-left py-3 px-4 font-semibold text-gray-900">Premio</th>
                                        <th class="text-left py-3 px-4 font-semibold text-gray-900">Participantes</th>
                                        <th class="text-left py-3 px-4 font-semibold text-gray-900">Estado</th>
                                        <th class="text-left py-3 px-4 font-semibold text-gray-900">Fecha</th>
                                        <th class="text-left py-3 px-4 font-semibold text-gray-900">Acciones</th>
                                    </tr>
                                </thead>
                                <tbody id="rifasTable">
                                    <tr>
                                        <td colspan="6" class="text-center py-8 text-gray-500">No hay rifas creadas</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Participants Section -->
            <div id="participants" class="section hidden">
                <div class="mb-8">
                    <div class="flex justify-between items-center">
                        <div>
                            <h2 class="text-3xl font-bold text-gray-900 mb-2">Participantes</h2>
                            <p class="text-gray-600">Gestionar participantes de las rifas</p>
                        </div>
                        <button onclick="showAddParticipantModal()" class="bg-green-600 text-white px-6 py-3 rounded-lg hover:bg-green-700 transition-colors flex items-center gap-2">
                            ➕ Agregar Participante
                        </button>
                    </div>
                </div>

                <!-- Search and Filter -->
                <div class="bg-white rounded-xl shadow-sm p-6 border border-gray-200 mb-6">
                    <div class="flex gap-4">
                        <input type="text" id="searchParticipants" placeholder="Buscar participantes..." 
                               class="flex-1 px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <select id="filterRifa" class="px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                            <option value="">Todas las rifas</option>
                        </select>
                    </div>
                </div>

                <!-- Participants List -->
                <div class="bg-white rounded-xl shadow-sm border border-gray-200">
                    <div class="p-6">
                        <div class="overflow-x-auto">
                            <table class="w-full">
                                <thead>
                                    <tr class="border-b border-gray-200">
                                        <th class="text-left py-3 px-4 font-semibold text-gray-900">Nombre</th>
                                        <th class="text-left py-3 px-4 font-semibold text-gray-900">Email</th>
                                        <th class="text-left py-3 px-4 font-semibold text-gray-900">Teléfono</th>
                                        <th class="text-left py-3 px-4 font-semibold text-gray-900">Número</th>
                                        <th class="text-left py-3 px-4 font-semibold text-gray-900">Rifa</th>
                                        <th class="text-left py-3 px-4 font-semibold text-gray-900">Acciones</th>
                                    </tr>
                                </thead>
                                <tbody id="participantsTable">
                                    <tr>
                                        <td colspan="6" class="text-center py-8 text-gray-500">No hay participantes registrados</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Winners Section -->
            <div id="winners" class="section hidden">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-gray-900 mb-2">Ganadores</h2>
                    <p class="text-gray-600">Historial de ganadores de todas las rifas</p>
                </div>

                <div class="bg-white rounded-xl shadow-sm border border-gray-200">
                    <div class="p-6">
                        <div id="winnersContent" class="space-y-4">
                            <div class="text-center py-8 text-gray-500">No hay ganadores registrados</div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Reports Section -->
            <div id="reports" class="section hidden">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-gray-900 mb-2">Reportes</h2>
                    <p class="text-gray-600">Análisis y estadísticas detalladas</p>
                </div>

                <div class="grid lg:grid-cols-2 gap-8">
                    <div class="bg-white rounded-xl shadow-sm p-6 border border-gray-200">
                        <h3 class="text-lg font-semibold text-gray-900 mb-4">Participación por Mes</h3>
                        <div id="monthlyChart" class="h-64 flex items-end justify-around gap-2">
                            <!-- Monthly chart will be generated here -->
                        </div>
                    </div>

                    <div class="bg-white rounded-xl shadow-sm p-6 border border-gray-200">
                        <h3 class="text-lg font-semibold text-gray-900 mb-4">Top Rifas</h3>
                        <div id="topRifas" class="space-y-3">
                            <div class="text-gray-500 text-center py-8">No hay datos suficientes</div>
                        </div>
                    </div>
                </div>

                <!-- Export Options -->
                <div class="mt-8 bg-white rounded-xl shadow-sm p-6 border border-gray-200">
                    <h3 class="text-lg font-semibold text-gray-900 mb-4">Exportar Datos</h3>
                    <div class="flex gap-4">
                        <button onclick="exportData('csv')" class="bg-green-600 text-white px-6 py-3 rounded-lg hover:bg-green-700 transition-colors">
                            📊 Exportar CSV
                        </button>
                        <button onclick="exportData('pdf')" class="bg-red-600 text-white px-6 py-3 rounded-lg hover:bg-red-700 transition-colors">
                            📄 Exportar PDF
                        </button>
                        <button onclick="generateReport()" class="bg-blue-600 text-white px-6 py-3 rounded-lg hover:bg-blue-700 transition-colors">
                            📈 Generar Reporte
                        </button>
                    </div>
                </div>
            </div>

            <!-- Settings Section -->
            <div id="settings" class="section hidden">
                <div class="mb-8">
                    <h2 class="text-3xl font-bold text-gray-900 mb-2">Configuración</h2>
                    <p class="text-gray-600">Configurar el sistema de rifas</p>
                </div>

                <div class="grid lg:grid-cols-2 gap-8">
                    <div class="bg-white rounded-xl shadow-sm p-6 border border-gray-200">
                        <h3 class="text-lg font-semibold text-gray-900 mb-4">Configuración General</h3>
                        <div class="space-y-4">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Nombre de la Organización</label>
                                <input type="text" id="orgName" value="Mi Organización" 
                                       class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Email de Contacto</label>
                                <input type="email" id="contactEmail" value="admin@miorg.com" 
                                       class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                            </div>
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">Moneda</label>
                                <select id="currency" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                                    <option value="$">Dólar ($)</option>
                                    <option value="€">Euro (€)</option>
                                    <option value="£">Libra (£)</option>
                                    <option value="¥">Yen (¥)</option>
                                </select>
                            </div>
                        </div>
                    </div>

                    <div class="bg-white rounded-xl shadow-sm p-6 border border-gray-200">
                        <h3 class="text-lg font-semibold text-gray-900 mb-4">Configuración de Rifas</h3>
                        <div class="space-y-4">
                            <div class="flex items-center justify-between">
                                <span class="text-sm font-medium text-gray-700">Permitir números duplicados</span>
                                <input type="checkbox" id="allowDuplicates" class="rounded">
                            </div>
                            <div class="flex items-center justify-between">
                                <span class="text-sm font-medium text-gray-700">Notificaciones automáticas</span>
                                <input type="checkbox" id="autoNotifications" checked class="rounded">
                            </div>
                            <div class="flex items-center justify-between">
                                <span class="text-sm font-medium text-gray-700">Backup automático</span>
                                <input type="checkbox" id="autoBackup" checked class="rounded">
                            </div>
                        </div>
                    </div>
                </div>

                <div class="mt-8 text-center">
                    <button onclick="saveSettings()" class="bg-blue-600 text-white px-8 py-3 rounded-lg hover:bg-blue-700 transition-colors">
                        💾 Guardar Configuración
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Create Rifa Modal -->
    <div id="createRifaModal" class="fixed inset-0 bg-black/50 backdrop-blur-sm hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-2xl mx-4 max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-6">
                <h2 class="text-2xl font-bold text-gray-900">Crear Nueva Rifa</h2>
                <button onclick="hideCreateRifaModal()" class="text-gray-500 hover:text-gray-700 text-2xl">×</button>
            </div>
            
            <form id="createRifaForm" class="space-y-6">
                <div class="grid md:grid-cols-2 gap-6">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Nombre de la Rifa</label>
                        <input type="text" id="newRifaName" required 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Premio</label>
                        <input type="text" id="newRifaPrize" required 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                </div>
                
                <div class="grid md:grid-cols-3 gap-6">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Precio del Boleto</label>
                        <input type="number" id="ticketPrice" min="0" step="0.01" 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Número Inicial</label>
                        <input type="number" id="newStartNumber" value="1" min="0" 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Número Final</label>
                        <input type="number" id="newEndNumber" value="100" min="1" 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Descripción</label>
                    <textarea id="rifaDescription" rows="3" 
                              class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"></textarea>
                </div>
                
                <div class="grid md:grid-cols-2 gap-6">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Fecha de Inicio</label>
                        <input type="datetime-local" id="startDate" 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Fecha de Sorteo</label>
                        <input type="datetime-local" id="drawDate" 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                </div>
                
                <div class="flex justify-end gap-4">
                    <button type="button" onclick="hideCreateRifaModal()" 
                            class="px-6 py-3 border border-gray-300 rounded-lg hover:bg-gray-50 transition-colors">
                        Cancelar
                    </button>
                    <button type="submit" 
                            class="bg-blue-600 text-white px-6 py-3 rounded-lg hover:bg-blue-700 transition-colors">
                        Crear Rifa
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Add Participant Modal -->
    <div id="addParticipantModal" class="fixed inset-0 bg-black/50 backdrop-blur-sm hidden items-center justify-center z-50">
        <div class="bg-white rounded-2xl p-8 max-w-lg mx-4">
            <div class="flex justify-between items-center mb-6">
                <h2 class="text-2xl font-bold text-gray-900">Agregar Participante</h2>
                <button onclick="hideAddParticipantModal()" class="text-gray-500 hover:text-gray-700 text-2xl">×</button>
            </div>
            
            <form id="addParticipantForm" class="space-y-6">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Nombre Completo</label>
                    <input type="text" id="participantName" required 
                           class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Email</label>
                    <input type="email" id="participantEmail" 
                           class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Teléfono</label>
                    <input type="tel" id="participantPhone" 
                           class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                </div>
                
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Rifa</label>
                        <select id="participantRifa" required 
                                class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                            <option value="">Seleccionar rifa</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">Número</label>
                        <input type="number" id="participantNumber" min="1" 
                               class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                    </div>
                </div>
                
                <div class="flex justify-end gap-4">
                    <button type="button" onclick="hideAddParticipantModal()" 
                            class="px-6 py-3 border border-gray-300 rounded-lg hover:bg-gray-50 transition-colors">
                        Cancelar
                    </button>
                    <button type="submit" 
                            class="bg-green-600 text-white px-6 py-3 rounded-lg hover:bg-green-700 transition-colors">
                        Agregar Participante
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Notification Container -->
    <div id="notifications" class="fixed top-4 right-4 z-50 space-y-2"></div>

    <script>
        // Global data storage
        let rifas = [];
        let participants = [];
        let winners = [];
        let currentSection = 'dashboard';

        // Initialize the system
        function init() {
            updateDateTime();
            setInterval(updateDateTime, 1000);
            showSection('dashboard');
            updateDashboard();
            
            // Set default dates
            const now = new Date();
            const tomorrow = new Date(now.getTime() + 24 * 60 * 60 * 1000);
            document.getElementById('startDate').value = now.toISOString().slice(0, 16);
            document.getElementById('drawDate').value = tomorrow.toISOString().slice(0, 16);
        }

        // Update current date and time
        function updateDateTime() {
            const now = new Date();
            document.getElementById('currentDateTime').textContent = now.toLocaleString('es-ES');
        }

        // Show notification
        function showNotification(message, type = 'success') {
            const notification = document.createElement('div');
            notification.className = `notification px-6 py-4 rounded-lg shadow-lg text-white ${
                type === 'success' ? 'bg-green-500' : 
                type === 'error' ? 'bg-red-500' : 
                type === 'warning' ? 'bg-yellow-500' : 'bg-blue-500'
            }`;
            notification.textContent = message;
            
            document.getElementById('notifications').appendChild(notification);
            
            setTimeout(() => {
                notification.remove();
            }, 5000);
        }

        // Show section
        function showSection(sectionName) {
            // Hide all sections
            document.querySelectorAll('.section').forEach(section => {
                section.classList.add('hidden');
            });
            
            // Show selected section
            document.getElementById(sectionName).classList.remove('hidden');
            document.getElementById(sectionName).classList.add('fade-in');
            
            // Update navigation
            document.querySelectorAll('.nav-item').forEach(item => {
                item.classList.remove('bg-blue-100', 'text-blue-700');
            });
            event.target.classList.add('bg-blue-100', 'text-blue-700');
            
            currentSection = sectionName;
            
            // Update section-specific data
            if (sectionName === 'rifas') updateRifasTable();
            if (sectionName === 'participants') updateParticipantsTable();
            if (sectionName === 'winners') updateWinnersDisplay();
            if (sectionName === 'reports') updateReports();
        }

        // Update dashboard
        function updateDashboard() {
            const activeRifas = rifas.filter(r => r.status === 'active').length;
            const totalParticipants = participants.length;
            const totalWinners = winners.length;
            const totalRevenue = rifas.reduce((sum, rifa) => {
                const rifaParticipants = participants.filter(p => p.rifaId === rifa.id);
                return sum + (rifaParticipants.length * (rifa.ticketPrice || 0));
            }, 0);

            document.getElementById('activeRifas').textContent = activeRifas;
            document.getElementById('totalParticipants').textContent = totalParticipants;
            document.getElementById('totalWinners').textContent = totalWinners;
            document.getElementById('totalRevenue').textContent = `$${totalRevenue.toFixed(2)}`;

            updateRecentActivity();
            updateRifaChart();
        }

        // Update recent activity
        function updateRecentActivity() {
            const activities = [];
            
            // Add recent rifas
            rifas.slice(-5).forEach(rifa => {
                activities.push({
                    type: 'rifa',
                    message: `Nueva rifa creada: ${rifa.name}`,
                    time: rifa.createdAt
                });
            });
            
            // Add recent participants
            participants.slice(-5).forEach(participant => {
                const rifa = rifas.find(r => r.id === participant.rifaId);
                activities.push({
                    type: 'participant',
                    message: `${participant.name} se unió a ${rifa?.name || 'una rifa'}`,
                    time: participant.createdAt
                });
            });
            
            // Sort by time
            activities.sort((a, b) => new Date(b.time) - new Date(a.time));
            
            const container = document.getElementById('recentActivity');
            if (activities.length === 0) {
                container.innerHTML = '<div class="text-gray-500 text-center py-8">No hay actividad reciente</div>';
                return;
            }
            
            container.innerHTML = activities.slice(0, 5).map(activity => `
                <div class="flex items-center gap-3 p-3 bg-gray-50 rounded-lg">
                    <div class="text-2xl">
                        ${activity.type === 'rifa' ? '🎯' : '👤'}
                    </div>
                    <div class="flex-1">
                        <div class="text-sm font-medium text-gray-900">${activity.message}</div>
                        <div class="text-xs text-gray-500">${new Date(activity.time).toLocaleString('es-ES')}</div>
                    </div>
                </div>
            `).join('');
        }

        // Update rifa chart
        function updateRifaChart() {
            const statusCounts = {
                active: rifas.filter(r => r.status === 'active').length,
                completed: rifas.filter(r => r.status === 'completed').length,
                pending: rifas.filter(r => r.status === 'pending').length
            };
            
            const total = Object.values(statusCounts).reduce((a, b) => a + b, 0);
            
            const container = document.getElementById('rifaChart');
            if (total === 0) {
                container.innerHTML = '<div class="text-gray-500 text-center py-8">No hay rifas para mostrar</div>';
                return;
            }
            
            container.innerHTML = Object.entries(statusCounts).map(([status, count]) => {
                const percentage = (count / total) * 100;
                const color = status === 'active' ? 'bg-green-500' : 
                             status === 'completed' ? 'bg-blue-500' : 'bg-yellow-500';
                
                return `
                    <div class="flex items-center justify-between mb-2">
                        <span class="text-sm font-medium text-gray-700 capitalize">${status}</span>
                        <span class="text-sm text-gray-500">${count}</span>
                    </div>
                    <div class="w-full bg-gray-200 rounded-full h-2 mb-3">
                        <div class="${color} h-2 rounded-full chart-bar" style="width: ${percentage}%"></div>
                    </div>
                `;
            }).join('');
        }

        // Show create rifa modal
        function showCreateRifaModal() {
            document.getElementById('createRifaModal').classList.remove('hidden');
            document.getElementById('createRifaModal').classList.add('flex');
        }

        // Hide create rifa modal
        function hideCreateRifaModal() {
            document.getElementById('createRifaModal').classList.add('hidden');
            document.getElementById('createRifaModal').classList.remove('flex');
            document.getElementById('createRifaForm').reset();
        }

        // Create new rifa
        document.getElementById('createRifaForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const newRifa = {
                id: Date.now(),
                name: document.getElementById('newRifaName').value,
                prize: document.getElementById('newRifaPrize').value,
                ticketPrice: parseFloat(document.getElementById('ticketPrice').value) || 0,
                startNumber: parseInt(document.getElementById('newStartNumber').value),
                endNumber: parseInt(document.getElementById('newEndNumber').value),
                description: document.getElementById('rifaDescription').value,
                startDate: document.getElementById('startDate').value,
                drawDate: document.getElementById('drawDate').value,
                status: 'active',
                createdAt: new Date().toISOString()
            };
            
            rifas.push(newRifa);
            hideCreateRifaModal();
            showNotification('Rifa creada exitosamente');
            updateDashboard();
            updateRifasTable();
            updateParticipantRifaOptions();
        });

        // Update rifas table
        function updateRifasTable() {
            const tbody = document.getElementById('rifasTable');
            
            if (rifas.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" class="text-center py-8 text-gray-500">No hay rifas creadas</td></tr>';
                return;
            }
            
            tbody.innerHTML = rifas.map(rifa => {
                const participantCount = participants.filter(p => p.rifaId === rifa.id).length;
                const statusColor = rifa.status === 'active' ? 'bg-green-100 text-green-800' : 
                                   rifa.status === 'completed' ? 'bg-blue-100 text-blue-800' : 
                                   'bg-yellow-100 text-yellow-800';
                
                return `
                    <tr class="border-b border-gray-100">
                        <td class="py-4 px-4 font-medium text-gray-900">${rifa.name}</td>
                        <td class="py-4 px-4 text-gray-600">${rifa.prize}</td>
                        <td class="py-4 px-4 text-gray-600">${participantCount}</td>
                        <td class="py-4 px-4">
                            <span class="px-2 py-1 rounded-full text-xs font-medium ${statusColor}">
                                ${rifa.status}
                            </span>
                        </td>
                        <td class="py-4 px-4 text-gray-600">${new Date(rifa.createdAt).toLocaleDateString('es-ES')}</td>
                        <td class="py-4 px-4">
                            <div class="flex gap-2">
                                <button onclick="performDraw(${rifa.id})" class="bg-blue-600 text-white px-3 py-1 rounded text-sm hover:bg-blue-700 transition-colors">
                                    Sortear
                                </button>
                                <button onclick="deleteRifa(${rifa.id})" class="bg-red-600 text-white px-3 py-1 rounded text-sm hover:bg-red-700 transition-colors">
                                    Eliminar
                                </button>
                            </div>
                        </td>
                    </tr>
                `;
            }).join('');
        }

        // Perform draw
        function performDraw(rifaId) {
            const rifa = rifas.find(r => r.id === rifaId);
            const rifaParticipants = participants.filter(p => p.rifaId === rifaId);
            
            if (rifaParticipants.length === 0) {
                showNotification('No hay participantes en esta rifa', 'error');
                return;
            }
            
            const winner = rifaParticipants[Math.floor(Math.random() * rifaParticipants.length)];
            
            const winnerRecord = {
                id: Date.now(),
                rifaId: rifaId,
                rifaName: rifa.name,
                prize: rifa.prize,
                participantId: winner.id,
                participantName: winner.name,
                participantEmail: winner.email,
                number: winner.number,
                date: new Date().toISOString()
            };
            
            winners.push(winnerRecord);
            rifa.status = 'completed';
            
            showNotification(`¡${winner.name} ha ganado ${rifa.prize}!`, 'success');
            updateDashboard();
            updateRifasTable();
            updateWinnersDisplay();
        }

        // Delete rifa
        function deleteRifa(rifaId) {
            if (confirm('¿Estás seguro de que quieres eliminar esta rifa?')) {
                rifas = rifas.filter(r => r.id !== rifaId);
                participants = participants.filter(p => p.rifaId !== rifaId);
                winners = winners.filter(w => w.rifaId !== rifaId);
                
                showNotification('Rifa eliminada exitosamente');
                updateDashboard();
                updateRifasTable();
                updateParticipantsTable();
                updateWinnersDisplay();
            }
        }

        // Show add participant modal
        function showAddParticipantModal() {
            updateParticipantRifaOptions();
            document.getElementById('addParticipantModal').classList.remove('hidden');
            document.getElementById('addParticipantModal').classList.add('flex');
        }

        // Hide add participant modal
        function hideAddParticipantModal() {
            document.getElementById('addParticipantModal').classList.add('hidden');
            document.getElementById('addParticipantModal').classList.remove('flex');
            document.getElementById('addParticipantForm').reset();
        }

        // Update participant rifa options
        function updateParticipantRifaOptions() {
            const select = document.getElementById('participantRifa');
            const activeRifas = rifas.filter(r => r.status === 'active');
            
            select.innerHTML = '<option value="">Seleccionar rifa</option>' + 
                activeRifas.map(rifa => `<option value="${rifa.id}">${rifa.name}</option>`).join('');
        }

        // Add participant
        document.getElementById('addParticipantForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const rifaId = parseInt(document.getElementById('participantRifa').value);
            const number = parseInt(document.getElementById('participantNumber').value);
            
            // Check if number is already taken
            if (participants.some(p => p.rifaId === rifaId && p.number === number)) {
                showNotification('Este número ya está ocupado en esta rifa', 'error');
                return;
            }
            
            const newParticipant = {
                id: Date.now(),
                name: document.getElementById('participantName').value,
                email: document.getElementById('participantEmail').value,
                phone: document.getElementById('participantPhone').value,
                rifaId: rifaId,
                number: number,
                createdAt: new Date().toISOString()
            };
            
            participants.push(newParticipant);
            hideAddParticipantModal();
            showNotification('Participante agregado exitosamente');
            updateDashboard();
            updateParticipantsTable();
        });

        // Update participants table
        function updateParticipantsTable() {
            const tbody = document.getElementById('participantsTable');
            
            if (participants.length === 0) {
                tbody.innerHTML = '<tr><td colspan="6" class="text-center py-8 text-gray-500">No hay participantes registrados</td></tr>';
                return;
            }
            
            tbody.innerHTML = participants.map(participant => {
                const rifa = rifas.find(r => r.id === participant.rifaId);
                
                return `
                    <tr class="border-b border-gray-100">
                        <td class="py-4 px-4 font-medium text-gray-900">${participant.name}</td>
                        <td class="py-4 px-4 text-gray-600">${participant.email || 'N/A'}</td>
                        <td class="py-4 px-4 text-gray-600">${participant.phone || 'N/A'}</td>
                        <td class="py-4 px-4">
                            <span class="bg-blue-100 text-blue-800 px-2 py-1 rounded-full text-sm font-medium">
                                #${participant.number}
                            </span>
                        </td>
                        <td class="py-4 px-4 text-gray-600">${rifa?.name || 'Rifa eliminada'}</td>
                        <td class="py-4 px-4">
                            <button onclick="deleteParticipant(${participant.id})" class="bg-red-600 text-white px-3 py-1 rounded text-sm hover:bg-red-700 transition-colors">
                                Eliminar
                            </button>
                        </td>
                    </tr>
                `;
            }).join('');
        }

        // Delete participant
        function deleteParticipant(participantId) {
            if (confirm('¿Estás seguro de que quieres eliminar este participante?')) {
                participants = participants.filter(p => p.id !== participantId);
                showNotification('Participante eliminado exitosamente');
                updateDashboard();
                updateParticipantsTable();
            }
        }

        // Update winners display
        function updateWinnersDisplay() {
            const container = document.getElementById('winnersContent');
            
            if (winners.length === 0) {
                container.innerHTML = '<div class="text-center py-8 text-gray-500">No hay ganadores registrados</div>';
                return;
            }
            
            container.innerHTML = winners.map(winner => `
                <div class="bg-gradient-to-r from-yellow-50 to-orange-50 border border-yellow-200 rounded-lg p-6 winner-animation">
                    <div class="flex items-center justify-between">
                        <div class="flex items-center gap-4">
                            <div class="text-4xl">🏆</div>
                            <div>
                                <h3 class="text-xl font-bold text-gray-900">${winner.participantName}</h3>
                                <p class="text-gray-600">Ganó: ${winner.prize}</p>
                                <p class="text-sm text-gray-500">Rifa: ${winner.rifaName}</p>
                            </div>
                        </div>
                        <div class="text-right">
                            <div class="bg-yellow-500 text-white px-4 py-2 rounded-full text-lg font-bold">
                                #${winner.number}
                            </div>
                            <div class="text-sm text-gray-500 mt-2">
                                ${new Date(winner.date).toLocaleDateString('es-ES')}
                            </div>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        // Update reports
        function updateReports() {
            updateMonthlyChart();
            updateTopRifas();
        }

        // Update monthly chart
        function updateMonthlyChart() {
            const monthlyData = {};
            const months = ['Ene', 'Feb', 'Mar', 'Abr', 'May', 'Jun', 'Jul', 'Ago', 'Sep', 'Oct', 'Nov', 'Dic'];
            
            participants.forEach(participant => {
                const month = new Date(participant.createdAt).getMonth();
                monthlyData[month] = (monthlyData[month] || 0) + 1;
            });
            
            const maxValue = Math.max(...Object.values(monthlyData), 1);
            const container = document.getElementById('monthlyChart');
            
            container.innerHTML = months.map((month, index) => {
                const value = monthlyData[index] || 0;
                const height = (value / maxValue) * 200;
                
                return `
                    <div class="flex flex-col items-center">
                        <div class="bg-blue-500 rounded-t chart-bar" style="height: ${height}px; width: 20px; min-height: 4px;"></div>
                        <div class="text-xs text-gray-600 mt-2">${month}</div>
                        <div class="text-xs font-semibold text-gray-800">${value}</div>
                    </div>
                `;
            }).join('');
        }

        // Update top rifas
        function updateTopRifas() {
            const rifaStats = rifas.map(rifa => ({
                ...rifa,
                participantCount: participants.filter(p => p.rifaId === rifa.id).length,
                revenue: participants.filter(p => p.rifaId === rifa.id).length * (rifa.ticketPrice || 0)
            })).sort((a, b) => b.participantCount - a.participantCount);
            
            const container = document.getElementById('topRifas');
            
            if (rifaStats.length === 0) {
                container.innerHTML = '<div class="text-gray-500 text-center py-8">No hay datos suficientes</div>';
                return;
            }
            
            container.innerHTML = rifaStats.slice(0, 5).map((rifa, index) => `
                <div class="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                    <div class="flex items-center gap-3">
                        <div class="bg-blue-100 text-blue-600 rounded-full w-8 h-8 flex items-center justify-center text-sm font-bold">
                            ${index + 1}
                        </div>
                        <div>
                            <div class="font-medium text-gray-900">${rifa.name}</div>
                            <div class="text-sm text-gray-500">${rifa.participantCount} participantes</div>
                        </div>
                    </div>
                    <div class="text-right">
                        <div class="font-semibold text-gray-900">$${rifa.revenue.toFixed(2)}</div>
                        <div class="text-sm text-gray-500">ingresos</div>
                    </div>
                </div>
            `).join('');
        }

        // Export data
        function exportData(format) {
            if (format === 'csv') {
                exportCSV();
            } else if (format === 'pdf') {
                showNotification('Función de exportar PDF en desarrollo', 'info');
            }
        }

        // Export CSV
        function exportCSV() {
            const csvData = [
                ['Nombre', 'Email', 'Teléfono', 'Número', 'Rifa', 'Fecha'],
                ...participants.map(p => {
                    const rifa = rifas.find(r => r.id === p.rifaId);
                    return [p.name, p.email || '', p.phone || '', p.number, rifa?.name || '', new Date(p.createdAt).toLocaleDateString('es-ES')];
                })
            ];
            
            const csvContent = csvData.map(row => row.join(',')).join('\n');
            const blob = new Blob([csvContent], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'participantes.csv';
            a.click();
            window.URL.revokeObjectURL(url);
            
            showNotification('Datos exportados exitosamente');
        }

        // Generate report
        function generateReport() {
            const report = {
                fecha: new Date().toLocaleDateString('es-ES'),
                rifas: rifas.length,
                participantes: participants.length,
                ganadores: winners.length,
                ingresos: rifas.reduce((sum, rifa) => {
                    const rifaParticipants = participants.filter(p => p.rifaId === rifa.id);
                    return sum + (rifaParticipants.length * (rifa.ticketPrice || 0));
                }, 0)
            };
            
            const reportContent = `
                REPORTE DEL SISTEMA DE RIFAS
                ============================
                Fecha: ${report.fecha}
                
                RESUMEN GENERAL:
                - Total de rifas: ${report.rifas}
                - Total de participantes: ${report.participantes}
                - Total de ganadores: ${report.ganadores}
                - Ingresos totales: $${report.ingresos.toFixed(2)}
                
                RIFAS ACTIVAS:
                ${rifas.filter(r => r.status === 'active').map(r => `- ${r.name}: ${participants.filter(p => p.rifaId === r.id).length} participantes`).join('\n')}
                
                GANADORES RECIENTES:
                ${winners.slice(-5).map(w => `- ${w.participantName} ganó ${w.prize} (${new Date(w.date).toLocaleDateString('es-ES')})`).join('\n')}
            `;
            
            const blob = new Blob([reportContent], { type: 'text/plain' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `reporte_rifas_${new Date().toISOString().split('T')[0]}.txt`;
            a.click();
            window.URL.revokeObjectURL(url);
            
            showNotification('Reporte generado exitosamente');
        }

        // Save settings
        function saveSettings() {
            const settings = {
                orgName: document.getElementById('orgName').value,
                contactEmail: document.getElementById('contactEmail').value,
                currency: document.getElementById('currency').value,
                allowDuplicates: document.getElementById('allowDuplicates').checked,
                autoNotifications: document.getElementById('autoNotifications').checked,
                autoBackup: document.getElementById('autoBackup').checked
            };
            
            localStorage.setItem('rifaSettings', JSON.stringify(settings));
            showNotification('Configuración guardada exitosamente');
        }

        // Load settings
        function loadSettings() {
            const settings = JSON.parse(localStorage.getItem('rifaSettings') || '{}');
            
            if (settings.orgName) document.getElementById('orgName').value = settings.orgName;
            if (settings.contactEmail) document.getElementById('contactEmail').value = settings.contactEmail;
            if (settings.currency) document.getElementById('currency').value = settings.currency;
            if (settings.allowDuplicates !== undefined) document.getElementById('allowDuplicates').checked = settings.allowDuplicates;
            if (settings.autoNotifications !== undefined) document.getElementById('autoNotifications').checked = settings.autoNotifications;
            if (settings.autoBackup !== undefined) document.getElementById('autoBackup').checked = settings.autoBackup;
        }

        // Initialize the application
        document.addEventListener('DOMContentLoaded', function() {
            init();
            loadSettings();
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9679d4a7c28ee716',t:'MTc1MzkzMDY3MS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
