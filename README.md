<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Avaliação de Perfil de Investimento - Samir Fernandes/CPA-20</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
    <h1>Avaliação de Perfil de Investimento</h1>
    <form id="investment-form">
        <label for="name">Nome:</label>
        <input type="text" id="name" name="name" required><br><br>
        
        <label for="age">Idade:</label>
        <input type="number" id="age" name="age" required><br><br>
        
        <label for="income">Renda Mensal:</label>
        <input type="number" id="income" name="income" required><br><br>
        
        <label for="investment-goal">Objetivo de Investimento:</label>
        <select id="investment-goal" name="investment-goal" required>
            <option value="short-term">Curto Prazo (0-1 ano)</option>
            <option value="medium-term">Médio Prazo (1-5 anos)</option>
            <option value="long-term">Longo Prazo (5-10 anos)</option>
        </select><br><br>
        
        <label for="risk-tolerance">Tolerância ao Risco:</label>
        <select id="risk-tolerance" name="risk-tolerance" required>
            <option value="low">Baixa</option>
            <option value="medium">Média</option>
            <option value="high">Alta</option>
        </select><br><br>
        
        <label for="market-drop">Se houver uma queda de 15% no seu investimento, você:</label>
        <select id="market-drop" name="market-drop" required>
            <option value="sell">Vende</option>
            <option value="invest-more">Investe mais</option>
            <option value="hold-position">Mantém posição</option>
        </select><br><br>
        
        <label for="previous-experience">Qual é sua experiência anterior com investimentos?</label>
        <select id="previous-experience" name="previous-experience" required>
            <option value="none">Nenhuma</option>
            <option value="some">Alguma</option>
            <option value="extensive">Extensiva</option>
        </select><br><br>
        
        <label for="investment-knowledge">Qual é o seu nível de conhecimento sobre investimentos?</label>
        <select id="investment-knowledge" name="investment-knowledge" required>
            <option value="beginner">Iniciante</option>
            <option value="intermediate">Intermediário</option>
            <option value="expert">Especialista</option>
        </select><br><br>
        
        <button type="submit">Enviar</button>
    </form>

    <script>
        document.getElementById('investment-form').addEventListener('submit', function(event) {
            event.preventDefault();
            
            const formData = {
                name: document.getElementById('name').value,
                age: document.getElementById('age').value,
                income: document.getElementById('income').value,
                investmentGoal: document.getElementById('investment-goal').value,
                riskTolerance: document.getElementById('risk-tolerance').value,
                marketDrop: document.getElementById('market-drop').value,
                previousExperience: document.getElementById('previous-experience').value,
                investmentKnowledge: document.getElementById('investment-knowledge').value
            };

            // Simulação de resposta do servidor
            let profile = '';
            if (formData.riskTolerance === 'low') {
                profile = 'Conservador';
            } else if (formData.riskTolerance === 'medium') {
                profile = 'Moderado';
            } else if (formData.riskTolerance === 'high') {
                profile = 'Agressivo';
            }

            let profileDescription = '';
            let portfolioRecommendation = '';
            let chartData = {};

            if (profile === 'Conservador') {
                profileDescription = 'Seu perfil é Conservador. Você prefere segurança e estabilidade em seus investimentos, aceitando menos riscos para proteger seu capital.';
                portfolioRecommendation = 'Vamos preparar uma carteira para você baseada nessas métricas:';
                chartData = {
                    labels: ['Renda Fixa', 'Renda Variável'],
                    datasets: [{
                        data: [80, 20],
                        backgroundColor: ['#4caf50', '#ff9800']
                    }]
                };
            } else if (profile === 'Moderado') {
                profileDescription = 'Seu perfil é Moderado. Você busca um equilíbrio entre segurança e rentabilidade, aceitando riscos moderados para obter retornos melhores.';
                portfolioRecommendation = 'Vamos preparar uma carteira para você baseada nessas métricas:';
                chartData = {
                    labels: ['Renda Fixa', 'Renda Variável', 'Criptos'],
                    datasets: [{
                        data: [50, 40, 10],
                        backgroundColor: ['#4caf50', '#ff9800', '#2196f3']
                    }]
                };
            } else if (profile === 'Agressivo') {
                profileDescription = 'Seu perfil é Agressivo. Você está disposto a correr maiores riscos em busca de retornos mais altos, investindo em opções com maior volatilidade.';
                portfolioRecommendation = 'Vamos preparar uma carteira para você baseada nessas métricas:';
                chartData = {
                    labels: ['Renda Fixa', 'Renda Variável', 'Criptos'],
                    datasets: [{
                        data: [30, 50, 20],
                        backgroundColor: ['#4caf50', '#ff9800', '#2196f3']
                    }]
                };
            }

            document.body.innerHTML = `
                <h1>O seu perfil de investidor é: ${profile}</h1>
                <p>${profileDescription}</p>
                <p>${portfolioRecommendation}</p>
                <canvas id="portfolioChart"></canvas>
            `;

            const ctx = document.getElementById('portfolioChart').getContext('2d');
            new Chart(ctx, {
                type: 'pie',
                data: chartData,
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            position: 'top',
                        },
                        tooltip: {
                            callbacks: {
                                label: function(tooltipItem) {
                                    return tooltipItem.label + ': ' + tooltipItem.raw + '%';
                                }
                            }
                        }
                    }
                }
            });
        });
    </script>
</body>
</html>
