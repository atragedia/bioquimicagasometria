<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz de Gasometria Clínica - 10 Perguntas</title>
    <style>
        body {
            font-family: 'Segoe UI', Arial, sans-serif;
            background: #f6f8fa;
            color: #222;
            margin: 0;
            padding: 0;
        }
        .container {
            max-width: 700px;
            margin: auto;
            background: #fff;
            box-shadow: 0 2px 14px rgba(0,0,0,0.08);
            border-radius: 10px;
            padding: 30px 24px 24px 24px;
            margin-top: 36px;
        }
        h1 {
            text-align: center;
            color: #117a8b;
        }
        .start-btn, .nav-btn, .finish-btn, .restart-btn {
            background: #117a8b;
            color: #fff;
            border: none;
            padding: 12px 24px;
            border-radius: 7px;
            font-size: 1.1rem;
            margin: 16px auto;
            display: block;
            cursor: pointer;
            box-shadow: 0 2px 4px rgba(0,0,0,0.06);
            transition: background 0.2s;
        }
        .start-btn:hover, .nav-btn:hover, .finish-btn:hover, .restart-btn:hover { background: #0e606b; }
        .question-count { text-align: right; font-size: 0.98rem; color: #555; margin-bottom: 10px; }
        .question-text { font-size: 1.18rem; margin-bottom: 18px; color: #1b4f72; }
        .options label { display: block; background: #f4f6f9; padding: 12px 14px; margin-bottom: 10px; border-radius: 6px; cursor: pointer; transition: background 0.2s; }
        .options input[type=radio] { margin-right: 14px; }
        .options label.selected { background: #e9f7ef; border-left: 4px solid #117a8b; }
        .feedback { margin-top: 14px; font-weight: bold; border-radius: 6px; padding: 12px; display: none; }
        .correct { background: #e9f7ef; color: #155724; border: 1px solid #c3e6cb; }
        .incorrect { background: #fdecea; color: #7a1f1f; border: 1px solid #f5c6cb; }
        .note { color: #555; font-size: 0.96rem; text-align: center; margin-bottom: 22px;}
        .result { text-align: center; margin-top: 40px; }
        .score { font-size: 1.35rem; font-weight: bold; margin-bottom: 16px; color: #117a8b; }
    </style>
</head>
<body>
    <div class="container" id="main-container">
        <h1>Quiz de Gasometria Clínica</h1>
        <div class="note">Teste seus conhecimentos em distúrbios ácido-base! 10 perguntas clínicas com feedback explicativo após cada resposta.</div>
        <button class="start-btn" id="start-btn">Iniciar Quiz</button>
    </div>

    <script>
        // Perguntas do quiz
        const questions = [
            {
                text: "Paciente com diarreia intensa apresenta queda do HCO₃⁻ e hiperventilação. Qual o distúrbio principal?",
                options: [
                    {text: "Acidose metabólica compensada", value: "a"},
                    {text: "Acidose respiratória", value: "b"},
                    {text: "Alcalose metabólica", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Perda de HCO₃⁻ → acidose metabólica; hiperventilação é compensação respiratória."
            },
            {
                text: "Paciente com perda de HCO₃⁻ e hipoventilação. O que ocorre?",
                options: [
                    {text: "Acidose metabólica com compensação", value: "a"},
                    {text: "Acidose metabólica + respiratória (mista)", value: "b"},
                    {text: "Alcalose metabólica", value: "c"}
                ],
                correct: "b",
                explanation: "✅ Correto! Hipoventilar retém CO₂ e piora acidose — quadro misto."
            },
            {
                text: "Paciente com vômitos prolongados apresenta ganho de HCO₃⁻ e hipoventilação. Qual o diagnóstico?",
                options: [
                    {text: "Alcalose metabólica compensada", value: "a"},
                    {text: "Acidose metabólica", value: "b"},
                    {text: "Alcalose respiratória", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Ganho de HCO₃⁻ → alcalose metabólica; hipoventilação retém CO₂ para compensar."
            },
            {
                text: "Paciente com ganho de HCO₃⁻ e hiperventilação apresenta:",
                options: [
                    {text: "Alcalose mista (metabólica + respiratória)", value: "a"},
                    {text: "Acidose metabólica", value: "b"},
                    {text: "Compensação adequada", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Ganho de HCO₃⁻ já causa alcalose, e hiperventilar reduz CO₂ → piora alcalose."
            },
            {
                text: "Em acidose respiratória crônica, o rim compensa como?",
                options: [
                    {text: "Excretando mais H⁺ e retendo HCO₃⁻", value: "a"},
                    {text: "Excretando mais HCO₃⁻", value: "b"},
                    {text: "Retendo CO₂", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! O rim aumenta HCO₃⁻ para neutralizar a acidose causada pelo CO₂ retido."
            },
            {
                text: "Em alcalose respiratória, a compensação metabólica consiste em:",
                options: [
                    {text: "Excreção renal de HCO₃⁻", value: "a"},
                    {text: "Retenção de HCO₃⁻", value: "b"},
                    {text: "Aumento da ventilação", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Menos CO₂ (alcalose respiratória) → rim elimina HCO₃⁻ para reduzir o pH."
            },
            {
                text: "Paciente hipoventilando apresenta pCO₂ elevado e pH baixo. Qual o distúrbio?",
                options: [
                    {text: "Acidose respiratória", value: "a"},
                    {text: "Alcalose respiratória", value: "b"},
                    {text: "Acidose metabólica", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Hipoventilação → CO₂ ↑ → acidose respiratória."
            },
            {
                text: "Mulher em crise de ansiedade está hiperventilando e apresenta pH alto e pCO₂ baixo. Diagnóstico?",
                options: [
                    {text: "Alcalose respiratória", value: "a"},
                    {text: "Acidose metabólica", value: "b"},
                    {text: "Alcalose metabólica", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! Hiperventilação elimina CO₂, elevando o pH — alcalose respiratória."
            },
            {
                text: "Em acidose metabólica, qual é a resposta respiratória esperada?",
                options: [
                    {text: "Hipoventilação", value: "a"},
                    {text: "Hiperventilação", value: "b"},
                    {text: "Sem alteração ventilatória", value: "c"}
                ],
                correct: "b",
                explanation: "✅ Correto! Acidose → hiperventilação para eliminar CO₂ e aumentar o pH."
            },
            {
                text: "Paciente com DPOC crônico apresenta pCO₂ alto, HCO₃⁻ alto e pH quase normal. O que isso indica?",
                options: [
                    {text: "Compensação renal completa de acidose respiratória crônica", value: "a"},
                    {text: "Acidose metabólica aguda", value: "b"},
                    {text: "Alcalose mista", value: "c"}
                ],
                correct: "a",
                explanation: "✅ Correto! DPOC causa acidose respiratória crônica; rim aumenta HCO₃⁻ e normaliza pH."
            }
        ];

        // O resto do código do quiz permanece igual e funcional
        let current = 0;
        let userAnswers = [];
        let feedbackStates = [];
        let score = 0;

        const container = document.getElementById('main-container');
        const startBtn = document.getElementById('start-btn');

        startBtn.onclick = () => { startQuiz(); };

        function startQuiz() {
            current = 0;
            userAnswers = Array(questions.length).fill(null);
            feedbackStates = Array(questions.length).fill(false);
            score = 0;
            showQuestion();
        }

        function showQuestion() {
            const q = questions[current];
            let html = `
                <div class="question-count">Pergunta ${current+1} de ${questions.length}</div>
                <div class="question-text">${q.text}</div>
                <form id="question-form">
                    <div class="options">
                        ${q.options.map((opt, i) => `
                            <label class="${userAnswers[current] === opt.value ? 'selected' : ''}">
                                <input type="radio" name="option" value="${opt.value}" ${userAnswers[current] === opt.value ? 'checked' : ''}>
                                ${opt.text}
                            </label>
                        `).join('')}
                    </div>
                    ${!feedbackStates[current] ? `<button type="button" class="nav-btn" id="check-btn">Verificar Resposta</button>` : ''}
                </form>
                <div class="feedback" id="feedback"></div>
                <div style="margin-top:18px;">
                    ${current > 0 ? '<button class="nav-btn" id="prev-btn">&larr; Anterior</button>' : ''}
                    ${current < questions.length-1 ? `<button class="nav-btn" id="next-btn" style="display:${feedbackStates[current] ? 'inline-block' : 'none'};">Próxima &rarr;</button>` : ''}
                    ${current === questions.length-1 && feedbackStates[current] ? '<button class="finish-btn" id="finish-btn">Ver Resultado</button>' : ''}
                </div>
            `;
            container.innerHTML = html;

            if (!feedbackStates[current]) {
                document.getElementById('check-btn').onclick = () => checkAnswer();
            }
            if (current > 0) document.getElementById('prev-btn').onclick = () => prevQuestion();
            if (current < questions.length-1) document.getElementById('next-btn').onclick = () => nextQuestion();
            if (current === questions.length-1 && feedbackStates[current]) document.getElementById('finish-btn').onclick = () => showResult();

            if (feedbackStates[current]) showFeedback();
        }

        function checkAnswer() {
            const radios = document.getElementsByName('option');
            let selected = null;
            for (const r of radios) {
                if (r.checked) selected = r.value;
            }
            const feedback = document.getElementById('feedback');
            if (!selected) {
                feedback.textContent = "Por favor, selecione uma opção!";
                feedback.className = "feedback incorrect";
                feedback.style.display = "block";
                return;
            }
            userAnswers[current] = selected;
            feedbackStates[current] = true;
            if (!feedback.dataset.scored) {
                if (selected === questions[current].correct) score++;
                feedback.dataset.scored = "1";
            }
            showQuestion();
        }

        function showFeedback() {
            const feedback = document.getElementById('feedback');
            const q = questions[current];
            if (userAnswers[current] === q.correct) {
                feedback.innerHTML = q.explanation;
                feedback.className = "feedback correct";
            } else {
                let wrongText = q.explanation.replace('✅ Correto! ', '');
                feedback.innerHTML = `❌ Incorreto. ${wrongText}`;
                feedback.className = "feedback incorrect";
            }
            feedback.style.display = "block";
        }

        function nextQuestion() {
            current++;
            showQuestion();
        }
        function prevQuestion() {
            current--;
            showQuestion();
        }

        function showResult() {
            let html = `
                <div class="result">
                    <div class="score">Você acertou ${score} de ${questions.length} perguntas.</div>
                    <div style="margin:24px 0">
                        <button class="restart-btn" onclick="window.location.reload()">Refazer Quiz</button>
                    </div>
                    <div>
                        <h3>Gabarito:</h3>
                        <ul style="text-align:left;">
                            ${questions.map((q, i) => {
                                let user = userAnswers[i];
                                let isCorrect = user === q.correct;
                                let letter = q.options.find(opt => opt.value === q.correct).text;
                                return `<li>
                                        <strong>P${i+1}:</strong> <span style="color:${isCorrect?'#117a8b':'#7a1f1f'}">
                                            ${isCorrect ? "✔️" : "❌"}
                                        </span>
                                        <span>${q.text}<br>
                                        <em>Resposta correta: ${letter}</em>
                                        <br>
                                        <span style="font-size:0.97em">${q.explanation.replace('✅ Correto! ','')}</span>
                                        </span>
                                    </li>`;
                            }).join('')}
                        </ul>
                    </div>
                </div>
            `;
            container.innerHTML = html;
        }
    </script>
</body>
</html>
