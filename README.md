<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trivial Pursuit Électricité</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
            background: linear-gradient(135deg, #e0f2fe 0%, #e9d5ff 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            max-width: 700px;
            width: 100%;
            background: white;
            border-radius: 16px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
            padding: 40px;
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
        }

        .title-section {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .icon {
            font-size: 32px;
        }

        h1 {
            font-size: 28px;
            color: #1f2937;
            font-weight: 700;
        }

        .score-section {
            text-align: right;
        }

        .question-number {
            font-size: 14px;
            color: #6b7280;
            margin-bottom: 4px;
        }

        .score {
            font-size: 18px;
            color: #2563eb;
            font-weight: 600;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: #e5e7eb;
            border-radius: 10px;
            overflow: hidden;
            margin-bottom: 30px;
        }

        .progress-fill {
            height: 100%;
            background: #3b82f6;
            transition: width 0.3s ease;
        }

        .category-badge {
            display: inline-block;
            padding: 10px 20px;
            border-radius: 25px;
            color: white;
            font-size: 14px;
            font-weight: 600;
            margin-bottom: 20px;
        }

        .bg-blue { background: #3b82f6; }
        .bg-red { background: #ef4444; }
        .bg-green { background: #10b981; }
        .bg-purple { background: #8b5cf6; }
        .bg-yellow { background: #f59e0b; }
        .bg-pink { background: #ec4899; }
        .bg-orange { background: #f97316; }

        .question-box {
            background: #f9fafb;
            padding: 30px;
            border-radius: 12px;
            margin-bottom: 30px;
        }

        .question {
            font-size: 20px;
            color: #1f2937;
            font-weight: 600;
            margin-bottom: 25px;
        }

        .answers {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .answer-btn {
            width: 100%;
            padding: 18px;
            text-align: left;
            border: 2px solid #e5e7eb;
            background: white;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .answer-btn:hover:not(:disabled) {
            border-color: #3b82f6;
            background: #eff6ff;
        }

        .answer-btn.correct {
            border-color: #10b981;
            background: #d1fae5;
            color: #065f46;
        }

        .answer-btn.incorrect {
            border-color: #ef4444;
            background: #fee2e2;
            color: #991b1b;
        }

        .answer-btn.disabled {
            background: #f9fafb;
            color: #9ca3af;
            cursor: not-allowed;
        }

        .explanation {
            margin-top: 25px;
            padding: 20px;
            background: #eff6ff;
            border-left: 4px solid #3b82f6;
            border-radius: 8px;
        }

        .explanation-title {
            color: #1e40af;
            font-weight: 600;
            margin-bottom: 8px;
        }

        .explanation-text {
            color: #1e3a8a;
            line-height: 1.6;
        }

        .next-btn, .start-btn, .restart-btn {
            width: 100%;
            padding: 16px;
            background: #3b82f6;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .next-btn:hover, .start-btn:hover, .restart-btn:hover {
            background: #2563eb;
        }

        .start-screen, .results-screen {
            text-align: center;
        }

        .start-screen h1 {
            font-size: 32px;
            margin-bottom: 20px;
        }

        .start-screen p {
            font-size: 18px;
            color: #6b7280;
            margin-bottom: 40px;
        }

        .question-selector {
            background: white;
            padding: 30px;
            border-radius: 12px;
            margin-bottom: 30px;
        }

        .selector-label {
            font-size: 14px;
            font-weight: 500;
            color: #374151;
            margin-bottom: 20px;
        }

        .selector-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
        }

        .selector-btn {
            padding: 12px;
            background: #f3f4f6;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
        }

        .selector-btn:hover {
            background: #e5e7eb;
        }

        .selector-btn.selected {
            background: #3b82f6;
            color: white;
        }

        .trophy-icon {
            font-size: 64px;
            margin-bottom: 20px;
        }

        .results-title {
            font-size: 32px;
            color: #1f2937;
            margin-bottom: 30px;
        }

        .score-display {
            background: white;
            padding: 30px;
            border-radius: 12px;
            margin-bottom: 30px;
        }

        .final-score {
            font-size: 28px;
            color: #2563eb;
            font-weight: 700;
            margin-bottom: 15px;
        }

        .score-message {
            font-size: 18px;
            color: #374151;
        }

        .hidden {
            display: none;
        }

        @media (max-width: 600px) {
            .container {
                padding: 20px;
            }

            h1 {
                font-size: 20px;
            }

            .question {
                font-size: 18px;
            }

            .selector-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Écran de démarrage -->
        <div id="startScreen" class="start-screen">
            <div class="icon">⚡</div>
            <h1>Trivial Pursuit Électricité</h1>
            <p>Toutes les questions sont mélangées aléatoirement !</p>
            
            <div class="question-selector">
                <div class="selector-label">Nombre de questions :</div>
                <div class="selector-grid">
                    <button class="selector-btn selected" onclick="selectQuestions(10)">10 questions</button>
                    <button class="selector-btn" onclick="selectQuestions(15)">15 questions</button>
                    <button class="selector-btn" onclick="selectQuestions(20)">20 questions</button>
                </div>
            </div>

            <button class="start-btn" onclick="startQuiz()">
                <span>🔀</span>
                Commencer le Quiz
            </button>
        </div>

        <!-- Écran de jeu -->
        <div id="gameScreen" class="hidden">
            <div class="header">
                <div class="title-section">
                    <span class="icon">⚡</span>
                    <h1>Trivial Pursuit Électricité</h1>
                </div>
                <div class="score-section">
                    <div class="question-number" id="questionNumber">Question 1/10</div>
                    <div class="score" id="score">Score: 0</div>
                </div>
            </div>

            <div class="progress-bar">
                <div class="progress-fill" id="progressBar"></div>
            </div>

            <div id="categoryBadge" class="category-badge bg-blue">Catégorie</div>

            <div class="question-box">
                <div class="question" id="question">Question ici</div>
                <div class="answers" id="answers"></div>
                <div id="explanation" class="explanation hidden">
                    <div class="explanation-title">Explication :</div>
                    <div class="explanation-text" id="explanationText"></div>
                </div>
            </div>

            <button id="nextBtn" class="next-btn hidden" onclick="nextQuestion()">
                Question suivante
            </button>
        </div>

        <!-- Écran de résultats -->
        <div id="resultsScreen" class="results-screen hidden">
            <div class="trophy-icon">🏆</div>
            <h2 class="results-title">Quiz Terminé !</h2>
            <div class="score-display">
                <div class="final-score" id="finalScore">Score : 0/10</div>
                <div class="score-message" id="scoreMessage"></div>
            </div>
            <button class="restart-btn" onclick="restartQuiz()">
                <span>🔄</span>
                Rejouer
            </button>
        </div>
    </div>

    <script>
        const allQuestions = [
            {
                category: "Loi d'Ohm",
                question: "Quelle est la formule de la loi d'Ohm ?",
                answers: ["U = R × I", "I = U × R", "R = U × I", "P = U × I"],
                correct: 0,
                explanation: "La loi d'Ohm s'écrit U = R × I, où U est la tension, R la résistance et I l'intensité."
            },
            {
                category: "Loi d'Ohm",
                question: "Si U = 12V et R = 4Ω, alors I = ?",
                answers: ["48A", "3A", "8A", "16A"],
                correct: 1,
                explanation: "I = U/R = 12/4 = 3A"
            },
            {
                category: "Loi d'Ohm",
                question: "Si I = 2A et R = 6Ω, alors U = ?",
                answers: ["12V", "3V", "8V", "4V"],
                correct: 0,
                explanation: "U = R × I = 6 × 2 = 12V"
            },
            {
                category: "Puissance",
                question: "Comment calcule-t-on la puissance électrique ?",
                answers: ["P = U / I", "P = U × I", "P = U + I", "P = U - I"],
                correct: 1,
                explanation: "La puissance électrique se calcule par P = U × I (tension × intensité)."
            },
            {
                category: "Puissance",
                question: "L'unité de la puissance électrique est :",
                answers: ["Le Joule (J)", "Le Watt (W)", "L'Ampère (A)", "Le Volt (V)"],
                correct: 1,
                explanation: "La puissance s'exprime en Watts (W)."
            },
            {
                category: "Puissance",
                question: "Si U = 12V et I = 2A, alors P = ?",
                answers: ["6W", "14W", "24W", "10W"],
                correct: 2,
                explanation: "P = U × I = 12 × 2 = 24W"
            },
            {
                category: "Résistances",
                question: "Comment se comportent des résistances en série ?",
                answers: ["R_totale = R1 + R2 + R3", "1/R_totale = 1/R1 + 1/R2", "R_totale = R1 × R2", "R_totale = R1 / R2"],
                correct: 0,
                explanation: "En série, les résistances s'additionnent : R_totale = R1 + R2 + R3..."
            },
            {
                category: "Résistances",
                question: "Deux résistances de 10Ω en parallèle donnent une résistance équivalente de :",
                answers: ["20Ω", "10Ω", "5Ω", "1Ω"],
                correct: 2,
                explanation: "1/R = 1/10 + 1/10 = 2/10, donc R = 5Ω"
            },
            {
                category: "Résistances",
                question: "Trois résistances de 6Ω en série donnent :",
                answers: ["2Ω", "6Ω", "18Ω", "36Ω"],
                correct: 2,
                explanation: "R_série = 6 + 6 + 6 = 18Ω"
            },
            {
                category: "Circuits",
                question: "Dans un circuit en parallèle, que peut-on dire de la tension ?",
                answers: ["Elle diminue à chaque branche", "Elle est différente sur chaque branche", "Elle est identique sur toutes les branches", "Elle s'additionne"],
                correct: 2,
                explanation: "En parallèle, la tension est identique aux bornes de chaque branche."
            },
            {
                category: "Circuits",
                question: "Un voltmètre se branche :",
                answers: ["En série", "En parallèle", "N'importe comment", "Seulement aux bornes du générateur"],
                correct: 1,
                explanation: "Un voltmètre se branche en parallèle avec l'élément dont on veut mesurer la tension."
            },
            {
                category: "Circuits",
                question: "Un ampèremètre se branche :",
                answers: ["En série", "En parallèle", "N'importe comment", "Seulement aux bornes du générateur"],
                correct: 0,
                explanation: "Un ampèremètre se branche en série dans la branche où on veut mesurer l'intensité."
            },
            {
                category: "Énergie",
                question: "L'unité de l'énergie électrique est :",
                answers: ["Le Watt (W)", "Le Joule (J)", "L'Ampère (A)", "Le Volt (V)"],
                correct: 1,
                explanation: "L'énergie s'exprime en Joules (J). Le Watt est l'unité de puissance."
            },
            {
                category: "Énergie",
                question: "1 kWh équivaut à :",
                answers: ["1000 J", "3600 J", "3600000 J", "1000000 J"],
                correct: 2,
                explanation: "1 kWh = 1000 W × 3600 s = 3 600 000 J = 3,6 MJ"
            },
            {
                category: "Énergie",
                question: "Un radiateur de 1500W fonctionne 2h. Il consomme :",
                answers: ["750 Wh", "3000 Wh", "3 kWh", "1,5 kWh"],
                correct: 2,
                explanation: "E = P × t = 1500W × 2h = 3000 Wh = 3 kWh"
            },
            {
                category: "Intensité",
                question: "L'unité de l'intensité électrique est :",
                answers: ["Le Volt (V)", "L'Ohm (Ω)", "L'Ampère (A)", "Le Watt (W)"],
                correct: 2,
                explanation: "L'intensité s'exprime en Ampères (A)."
            },
            {
                category: "Intensité",
                question: "Dans un circuit série, l'intensité :",
                answers: ["Varie selon la résistance", "Est identique partout", "S'additionne", "Diminue"],
                correct: 1,
                explanation: "En série, l'intensité est la même en tout point du circuit."
            },
            {
                category: "Histoire",
                question: "Qui a découvert la loi qui porte son nom : U = R × I ?",
                answers: ["Ampère", "Volta", "Ohm", "Coulomb"],
                correct: 2,
                explanation: "Georg Simon Ohm (1789-1854) a découvert la relation entre tension, courant et résistance en 1827."
            },
            {
                category: "Histoire",
                question: "Le nom de l'unité 'Ampère' vient de :",
                answers: ["André-Marie Ampère", "Alessandro Volta", "Charles Coulomb", "Michael Faraday"],
                correct: 0,
                explanation: "André-Marie Ampère (1775-1836) est le physicien français qui a étudié l'électrodynamique."
            },
            {
                category: "Histoire",
                question: "Le 'Volt' tire son nom de :",
                answers: ["Thomas Edison", "Alessandro Volta", "Nikola Tesla", "Benjamin Franklin"],
                correct: 1,
                explanation: "Alessandro Volta (1745-1827) a inventé la première pile électrique en 1800."
            }
        ];

        const categoryColors = {
            "Loi d'Ohm": "bg-blue",
            "Puissance": "bg-red", 
            "Résistances": "bg-green",
            "Circuits": "bg-purple",
            "Énergie": "bg-yellow",
            "Intensité": "bg-pink",
            "Histoire": "bg-orange"
        };

        let shuffledQuestions = [];
        let currentQuestionIndex = 0;
        let score = 0;
        let selectedQuestionsCount = 10;
        let answered = false;

        function selectQuestions(count) {
            selectedQuestionsCount = count;
            document.querySelectorAll('.selector-btn').forEach(btn => {
                btn.classList.remove('selected');
            });
            event.target.classList.add('selected');
        }

        function shuffleArray(array) {
            const shuffled = [...array];
            for (let i = shuffled.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
            }
            return shuffled;
        }

        function startQuiz() {
            shuffledQuestions = shuffleArray(allQuestions).slice(0, selectedQuestionsCount);
            currentQuestionIndex = 0;
            score = 0;
            answered = false;
            
            document.getElementById('startScreen').classList.add('hidden');
            document.getElementById('gameScreen').classList.remove('hidden');
            
            displayQuestion();
        }

        function displayQuestion() {
            const question = shuffledQuestions[currentQuestionIndex];
            answered = false;
            
            document.getElementById('questionNumber').textContent = 
                `Question ${currentQuestionIndex + 1}/${shuffledQuestions.length}`;
            document.getElementById('score').textContent = `Score: ${score}`;
            document.getElementById('question').textContent = question.question;
            
            const categoryBadge = document.getElementById('categoryBadge');
            categoryBadge.textContent = question.category;
            categoryBadge.className = `category-badge ${categoryColors[question.category]}`;
            
            const progressBar = document.getElementById('progressBar');
            progressBar.style.width = `${((currentQuestionIndex + 1) / shuffledQuestions.length) * 100}%`;
            
            const answersDiv = document.getElementById('answers');
            answersDiv.innerHTML = '';
            
            question.answers.forEach((answer, index) => {
                const btn = document.createElement('button');
                btn.className = 'answer-btn';
                btn.innerHTML = `<span>${answer}</span>`;
                btn.onclick = () => selectAnswer(index);
                answersDiv.appendChild(btn);
            });
            
            document.getElementById('explanation').classList.add('hidden');
            document.getElementById('nextBtn').classList.add('hidden');
        }

        function selectAnswer(index) {
            if (answered) return;
            answered = true;
            
            const question = shuffledQuestions[currentQuestionIndex];
            const buttons = document.querySelectorAll('.answer-btn');
            
            buttons.forEach((btn, i) => {
                btn.disabled = true;
                if (i === question.correct) {
                    btn.classList.add('correct');
                    btn.innerHTML += '<span>✓</span>';
                } else if (i === index) {
                    btn.classList.add('incorrect');
                    btn.innerHTML += '<span>✗</span>';
                } else {
                    btn.classList.add('disabled');
                }
            });
            
            if (index === question.correct) {
                score++;
                document.getElementById('score').textContent = `Score: ${score}`;
            }
            
            document.getElementById('explanationText').textContent = question.explanation;
            document.getElementById('explanation').classList.remove('hidden');
            document.getElementById('nextBtn').classList.remove('hidden');
        }

        function nextQuestion() {
            if (currentQuestionIndex < shuffledQuestions.length - 1) {
                currentQuestionIndex++;
                displayQuestion();
            } else {
                showResults();
            }
        }

        function showResults() {
            document.getElementById('gameScreen').classList.add('hidden');
            document.getElementById('resultsScreen').classList.remove('hidden');
            
            document.getElementById('finalScore').textContent = 
                `Score : ${score}/${shuffledQuestions.length}`;
            
            const percentage = (score / shuffledQuestions.length) * 100;
            let message;
            if (percentage >= 80) message = "🏆 Excellent ! Tu maîtrises parfaitement l'électricité !";
            else if (percentage >= 60) message = "👍 Bien joué ! Tu as de bonnes bases.";
            else if (percentage >= 40) message = "📚 Pas mal, mais il faut encore réviser un peu.";
            else message = "⚡ Il faut revoir tes cours d'électricité !";
            
            document.getElementById('scoreMessage').textContent = message;
        }

        function restartQuiz() {
            document.getElementById('resultsScreen').classList.add('hidden');
            document.getElementById('startScreen').classList.remove('hidden');
        }
    </script>
</body>
</html>
