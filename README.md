<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Relatório de Monitoramento: Atendimentos e Beneficiários</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700;900&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Roboto', sans-serif; background-color: #F3F4F6; }
        .chart-container { 
            position: relative; 
            width: 100%; 
            max-width: 800px; 
            margin-left: auto; 
            margin-right: auto; 
            height: 400px; 
            max-height: 500px; 
        }
        @media (max-width: 768px) {
            .chart-container { height: 300px; }
        }
        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #E5E7EB; }
        ::-webkit-scrollbar-thumb { background: #4A148C; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #311B92; }
    </style>
    <!-- 
    PALETTE: Vibrant Health Analytics
    Primary: #4A148C (Deep Purple)
    Secondary: #009688 (Teal)
    Accent: #FFEB3B (Vibrant Yellow)
    Info: #2196F3 (Blue)
    Background: #F3F4F6 (Light Gray)
    -->
    <!-- 
    NARRATIVE PLAN:
    1. Header: High-level context and purpose.
    2. Executive Summary: Key KPIs (Big Numbers) - "Sem Equipe" alert.
    3. Team Load Analysis: Horizontal Bar Chart showing distribution.
    4. Demographics: Stacked Bar showing Age/Sex breakdown.
    5. Operational Modalities: Grouped Bar comparing Tele vs Presential.
    6. Insights & Recommendations: Text-based actionable takeaways.
    -->
    <!-- 
    CHART SELECTION JUSTIFICATION (NO SVG):
    1. Team Load -> Horizontal Bar Chart (Chart.js). Goal: Compare. Justification: Best for comparing many categories with long names (Team names).
    2. Demographics -> Stacked Bar Chart (Chart.js). Goal: Compare/Composition. Justification: effectively shows age brackets split by gender.
    3. Modalities -> Grouped Bar Chart (Chart.js). Goal: Compare. Justification: Clear side-by-side comparison of two distinct metrics per category.
    4. KPIs -> HTML Cards. Goal: Inform. Justification: Direct text is most readable.
    -->
    <!-- CONFIRMATION: NEITHER Mermaid JS NOR SVG were used anywhere in the output. -->
</head>
<body class="text-gray-800">

    <!-- Header Section -->
    <header class="bg-gradient-to-r from-[#4A148C] to-[#7B1FA2] text-white p-8 shadow-lg">
        <div class="max-w-6xl mx-auto">
            <h1 class="text-4xl md:text-5xl font-black mb-2 tracking-tight">Monitoramento de Saúde</h1>
            <p class="text-xl opacity-90 font-light">Análise de Atendimentos, Cobertura de Equipes e Perfil de Beneficiários</p>
            <div class="mt-6 flex flex-wrap gap-4">
                <span class="bg-white/20 px-3 py-1 rounded-full text-sm font-semibold backdrop-blur-sm">Relatório Executivo</span>
                <span class="bg-white/20 px-3 py-1 rounded-full text-sm font-semibold backdrop-blur-sm">Dados Atualizados</span>
            </div>
        </div>
    </header>

    <main class="max-w-6xl mx-auto p-6 space-y-12">

        <!-- Section 1: Executive Summary / KPIs -->
        <section class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <div class="md:col-span-3 mb-4">
                <h2 class="text-3xl font-bold text-[#4A148C] border-l-8 border-[#FFEB3B] pl-4">Resumo Executivo</h2>
                <p class="mt-2 text-gray-600">Uma visão geral rápida dos indicadores mais críticos identificados no período. A disparidade na alocação de equipes é o ponto focal de atenção.</p>
            </div>

            <!-- KPI Card 1 -->
            <div class="bg-white rounded-xl shadow-md p-6 border-t-4 border-[#D32F2F] hover:shadow-lg transition-shadow">
                <div class="flex items-center justify-between">
                    <div>
                        <p class="text-sm font-bold text-gray-400 uppercase tracking-wide">Alerta Crítico</p>
                        <p class="text-4xl font-black text-[#D32F2F]">535</p>
                    </div>
                    <div class="text-4xl">⚠️</div>
                </div>
                <p class="mt-2 text-gray-600 font-medium">Beneficiários "Sem Equipe"</p>
                <p class="text-xs text-gray-400 mt-1">Requer ação imediata de vinculação.</p>
            </div>

            <!-- KPI Card 2 -->
            <div class="bg-white rounded-xl shadow-md p-6 border-t-4 border-[#009688] hover:shadow-lg transition-shadow">
                <div class="flex items-center justify-between">
                    <div>
                        <p class="text-sm font-bold text-gray-400 uppercase tracking-wide">Equipe Mais Ativa</p>
                        <p class="text-2xl font-black text-[#009688]">Teatro Nacional</p>
                    </div>
                    <div class="text-4xl">🏥</div>
                </div>
                <p class="mt-2 text-gray-600 font-medium">Líder em Volume & Telemonitoramento</p>
                <p class="text-xs text-gray-400 mt-1">Modelo de alta produtividade.</p>
            </div>

            <!-- KPI Card 3 -->
            <div class="bg-white rounded-xl shadow-md p-6 border-t-4 border-[#2196F3] hover:shadow-lg transition-shadow">
                <div class="flex items-center justify-between">
                    <div>
                        <p class="text-sm font-bold text-gray-400 uppercase tracking-wide">Perfil Predominante</p>
                        <p class="text-3xl font-black text-[#2196F3]">40-44 Anos</p>
                    </div>
                    <div class="text-4xl">👥</div>
                </div>
                <p class="mt-2 text-gray-600 font-medium">Faixa Etária Principal</p>
                <p class="text-xs text-gray-400 mt-1">Maioria do gênero feminino.</p>
            </div>
        </section>

        <!-- Section 2: Beneficiary Distribution -->
        <section class="bg-white rounded-2xl shadow-sm p-8">
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                <div class="lg:col-span-1">
                    <h3 class="text-2xl font-bold text-[#4A148C] mb-4">Distribuição por Equipe</h3>
                    <p class="text-gray-600 mb-4 text-justify">
                        A análise de carga de trabalho revela uma distribuição desigual. A categoria <strong>"Sem Equipe"</strong> representa o maior volume, indicando um gargalo no processo de triagem ou cadastro inicial.
                    </p>
                    <p class="text-gray-600 mb-4 text-justify">
                        Entre as equipes ativas, a <strong>Equipe Teatro Nacional</strong> e a <strong>Equipe Parque da Cidade</strong> absorvem a maior parte da demanda, o que pode indicar sobrecarga ou alta eficiência operacional.
                    </p>
                    <ul class="space-y-2 mt-6">
                        <li class="flex items-center text-sm font-medium text-gray-500">
                            <span class="w-3 h-3 rounded-full bg-[#4A148C] mr-2"></span> Maior Volume: Sem Equipe
                        </li>
                        <li class="flex items-center text-sm font-medium text-gray-500">
                            <span class="w-3 h-3 rounded-full bg-[#7B1FA2] mr-2"></span> Equipe Ativa Top 1: Teatro Nacional
                        </li>
                    </ul>
                </div>
                <div class="lg:col-span-2 flex items-center justify-center bg-gray-50 rounded-xl p-4">
                    <div class="chart-container">
                        <canvas id="teamDistributionChart"></canvas>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section 3: Demographics -->
        <section class="bg-white rounded-2xl shadow-sm p-8">
            <div class="mb-6">
                <h3 class="text-2xl font-bold text-[#4A148C]">Perfil Demográfico</h3>
                <p class="text-gray-600 mt-2">Análise da pirâmide etária e distribuição por sexo dos beneficiários atendidos.</p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
                <div class="order-2 md:order-1 flex items-center justify-center bg-gray-50 rounded-xl p-4">
                    <div class="chart-container">
                        <canvas id="demographicsChart"></canvas>
                    </div>
                </div>
                <div class="order-1 md:order-2">
                    <h4 class="text-xl font-bold text-[#2196F3] mb-3">Concentração na Meia-Idade</h4>
                    <p class="text-gray-600 mb-4">
                        Os dados apontam para um pico significativo de atendimentos na faixa dos <strong>35 aos 49 anos</strong>. 
                        A faixa de <strong>40 a 44 anos</strong> isoladamente representa a maior demanda do sistema.
                    </p>
                    <div class="bg-[#E3F2FD] border-l-4 border-[#2196F3] p-4 rounded-r-lg">
                        <p class="text-sm text-[#0D47A1]">
                            <strong>Insight:</strong> Há uma predominância consistente do público feminino em quase todas as faixas etárias ativas, sugerindo que as mulheres buscam mais ativamente os serviços de monitoramento ou são o foco principal dos programas atuais.
                        </p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section 4: Modalities -->
        <section class="bg-white rounded-2xl shadow-sm p-8">
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                <div class="lg:col-span-1">
                    <h3 class="text-2xl font-bold text-[#4A148C] mb-4">Modalidade de Atendimento</h3>
                    <p class="text-gray-600 mb-4">
                        Comparativo entre a eficácia do Telemonitoramento versus Consultas Presenciais por unidade.
                    </p>
                    <p class="text-gray-600 mb-4">
                        A <strong>Equipe Teatro Nacional</strong> demonstra como o telemonitoramento pode escalar o atendimento, superando largamente as consultas presenciais. Em contraste, a categoria "Sem Equipe" possui um alto índice de telemonitoramento, sugerindo uma triagem remota inicial sem vínculo presencial estabelecido.
                    </p>
                </div>
                <div class="lg:col-span-2 flex items-center justify-center bg-gray-50 rounded-xl p-4">
                    <div class="chart-container">
                        <canvas id="modalitiesChart"></canvas>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section 5: Recommendations -->
        <section class="grid grid-cols-1 md:grid-cols-2 gap-6 pb-12">
            <div class="bg-[#4A148C] text-white rounded-2xl shadow-lg p-8">
                <h3 class="text-2xl font-bold mb-6 flex items-center">
                    <span class="text-3xl mr-3">🚀</span> Próximos Passos
                </h3>
                <ul class="space-y-4">
                    <li class="flex items-start bg-white/10 p-3 rounded-lg backdrop-blur-sm">
                        <span class="font-bold text-[#FFEB3B] mr-3 mt-1">01.</span>
                        <div>
                            <strong class="block text-[#FFEB3B]">Força Tarefa de Vinculação</strong>
                            <span class="text-sm opacity-90">Investigar e redistribuir imediatamente os 535 beneficiários "Sem Equipe" para unidades com menor carga.</span>
                        </div>
                    </li>
                    <li class="flex items-start bg-white/10 p-3 rounded-lg backdrop-blur-sm">
                        <span class="font-bold text-[#FFEB3B] mr-3 mt-1">02.</span>
                        <div>
                            <strong class="block text-[#FFEB3B]">Balanceamento de Carga</strong>
                            <span class="text-sm opacity-90">Avaliar apoio para a Equipe Teatro Nacional ou replicar seu modelo de eficiência para outras unidades.</span>
                        </div>
                    </li>
                </ul>
            </div>

            <div class="bg-white rounded-2xl shadow-lg p-8 border border-gray-200">
                <h3 class="text-2xl font-bold text-[#4A148C] mb-6 flex items-center">
                    <span class="text-3xl mr-3">💡</span> Oportunidades
                </h3>
                <div class="space-y-4">
                    <div>
                        <h4 class="font-bold text-gray-800">Expansão do Telemonitoramento</h4>
                        <p class="text-sm text-gray-600 mt-1">Equipes como "Torre de TV" e "Ermida" possuem potencial para aumentar a cobertura via teleatendimento, seguindo o benchmark do Teatro Nacional.</p>
                    </div>
                    <div class="h-px bg-gray-200 w-full"></div>
                    <div>
                        <h4 class="font-bold text-gray-800">Foco na Saúde da Mulher (40+)</h4>
                        <p class="text-sm text-gray-600 mt-1">Dado o perfil demográfico, campanhas preventivas focadas em mulheres acima de 40 anos teriam altíssima aderência.</p>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <footer class="bg-gray-800 text-gray-400 py-8 text-center text-sm">
        <p>Gerado automaticamente pelo Sistema de Inteligência de Dados.</p>
        <p class="mt-2">© 2024 Departamento de Monitoramento e Avaliação em Saúde.</p>
    </footer>

    <!-- Chart Logic -->
    <script>
        // --- Utility: Label Wrapping (>16 chars) ---
        function wrapLabel(label) {
            if (label.length <= 16) return label;
            const words = label.split(' ');
            const lines = [];
            let currentLine = words[0];

            for (let i = 1; i < words.length; i++) {
                if ((currentLine + " " + words[i]).length <= 16) {
                    currentLine += " " + words[i];
                } else {
                    lines.push(currentLine);
                    currentLine = words[i];
                }
            }
            lines.push(currentLine);
            return lines;
        }

        // --- Common Config ---
        Chart.defaults.font.family = "'Roboto', sans-serif";
        Chart.defaults.color = '#666';
        
        // Tooltip Callback Requirement
        const commonTooltip = {
            callbacks: {
                title: function(tooltipItems) {
                    const item = tooltipItems[0];
                    let label = item.chart.data.labels[item.dataIndex];
                    if (Array.isArray(label)) {
                        return label.join(' ');
                    } else {
                        return label;
                    }
                }
            },
            backgroundColor: 'rgba(74, 20, 140, 0.9)',
            titleFont: { size: 14, weight: 'bold' },
            bodyFont: { size: 13 },
            padding: 12,
            cornerRadius: 8,
            displayColors: true
        };

        // --- 1. Team Distribution Chart (Horizontal Bar) ---
        const ctxTeam = document.getElementById('teamDistributionChart').getContext('2d');
        const rawLabelsTeam = [
            "Sem Equipe", "Equipe Teatro Nacional", "Equipe Parque da Cidade", 
            "Equipe Ponte JK", "Equipe Torre de TV", "Equipe Ermida", 
            "Equipe Catetinho", "Equipe Eixão", "Equipe Pontão", 
            "Projeto Integrar", "Equipe Catedral"
        ];
        
        new Chart(ctxTeam, {
            type: 'bar',
            data: {
                labels: rawLabelsTeam.map(wrapLabel),
                datasets: [{
                    label: 'Beneficiários',
                    data: [535, 180, 152, 118, 66, 62, 47, 45, 17, 13, 6],
                    backgroundColor: [
                        '#D32F2F', // Alert for Sem Equipe
                        '#4A148C', '#4A148C', '#4A148C', '#7B1FA2', 
                        '#7B1FA2', '#009688', '#009688', '#009688', 
                        '#FFEB3B', '#FFEB3B'
                    ],
                    borderRadius: 6,
                }]
            },
            options: {
                indexAxis: 'y', // Horizontal
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { display: false },
                    tooltip: commonTooltip,
                    title: { display: false }
                },
                scales: {
                    x: {
                        grid: { display: false },
                        ticks: { font: { size: 10 } }
                    },
                    y: {
                        grid: { display: false },
                        ticks: { font: { size: 11, weight: '500' } }
                    }
                }
            }
        });

        // --- 2. Demographics Chart (Stacked Bar - Age/Sex) ---
        const ctxDemo = document.getElementById('demographicsChart').getContext('2d');
        const labelsAge = [
            "0-4", "5-9", "10-14", "15-19", "20-24", "25-29", "30-34", 
            "35-39", "40-44", "45-49", "50-54", "55-59", "60-64", "65-69"
        ];
        
        new Chart(ctxDemo, {
            type: 'bar',
            data: {
                labels: labelsAge, // Short enough, no wrap needed
                datasets: [
                    {
                        label: 'Feminino',
                        data: [0, 2, 15, 45, 55, 25, 70, 115, 155, 100, 45, 40, 65, 25],
                        backgroundColor: '#F06292', // Pinkish
                        borderRadius: 4,
                    },
                    {
                        label: 'Masculino',
                        data: [0, 1, 25, 35, 25, 15, 35, 65, 95, 55, 25, 25, 30, 10],
                        backgroundColor: '#2196F3', // Blue
                        borderRadius: 4,
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    tooltip: commonTooltip,
                    legend: { position: 'top' }
                },
                scales: {
                    x: { 
                        stacked: true,
                        grid: { display: false }
                    },
                    y: { 
                        stacked: true,
                        grid: { color: '#f0f0f0' }
                    }
                }
            }
        });

        // --- 3. Modalities Chart (Grouped Bar) ---
        const ctxModalities = document.getElementById('modalitiesChart').getContext('2d');
        const rawLabelsModalities = [
            "Equipe Teatro Nacional", "Sem Equipe", "Equipe Ponte JK", 
            "Equipe Parque da Cidade", "Equipe Torre de TV", "Equipe Ermida", 
            "Equipe Catetinho", "Equipe Eixão"
        ];

        new Chart(ctxModalities, {
            type: 'bar',
            data: {
                labels: rawLabelsModalities.map(wrapLabel),
                datasets: [
                    {
                        label: 'Telemonitoramento',
                        data: [210, 180, 130, 135, 75, 60, 40, 35],
                        backgroundColor: '#009688', // Teal
                        borderRadius: 4,
                        barPercentage: 0.7,
                        categoryPercentage: 0.8
                    },
                    {
                        label: 'Consulta Presencial',
                        data: [150, 60, 110, 95, 60, 60, 30, 25],
                        backgroundColor: '#2196F3', // Blue
                        borderRadius: 4,
                        barPercentage: 0.7,
                        categoryPercentage: 0.8
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    tooltip: commonTooltip,
                    legend: { position: 'bottom' }
                },
                scales: {
                    x: {
                        grid: { display: false }
                    },
                    y: {
                        grid: { color: '#f0f0f0' },
                        beginAtZero: true
                    }
                }
            }
        });
    </script>
</body>
</html>
