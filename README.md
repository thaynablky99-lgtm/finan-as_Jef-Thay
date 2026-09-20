<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Finanças & Metas Família - Thayna & Jeferson</title>

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <!-- Chart.js para os Gráficos -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- SheetJS (XLSX) Completo para Geração e Leitura de Planilhas -->
    <script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        pastel: {
                            blue: '#e0f2fe',
                            blueDark: '#0284c7',
                            green: '#d1fae5',
                            greenDark: '#059669',
                            amber: '#fef3c7',
                            amberDark: '#d97706',
                            rose: '#ffe4e6',
                            roseDark: '#e11d48',
                            bg: '#f8fafc',
                            card: '#ffffff',
                            border: '#e2e8f0',
                            text: '#334155'
                        }
                    }
                }
            }
        }
    </script>
    <style>
        ::-webkit-scrollbar { width: 5px; height: 5px; }
        ::-webkit-scrollbar-track { background: #f8fafc; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
        .tab-content { display: none; }
        .tab-content.active { display: block; }
    </style>
</head>
<body class="bg-slate-50 text-slate-700 font-sans antialiased min-h-screen pb-24 md:pb-6">

    <!-- TOP HEADER -->
    <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="bg-sky-100 text-sky-700 p-2.5 rounded-2xl shadow-sm border border-sky-200">
                    <i class="fa-solid fa-chart-pie text-lg"></i>
                </div>
                <div>
                    <h1 class="font-bold text-slate-800 text-base leading-tight">Finanças & Metas</h1>
                    <p class="text-xs text-slate-400">Thayna & Jeferson • Firebase 🔥</p>
                </div>
            </div>

            <div class="flex items-center space-x-2 text-xs font-bold text-slate-600">
                <span>Painel Principal Família</span>
            </div>
        </div>
    </header>

    <!-- CONTAINER PRINCIPAL -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex flex-col md:flex-row gap-6">

        <!-- NAV LATERAL -->
        <aside class="hidden md:block w-64 shrink-0 bg-white border border-slate-200 rounded-2xl p-4 h-fit shadow-sm space-y-1 text-xs font-semibold text-slate-600">
            <button onclick="switchTab('dashboard')" class="nav-btn w-full text-left py-2.5 px-3 rounded-xl flex items-center gap-3 hover:bg-sky-50 hover:text-sky-700 transition active-tab bg-sky-50 text-sky-700 font-bold" id="btn-dashboard">
                <i class="fa-solid fa-house text-sky-600 w-5"></i> 1. Dashboard & Insights
            </button>
            <button onclick="switchTab('planejamento')" class="nav-btn w-full text-left py-2.5 px-3 rounded-xl flex items-center gap-3 hover:bg-sky-50 hover:text-sky-700 transition" id="btn-planejamento">
                <i class="fa-solid fa-calendar-days text-sky-600 w-5"></i> 2. Planejamento Anual
            </button>
            <button onclick="switchTab('realizado')" class="nav-btn w-full text-left py-2.5 px-3 rounded-xl flex items-center gap-3 hover:bg-sky-50 hover:text-sky-700 transition" id="btn-realizado">
                <i class="fa-solid fa-list-check text-sky-600 w-5"></i> 3. Realizado (Entradas/Saídas)
            </button>
            <button onclick="switchTab('planVsReal')" class="nav-btn w-full text-left py-2.5 px-3 rounded-xl flex items-center gap-3 hover:bg-sky-50 hover:text-sky-700 transition" id="btn-planVsReal">
                <i class="fa-solid fa-scale-balanced text-sky-600 w-5"></i> 4. Planejado VS Realizado
            </button>
            <button onclick="switchTab('recorrentes')" class="nav-btn w-full text-left py-2.5 px-3 rounded-xl flex items-center gap-3 hover:bg-sky-50 hover:text-sky-700 transition" id="btn-recorrentes">
                <i class="fa-solid fa-rotate text-sky-600 w-5"></i> 5. Contas Recorrentes
            </button>
            <button onclick="switchTab('parcelamentos')" class="nav-btn w-full text-left py-2.5 px-3 rounded-xl flex items-center gap-3 hover:bg-sky-50 hover:text-sky-700 transition" id="btn-parcelamentos">
                <i class="fa-solid fa-credit-card text-sky-600 w-5"></i> 6. Parcelamentos & Cartões
            </button>
            <button onclick="switchTab('investimentos')" class="nav-btn w-full text-left py-2.5 px-3 rounded-xl flex items-center gap-3 hover:bg-sky-50 hover:text-sky-700 transition" id="btn-investimentos">
                <i class="fa-solid fa-chart-line text-sky-600 w-5"></i> 7. Investimentos
            </button>
            <button onclick="switchTab('pdca')" class="nav-btn w-full text-left py-2.5 px-3 rounded-xl flex items-center gap-3 hover:bg-sky-50 hover:text-sky-700 transition" id="btn-pdca">
                <i class="fa-solid fa-diagram-project text-sky-600 w-5"></i> 8. Plano PDCA
            </button>
            <button onclick="switchTab('mercado')" class="nav-btn w-full text-left py-2.5 px-3 rounded-xl flex items-center gap-3 hover:bg-sky-50 hover:text-sky-700 transition" id="btn-mercado">
                <i class="fa-solid fa-cart-shopping text-sky-600 w-5"></i> 9. Mercado & Insights
            </button>
            <button onclick="switchTab('desejos')" class="nav-btn w-full text-left py-2.5 px-3 rounded-xl flex items-center gap-3 hover:bg-sky-50 hover:text-sky-700 transition" id="btn-desejos">
                <i class="fa-solid fa-gift text-sky-600 w-5"></i> 10. Lista de Desejos
            </button>
            <button onclick="switchTab('metas')" class="nav-btn w-full text-left py-2.5 px-3 rounded-xl flex items-center gap-3 hover:bg-sky-50 hover:text-sky-700 transition" id="btn-metas">
                <i class="fa-solid fa-bullseye text-sky-600 w-5"></i> 11. Metas do Casal
            </button>
            <button onclick="switchTab('configuracoes')" class="nav-btn w-full text-left py-2.5 px-3 rounded-xl flex items-center gap-3 hover:bg-sky-50 hover:text-sky-700 transition" id="btn-configuracoes">
                <i class="fa-solid fa-gear text-sky-600 w-5"></i> 12. Configurações
            </button>
        </aside>

        <!-- CONTEÚDO PRINCIPAL -->
        <main class="flex-1 space-y-6 min-w-0">

            <!-- TAB 1: DASHBOARD & INSIGHTS -->
            <div id="tab-dashboard" class="tab-content active space-y-6">
                <div class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm flex flex-wrap items-center justify-between gap-3">
                    <h3 class="font-bold text-slate-800 text-sm"><i class="fa-solid fa-house text-sky-600"></i> Dashboard & Insights Unificados</h3>
                    <div class="flex items-center space-x-2">
                        <div class="flex items-center bg-slate-50 rounded-xl px-2.5 py-1 text-xs border border-slate-200">
                            <i class="fa-regular fa-calendar text-sky-600 mr-2"></i>
                            <input type="month" id="filtroMesDash" value="2026-09" onchange="dispararAtualizacaoGeral()" class="bg-transparent font-bold text-slate-700 outline-none">
                        </div>
                    </div>
                </div>

                <div class="grid grid-cols-2 lg:grid-cols-4 gap-3">
                    <div class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm border-l-4 border-l-emerald-400">
                        <span class="text-[10px] font-bold text-slate-400 uppercase">Entradas Totais</span>
                        <h3 class="text-lg md:text-xl font-bold text-emerald-700 mt-1" id="dashEntradas">R$ 0,00</h3>
                        <p class="text-[10px] text-slate-400 mt-1">Salários + Receitas</p>
                    </div>
                    <div class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm border-l-4 border-l-rose-400">
                        <span class="text-[10px] font-bold text-slate-400 uppercase">Gastos Realizados</span>
                        <h3 class="text-lg md:text-xl font-bold text-rose-700 mt-1" id="dashGastos">R$ 0,00</h3>
                        <p class="text-[10px] font-bold text-slate-500 mt-1" id="dashComprometido">0% da Renda</p>
                    </div>
                    <div class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm border-l-4 border-l-sky-400">
                        <span class="text-[10px] font-bold text-slate-400 uppercase">Saldo Livre</span>
                        <h3 class="text-lg md:text-xl font-bold text-sky-800 mt-1" id="dashSaldo">R$ 0,00</h3>
                        <p class="text-[10px] text-slate-400 mt-1">Disponível no Mês</p>
                    </div>
                    <div class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm border-l-4 border-l-amber-400">
                        <span class="text-[10px] font-bold text-slate-400 uppercase">Aportes / Invest.</span>
                        <h3 class="text-lg md:text-xl font-bold text-amber-700 mt-1" id="dashInvest">R$ 0,00</h3>
                        <p class="text-[10px] text-slate-400 mt-1">Patrimônio</p>
                    </div>
                </div>

                <!-- INSIGHTS -->
                <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm space-y-3 bg-gradient-to-br from-amber-50/40 to-white">
                    <h4 class="font-bold text-slate-800 text-xs flex items-center gap-2">
                        <i class="fa-solid fa-lightbulb text-amber-500"></i> Insights Financeiros, Alertas e Oportunidades
                    </h4>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-3 text-xs" id="listaInsightsDashboard">
                        <div class="p-3 bg-amber-50/60 border border-amber-200/60 rounded-xl text-amber-900">Analisando dados do mês...</div>
                    </div>
                </div>

                <!-- 4 GRÁFICOS -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm space-y-3">
                        <h4 class="font-bold text-slate-700 text-xs flex items-center gap-2">
                            <i class="fa-solid fa-chart-pie text-sky-500"></i> Distribuição de Gastos por Categoria (Valor & %)
                        </h4>
                        <div class="h-60 relative flex items-center justify-center">
                            <canvas id="chartPizzaCategorias"></canvas>
                        </div>
                    </div>

                    <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm space-y-3">
                        <h4 class="font-bold text-slate-700 text-xs flex items-center gap-2">
                            <i class="fa-solid fa-chart-column text-sky-500"></i> Entradas vs Saídas Mensais
                        </h4>
                        <div class="h-60 relative">
                            <canvas id="chartBarraEntradasSaidas"></canvas>
                        </div>
                    </div>

                    <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm space-y-3">
                        <h4 class="font-bold text-slate-700 text-xs flex items-center gap-2">
                            <i class="fa-solid fa-chart-line text-emerald-500"></i> Evolução do Saldo Acumulado
                        </h4>
                        <div class="h-60 relative">
                            <canvas id="chartEvolucaoSaldo"></canvas>
                        </div>
                    </div>

                    <div class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm space-y-3">
                        <h4 class="font-bold text-slate-700 text-xs flex items-center gap-2">
                            <i class="fa-solid fa-wallet text-amber-500"></i> Fluxo de Caixa por Forma de Pagamento
                        </h4>
                        <div class="h-60 relative">
                            <canvas id="chartFluxoPagamentos"></canvas>
                        </div>
                    </div>
                </div>
            </div>

            <!-- TAB 2: PLANEJAMENTO ANUAL -->
            <div id="tab-planejamento" class="tab-content space-y-6">
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-4">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between border-b border-slate-100 pb-3 gap-3">
                        <div>
                            <h3 class="font-bold text-slate-800 text-sm">📋 Planejamento Anual por Categoria (Visão em Cards & Replicador)</h3>
                            <p class="text-xs text-slate-400">Abra a categoria para preencher os meses ou use o preenchimento rápido para o ano todo.</p>
                        </div>
                        <div class="flex items-center space-x-2">
                            <div class="flex items-center bg-slate-50 rounded-xl px-2.5 py-1 text-xs border border-slate-200">
                                <span class="text-slate-400 mr-1 font-bold"><i class="fa-solid fa-calendar-alt text-sky-600"></i> Ano:</span>
                                <select id="filtroAnoPlanejamento" onchange="renderPlanejamentoAnualCards(this.value)" class="bg-transparent font-bold text-slate-700 outline-none">
                                    <option value="2026" selected>2026</option>
                                    <option value="2025">2025</option>
                                    <option value="2027">2027</option>
                                </select>
                            </div>
                        </div>
                    </div>

                    <!-- CONTAINER DOS CARDS DE CATEGORIA -->
                    <div id="listaPlanejamentoCards" class="space-y-3"></div>
                </div>
            </div>

            <!-- TAB 3: REALIZADO (ENTRADAS/SAÍDAS) -->
            <div id="tab-realizado" class="tab-content space-y-6">
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-4">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between border-b border-slate-100 pb-3 gap-2">
                        <div>
                            <h3 class="font-bold text-slate-800 text-sm">📋 Lançamentos Realizados no Mês</h3>
                            <p class="text-xs text-slate-400">Gerencie entradas, saídas, parcelas automáticas e upload de planilhas.</p>
                        </div>
                        <div class="flex flex-wrap items-center gap-2">
                            <div class="flex items-center bg-slate-50 rounded-xl px-2.5 py-1 text-xs border border-slate-200">
                                <i class="fa-regular fa-calendar text-sky-600 mr-2"></i>
                                <input type="month" id="filtroMesRealizado" value="2026-09" onchange="sincronizarMesFiltro(this.value)" class="bg-transparent font-bold text-slate-700 outline-none">
                            </div>
                            <button onclick="openModal('modalLançamento')" class="bg-sky-600 hover:bg-sky-700 text-white px-3 py-1.5 rounded-xl text-xs font-bold flex items-center gap-1.5 shadow-sm transition">
                                <i class="fa-solid fa-plus text-sm"></i> Novo Lançamento
                            </button>
                            <button onclick="openModal('modalUploadLancamentos')" class="bg-emerald-600 hover:bg-emerald-700 text-white px-3 py-1.5 rounded-xl text-xs font-bold flex items-center gap-1.5 shadow-sm transition">
                                <i class="fa-solid fa-file-excel"></i> Upload Planilha
                            </button>
                            <button onclick="toggleTabelaRapida('containerTabelaRapidaLanc')" class="bg-amber-500 hover:bg-amber-600 text-white px-3 py-1.5 rounded-xl text-xs font-bold flex items-center gap-1.5 shadow-sm transition">
                                <i class="fa-solid fa-table"></i> Lote
                            </button>
                        </div>
                    </div>

                    <!-- TABELA EM LOTE -->
                    <div id="containerTabelaRapidaLanc" class="hidden p-4 bg-amber-50/50 border border-amber-200 rounded-2xl space-y-3">
                        <div class="flex justify-between items-center">
                            <h4 class="font-bold text-amber-900 text-xs"><i class="fa-solid fa-pen-to-square"></i> Cadastro em Lote (Estilo Planilha)</h4>
                            <button onclick="toggleTabelaRapida('containerTabelaRapidaLanc')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
                        </div>
                        <div class="overflow-x-auto">
                            <table class="w-full text-left text-xs min-w-[700px]">
                                <thead>
                                    <tr class="font-bold text-slate-400 uppercase text-[10px]">
                                        <th class="p-1">Data</th>
                                        <th class="p-1">Tipo</th>
                                        <th class="p-1">Descrição</th>
                                        <th class="p-1">Valor</th>
                                        <th class="p-1">Categoria</th>
                                        <th class="p-1">Pagamento</th>
                                        <th class="p-1">Cartão</th>
                                        <th class="p-1">Compra</th>
                                        <th class="p-1">Parc.</th>
                                        <th class="p-1 text-center">Ação</th>
                                    </tr>
                                </thead>
                                <tbody id="tbodyTabelaRapidaLanc" class="space-y-1"></tbody>
                            </table>
                        </div>
                        <div class="flex justify-between pt-2">
                            <button onclick="addLinhaTabelaLanc()" class="text-sky-700 font-bold text-xs">+ Adicionar Linha</button>
                            <button onclick="salvarTabelaLoteLanc()" class="bg-emerald-600 text-white px-3.5 py-1.5 rounded-xl text-xs font-bold shadow-sm">Salvar Lote no Firebase 🔥</button>
                        </div>
                    </div>

                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse text-xs">
                            <thead>
                                <tr class="font-bold text-slate-400 uppercase border-b border-slate-100 text-[10px]">
                                    <th class="pb-2">Data</th>
                                    <th class="pb-2">Descrição</th>
                                    <th class="pb-2">Categoria</th>
                                    <th class="pb-2">Pagamento</th>
                                    <th class="pb-2 text-right">Valor</th>
                                    <th class="pb-2 text-center">Ações</th>
                                </tr>
                            </thead>
                            <tbody id="listaLançamentos" class="divide-y divide-slate-100">
                                <tr><td colspan="6" class="py-4 text-center text-slate-400">Carregando lançamentos...</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- TAB 4: PLANEJADO VS REALIZADO -->
            <div id="tab-planVsReal" class="tab-content space-y-6">
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-4">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between border-b border-slate-100 pb-3 gap-2">
                        <div>
                            <h3 class="font-bold text-slate-800 text-sm">📊 Planejado VS Realizado (Comparativo Mensal)</h3>
                            <p class="text-xs text-slate-400">Cruzamento automático entre o orçamento planejado e os gastos reais do mês.</p>
                        </div>
                        <div class="flex items-center space-x-2">
                            <div class="flex items-center bg-slate-50 rounded-xl px-2.5 py-1 text-xs border border-slate-200">
                                <i class="fa-regular fa-calendar text-sky-600 mr-2"></i>
                                <input type="month" id="filtroMesPlanReal" value="2026-09" onchange="sincronizarMesFiltro(this.value)" class="bg-transparent font-bold text-slate-700 outline-none">
                            </div>
                        </div>
                    </div>

                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs border-collapse">
                            <thead>
                                <tr class="font-bold text-slate-400 uppercase border-b pb-2 text-[10px]">
                                    <th class="pb-2">Categoria</th>
                                    <th class="pb-2 text-right">Meta Planejada</th>
                                    <th class="pb-2 text-right">Gasto Realizado</th>
                                    <th class="pb-2 text-right">Diferença / Saldo</th>
                                    <th class="pb-2 text-center">Status</th>
                                </tr>
                            </thead>
                            <tbody id="listaPlanVsRealTabela" class="divide-y divide-slate-100 font-medium"></tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- TAB 5: CONTAS RECORRENTES -->
            <div id="tab-recorrentes" class="tab-content space-y-6">
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-4">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between border-b border-slate-100 pb-3 gap-2">
                        <div>
                            <h3 class="font-bold text-slate-800 text-sm">🔁 Contas Recorrentes do Casal</h3>
                            <p class="text-xs text-slate-400">Dê OK para registrar o pagamento no Realizado ou estorne se marcou por engano.</p>
                        </div>
                        <div class="flex items-center space-x-2">
                            <div class="flex items-center bg-slate-50 rounded-xl px-2.5 py-1 text-xs border border-slate-200">
                                <i class="fa-regular fa-calendar text-sky-600 mr-2"></i>
                                <input type="month" id="filtroMesRecorrentes" value="2026-09" onchange="sincronizarMesFiltro(this.value)" class="bg-transparent font-bold text-slate-700 outline-none">
                            </div>
                            <button onclick="openModal('modalRecorrente')" class="bg-sky-600 hover:bg-sky-700 text-white px-3.5 py-1.5 rounded-xl text-xs font-bold shadow-sm transition">➕ Nova</button>
                        </div>
                    </div>
                    <div id="listaRecorrentes" class="space-y-2 text-xs"></div>
                </div>
            </div>

            <!-- TAB 6: PARCELAMENTOS & CARTÕES -->
            <div id="tab-parcelamentos" class="tab-content space-y-6">
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-6">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between border-b border-slate-100 pb-3 gap-2">
                        <div>
                            <h3 class="font-bold text-slate-800 text-sm">💳 Cartões de Crédito & Comprometimento Futuro</h3>
                            <p class="text-xs text-slate-400">Acompanhe limites, metas e o valor exato que cai em cada fatura futura.</p>
                        </div>
                        <div class="flex items-center space-x-2">
                            <div class="flex items-center bg-slate-50 rounded-xl px-2.5 py-1 text-xs border border-slate-200">
                                <span class="text-slate-400 mr-1 font-bold"><i class="fa-solid fa-calendar-alt text-sky-600"></i> Ano Base:</span>
                                <select id="filtroAnoParcelamentos" onchange="renderMatrizParcelamentosGlobal()" class="bg-transparent font-bold text-slate-700 outline-none">
                                    <option value="2026" selected>2026</option>
                                    <option value="2025">2025</option>
                                    <option value="2027">2027</option>
                                </select>
                            </div>
                            <button onclick="openModal('modalConfigCartoes')" class="bg-sky-50 hover:bg-sky-100 text-sky-700 px-3 py-1.5 rounded-xl text-xs font-bold flex items-center gap-1.5 border border-sky-200 transition">
                                <i class="fa-solid fa-gear"></i> Configurar Cartões
                            </button>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4" id="cardsCartoesComLimite"></div>

                    <!-- MATRIZ DE PARCELAMENTOS MÊS A MÊS -->
                    <div class="pt-4 border-t border-slate-100 space-y-3">
                        <h4 class="font-bold text-slate-800 text-xs uppercase flex items-center gap-2">
                            <i class="fa-solid fa-layer-group text-sky-600"></i> Matriz de Comprometimento de Renda Futura (Parcelamentos Ativos)
                        </h4>
                        <div class="overflow-x-auto">
                            <table class="w-full text-left text-xs border-collapse min-w-[1200px]">
                                <thead>
                                    <tr class="font-bold text-slate-400 uppercase border-b text-[10px]">
                                        <th class="pb-2">Descrição</th>
                                        <th class="pb-2">Cartão</th>
                                        <th class="pb-2 text-center">Parcelas</th>
                                        <th class="pb-2 text-right">Vlr. Parcela</th>
                                        <th class="pb-2 text-right">Total Restante</th>
                                        <th class="pb-2 text-center">Jan</th><th class="pb-2 text-center">Fev</th><th class="pb-2 text-center">Mar</th>
                                        <th class="pb-2 text-center">Abr</th><th class="pb-2 text-center">Mai</th><th class="pb-2 text-center">Jun</th>
                                        <th class="pb-2 text-center">Jul</th><th class="pb-2 text-center">Ago</th><th class="pb-2 text-center">Set</th>
                                        <th class="pb-2 text-center">Out</th><th class="pb-2 text-center">Nov</th><th class="pb-2 text-center">Dez</th>
                                        <th class="pb-2 text-center">Status</th>
                                        <th class="pb-2 text-center">Ações</th>
                                    </tr>
                                </thead>
                                <tbody id="listaMatrizParcelamentos" class="divide-y divide-slate-100 font-medium">
                                    <tr><td colspan="19" class="py-4 text-center text-slate-400">Nenhum parcelamento ativo.</td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>

            <!-- TAB 7: INVESTIMENTOS -->
            <div id="tab-investimentos" class="tab-content space-y-6">
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-4">
                    <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                        <h3 class="font-bold text-slate-800 text-sm">📈 Gestão Patrimonial e Aportes</h3>
                        <button onclick="openModal('modalInvestimento')" class="bg-sky-600 hover:bg-sky-700 text-white px-3.5 py-1.5 rounded-xl text-xs font-bold shadow-sm transition">➕ Novo Aporte / Rendimento</button>
                    </div>

                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
                        <div class="p-4 bg-sky-50/50 rounded-2xl border border-sky-100">
                            <span class="text-[10px] text-sky-700 font-bold uppercase">Patrimônio Total</span>
                            <h4 class="text-xl font-bold text-sky-900 mt-1" id="invPatrimonio">R$ 0,00</h4>
                        </div>
                        <div class="p-4 bg-emerald-50/50 rounded-2xl border border-emerald-100">
                            <span class="text-[10px] text-emerald-700 font-bold uppercase">Aporte Mês Atual</span>
                            <h4 class="text-xl font-bold text-emerald-800 mt-1" id="invAporteMes">R$ 0,00</h4>
                        </div>
                        <div class="p-4 bg-amber-50/50 rounded-2xl border border-amber-100">
                            <span class="text-[10px] text-amber-700 font-bold uppercase">Rendimento do Mês</span>
                            <h4 class="text-xl font-bold text-amber-800 mt-1" id="invRendimentoMes">+ R$ 0,00</h4>
                        </div>
                    </div>

                    <div class="pt-3">
                        <h4 class="font-bold text-slate-800 text-xs mb-2">Histórico de Ativos & Investimentos</h4>
                        <div class="overflow-x-auto">
                            <table class="w-full text-left text-xs border-collapse">
                                <thead>
                                    <tr class="font-bold text-slate-400 uppercase border-b text-[10px]">
                                        <th class="pb-2">Data</th>
                                        <th class="pb-2">Tipo</th>
                                        <th class="pb-2">Ativo / Banco</th>
                                        <th class="pb-2 text-right">Valor</th>
                                        <th class="pb-2 text-right">Rendimento</th>
                                        <th class="pb-2 text-center">Ações</th>
                                    </tr>
                                </thead>
                                <tbody id="listaInvestimentosHist" class="divide-y divide-slate-100 font-medium">
                                    <tr><td colspan="6" class="py-4 text-center text-slate-400">Nenhum aporte lançado.</td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>

            <!-- TAB 8: PLANO PDCA -->
            <div id="tab-pdca" class="tab-content space-y-6">
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-4">
                    <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                        <div>
                            <h3 class="font-bold text-slate-800 text-sm">🔄 Ciclo PDCA - Melhoria Contínua & Planos de Ação</h3>
                            <p class="text-xs text-slate-400">Plan (Planejar), Do (Executar), Check (Verificar) e Act (Agir).</p>
                        </div>
                        <button onclick="openModal('modalPDCA')" class="bg-sky-600 hover:bg-sky-700 text-white px-3.5 py-1.5 rounded-xl text-xs font-bold shadow-sm transition">➕ Novo Plano PDCA</button>
                    </div>
                    <div id="listaPDCA" class="space-y-4 text-xs"></div>
                </div>
            </div>

            <!-- TAB 9: MERCADO & INSIGHTS -->
            <div id="tab-mercado" class="tab-content space-y-6">
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-4">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between border-b border-slate-100 pb-3 gap-2">
                        <div>
                            <h3 class="font-bold text-slate-800 text-sm">🛒 Controle de Mercado, Preços & Inflação</h3>
                            <p class="text-xs text-slate-400">Insights automáticos de variação de preços e cadastro de produtos.</p>
                        </div>
                        <div class="flex items-center space-x-2">
                            <button onclick="openModal('modalUploadMercado')" class="bg-emerald-600 hover:bg-emerald-700 text-white px-3 py-1.5 rounded-xl text-xs font-bold flex items-center gap-1.5 shadow-sm transition">
                                <i class="fa-solid fa-file-excel"></i> Upload
                            </button>
                            <button onclick="toggleTabelaRapida('containerTabelaRapidaMercado')" class="bg-amber-500 hover:bg-amber-600 text-white px-3 py-1.5 rounded-xl text-xs font-bold flex items-center gap-1.5 shadow-sm transition">
                                <i class="fa-solid fa-table"></i> Lote
                            </button>
                            <button onclick="openModal('modalItemMercado')" class="bg-sky-600 hover:bg-sky-700 text-white px-3 py-1.5 rounded-xl text-xs font-bold transition">➕ Item</button>
                        </div>
                    </div>

                    <!-- INSIGHTS DE MERCADO NO TOPO -->
                    <div class="p-4 bg-amber-50/50 border border-amber-200 rounded-2xl space-y-2 text-xs text-amber-900" id="boxInsightsMercado">
                        <strong class="font-bold flex items-center gap-1 text-amber-950"><i class="fa-solid fa-lightbulb text-amber-600"></i> Insights Automáticos e Inflação de Mercado:</strong>
                        <ul class="list-disc pl-4 space-y-1 text-[11px]" id="listaInsightsMercado">
                            <li>Carregando histórico e variações de preços...</li>
                        </ul>
                    </div>

                    <div id="containerTabelaRapidaMercado" class="hidden p-4 bg-amber-50/50 border border-amber-200 rounded-2xl space-y-3">
                        <div class="flex justify-between items-center">
                            <h4 class="font-bold text-amber-900 text-xs"><i class="fa-solid fa-pen-to-square"></i> Cadastro em Lote de Produtos</h4>
                            <button onclick="toggleTabelaRapida('containerTabelaRapidaMercado')" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark"></i></button>
                        </div>
                        <div class="overflow-x-auto">
                            <table class="w-full text-left text-xs">
                                <thead>
                                    <tr class="font-bold text-slate-400 uppercase text-[10px]">
                                        <th class="p-1">Data</th>
                                        <th class="p-1">Produto</th>
                                        <th class="p-1">Código</th>
                                        <th class="p-1">Qtd</th>
                                        <th class="p-1">Unidade</th>
                                        <th class="p-1">Vlr. Unit (R$)</th>
                                        <th class="p-1 text-center">Ação</th>
                                    </tr>
                                </thead>
                                <tbody id="tbodyTabelaRapidaMercado" class="space-y-1"></tbody>
                            </table>
                        </div>
                        <div class="flex justify-between pt-2">
                            <button onclick="addLinhaTabelaMercado()" class="text-sky-700 font-bold text-xs">+ Adicionar Item</button>
                            <button onclick="salvarTabelaLoteMercado()" class="bg-emerald-600 text-white px-3.5 py-1.5 rounded-xl text-xs font-bold shadow-sm">Salvar Todos no Firebase 🔥</button>
                        </div>
                    </div>

                    <!-- LANÇAMENTOS DE MERCADO NA PARTE INFERIOR -->
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-xs border-collapse">
                            <thead>
                                <tr class="font-bold text-slate-400 uppercase border-b text-[10px] pb-2">
                                    <th class="pb-2">Data</th>
                                    <th class="pb-2">Produto</th>
                                    <th class="pb-2">Código</th>
                                    <th class="pb-2 text-center">Qtd</th>
                                    <th class="pb-2 text-center">Unidade</th>
                                    <th class="pb-2 text-right">Vlr. Unit.</th>
                                    <th class="pb-2 text-right">Valor Total</th>
                                    <th class="pb-2 text-center">Ações</th>
                                </tr>
                            </thead>
                            <tbody id="listaMercado" class="divide-y divide-slate-100 font-medium"></tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- TAB 10: LISTA DE DESEJOS -->
            <div id="tab-desejos" class="tab-content space-y-6">
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-4">
                    <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                        <div>
                            <h3 class="font-bold text-slate-800 text-sm">🛍️ Lista de Desejos (Regra Automática dos 10% da Renda Livre)</h3>
                            <p class="text-xs text-slate-400">Itens liberados automaticamente quando 10% do Saldo Livre cobrirem o valor.</p>
                        </div>
                        <button onclick="openModal('modalDesejo')" class="bg-sky-600 hover:bg-sky-700 text-white px-3.5 py-1.5 rounded-xl text-xs font-bold shadow-sm transition">➕ Novo Desejo</button>
                    </div>
                    <div id="listaDesejos" class="space-y-2 text-xs"></div>
                </div>
            </div>

            <!-- TAB 11: METAS DO CASAL -->
            <div id="tab-metas" class="tab-content space-y-6">
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-4">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between border-b border-slate-100 pb-3 gap-3">
                        <div class="flex items-center space-x-2">
                            <span class="font-bold text-slate-800 text-sm">🎯 Metas e Objetivos do Casal</span>
                            <select id="filtroAnoMeta" onchange="renderMetas()" class="bg-sky-50 font-bold text-xs rounded-xl px-2.5 py-1 text-sky-800 border border-sky-200">
                                <option value="2026">2026</option>
                                <option value="2025">2025</option>
                                <option value="2027">2027</option>
                            </select>
                        </div>

                        <div class="flex items-center space-x-2">
                            <div class="bg-slate-100 p-1 rounded-xl flex text-xs border border-slate-200">
                                <button onclick="setVisaoMetas('tabela')" id="btnMetaTabela" class="px-3 py-1 rounded-lg font-bold bg-white text-slate-800 shadow-sm">Tabela</button>
                                <button onclick="setVisaoMetas('galeria')" id="btnMetaGaleria" class="px-3 py-1 rounded-lg font-bold text-slate-500">Galeria</button>
                            </div>
                            <button onclick="openModal('modalMeta')" class="bg-sky-600 hover:bg-sky-700 text-white px-3.5 py-1.5 rounded-xl text-xs font-bold flex items-center gap-1 shadow-sm transition">
                                <i class="fa-solid fa-plus"></i> Nova Meta
                            </button>
                        </div>
                    </div>

                    <div id="visaoMetaTabela" class="overflow-x-auto">
                        <table class="w-full text-left text-xs border-collapse">
                            <thead>
                                <tr class="font-bold text-slate-400 uppercase border-b pb-2 text-[10px]">
                                    <th class="w-28 pb-2">Progresso</th>
                                    <th class="pb-2">Nome</th>
                                    <th class="w-20 pb-2 text-center">Realizado</th>
                                    <th class="w-20 pb-2 text-center">Meta</th>
                                    <th class="pb-2">Categoria</th>
                                    <th class="pb-2">Recompensa</th>
                                    <th class="w-20 pb-2 text-center">Ações</th>
                                </tr>
                            </thead>
                            <tbody id="listaMetasTabela" class="divide-y divide-slate-100 font-medium">
                                <tr><td colspan="7" class="py-4 text-center text-slate-400">Carregando metas...</td></tr>
                            </tbody>
                        </table>
                    </div>

                    <div id="visaoMetaGaleria" class="hidden grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"></div>
                </div>
            </div>

            <!-- TAB 12: CONFIGURAÇÕES -->
            <div id="tab-configuracoes" class="tab-content space-y-6">
                <div class="bg-white rounded-2xl border border-slate-200 shadow-sm p-5 space-y-6">
                    <div class="border-b border-slate-100 pb-3">
                        <h3 class="font-bold text-slate-800 text-base">⚙️ Configurações das Listas Suspensas</h3>
                        <p class="text-xs text-slate-400">Gerencie todas as opções que populam os selects do aplicativo em tempo real.</p>
                    </div>

                    <div class="space-y-3">
                        <h4 class="font-bold text-xs text-sky-700 uppercase flex items-center gap-2">
                            <i class="fa-solid fa-arrow-right-arrow-left"></i> 1. Categorias de Lançamentos & Planejamento
                        </h4>
                        <div class="p-4 bg-sky-50/40 border border-sky-100 rounded-2xl space-y-2 text-xs">
                            <div class="flex gap-2">
                                <input type="text" id="addCategoriaInput" placeholder="Nova categoria" class="w-full border rounded-xl p-2 bg-white">
                                <button onclick="addListItem('categorias', 'addCategoriaInput')" class="bg-sky-600 text-white px-3.5 py-1 rounded-xl font-bold shadow-sm">+</button>
                            </div>
                            <ul id="listConfigCategorias" class="divide-y divide-sky-100 pt-2 max-h-36 overflow-y-auto"></ul>
                        </div>
                    </div>

                    <div class="space-y-3 pt-2 border-t border-slate-100">
                        <h4 class="font-bold text-xs text-sky-700 uppercase flex items-center gap-2">
                            <i class="fa-solid fa-credit-card"></i> 2. Formas de Pagamento & Bancos / Cartões
                        </h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-xs">
                            <div class="p-4 bg-sky-50/40 border border-sky-100 rounded-2xl space-y-2">
                                <span class="font-bold text-slate-700 block">Formas de Pagamento</span>
                                <div class="flex gap-2">
                                    <input type="text" id="addPagtoInput" placeholder="Nova forma" class="w-full border rounded-xl p-2 bg-white">
                                    <button onclick="addListItem('pagamentos', 'addPagtoInput')" class="bg-sky-600 text-white px-3.5 py-1 rounded-xl font-bold shadow-sm">+</button>
                                </div>
                                <ul id="listConfigPagamentos" class="divide-y divide-sky-100 pt-2 max-h-36 overflow-y-auto"></ul>
                            </div>
                            <div class="p-4 bg-sky-50/40 border border-sky-100 rounded-2xl space-y-2">
                                <span class="font-bold text-slate-700 block">Bancos / Cartões de Crédito</span>
                                <div class="flex gap-2">
                                    <input type="text" id="addBancoInput" placeholder="Novo banco/cartão" class="w-full border rounded-xl p-2 bg-white">
                                    <button onclick="addListItem('bancos', 'addBancoInput')" class="bg-sky-600 text-white px-3.5 py-1 rounded-xl font-bold shadow-sm">+</button>
                                </div>
                                <ul id="listConfigBancos" class="divide-y divide-sky-100 pt-2 max-h-36 overflow-y-auto"></ul>
                            </div>
                        </div>
                    </div>

                    <div class="space-y-3 pt-2 border-t border-slate-100">
                        <h4 class="font-bold text-xs text-sky-700 uppercase flex items-center gap-2">
                            <i class="fa-solid fa-chart-line"></i> 3. Investimentos & Metas
                        </h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 text-xs">
                            <div class="p-4 bg-sky-50/40 border border-sky-100 rounded-2xl space-y-2">
                                <span class="font-bold text-slate-700 block">Tipos de Ativos / Investimentos</span>
                                <div class="flex gap-2">
                                    <input type="text" id="addAtivoInput" placeholder="Novo ativo" class="w-full border rounded-xl p-2 bg-white">
                                    <button onclick="addListItem('ativos', 'addAtivoInput')" class="bg-sky-600 text-white px-3.5 py-1 rounded-xl font-bold shadow-sm">+</button>
                                </div>
                                <ul id="listConfigAtivos" class="divide-y divide-sky-100 pt-2 max-h-36 overflow-y-auto"></ul>
                            </div>
                            <div class="p-4 bg-sky-50/40 border border-sky-100 rounded-2xl space-y-2">
                                <span class="font-bold text-slate-700 block">Categorias de Metas do Casal</span>
                                <div class="flex gap-2">
                                    <input type="text" id="addMetaCatInput" placeholder="Nova categoria de meta" class="w-full border rounded-xl p-2 bg-white">
                                    <button onclick="addListItem('metaCategorias', 'addMetaCatInput')" class="bg-sky-600 text-white px-3.5 py-1 rounded-xl font-bold shadow-sm">+</button>
                                </div>
                                <ul id="listConfigMetaCat" class="divide-y divide-sky-100 pt-2 max-h-36 overflow-y-auto"></ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

        </main>
    </div>

    <!-- MODAIS -->

    <div id="modalUploadLancamentos" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 space-y-4 shadow-xl">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-sm">📊 Upload de Planilha de Lançamentos</h3>
                <button onclick="closeModal('modalUploadLancamentos')" class="text-slate-400"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div class="text-xs text-slate-600 space-y-3">
                <p>Baixe o modelo pré-formatado para preencher e subir os seus lançamentos:</p>
                <button onclick="baixarModeloExcelLancamentos()" class="w-full bg-emerald-50 hover:bg-emerald-100 text-emerald-800 font-bold py-2.5 px-3 rounded-xl border border-emerald-200 flex items-center justify-center gap-2 shadow-sm transition">
                    <i class="fa-solid fa-download text-emerald-600"></i> Baixar Planilha Modelo (.xlsx)
                </button>
                <div class="pt-2 border-t">
                    <label class="block font-bold text-slate-700 mb-1">Selecione o arquivo:</label>
                    <input type="file" id="fileUploadLancamentosModal" accept=".xlsx, .xls, .csv" class="w-full border p-2 rounded-xl text-xs">
                </div>
            </div>
            <button onclick="importarPlanilhaLancamentosModal()" class="w-full bg-sky-600 hover:bg-sky-700 text-white font-bold py-2.5 rounded-xl shadow-sm transition">Realizar Importação 🔥</button>
        </div>
    </div>

    <div id="modalUploadMercado" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 space-y-4 shadow-xl">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-sm">🛒 Upload de Planilha de Mercado</h3>
                <button onclick="closeModal('modalUploadMercado')" class="text-slate-400"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div class="text-xs text-slate-600 space-y-3">
                <p>Baixe o modelo em Excel com as colunas aceitas para mercado:</p>
                <button onclick="baixarModeloExcelMercado()" class="w-full bg-emerald-50 hover:bg-emerald-100 text-emerald-800 font-bold py-2.5 px-3 rounded-xl border border-emerald-200 flex items-center justify-center gap-2 shadow-sm transition">
                    <i class="fa-solid fa-download text-emerald-600"></i> Baixar Modelo Mercado (.xlsx)
                </button>
                <div class="pt-2 border-t">
                    <label class="block font-bold text-slate-700 mb-1">Selecione o arquivo:</label>
                    <input type="file" id="fileExcelMercadoModal" accept=".xlsx, .xls, .csv" class="w-full border p-2 rounded-xl text-xs">
                </div>
            </div>
            <button onclick="importarExcelMercadoModal()" class="w-full bg-sky-600 hover:bg-sky-700 text-white font-bold py-2.5 rounded-xl shadow-sm transition">Importar Itens 🔥</button>
        </div>
    </div>

    <div id="modalLançamento" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl max-w-lg w-full p-6 space-y-4 shadow-xl max-h-[90vh] overflow-y-auto">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-sm" id="modalLancTitle">➕ Novo Lançamento</h3>
                <button onclick="closeModal('modalLançamento')" class="text-slate-400"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>

            <form id="formLancamento" onsubmit="salvarLancamento(event)" class="space-y-3 text-xs font-medium">
                <input type="hidden" id="lancEditId" value="">
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-slate-600 mb-1">Data</label>
                        <input type="date" id="dataInput" class="w-full border rounded-xl p-2.5 text-slate-800 font-bold" required>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Tipo</label>
                        <select id="tipoInput" class="w-full border rounded-xl p-2.5 text-slate-800 font-bold">
                            <option value="Despesa">💸 Despesa (Saída)</option>
                            <option value="Receita">💰 Receita (Entrada)</option>
                        </select>
                    </div>
                </div>

                <div>
                    <label class="block text-slate-600 mb-1">Descrição</label>
                    <input type="text" id="descInput" placeholder="Ex: Mercado, Salário" class="w-full border rounded-xl p-2.5 text-slate-800" required>
                </div>

                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-slate-600 mb-1">Valor (R$)</label>
                        <input type="number" step="0.01" id="valorInput" placeholder="0,00" class="w-full border rounded-xl p-2.5 font-bold text-slate-800" required>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Categoria (Configurações)</label>
                        <select id="categoriaInput" class="select-dynamic-categorias w-full border rounded-xl p-2.5 text-slate-800 font-bold"></select>
                    </div>
                </div>

                <div>
                    <label class="block text-slate-600 mb-1">Forma de Pagamento</label>
                    <select id="pagamentoInput" onchange="toggleCartaoModal()" class="select-dynamic-pagamentos w-full border rounded-xl p-2.5 text-slate-800 font-bold"></select>
                </div>

                <div id="boxCartaoModal" class="hidden p-3 bg-slate-50 border rounded-xl space-y-2">
                    <label class="block text-slate-600 font-bold">Cartão de Crédito</label>
                    <select id="cartaoInput" class="select-dynamic-bancos w-full border rounded-lg p-2 text-slate-800 font-bold"></select>

                    <div class="grid grid-cols-2 gap-2 pt-2">
                        <div>
                            <label class="block text-slate-600 mb-1">Tipo da Compra</label>
                            <select id="tipoCompraInput" onchange="toggleParcelasBox()" class="w-full border rounded-lg p-2 text-slate-800 font-bold">
                                <option value="À vista">À vista</option>
                                <option value="Parcelada">Parcelada</option>
                            </select>
                        </div>
                        <div id="boxNumParcelas" class="hidden">
                            <label class="block text-slate-600 mb-1">Nº de Parcelas</label>
                            <input type="number" id="numParcelasInput" min="2" max="48" value="2" class="w-full border rounded-lg p-2 font-bold text-slate-800">
                        </div>
                    </div>
                </div>

                <button type="submit" class="w-full bg-sky-600 hover:bg-sky-700 text-white font-bold py-3 rounded-xl shadow-md transition">Salvar Lançamento 🔥</button>
            </form>
        </div>
    </div>

    <div id="modalRecorrente" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 space-y-4 shadow-xl">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-sm" id="modalRecTitle">🔁 Cadastrar Conta Recorrente</h3>
                <button onclick="closeModal('modalRecorrente')" class="text-slate-400"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>

            <form id="formRecorrente" onsubmit="salvarRecorrente(event)" class="space-y-3 text-xs font-medium">
                <input type="hidden" id="recEditId">
                <div>
                    <label class="block text-slate-600 mb-1">Nome da Conta / Serviço</label>
                    <input type="text" id="recNome" placeholder="Ex: Internet, Academia" class="w-full border rounded-xl p-2.5" required>
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-slate-600 mb-1">Valor Fixo (R$)</label>
                        <input type="number" step="0.01" id="recValor" placeholder="100.00" class="w-full border rounded-xl p-2.5 font-bold" required>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Dia Vencimento</label>
                        <input type="number" id="recDia" min="1" max="31" placeholder="Ex: 10" class="w-full border rounded-xl p-2.5 font-bold" required>
                    </div>
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-slate-600 mb-1">Categoria</label>
                        <select id="recCategoria" class="select-dynamic-categorias w-full border rounded-xl p-2.5 font-bold"></select>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Pagamento</label>
                        <select id="recPagamento" class="select-dynamic-pagamentos w-full border rounded-xl p-2.5 font-bold"></select>
                    </div>
                </div>
                <button type="submit" class="w-full bg-sky-600 hover:bg-sky-700 text-white font-bold py-3 rounded-xl shadow-md transition">Salvar Recorrente 🔥</button>
            </form>
        </div>
    </div>

    <div id="modalDesejo" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 space-y-4 shadow-xl">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-sm" id="modalDesejoTitle">🛍️ Novo Item na Lista de Desejos</h3>
                <button onclick="closeModal('modalDesejo')" class="text-slate-400"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>

            <form id="formDesejo" onsubmit="salvarDesejo(event)" class="space-y-3 text-xs font-medium">
                <input type="hidden" id="desejoEditId">
                <div>
                    <label class="block text-slate-600 mb-1">Item Desejado</label>
                    <input type="text" id="desejoItem" placeholder="Ex: Panela Elétrica" class="w-full border rounded-xl p-2.5" required>
                </div>
                <div>
                    <label class="block text-slate-600 mb-1">Valor Estimado (R$)</label>
                    <input type="number" step="0.01" id="desejoValor" placeholder="350.00" class="w-full border rounded-xl p-2.5 font-bold" required>
                </div>
                <button type="submit" class="w-full bg-sky-600 hover:bg-sky-700 text-white font-bold py-3 rounded-xl shadow-md transition">Salvar Desejo 🔥</button>
            </form>
        </div>
    </div>

    <div id="modalConfigCartoes" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 space-y-4 shadow-xl">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-sm">💳 Configurar Limites, Metas e Datas</h3>
                <button onclick="closeModal('modalConfigCartoes')" class="text-slate-400"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>

            <form id="formConfigCartao" onsubmit="salvarConfigCartao(event)" class="space-y-3 text-xs font-medium">
                <div>
                    <label class="block text-slate-600 mb-1">Cartão / Banco (Configurações)</label>
                    <select id="cfgCartaoNome" class="select-dynamic-bancos w-full border rounded-xl p-2.5 font-bold"></select>
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-slate-600 mb-1">Limite Total (R$)</label>
                        <input type="number" step="0.01" id="cfgCartaoLimite" placeholder="5000.00" class="w-full border rounded-xl p-2.5 font-bold" required>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Meta de Gasto (R$)</label>
                        <input type="number" step="0.01" id="cfgCartaoMeta" placeholder="2500.00" class="w-full border rounded-xl p-2.5 font-bold" required>
                    </div>
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-slate-600 mb-1">Dia Fechamento</label>
                        <input type="number" id="cfgCartaoFechamento" min="1" max="31" placeholder="28" class="w-full border rounded-xl p-2.5 font-bold" required>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Dia Vencimento</label>
                        <input type="number" id="cfgCartaoVencimento" min="1" max="31" placeholder="05" class="w-full border rounded-xl p-2.5 font-bold" required>
                    </div>
                </div>
                <button type="submit" class="w-full bg-sky-600 hover:bg-sky-700 text-white font-bold py-3 rounded-xl shadow-md transition">Salvar Configuração 🔥</button>
            </form>
        </div>
    </div>

    <div id="modalItemMercado" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 space-y-4 shadow-xl">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-sm">🛒 Cadastrar Item de Mercado</h3>
                <button onclick="closeModal('modalItemMercado')" class="text-slate-400"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>

            <form id="formMercado" onsubmit="salvarItemMercado(event)" class="space-y-3 text-xs font-medium">
                <div>
                    <label class="block text-slate-600 mb-1">Data da Compra</label>
                    <input type="date" id="mercData" class="w-full border rounded-xl p-2.5 font-bold" required>
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-slate-600 mb-1">Nome do Produto</label>
                        <input type="text" id="mercProduto" placeholder="Ex: Arroz, Leite" class="w-full border rounded-xl p-2.5" required>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Código do Produto</label>
                        <input type="text" id="mercCodigo" placeholder="Ex: 789102" class="w-full border rounded-xl p-2.5" required>
                    </div>
                </div>
                <div class="grid grid-cols-3 gap-2">
                    <div>
                        <label class="block text-slate-600 mb-1">Quantidade</label>
                        <input type="number" id="mercQtd" value="1" min="1" class="w-full border rounded-xl p-2.5 font-bold" required>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Unidade</label>
                        <select id="mercUnidade" class="w-full border rounded-xl p-2.5 font-bold">
                            <option value="UN">UN</option>
                            <option value="KG">KG</option>
                            <option value="L">L</option>
                            <option value="PCT">PCT</option>
                            <option value="CX">CX</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Vlr. Unit. (R$)</label>
                        <input type="number" step="0.01" id="mercValor" placeholder="0.00" class="w-full border rounded-xl p-2.5 font-bold" required>
                    </div>
                </div>
                <button type="submit" class="w-full bg-sky-600 hover:bg-sky-700 text-white font-bold py-3 rounded-xl shadow-md transition">Salvar Item 🔥</button>
            </form>
        </div>
    </div>

    <div id="modalPDCAUpdate" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 space-y-4 shadow-xl">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-sm">🔄 Atualizar Monitoramento PDCA</h3>
                <button onclick="closeModal('modalPDCAUpdate')" class="text-slate-400"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>

            <form id="formPDCAUpdate" onsubmit="salvarPDCAUpdate(event)" class="space-y-3 text-xs font-medium">
                <input type="hidden" id="pdcaUpdateId">
                <div>
                    <label class="block text-slate-600 mb-1 font-bold">DO (Execução)</label>
                    <textarea id="pdcaDoText" rows="2" class="w-full border rounded-xl p-2"></textarea>
                </div>
                <div>
                    <label class="block text-slate-600 mb-1 font-bold">CHECK (Checagem)</label>
                    <textarea id="pdcaCheckText" rows="2" class="w-full border rounded-xl p-2"></textarea>
                </div>
                <div>
                    <label class="block text-slate-600 mb-1 font-bold">ACT (Ação Corretiva)</label>
                    <textarea id="pdcaActText" rows="2" class="w-full border rounded-xl p-2"></textarea>
                </div>
                <div>
                    <label class="block text-slate-600 mb-1">Status</label>
                    <select id="pdcaUpdateStatus" class="w-full border rounded-xl p-2.5 font-bold">
                        <option value="🟡 Em andamento">🟡 Em andamento</option>
                        <option value="🟢 Meta atingida">🟢 Meta atingida</option>
                        <option value="🔴 Não atingida">🔴 Não atingida</option>
                    </select>
                </div>
                <button type="submit" class="w-full bg-sky-600 hover:bg-sky-700 text-white font-bold py-3 rounded-xl shadow-md transition">Salvar Atualização 🔥</button>
            </form>
        </div>
    </div>

    <div id="modalInvestimento" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 space-y-4 shadow-xl">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-sm">📈 Novo Aporte ou Rendimento</h3>
                <button onclick="closeModal('modalInvestimento')" class="text-slate-400"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>

            <form id="formInvestimento" onsubmit="salvarInvestimento(event)" class="space-y-3 text-xs font-medium">
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-slate-600 mb-1">Data</label>
                        <input type="date" id="invData" class="w-full border rounded-xl p-2.5 font-bold" required>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Tipo</label>
                        <select id="invTipo" class="w-full border rounded-xl p-2.5 font-bold">
                            <option value="Aporte">🟢 Aporte</option>
                            <option value="Rendimento">📈 Rendimento</option>
                            <option value="Resgate">🔴 Resgate</option>
                        </select>
                    </div>
                </div>
                <div>
                    <label class="block text-slate-600 mb-1">Ativo (Configurações)</label>
                    <select id="invAtivo" class="select-dynamic-ativos w-full border rounded-xl p-2.5 font-bold"></select>
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-slate-600 mb-1">Valor (R$)</label>
                        <input type="number" step="0.01" id="invValor" placeholder="0.00" class="w-full border rounded-xl p-2.5 font-bold" required>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Rendimento (R$)</label>
                        <input type="number" step="0.01" id="invRendimento" placeholder="0.00" class="w-full border rounded-xl p-2.5 font-bold">
                    </div>
                </div>
                <button type="submit" class="w-full bg-sky-600 hover:bg-sky-700 text-white font-bold py-3 rounded-xl shadow-md transition">Salvar Investimento 🔥</button>
            </form>
        </div>
    </div>

    <div id="modalMeta" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 space-y-4 shadow-xl">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-sm" id="modalMetaTitle">🎯 Cadastrar Nova Meta</h3>
                <button onclick="closeModal('modalMeta')" class="text-slate-400"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>

            <form id="formMeta" onsubmit="salvarMeta(event)" class="space-y-3 text-xs font-medium">
                <input type="hidden" id="metaEditId">
                <div>
                    <label class="block text-slate-600 mb-1">Nome da Meta</label>
                    <input type="text" id="metaNome" placeholder="Ex: Viagem, Reserva" class="w-full border rounded-xl p-2.5" required>
                </div>
                <div class="grid grid-cols-3 gap-2">
                    <div>
                        <label class="block text-slate-600 mb-1">Realizado</label>
                        <input type="number" id="metaRealizado" value="0" class="w-full border rounded-xl p-2.5 font-bold" required>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Meta Alvo</label>
                        <input type="number" id="metaAlvo" placeholder="50" class="w-full border rounded-xl p-2.5 font-bold" required>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Ano</label>
                        <select id="metaAno" class="w-full border rounded-xl p-2.5 font-bold">
                            <option value="2026">2026</option>
                            <option value="2025">2025</option>
                            <option value="2027">2027</option>
                        </select>
                    </div>
                </div>
                <div>
                    <label class="block text-slate-600 mb-1">Categoria (Configurações)</label>
                    <select id="metaCategoria" class="select-dynamic-metacat w-full border rounded-xl p-2.5 font-bold"></select>
                </div>
                <div>
                    <label class="block text-slate-600 mb-1">Recompensa</label>
                    <input type="text" id="metaRecompensa" placeholder="Ex: Jantar especial" class="w-full border rounded-xl p-2.5">
                </div>
                <button type="submit" class="w-full bg-sky-600 hover:bg-sky-700 text-white font-bold py-3 rounded-xl shadow-md transition">Salvar Meta 🔥</button>
            </form>
        </div>
    </div>

    <div id="modalPDCA" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 space-y-4 shadow-xl">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-sm">🔄 Novo Plano PDCA</h3>
                <button onclick="closeModal('modalPDCA')" class="text-slate-400"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>

            <form id="formPDCA" onsubmit="salvarPDCA(event)" class="space-y-3 text-xs font-medium">
                <div>
                    <label class="block text-slate-600 mb-1">Título do Plano</label>
                    <input type="text" id="pdcaTitulo" placeholder="Ex: Reduzir Delivery" class="w-full border rounded-xl p-2.5" required>
                </div>
                <div>
                    <label class="block text-slate-600 mb-1">Ação (Plan)</label>
                    <input type="text" id="pdcaAcao" placeholder="Cozinhar em casa" class="w-full border rounded-xl p-2.5" required>
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-slate-600 mb-1">Meta (R$)</label>
                        <input type="number" id="pdcaMeta" placeholder="200" class="w-full border rounded-xl p-2.5" required>
                    </div>
                    <div>
                        <label class="block text-slate-600 mb-1">Prazo</label>
                        <input type="month" id="pdcaPrazo" value="2026-10" class="w-full border rounded-xl p-2.5" required>
                    </div>
                </div>
                <button type="submit" class="w-full bg-sky-600 hover:bg-sky-700 text-white font-bold py-3 rounded-xl shadow-md transition">Criar Plano PDCA 🔥</button>
            </form>
        </div>
    </div>

    <!-- FIREBASE & SCRIPT DE LÓGICA -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getFirestore, collection, addDoc, onSnapshot, query, orderBy, deleteDoc, doc, updateDoc, serverTimestamp, writeBatch } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

        const firebaseConfig = {
            apiKey: "AIzaSyCGdf0mBimkX3sJ0_EAxbGkI6cIlH_ylz4",
            authDomain: "financas-thayna-jeferson.firebaseapp.com",
            projectId: "financas-thayna-jeferson",
            storageBucket: "financas-thayna-jeferson.firebasestorage.app",
            messagingSenderId: "448022589635",
            appId: "1:448022589635:web:51d81e5d04ccee92a9b276"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        window.firebaseDbInstance = db;

        document.getElementById('dataInput').value = new Date().toISOString().split('T')[0];
        document.getElementById('invData').value = new Date().toISOString().split('T')[0];
        document.getElementById('mercData').value = new Date().toISOString().split('T')[0];

        window.sincronizarMesFiltro = function(val) {
            document.getElementById('filtroMesDash').value = val;
            document.getElementById('filtroMesRealizado').value = val;
            document.getElementById('filtroMesPlanReal').value = val;
            document.getElementById('filtroMesRecorrentes').value = val;
            if(window.cacheLancamentosGlobal) {
                processarDadosGerais(window.cacheLancamentosGlobal);
            }
        };

        window.dispararAtualizacaoGeral = function() {
            const val = document.getElementById('filtroMesDash').value;
            window.sincronizarMesFiltro(val);
        };

        window.salvarLancamento = async function(e) {
            e.preventDefault();
            const editId = document.getElementById('lancEditId').value;
            const pagamento = document.getElementById('pagamentoInput').value;
            const tipoCompra = pagamento === 'Crédito' ? document.getElementById('tipoCompraInput').value : 'À vista';
            const numParcelas = tipoCompra === 'Parcelada' ? parseInt(document.getElementById('numParcelasInput').value) || 1 : 1;

            const dataObj = {
                data: document.getElementById('dataInput').value,
                tipo: document.getElementById('tipoInput').value,
                descricao: document.getElementById('descInput').value,
                valor: parseFloat(document.getElementById('valorInput').value),
                categoria: document.getElementById('categoriaInput').value,
                pagamento: pagamento,
                cartao: pagamento === 'Crédito' ? document.getElementById('cartaoInput').value : '-',
                tipoCompra: tipoCompra,
                numParcelas: numParcelas
            };

            if(editId) {
                await updateDoc(doc(db, "lancamentos", editId), dataObj);
            } else {
                dataObj.criadoEm = serverTimestamp();
                await addDoc(collection(db, "lancamentos"), dataObj);
            }

            document.getElementById('formLancamento').reset();
            document.getElementById('lancEditId').value = '';
            closeModal('modalLançamento');
        };

        window.excluirLancamento = async function(id) {
            if(confirm("Excluir este lançamento?")) await deleteDoc(doc(db, "lancamentos", id));
        };

        window.carregarLancamentoParaEdicao = function(item, id) {
            document.getElementById('lancEditId').value = id;
            document.getElementById('dataInput').value = item.data;
            document.getElementById('tipoInput').value = item.tipo;
            document.getElementById('descInput').value = item.descricao;
            document.getElementById('valorInput').value = item.valor;
            document.getElementById('categoriaInput').value = item.categoria;
            document.getElementById('pagamentoInput').value = item.pagamento;
            if(item.pagamento === 'Crédito') {
                document.getElementById('cartaoInput').value = item.cartao;
                document.getElementById('tipoCompraInput').value = item.tipoCompra || 'À vista';
                document.getElementById('numParcelasInput').value = item.numParcelas || 1;
            }
            toggleCartaoModal();
            openModal('modalLançamento');
        };

        window.salvarTabelaLoteLanc = async function() {
            const rows = document.querySelectorAll('#tbodyTabelaRapidaLanc tr');
            let count = 0;
            for(const tr of rows) {
                const desc = tr.querySelector('.row-desc').value;
                const val = parseFloat(tr.querySelector('.row-valor').value);
                if(desc && !isNaN(val)) {
                    const pag = tr.querySelector('.row-pag').value;
                    const isCred = pag === 'Crédito';
                    const tcompra = isCred ? tr.querySelector('.row-tcompra').value : 'À vista';
                    const parc = isCred && tcompra === 'Parcelada' ? parseInt(tr.querySelector('.row-parc').value) || 1 : 1;
                    await addDoc(collection(db, "lancamentos"), {
                        data: tr.querySelector('.row-data').value,
                        tipo: tr.querySelector('.row-tipo').value,
                        descricao: desc,
                        valor: val,
                        categoria: tr.querySelector('.row-cat').value,
                        pagamento: pag,
                        cartao: isCred ? tr.querySelector('.row-cartao').value : '-',
                        tipoCompra: tcompra,
                        numParcelas: parc,
                        criadoEm: serverTimestamp()
                    });
                    count++;
                }
            }
            if(count > 0) {
                alert(`${count} lançamentos salvos com sucesso!`);
                toggleTabelaRapida('containerTabelaRapidaLanc');
            }
        };

        window.cacheLancamentosGlobal = [];

        onSnapshot(query(collection(db, "lancamentos"), orderBy("data", "desc")), (snapshot) => {
            window.cacheLancamentosGlobal = [];
            snapshot.forEach(docSnap => {
                window.cacheLancamentosGlobal.push({ id: docSnap.id, ...docSnap.data() });
            });
            processarDadosGerais(window.cacheLancamentosGlobal);
        });

        function processarDadosGerais(lancamentos) {
            const tbody = document.getElementById('listaLançamentos');
            if(!tbody) return;
            tbody.innerHTML = '';
            let totalE = 0, totalG = 0;
            const catMap = {};
            const parcelamentosArr = [];
            const gastosPorCartao = {};
            const historicoMensal = {};
            const fluxoPagamentos = {};

            const periodoRealizado = document.getElementById('filtroMesRealizado').value;

            lancamentos.forEach(item => {
                const mesAno = item.data ? item.data.substring(0, 7) : '';

                if(mesAno) {
                    if(!historicoMensal[mesAno]) historicoMensal[mesAno] = { entradas: 0, saidas: 0 };
                    if(item.tipo === 'Receita') historicoMensal[mesAno].entradas += item.valor;
                    else historicoMensal[mesAno].saidas += item.valor;
                }

                if(item.tipo === 'Despesa') {
                    fluxoPagamentos[item.pagamento] = (fluxoPagamentos[item.pagamento] || 0) + item.valor;
                    if(item.pagamento === 'Crédito' && item.cartao !== '-') {
                        gastosPorCartao[item.cartao] = (gastosPorCartao[item.cartao] || 0) + item.valor;
                    }
                }

                const numP = parseInt(item.numParcelas) || 1;
                if((item.pagamento === 'Crédito' || item.tipoCompra === 'Parcelada') && numP > 1) {
                    parcelamentosArr.push(item);
                }

                if(item.data && item.data.startsWith(periodoRealizado)) {
                    if(item.tipo === 'Receita') totalE += item.valor;
                    else {
                        totalG += item.valor;
                        catMap[item.categoria] = (catMap[item.categoria] || 0) + item.valor;
                    }

                    const tr = document.createElement('tr');
                    tr.innerHTML = `
                        <td class="py-2.5 font-bold text-slate-500">${item.data.split('-').reverse().join('/')}</td>
                        <td class="py-2.5 font-bold text-slate-800">${item.descricao} ${numP > 1 ? `<span class="text-[10px] bg-sky-50 text-sky-700 px-1.5 py-0.5 rounded ml-1 font-bold border border-sky-200">${numP}x</span>` : ''}</td>
                        <td class="py-2.5"><span class="bg-sky-50 text-sky-800 px-2.5 py-1 rounded-xl text-[10px] font-bold border border-sky-200">${item.categoria}</span></td>
                        <td class="py-2.5 text-slate-500">${item.pagamento} ${item.cartao !== '-' ? `(${item.cartao})` : ''}</td>
                        <td class="py-2.5 text-right font-bold ${item.tipo === 'Receita' ? 'text-emerald-700' : 'text-slate-800'}">
                            ${item.tipo === 'Receita' ? '+' : '-'} R$ ${item.valor.toFixed(2)}
                        </td>
                        <td class="py-2.5 text-center space-x-1">
                            <button onclick='carregarLancamentoParaEdicao(${JSON.stringify(item)}, "${item.id}")' class="text-sky-600 hover:text-sky-900 font-bold"><i class="fa-solid fa-pen"></i></button>
                            <button onclick="excluirLancamento('${item.id}')" class="text-rose-500 hover:text-rose-700 font-bold"><i class="fa-solid fa-trash"></i></button>
                        </td>
                    `;
                    tbody.appendChild(tr);
                }
            });

            document.getElementById('dashEntradas').innerText = `R$ ${totalE.toFixed(2)}`;
            document.getElementById('dashGastos').innerText = `R$ ${totalG.toFixed(2)}`;
            const saldoLivre = totalE - totalG;
            document.getElementById('dashSaldo').innerText = `R$ ${saldoLivre.toFixed(2)}`;
            const pctComprometida = totalE > 0 ? ((totalG / totalE) * 100).toFixed(1) : 0;
            document.getElementById('dashComprometido').innerText = `${pctComprometida}% da Renda`;

            renderCharts(totalE, totalG, catMap, historicoMensal, fluxoPagamentos);
            renderMatrizParcelamentos(parcelamentosArr, gastosPorCartao);
            renderPlanVsReal(catMap);
            renderDesejosComStatusAuto(saldoLivre);
            renderDashboardInsights(totalE, totalG, pctComprometida, catMap);
        }

        // RECORRENTES
        window.salvarRecorrente = async function(e) {
            e.preventDefault();
            const editId = document.getElementById('recEditId').value;
            const dataObj = {
                nome: document.getElementById('recNome').value,
                valor: parseFloat(document.getElementById('recValor').value),
                dia: parseInt(document.getElementById('recDia').value)
            };
            if(editId) {
                await updateDoc(doc(db, "recorrentes", editId), dataObj);
            } else {
                dataObj.criadoEm = serverTimestamp();
                await addDoc(collection(db, "recorrentes"), dataObj);
            }
            document.getElementById('formRecorrente').reset();
            document.getElementById('recEditId').value = '';
            document.getElementById('modalRecTitle').innerText = '🔁 Cadastrar Conta Recorrente';
            closeModal('modalRecorrente');
        };

        window.excluirRecorrente = async function(id) {
            if(confirm("Remover esta conta recorrente?")) await deleteDoc(doc(db, "recorrentes", id));
        };

        window.carregarRecorrenteEdicao = function(item, id) {
            document.getElementById('recEditId').value = id;
            document.getElementById('recNome').value = item.nome;
            document.getElementById('recValor').value = item.valor;
            document.getElementById('recDia').value = item.dia;
            document.getElementById('modalRecTitle').innerText = '✏️ Editar Conta Recorrente';
            openModal('modalRecorrente');
        };

        window.pagarRecorrente = async function(nome, valor) {
            const periodo = document.getElementById('filtroMesRecorrentes').value;
            const dataPagamento = `${periodo}-${String(10).padStart(2, '0')}`;
            const docRef = await addDoc(collection(db, "lancamentos"), {
                data: dataPagamento, tipo: 'Despesa', descricao: `Recorrente: ${nome}`, valor: valor, categoria: 'Moradia/Contas', pagamento: 'Pix / Débito', cartao: '-', tipoCompra: 'À vista', numParcelas: 1, criadoEm: serverTimestamp()
            });
            localStorage.setItem(`rec_lanc_id_${nome}_${periodo}`, docRef.id);
            localStorage.setItem(`rec_paga_${nome}_${periodo}`, 'true');
            renderRecorrentesCards();
        };

        window.estornarRecorrente = async function(nome) {
            const periodo = document.getElementById('filtroMesRecorrentes').value;
            const lancId = localStorage.getItem(`rec_lanc_id_${nome}_${periodo}`);
            if(lancId) {
                try { await deleteDoc(doc(db, "lancamentos", lancId)); } catch(err) { console.log(err); }
            }
            localStorage.removeItem(`rec_paga_${nome}_${periodo}`);
            localStorage.removeItem(`rec_lanc_id_${nome}_${periodo}`);
            renderRecorrentesCards();
        };

        window.recorrentesCache = [];
        onSnapshot(collection(db, "recorrentes"), (snapshot) => {
            window.recorrentesCache = [];
            snapshot.forEach(docSnap => window.recorrentesCache.push({ id: docSnap.id, ...docSnap.data() }));
            renderRecorrentesCards();
        });

        window.renderRecorrentesCards = function() {
            const container = document.getElementById('listaRecorrentes');
            if(!container) return;
            container.innerHTML = '';
            const periodo = document.getElementById('filtroMesRecorrentes').value;

            if(window.recorrentesCache.length === 0) {
                container.innerHTML = '<div class="text-slate-400 py-4 text-center">Nenhuma conta recorrente cadastrada.</div>';
                return;
            }

            window.recorrentesCache.forEach(item => {
                const foiPaga = localStorage.getItem(`rec_paga_${item.nome}_${periodo}`) === 'true';
                const div = document.createElement('div');
                div.className = "p-3 bg-white border border-slate-200 rounded-2xl flex items-center justify-between shadow-sm";
                div.innerHTML = `
                    <div class="space-y-0.5">
                        <strong class="text-slate-800 text-sm">${item.nome}</strong>
                        <p class="text-slate-400 text-[11px]">Vencimento: Dia ${item.dia} | Valor: <strong>R$ ${item.valor.toFixed(2)}</strong></p>
                    </div>
                    <div class="flex items-center gap-2">
                        ${foiPaga ? 
                            `<button onclick="estornarRecorrente('${item.nome}')" class="bg-emerald-50 text-emerald-800 font-bold px-3 py-1.5 rounded-xl text-xs border border-emerald-200 hover:bg-rose-50 hover:text-rose-700 hover:border-rose-200 transition" title="Desfazer pagamento">
                                ✅ Pago (Desfazer)
                            </button>` : 
                            `<button onclick="pagarRecorrente('${item.nome}', ${item.valor})" class="bg-sky-600 text-white font-bold px-3 py-1.5 rounded-xl text-xs hover:bg-sky-700 shadow-sm transition">
                                <i class="fa-solid fa-check"></i> Dar OK / Pagar
                            </button>`
                        }
                        <button onclick='carregarRecorrenteEdicao(${JSON.stringify(item)}, "${item.id}")' class="text-sky-600 p-2 font-bold hover:bg-sky-50 rounded-xl"><i class="fa-solid fa-pen"></i></button>
                        <button onclick="excluirRecorrente('${item.id}')" class="text-rose-500 p-2 font-bold hover:bg-rose-50 rounded-xl"><i class="fa-solid fa-trash"></i></button>
                    </div>
                `;
                container.appendChild(div);
            });
        };

        // DESEJOS
        window.desejosCache = [];
        window.salvarDesejo = async function(e) {
            e.preventDefault();
            const editId = document.getElementById('desejoEditId').value;
            const itemObj = { item: document.getElementById('desejoItem').value, valor: parseFloat(document.getElementById('desejoValor').value) };
            if(editId) await updateDoc(doc(db, "desejos", editId), itemObj);
            else { itemObj.criadoEm = serverTimestamp(); await addDoc(collection(db, "desejos"), itemObj); }
            document.getElementById('formDesejo').reset();
            document.getElementById('desejoEditId').value = '';
            document.getElementById('modalDesejoTitle').innerText = '🛍️ Novo Item na Lista de Desejos';
            closeModal('modalDesejo');
        };

        window.excluirDesejo = async function(id) { if(confirm("Excluir desejo?")) await deleteDoc(doc(db, "desejos", id)); };
        window.carregarDesejoParaEdicao = function(item, id) {
            document.getElementById('desejoEditId').value = id;
            document.getElementById('desejoItem').value = item.item;
            document.getElementById('desejoValor').value = item.valor;
            document.getElementById('modalDesejoTitle').innerText = '✏️ Editar Item na Lista de Desejos';
            openModal('modalDesejo');
        };

        onSnapshot(collection(db, "desejos"), (snapshot) => {
            window.desejosCache = [];
            snapshot.forEach(docSnap => window.desejosCache.push({ id: docSnap.id, ...docSnap.data() }));
            const saldoLivre = parseFloat(document.getElementById('dashSaldo').innerText.replace('R$', '').replace('.', '').replace(',', '.')) || 0;
            renderDesejosComStatusAuto(saldoLivre);
        });

        function renderDesejosComStatusAuto(saldoLivre) {
            const container = document.getElementById('listaDesejos');
            if(!container) return;
            container.innerHTML = '';
            const margem10 = saldoLivre * 0.10;

            if(window.desejosCache.length === 0) {
                container.innerHTML = '<div class="text-slate-400 py-4 text-center">Nenhum desejo cadastrado.</div>';
                return;
            }

            window.desejosCache.forEach(d => {
                const liberado = margem10 >= d.valor;
                const div = document.createElement('div');
                div.className = "p-3 border rounded-2xl flex justify-between items-center bg-white shadow-sm";
                div.innerHTML = `
                    <div>
                        <strong class="block text-slate-800">${d.item}</strong>
                        <span class="text-slate-500 font-bold">R$ ${d.valor.toFixed(2)}</span>
                    </div>
                    <div class="flex items-center gap-2">
                        <span class="${liberado ? 'bg-emerald-50 text-emerald-800 border border-emerald-200' : 'bg-rose-50 text-rose-800 border border-rose-200'} font-bold px-2.5 py-1 rounded-xl text-[10px]">
                            ${liberado ? '🟢 Liberado (10%)' : '🔴 Aguardando Saldo'}
                        </span>
                        <button onclick='carregarDesejoParaEdicao(${JSON.stringify(d)}, "${d.id}")' class="text-sky-600 font-bold"><i class="fa-solid fa-pen"></i></button>
                        <button onclick="excluirDesejo('${d.id}')" class="text-rose-500 font-bold"><i class="fa-solid fa-trash"></i></button>
                    </div>
                `;
                container.appendChild(div);
            });
        }

        // MERCADO
        window.salvarItemMercado = async function(e) {
            e.preventDefault();
            await addDoc(collection(db, "mercado"), {
                data: document.getElementById('mercData').value,
                produto: document.getElementById('mercProduto').value,
                codigo: document.getElementById('mercCodigo').value,
                qtd: parseInt(document.getElementById('mercQtd').value),
                unidade: document.getElementById('mercUnidade').value,
                valor: parseFloat(document.getElementById('mercValor').value),
                criadoEm: serverTimestamp()
            });
            document.getElementById('formMercado').reset();
            closeModal('modalItemMercado');
        };

        window.excluirItemMercado = async function(id) { if(confirm("Remover item?")) await deleteDoc(doc(db, "mercado", id)); };

        onSnapshot(query(collection(db, "mercado"), orderBy("data", "desc")), (snapshot) => {
            const tbody = document.getElementById('listaMercado');
            if(!tbody) return;
            tbody.innerHTML = '';
            const produtosHist = {};
            const listaItens = [];

            snapshot.forEach(docSnap => {
                const item = docSnap.data();
                listaItens.push({ id: docSnap.id, ...item });
                if(!produtosHist[item.produto]) produtosHist[item.produto] = [];
                produtosHist[item.produto].push({ data: item.data, valor: item.valor });
            });

            if(listaItens.length === 0) {
                tbody.innerHTML = '<tr><td colspan="8" class="py-4 text-center text-slate-400">Nenhum item de mercado cadastrado.</td></tr>';
            } else {
                listaItens.forEach(item => {
                    const total = item.qtd * item.valor;
                    const tr = document.createElement('tr');
                    tr.innerHTML = `
                        <td class="py-2 font-bold text-slate-500">${item.data.split('-').reverse().join('/')}</td>
                        <td class="py-2 font-bold text-slate-800">${item.produto}</td>
                        <td class="py-2 text-slate-500">${item.codigo || '-'}</td>
                        <td class="py-2 text-center">${item.qtd}</td>
                        <td class="py-2 text-center">${item.unidade || 'UN'}</td>
                        <td class="py-2 text-right">R$ ${item.valor.toFixed(2)}</td>
                        <td class="py-2 text-right font-bold text-slate-800">R$ ${total.toFixed(2)}</td>
                        <td class="py-2 text-center">
                            <button onclick="excluirItemMercado('${item.id}')" class="text-rose-500 font-bold"><i class="fa-solid fa-trash"></i></button>
                        </td>
                    `;
                    tbody.appendChild(tr);
                });
            }

            renderInsightsMercado(produtosHist);
        });

        function renderInsightsMercado(produtosHist) {
            const ul = document.getElementById('listaInsightsMercado');
            if(!ul) return;
            ul.innerHTML = '';
            const insights = [];

            for(const [prod, historico] of Object.entries(produtosHist)) {
                if(historico.length >= 2) {
                    historico.sort((a,b) => new Date(a.data) - new Date(b.data));
                    const primeiro = historico[0].valor;
                    const ultimo = historico[historico.length - 1].valor;
                    const variacao = (((ultimo - primeiro) / primeiro) * 100).toFixed(1);
                    if(variacao > 0) {
                        insights.push(`<li>⚠️ O produto <strong>${prod}</strong> subiu <strong>${variacao}%</strong> desde a primeira compra (R$ ${primeiro.toFixed(2)} ➔ R$ ${ultimo.toFixed(2)}).</li>`);
                    } else if(variacao < 0) {
                        insights.push(`<li>🟢 O produto <strong>${prod}</strong> registrou queda de <strong>${Math.abs(variacao)}%</strong> no preço.</li>`);
                    }
                }
            }

            if(insights.length === 0) {
                ul.innerHTML = '<li>Cadastre compras do mesmo produto em datas diferentes para gerar insights automáticos de inflação.</li>';
            } else {
                insights.forEach(li => ul.innerHTML += li);
            }
        }

        // INVESTIMENTOS
        window.salvarInvestimento = async function(e) {
            e.preventDefault();
            await addDoc(collection(db, "investimentos"), {
                data: document.getElementById('invData').value,
                tipo: document.getElementById('invTipo').value,
                ativo: document.getElementById('invAtivo').value,
                valor: parseFloat(document.getElementById('invValor').value),
                rendimento: parseFloat(document.getElementById('invRendimento').value) || 0,
                criadoEm: serverTimestamp()
            });
            document.getElementById('formInvestimento').reset();
            closeModal('modalInvestimento');
        };

        window.excluirInvestimento = async function(id) { if(confirm("Excluir investimento?")) await deleteDoc(doc(db, "investimentos", id)); };

        onSnapshot(query(collection(db, "investimentos"), orderBy("data", "desc")), (snapshot) => {
            const tbody = document.getElementById('listaInvestimentosHist');
            if(!tbody) return;
            tbody.innerHTML = '';
            let totalAporte = 0, totalRendimento = 0, totalPatrimonio = 0;

            snapshot.forEach(docSnap => {
                const item = docSnap.data();
                if(item.tipo === 'Aporte') { totalAporte += item.valor; totalPatrimonio += item.valor; }
                else if(item.tipo === 'Resgate') totalPatrimonio -= item.valor;
                totalRendimento += item.rendimento || 0;

                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td class="py-2.5 font-bold text-slate-500">${item.data.split('-').reverse().join('/')}</td>
                    <td class="py-2.5"><span class="bg-sky-50 text-sky-800 px-2.5 py-1 rounded-xl text-[10px] font-bold border border-sky-200">${item.tipo}</span></td>
                    <td class="py-2.5 font-bold text-slate-800">${item.ativo}</td>
                    <td class="py-2.5 text-right font-bold text-slate-800">R$ ${item.valor.toFixed(2)}</td>
                    <td class="py-2.5 text-right font-bold text-emerald-700">+ R$ ${(item.rendimento || 0).toFixed(2)}</td>
                    <td class="py-2.5 text-center">
                        <button onclick="excluirInvestimento('${docSnap.id}')" class="text-rose-500 font-bold"><i class="fa-solid fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);
            });

            document.getElementById('invPatrimonio').innerText = `R$ ${(totalPatrimonio + totalRendimento).toFixed(2)}`;
            document.getElementById('invAporteMes').innerText = `R$ ${totalAporte.toFixed(2)}`;
            document.getElementById('invRendimentoMes').innerText = `+ R$ ${totalRendimento.toFixed(2)}`;
            document.getElementById('dashInvest').innerText = `R$ ${(totalPatrimonio + totalRendimento).toFixed(2)}`;
        });

        // METAS
        window.metasCache = [];
        window.salvarMeta = async function(e) {
            e.preventDefault();
            const editId = document.getElementById('metaEditId').value;
            const metaObj = {
                nome: document.getElementById('metaNome').value,
                realizado: parseFloat(document.getElementById('metaRealizado').value),
                alvo: parseFloat(document.getElementById('metaAlvo').value),
                ano: document.getElementById('metaAno').value,
                categoria: document.getElementById('metaCategoria').value,
                recompensa: document.getElementById('metaRecompensa').value || '-'
            };
            if(editId) {
                await updateDoc(doc(db, "metas", editId), metaObj);
            } else {
                metaObj.criadoEm = serverTimestamp();
                await addDoc(collection(db, "metas"), metaObj);
            }
            document.getElementById('formMeta').reset();
            document.getElementById('metaEditId').value = '';
            document.getElementById('modalMetaTitle').innerText = '🎯 Cadastrar Nova Meta';
            closeModal('modalMeta');
        };

        window.excluirMeta = async function(id) { if(confirm("Excluir meta?")) await deleteDoc(doc(db, "metas", id)); };
        window.carregarMetaEdicao = function(item, id) {
            document.getElementById('metaEditId').value = id;
            document.getElementById('metaNome').value = item.nome;
            document.getElementById('metaRealizado').value = item.realizado;
            document.getElementById('metaAlvo').value = item.alvo;
            document.getElementById('metaAno').value = item.ano;
            document.getElementById('metaCategoria').value = item.categoria;
            document.getElementById('metaRecompensa').value = item.recompensa;
            document.getElementById('modalMetaTitle').innerText = '✏️ Editar Meta do Casal';
            openModal('modalMeta');
        };

        onSnapshot(collection(db, "metas"), (snapshot) => {
            window.metasCache = [];
            snapshot.forEach(docSnap => window.metasCache.push({ id: docSnap.id, ...docSnap.data() }));
            renderMetas();
        });

        // PDCA
        window.salvarPDCA = async function(e) {
            e.preventDefault();
            await addDoc(collection(db, "pdca"), {
                titulo: document.getElementById('pdcaTitulo').value,
                plan: document.getElementById('pdcaAcao').value,
                meta: parseFloat(document.getElementById('pdcaMeta').value),
                prazo: document.getElementById('pdcaPrazo').value,
                do_text: "Em execução...", check_text: "Pendente...", act_text: "Aguardando...",
                status: "🟡 Em andamento",
                criadoEm: serverTimestamp()
            });
            document.getElementById('formPDCA').reset();
            closeModal('modalPDCA');
        };

        window.abrirModalPDCAUpdate = function(id) { document.getElementById('pdcaUpdateId').value = id; openModal('modalPDCAUpdate'); };
        window.salvarPDCAUpdate = async function(e) {
            e.preventDefault();
            const id = document.getElementById('pdcaUpdateId').value;
            await updateDoc(doc(db, "pdca", id), {
                do_text: document.getElementById('pdcaDoText').value,
                check_text: document.getElementById('pdcaCheckText').value,
                act_text: document.getElementById('pdcaActText').value,
                status: document.getElementById('pdcaUpdateStatus').value
            });
            closeModal('modalPDCAUpdate');
        };
        window.excluirPDCA = async function(id) { if(confirm("Excluir PDCA?")) await deleteDoc(doc(db, "pdca", id)); };

        onSnapshot(collection(db, "pdca"), (snapshot) => {
            const container = document.getElementById('listaPDCA');
            if(!container) return;
            container.innerHTML = '';
            if(snapshot.empty) {
                container.innerHTML = '<div class="text-slate-400 py-4 text-center">Nenhum plano PDCA cadastrado.</div>';
                return;
            }
            snapshot.forEach(docSnap => {
                const item = docSnap.data();
                const card = document.createElement('div');
                card.className = "p-4 bg-white border rounded-2xl space-y-2 shadow-sm";
                card.innerHTML = `
                    <div class="flex justify-between font-bold text-sm">
                        <span>${item.titulo}</span>
                        <div class="flex items-center gap-2">
                            <span class="bg-amber-50 border border-amber-200 text-amber-800 px-2.5 py-0.5 rounded-xl text-xs">${item.status}</span>
                            <button onclick="excluirPDCA('${docSnap.id}')" class="text-rose-500 font-bold"><i class="fa-solid fa-trash"></i></button>
                        </div>
                    </div>
                    <p class="text-slate-600"><strong>P (Plan):</strong> ${item.plan}</p>
                    <p class="text-slate-600"><strong>D (Do):</strong> ${item.do_text || '-'}</p>
                    <p class="text-slate-600"><strong>C (Check):</strong> ${item.check_text || '-'}</p>
                    <p class="text-slate-600"><strong>A (Act):</strong> ${item.act_text || '-'}</p>
                    <div class="text-[10px] text-slate-400 flex justify-between items-center pt-2 border-t">
                        <span>Meta: ≤ R$ ${item.meta} | Prazo: ${item.prazo}</span>
                        <button onclick="abrirModalPDCAUpdate('${docSnap.id}')" class="text-sky-700 font-bold hover:underline">
                            <i class="fa-solid fa-pen"></i> Atualizar DO / CHECK / ACT
                        </button>
                    </div>
                `;
                container.appendChild(card);
            });
        });
    </script>

    <!-- CONFIGS, EXCEL E UI -->
    <script>
        window.configListas = JSON.parse(localStorage.getItem('configListas')) || {
            categorias: ['Mercado', 'Moradia/Contas', 'Combustível', 'Lazer', 'Salário Thayna', 'Salário Jeferson', 'Aporte Investimentos', 'Educação'],
            pagamentos: ['Pix / Débito', 'Crédito', 'VA / VR'],
            bancos: ['Inter Thayna', 'Inter Jeferson', 'Santander Thayna', 'Santander Jeferson', 'Itaú Thayna'],
            ativos: ['Tesouro Selic', 'Ações', 'Fundos Imobiliários', 'CDB Inter'],
            metaCategorias: ['Finanças', 'Relacionamentos e Vida Social', 'Carreira/Profissional', 'Lazer e Hobbies', 'Saúde e Bem Estar', 'Educação e Conhecimento']
        };

        window.configCartoesLimites = JSON.parse(localStorage.getItem('configCartoesLimites')) || {
            'Inter Thayna': { limite: 5000, meta: 2500, fechamento: 28, vencimento: 5 },
            'Inter Jeferson': { limite: 5000, meta: 2500, fechamento: 2, vencimento: 10 },
            'Santander Thayna': { limite: 8000, meta: 3500, fechamento: 8, vencimento: 15 },
            'Santander Jeferson': { limite: 8000, meta: 3500, fechamento: 12, vencimento: 20 },
            'Itaú Thayna': { limite: 6000, meta: 3000, fechamento: 18, vencimento: 25 }
        };

        window.planejamentoMatriz = JSON.parse(localStorage.getItem('planejamentoMatrizV2') || localStorage.getItem('planejamentoMatriz') || '{}');
        
        function normalizarPlanejamento() {
            const keys = Object.keys(window.planejamentoMatriz || {});
            const pareceAntigo = keys.some(k => Array.isArray(window.planejamentoMatriz[k]));
            if (pareceAntigo) {
                window.planejamentoMatriz = { '2026': window.planejamentoMatriz };
                localStorage.setItem('planejamentoMatrizV2', JSON.stringify(window.planejamentoMatriz));
            }
            if (!window.planejamentoMatriz || typeof window.planejamentoMatriz !== 'object') window.planejamentoMatriz = {};
        }
        normalizarPlanejamento();

        function getPlanejado(cat, mesIndex, ano) {
            const y = String(ano || document.getElementById('filtroAnoPlanejamento')?.value || '2026');
            if(!window.planejamentoMatriz[y]) window.planejamentoMatriz[y] = {};
            if(!Array.isArray(window.planejamentoMatriz[y][cat])) {
                window.planejamentoMatriz[y][cat] = new Array(12).fill(0);
            }
            return window.planejamentoMatriz[y][cat][mesIndex] || 0;
        }

        window.setPlanejado = function(cat, mesIndex, val, ano) {
            const y = String(ano || document.getElementById('filtroAnoPlanejamento')?.value || '2026');
            if(!window.planejamentoMatriz[y]) window.planejamentoMatriz[y] = {};
            if(!Array.isArray(window.planejamentoMatriz[y][cat])) {
                window.planejamentoMatriz[y][cat] = new Array(12).fill(0);
            }
            window.planejamentoMatriz[y][cat][mesIndex] = parseFloat(val) || 0;
            localStorage.setItem('planejamentoMatrizV2', JSON.stringify(window.planejamentoMatriz));
        };

        window.replicarCategoriaAno = function(cat, ano) {
            const y = String(ano || document.getElementById('filtroAnoPlanejamento')?.value || '2026');
            if(!window.planejamentoMatriz[y]) window.planejamentoMatriz[y] = {};
            const primeiroMesVal = window.planejamentoMatriz[y][cat]?.[0] || 0;
            window.planejamentoMatriz[y][cat] = new Array(12).fill(primeiroMesVal);
            localStorage.setItem('planejamentoMatrizV2', JSON.stringify(window.planejamentoMatriz));
            renderPlanejamentoAnualCards(y);
        };

        window.renderPlanejamentoAnualCards = function(anoParam) {
            const ano = anoParam || document.getElementById('filtroAnoPlanejamento')?.value || '2026';
            const container = document.getElementById('listaPlanejamentoCards');
            if(!container) return;
            container.innerHTML = '';
            const meses = ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'];
            
            window.configListas.categorias.forEach((cat, idx) => {
                const cardId = `plan-card-${idx}`;
                const div = document.createElement('div');
                div.className = "border border-slate-200 rounded-2xl bg-white shadow-sm overflow-hidden";
                
                let inputsHTML = '';
                meses.forEach((m, mIdx) => {
                    const val = getPlanejado(cat, mIdx, ano);
                    inputsHTML += `
                        <div class="space-y-1">
                            <label class="text-[10px] font-bold text-slate-500">${m}</label>
                            <input type="number" step="0.01" value="${val}" onchange="setPlanejado('${cat}', ${mIdx}, this.value, '${ano}')" class="w-full border rounded-xl p-2 text-xs font-bold text-slate-700 bg-slate-50 focus:bg-white">
                        </div>
                    `;
                });

                div.innerHTML = `
                    <div class="p-4 bg-slate-50 border-b border-slate-100 flex items-center justify-between cursor-pointer" onclick="document.getElementById('${cardId}').classList.toggle('hidden')">
                        <div class="flex items-center gap-2">
                            <i class="fa-solid fa-folder-open text-sky-600"></i>
                            <span class="font-bold text-slate-800 text-xs">${cat}</span>
                        </div>
                        <div class="flex items-center gap-2">
                            <button type="button" onclick="event.stopPropagation(); replicarCategoriaAno('${cat}', '${ano}')" class="text-[10px] bg-sky-100 text-sky-700 font-bold px-2.5 py-1 rounded-xl border border-sky-200 hover:bg-sky-200 transition">Replicar Janeiro p/ Ano Todo</button>
                            <i class="fa-solid fa-chevron-down text-slate-400 text-xs"></i>
                        </div>
                    </div>
                    <div id="${cardId}" class="p-4 grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-3 hidden">
                        ${inputsHTML}
                    </div>
                `;
                container.appendChild(div);
            });
        };

        window.switchTab = function(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.remove('active'));
            document.querySelectorAll('.nav-btn').forEach(el => {
                el.classList.remove('bg-sky-50', 'text-sky-700', 'font-bold');
            });
            document.getElementById('tab-' + tabId)?.classList.add('active');
            document.getElementById('btn-' + tabId)?.classList.add('bg-sky-50', 'text-sky-700', 'font-bold');
        };

        window.openModal = function(id) { document.getElementById(id)?.classList.remove('hidden'); };
        window.closeModal = function(id) { document.getElementById(id)?.classList.add('hidden'); };

        window.toggleTabelaRapida = function(id) {
            const el = document.getElementById(id);
            if(el) {
                el.classList.toggle('hidden');
                if(!el.classList.contains('hidden') && id === 'containerTabelaRapidaLanc') {
                    if(document.getElementById('tbodyTabelaRapidaLanc').children.length === 0) {
                        addLinhaTabelaLanc();
                    }
                }
                if(!el.classList.contains('hidden') && id === 'containerTabelaRapidaMercado') {
                    if(document.getElementById('tbodyTabelaRapidaMercado').children.length === 0) {
                        addLinhaTabelaMercado();
                    }
                }
            }
        };

        window.addLinhaTabelaLanc = function() {
            const tbody = document.getElementById('tbodyTabelaRapidaLanc');
            const tr = document.createElement('tr');
            tr.innerHTML = `
                <td class="p-1"><input type="date" value="${new Date().toISOString().split('T')[0]}" class="row-data border rounded p-1 w-28 text-xs"></td>
                <td class="p-1"><select class="row-tipo border rounded p-1 text-xs"><option value="Despesa">Despesa</option><option value="Receita">Receita</option></select></td>
                <td class="p-1"><input type="text" placeholder="Descrição" class="row-desc border rounded p-1 w-full text-xs"></td>
                <td class="p-1"><input type="number" step="0.01" placeholder="0.00" class="row-valor border rounded p-1 w-20 text-xs"></td>
                <td class="p-1"><select class="row-cat border rounded p-1 text-xs select-dynamic-categorias"></select></td>
                <td class="p-1"><select class="row-pag border rounded p-1 text-xs select-dynamic-pagamentos" onchange="this.closest('tr').querySelector('.row-cartao').disabled = (this.value !== 'Crédito')"></select></td>
                <td class="p-1"><select class="row-cartao border rounded p-1 text-xs select-dynamic-bancos" disabled></select></td>
                <td class="p-1"><select class="row-tcompra border rounded p-1 text-xs"><option value="À vista">À vista</option><option value="Parcelada">Parcelada</option></select></td>
                <td class="p-1"><input type="number" value="1" min="1" class="row-parc border rounded p-1 w-12 text-xs"></td>
                <td class="p-1 text-center"><button type="button" onclick="this.closest('tr').remove()" class="text-rose-500 font-bold"><i class="fa-solid fa-trash"></i></button></td>
            `;
            tbody.appendChild(tr);
            atualizarSelectsDinamicos();
        };

        window.addLinhaTabelaMercado = function() {
            const tbody = document.getElementById('tbodyTabelaRapidaMercado');
            const tr = document.createElement('tr');
            tr.innerHTML = `
                <td class="p-1"><input type="date" value="${new Date().toISOString().split('T')[0]}" class="merc-data border rounded p-1 text-xs"></td>
                <td class="p-1"><input type="text" placeholder="Produto" class="merc-prod border rounded p-1 w-full text-xs"></td>
                <td class="p-1"><input type="text" placeholder="Código" class="merc-cod border rounded p-1 w-20 text-xs"></td>
                <td class="p-1"><input type="number" value="1" min="1" class="merc-qtd border rounded p-1 w-12 text-xs"></td>
                <td class="p-1"><select class="merc-un border rounded p-1 text-xs"><option value="UN">UN</option><option value="KG">KG</option><option value="L">L</option><option value="PCT">PCT</option><option value="CX">CX</option></select></td>
                <td class="p-1"><input type="number" step="0.01" placeholder="0.00" class="merc-vlr border rounded p-1 w-20 text-xs"></td>
                <td class="p-1 text-center"><button type="button" onclick="this.closest('tr').remove()" class="text-rose-500 font-bold"><i class="fa-solid fa-trash"></i></button></td>
            `;
            tbody.appendChild(tr);
        };

        window.salvarTabelaLoteMercado = async function() {
            const rows = document.querySelectorAll('#tbodyTabelaRapidaMercado tr');
            let count = 0;
            for(const tr of rows) {
                const prod = tr.querySelector('.merc-prod').value;
                const vlr = parseFloat(tr.querySelector('.merc-vlr').value);
                if(prod && !isNaN(vlr)) {
                    await window.firebaseDbInstance ? addDoc(collection(window.firebaseDbInstance, "mercado"), {
                        data: tr.querySelector('.merc-data').value,
                        produto: prod,
                        codigo: tr.querySelector('.merc-cod').value,
                        qtd: parseInt(tr.querySelector('.merc-qtd').value) || 1,
                        unidade: tr.querySelector('.merc-un').value,
                        valor: vlr,
                        criadoEm: serverTimestamp()
                    }) : null;
                    count++;
                }
            }
            if(count > 0) {
                alert(`${count} itens de mercado salvos com sucesso!`);
                toggleTabelaRapida('containerTabelaRapidaMercado');
            }
        };

        window.atualizarSelectsDinamicos = function() {
            const categorias = window.configListas.categorias || [];
            const pagamentos = window.configListas.pagamentos || [];
            const bancos = window.configListas.bancos || [];
            const ativos = window.configListas.ativos || [];
            const metaCats = window.configListas.metaCategorias || [];

            document.querySelectorAll('.select-dynamic-categorias').forEach(sel => {
                const val = sel.value;
                sel.innerHTML = categorias.map(c => `<option value="${c}">${c}</option>`).join('');
                if(val) sel.value = val;
            });
            document.querySelectorAll('.select-dynamic-pagamentos').forEach(sel => {
                const val = sel.value;
                sel.innerHTML = pagamentos.map(p => `<option value="${p}">${p}</option>`).join('');
                if(val) sel.value = val;
            });
            document.querySelectorAll('.select-dynamic-bancos').forEach(sel => {
                const val = sel.value;
                sel.innerHTML = bancos.map(b => `<option value="${b}">${b}</option>`).join('');
                if(val) sel.value = val;
            });
            document.querySelectorAll('.select-dynamic-ativos').forEach(sel => {
                const val = sel.value;
                sel.innerHTML = ativos.map(a => `<option value="${a}">${a}</option>`).join('');
                if(val) sel.value = val;
            });
            document.querySelectorAll('.select-dynamic-metacat').forEach(sel => {
                const val = sel.value;
                sel.innerHTML = metaCats.map(m => `<option value="${m}">${m}</option>`).join('');
                if(val) sel.value = val;
            });

            renderConfigListUI('categorias', 'listConfigCategorias');
            renderConfigListUI('pagamentos', 'listConfigPagamentos');
            renderConfigListUI('bancos', 'listConfigBancos');
            renderConfigListUI('ativos', 'listConfigAtivos');
            renderConfigListUI('metaCategorias', 'listConfigMetaCat');
        };

        window.renderConfigListUI = function(tipo, elementId) {
            const ul = document.getElementById(elementId);
            if(!ul) return;
            ul.innerHTML = '';
            (window.configListas[tipo] || []).forEach((item, idx) => {
                const li = document.createElement('li');
                li.className = "flex justify-between items-center py-1 text-slate-700";
                li.innerHTML = `
                    <span>${item}</span>
                    <button onclick="removeListItem('${tipo}', ${idx})" class="text-rose-500 hover:text-rose-700"><i class="fa-solid fa-trash text-xs"></i></button>
                `;
                ul.appendChild(li);
            });
        };

        window.addListItem = function(tipo, inputId) {
            const val = document.getElementById(inputId).value.trim();
            if(val) {
                if(!window.configListas[tipo]) window.configListas[tipo] = [];
                window.configListas[tipo].push(val);
                localStorage.setItem('configListas', JSON.stringify(window.configListas));
                document.getElementById(inputId).value = '';
                atualizarSelectsDinamicos();
            }
        };

        window.removeListItem = function(tipo, idx) {
            window.configListas[tipo].splice(idx, 1);
            localStorage.setItem('configListas', JSON.stringify(window.configListas));
            atualizarSelectsDinamicos();
        };

        window.toggleCartaoModal = function() {
            const pag = document.getElementById('pagamentoInput').value;
            const box = document.getElementById('boxCartaoModal');
            if(pag === 'Crédito') box.classList.remove('hidden');
            else box.classList.add('hidden');
        };

        window.toggleParcelasBox = function() {
            const tipo = document.getElementById('tipoCompraInput').value;
            const box = document.getElementById('boxNumParcelas');
            if(tipo === 'Parcelada') box.classList.remove('hidden');
            else box.classList.add('hidden');
        };

        window.baixarModeloExcelLancamentos = function() {
            const ws = XLSX.utils.json_to_sheet([
                { Data: "2026-09-01", Tipo: "Despesa", Descricao: "Supermercado", Valor: 150.50, Categoria: "Mercado", Pagamento: "Crédito", Cartao: "Inter Thayna", TipoCompra: "À vista", NumParcelas: 1 }
            ]);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, "Lancamentos");
            XLSX.writeFile(wb, "Modelo_Lancamentos.xlsx");
        };

        window.baixarModeloExcelMercado = function() {
            const ws = XLSX.utils.json_to_sheet([
                { Data: "2026-09-01", Produto: "Arroz 5kg", Codigo: "789102", Qtd: 1, Unidade: "UN", ValorUnitario: 29.90 }
            ]);
            const wb = XLSX.utils.book_new();
            XLSX.utils.book_append_sheet(wb, ws, "Mercado");
            XLSX.writeFile(wb, "Modelo_Mercado.xlsx");
        };

        window.importarPlanilhaLancamentosModal = function() {
            const fileInput = document.getElementById('fileUploadLancamentosModal');
            if(!fileInput.files[0]) { alert("Selecione um arquivo primeiro."); return; }
            const reader = new FileReader();
            reader.onload = async function(e) {
                try {
                    const data = new Uint8Array(e.target.result);
                    const workbook = XLSX.read(data, {type: 'array'});
                    const firstSheet = workbook.SheetNames[0];
                    const rows = XLSX.utils.sheet_to_json(workbook.Sheets[firstSheet]);
                    let count = 0;
                    for(const r of rows) {
                        await addDoc(collection(window.firebaseDbInstance, "lancamentos"), {
                            data: r.Data || new Date().toISOString().split('T')[0],
                            tipo: r.Tipo || 'Despesa',
                            descricao: r.Descricao || 'Importado',
                            valor: parseFloat(r.Valor) || 0,
                            categoria: r.Categoria || 'Mercado',
                            pagamento: r.Pagamento || 'Pix / Débito',
                            cartao: r.Cartao || '-',
                            tipoCompra: r.TipoCompra || 'À vista',
                            numParcelas: parseInt(r.NumParcelas) || 1,
                            criadoEm: serverTimestamp()
                        });
                        count++;
                    }
                    alert(`${count} lançamentos importados com sucesso!`);
                    closeModal('modalUploadLancamentos');
                } catch(err) {
                    alert("Erro ao importar planilha: " + err.message);
                }
            };
            reader.readAsArrayBuffer(fileInput.files[0]);
        };

        window.importarExcelMercadoModal = function() {
            const fileInput = document.getElementById('fileExcelMercadoModal');
            if(!fileInput.files[0]) { alert("Selecione um arquivo primeiro."); return; }
            const reader = new FileReader();
            reader.onload = async function(e) {
                try {
                    const data = new Uint8Array(e.target.result);
                    const workbook = XLSX.read(data, {type: 'array'});
                    const firstSheet = workbook.SheetNames[0];
                    const rows = XLSX.utils.sheet_to_json(workbook.Sheets[firstSheet]);
                    let count = 0;
                    for(const r of rows) {
                        await addDoc(collection(window.firebaseDbInstance, "mercado"), {
                            data: r.Data || new Date().toISOString().split('T')[0],
                            produto: r.Produto || 'Produto',
                            codigo: r.Codigo || '',
                            qtd: parseInt(r.Qtd) || 1,
                            unidade: r.Unidade || 'UN',
                            valor: parseFloat(r.ValorUnitario || r.Valor) || 0,
                            criadoEm: serverTimestamp()
                        });
                        count++;
                    }
                    alert(`${count} itens de mercado importados com sucesso!`);
                    closeModal('modalUploadMercado');
                } catch(err) {
                    alert("Erro ao importar mercado: " + err.message);
                }
            };
            reader.readAsArrayBuffer(fileInput.files[0]);
        };

        let chartPizza = null, chartBarra = null, chartEvolucao = null, chartFluxo = null;
        function renderCharts(totalE, totalG, catMap, historicoMensal, fluxoPagamentos) {
            const ctxPizza = document.getElementById('chartPizzaCategorias')?.getContext('2d');
            if(ctxPizza) {
                if(chartPizza) chartPizza.destroy();
                const labels = Object.keys(catMap);
                const data = Object.values(catMap);
                chartPizza = new Chart(ctxPizza, {
                    type: 'doughnut',
                    data: {
                        labels: labels,
                        datasets: [{ data: data, backgroundColor: ['#0284c7', '#059669', '#d97706', '#e11d48', '#8b5cf6', '#ec4899', '#14b8a6', '#f59e0b'] }]
                    },
                    options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'bottom', labels: { boxWidth: 12, font: { size: 10 } } } } }
                });
            }

            const ctxBarra = document.getElementById('chartBarraEntradasSaidas')?.getContext('2d');
            if(ctxBarra) {
                if(chartBarra) chartBarra.destroy();
                const meses = Object.keys(historicoMensal).sort();
                const ent = meses.map(m => historicoMensal[m].entradas);
                const sai = meses.map(m => historicoMensal[m].saidas);
                chartBarra = new Chart(ctxBarra, {
                    type: 'bar',
                    data: {
                        labels: meses,
                        datasets: [
                            { label: 'Entradas', data: ent, backgroundColor: '#059669' },
                            { label: 'Saídas', data: sai, backgroundColor: '#e11d48' }
                        ]
                    },
                    options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'bottom', labels: { boxWidth: 12, font: { size: 10 } } } } }
                });
            }

            const ctxEvolucao = document.getElementById('chartEvolucaoSaldo')?.getContext('2d');
            if(ctxEvolucao) {
                if(chartEvolucao) chartEvolucao.destroy();
                const meses = Object.keys(historicoMensal).sort();
                let acumulado = 0;
                const saldos = meses.map(m => {
                    acumulado += (historicoMensal[m].entradas - historicoMensal[m].saidas);
                    return acumulado;
                });
                chartEvolucao = new Chart(ctxEvolucao, {
                    type: 'line',
                    data: {
                        labels: meses,
                        datasets: [{ label: 'Saldo Acumulado', data: saldos, borderColor: '#0284c7', backgroundColor: 'rgba(2, 132, 199, 0.1)', fill: true, tension: 0.3 }]
                    },
                    options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'bottom', labels: { boxWidth: 12, font: { size: 10 } } } } }
                });
            }

            const ctxFluxo = document.getElementById('chartFluxoPagamentos')?.getContext('2d');
            if(ctxFluxo) {
                if(chartFluxo) chartFluxo.destroy();
                const labels = Object.keys(fluxoPagamentos);
                const data = Object.values(fluxoPagamentos);
                chartFluxo = new Chart(ctxFluxo, {
                    type: 'pie',
                    data: {
                        labels: labels,
                        datasets: [{ data: data, backgroundColor: ['#f59e0b', '#0284c7', '#10b981', '#6366f1'] }]
                    },
                    options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'bottom', labels: { boxWidth: 12, font: { size: 10 } } } } }
                });
            }
        }

        function renderMatrizParcelamentos(parcelamentos, gastosCartao) {
            const tbody = document.getElementById('listaMatrizParcelamentos');
            if(!tbody) return;
            tbody.innerHTML = '';
            if(parcelamentos.length === 0) {
                tbody.innerHTML = '<tr><td colspan="19" class="py-4 text-center text-slate-400">Nenhum parcelamento ativo encontrado.</td></tr>';
                return;
            }
            parcelamentos.forEach(p => {
                const tr = document.createElement('tr');
                const vlrParcela = p.valor / (p.numParcelas || 1);
                let mesesTD = '';
                for(let i=1; i<=12; i++) {
                    mesesTD += `<td class="text-center py-2 text-[11px]">R$ ${vlrParcela.toFixed(0)}</td>`;
                }
                tr.innerHTML = `
                    <td class="py-2.5 font-bold text-slate-800">${p.descricao}</td>
                    <td class="py-2.5">${p.cartao}</td>
                    <td class="py-2.5 text-center">${p.numParcelas}x</td>
                    <td class="py-2.5 text-right font-bold">R$ ${vlrParcela.toFixed(2)}</td>
                    <td class="py-2.5 text-right font-bold text-rose-700">R$ ${p.valor.toFixed(2)}</td>
                    ${mesesTD}
                    <td class="py-2.5 text-center"><span class="bg-amber-50 text-amber-800 px-2 py-0.5 rounded text-[10px] font-bold border border-amber-200">Ativo</span></td>
                    <td class="py-2.5 text-center"><button onclick="excluirLancamento('${p.id}')" class="text-rose-500"><i class="fa-solid fa-trash"></i></button></td>
                `;
                tbody.appendChild(tr);
            });
        }

        function renderMatrizParcelamentosGlobal() {}

        function renderPlanVsReal(catMap) {
            const tbody = document.getElementById('listaPlanVsRealTabela');
            if(!tbody) return;
            tbody.innerHTML = '';
            const ano = document.getElementById('filtroAnoPlanejamento')?.value || '2026';
            const mesStr = document.getElementById('filtroMesPlanReal')?.value || '2026-09';
            const mesIdx = parseInt(mesStr.split('-')[1]) - 1;

            window.configListas.categorias.forEach(cat => {
                const planejado = getPlanejado(cat, mesIdx, ano);
                const realizado = catMap[cat] || 0;
                const diff = planejado - realizado;
                const pct = planejado > 0 ? (realizado / planejado) * 100 : 0;

                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td class="py-2.5 font-bold text-slate-800">${cat}</td>
                    <td class="py-2.5 text-right font-bold">R$ ${planejado.toFixed(2)}</td>
                    <td class="py-2.5 text-right font-bold text-rose-700">R$ ${realizado.toFixed(2)}</td>
                    <td class="py-2.5 text-right font-bold ${diff >= 0 ? 'text-emerald-700' : 'text-rose-600'}">R$ ${diff.toFixed(2)}</td>
                    <td class="py-2.5 text-center">
                        <span class="px-2 py-0.5 rounded text-[10px] font-bold border ${pct <= 100 ? 'bg-emerald-50 text-emerald-800 border-emerald-200' : 'bg-rose-50 text-rose-800 border-rose-200'}">
                            ${pct.toFixed(0)}% da Meta
                        </span>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function renderDashboardInsights(totalE, totalG, pctComprometida, catMap) {
            const container = document.getElementById('listaInsightsDashboard');
            if(!container) return;
            container.innerHTML = '';
            const insights = [];

            if(pctComprometida > 80) {
                insights.push(`<div class="p-3 bg-rose-50 border border-rose-200 rounded-xl text-rose-900">⚠️ Atenção: O comprometimento da renda está em <strong>${pctComprometida}%</strong>, acima do limite recomendado de 80%.</div>`);
            } else {
                insights.push(`<div class="p-3 bg-emerald-50 border border-emerald-200 rounded-xl text-emerald-900">🟢 Ótimo controle: O comprometimento da renda está em <strong>${pctComprometida}%</strong>.</div>`);
            }

            let maiorCat = '';
            let maiorVal = 0;
            for(const [cat, val] of Object.entries(catMap)) {
                if(val > maiorVal) { maiorVal = val; maiorCat = cat; }
            }
            if(maiorCat) {
                insights.push(`<div class="p-3 bg-sky-50 border border-sky-200 rounded-xl text-sky-900">📊 A categoria com maior gasto no mês é <strong>${maiorCat}</strong> com <strong>R$ ${maiorVal.toFixed(2)}</strong>.</div>`);
            }

            insights.forEach(divStr => container.innerHTML += divStr);
        }

        function renderMetas() {
            const tbody = document.getElementById('listaMetasTabela');
            const galeria = document.getElementById('visaoMetaGaleria');
            if(!tbody || !galeria) return;
            tbody.innerHTML = '';
            galeria.innerHTML = '';

            const ano = document.getElementById('filtroAnoMeta')?.value || '2026';
            const metasFiltradas = (window.metasCache || []).filter(m => String(m.ano) === String(ano));

            if(metasFiltradas.length === 0) {
                tbody.innerHTML = '<tr><td colspan="7" class="py-4 text-center text-slate-400">Nenhuma meta cadastrada para este ano.</td></tr>';
                galeria.innerHTML = '<div class="col-span-full py-4 text-center text-slate-400">Nenhuma meta cadastrada para este ano.</div>';
                return;
            }

            metasFiltradas.forEach(m => {
                const pct = m.alvo > 0 ? Math.min(100, (m.realizado / m.alvo) * 100) : 0;
                
                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td class="py-2.5">
                        <div class="flex items-center gap-2">
                            <div class="w-16 bg-slate-200 h-2 rounded-full overflow-hidden">
                                <div class="bg-sky-600 h-full" style="width: ${pct}%"></div>
                            </div>
                            <span class="text-[10px] font-bold">${pct.toFixed(0)}%</span>
                        </div>
                    </td>
                    <td class="py-2.5 font-bold text-slate-800">${m.nome}</td>
                    <td class="py-2.5 text-center font-bold">R$ ${m.realizado}</td>
                    <td class="py-2.5 text-center font-bold">R$ ${m.alvo}</td>
                    <td class="py-2.5"><span class="bg-sky-50 text-sky-800 px-2 py-0.5 rounded text-[10px] font-bold border border-sky-200">${m.categoria}</span></td>
                    <td class="py-2.5 text-slate-500">${m.recompensa || '-'}</td>
                    <td class="py-2.5 text-center space-x-1">
                        <button onclick='carregarMetaEdicao(${JSON.stringify(m)}, "${m.id}")' class="text-sky-600"><i class="fa-solid fa-pen"></i></button>
                        <button onclick="excluirMeta('${m.id}')" class="text-rose-500"><i class="fa-solid fa-trash"></i></button>
                    </td>
                `;
                tbody.appendChild(tr);

                const card = document.createElement('div');
                card.className = "bg-white p-4 border border-slate-200 rounded-2xl shadow-sm space-y-3";
                card.innerHTML = `
                    <div class="flex justify-between items-center">
                        <span class="bg-sky-50 text-sky-800 px-2.5 py-1 rounded-xl text-[10px] font-bold border border-sky-200">${m.categoria}</span>
                        <div class="space-x-1">
                            <button onclick='carregarMetaEdicao(${JSON.stringify(m)}, "${m.id}")' class="text-sky-600"><i class="fa-solid fa-pen"></i></button>
                            <button onclick="excluirMeta('${m.id}')" class="text-rose-500"><i class="fa-solid fa-trash"></i></button>
                        </div>
                    </div>
                    <h4 class="font-bold text-slate-800 text-sm">${m.nome}</h4>
                    <div class="space-y-1">
                        <div class="flex justify-between text-xs">
                            <span class="text-slate-500">Progresso (${pct.toFixed(0)}%)</span>
                            <strong class="text-slate-800">R$ ${m.realizado} / R$ ${m.alvo}</strong>
                        </div>
                        <div class="w-full bg-slate-200 h-2.5 rounded-full overflow-hidden">
                            <div class="bg-sky-600 h-full" style="width: ${pct}%"></div>
                        </div>
                    </div>
                    <p class="text-[11px] text-slate-400">Recompensa: <strong>${m.recompensa || '-'}</strong></p>
                `;
                galeria.appendChild(card);
            });
        }

        window.setVisaoMetas = function(visao) {
            const tTab = document.getElementById('visaoMetaTabela');
            const gTab = document.getElementById('visaoMetaGaleria');
            const btnT = document.getElementById('btnMetaTabela');
            const btnG = document.getElementById('btnMetaGaleria');
            if(visao === 'tabela') {
                tTab.classList.remove('hidden');
                gTab.classList.add('hidden');
                btnT.className = "px-3 py-1 rounded-lg font-bold bg-white text-slate-800 shadow-sm";
                btnG.className = "px-3 py-1 rounded-lg font-bold text-slate-500";
            } else {
                tTab.classList.add('hidden');
                gTab.classList.remove('hidden');
                btnG.className = "px-3 py-1 rounded-lg font-bold bg-white text-slate-800 shadow-sm";
                btnT.className = "px-3 py-1 rounded-lg font-bold text-slate-500";
            }
        };

        window.addEventListener('DOMContentLoaded', () => {
            atualizarSelectsDinamicos();
            renderPlanejamentoAnualCards('2026');
        });
    </script>
</body>
</html>
