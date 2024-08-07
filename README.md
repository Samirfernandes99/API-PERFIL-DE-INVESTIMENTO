<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Avaliação de Perfil de Investimento</title>
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

            fetch('http://localhost:3000/evaluate', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(formData)
            })
            .then(response => response.json())
            .then(data => {
                alert('Perfil de Investimento: ' + data.profile);
            })
            .catch(error => {
                console.error('Erro:', error);
            });
        });
    </script>
</body>
</html>
