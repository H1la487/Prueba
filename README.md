# Prueba
Prueba diagnóstica de fránces
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prueba Diagnóstica de Francés</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .quiz-option {
            transition: all 0.2s ease-in-out;
        }
        .quiz-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }
        .correct {
            background-color: #22c55e !important; /* green-500 */
            color: white;
            border-color: #16a34a;
        }
        .incorrect {
            background-color: #ef4444 !important; /* red-500 */
            color: white;
            border-color: #dc2626;
        }
    </style>
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen p-4">

    <div id="quiz-container" class="bg-white p-6 md:p-8 rounded-2xl shadow-xl w-full max-w-2xl mx-auto">
        
        <!-- Header -->
        <div class="mb-6 text-center">
            <h1 class="text-2xl md:text-3xl font-bold text-gray-800">Prueba Diagnóstica de Francés</h1>
            <p class="text-gray-500 mt-1">Selecciona la respuesta correcta.</p>
        </div>
        
        <!-- Progress and Question -->
        <div id="question-area">
            <div class="flex justify-between items-center mb-4">
                <p id="question-counter" class="text-sm font-semibold text-gray-600"></p>
                <p id="score-counter" class="text-sm font-semibold text-indigo-600"></p>
            </div>
            <p id="question-text" class="text-lg font-semibold text-gray-700 mb-6 min-h-[60px]"></p>
        </div>

        <!-- Answer Options -->
        <div id="options-container" class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <!-- Options will be dynamically inserted here -->
        </div>

        <!-- Results Screen -->
        <div id="results-container" class="hidden text-center">
             <h2 class="text-2xl font-bold text-gray-800 mb-4">¡Prueba completada!</h2>
             <p id="results-text" class="text-xl text-gray-600 mb-2"></p>
             <p id="results-feedback" class="text-indigo-600 font-semibold mb-6"></p>
             <button id="restart-button" class="bg-indigo-600 text-white font-bold py-3 px-6 rounded-lg hover:bg-indigo-700 transition-colors w-full mb-3">
                 Volver a intentar
             </button>
             <button id="share-button" class="bg-green-500 text-white font-bold py-3 px-6 rounded-lg hover:bg-green-600 transition-colors w-full">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 inline-block mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
                 Compartir resultado en WhatsApp
             </button>
        </div>
    </div>

    <script>
        const quizData = [
            {
                question: "En la papelería, compras un cuaderno y un estuche. El estuche es de un color muy bonito. ¿Cómo describirías el estuche usando el adjetivo 'beau' correctamente?",
                options: [
                    { text: "C'est un beau estuche.", correct: false },
                    { text: "C'est une belle trousse.", correct: true },
                    { text: "C'est un bel trousse.", correct: false },
                    { text: "C'est une beau trousse.", correct: false }
                ]
            },
            {
                question: "Tu amigo te cuenta: 'A mi hermano le encantan las zapatillas grandes, los pantalones anchos y a veces usa una gorra'. ¿Qué estilo de ropa tiene su hermano?",
                options: [
                    { text: "Style hippie chic", correct: false },
                    { text: "Style hipster", correct: false },
                    { text: "Style skateur", correct: true },
                    { text: "Style BCBG", correct: false }
                ]
            },
            {
                question: "Si Pau Gasol es 'un sportif espagnol', ¿cómo nos referiríamos a Penélope Cruz, que es de la misma nacionalidad y también es una celebridad?",
                options: [
                    { text: "C'est une actrice espagnol.", correct: false },
                    { text: "C'est un acteur espagnole.", correct: false },
                    { text: "C'est une actrice espagnole.", correct: true },
                    { text: "C'est un actrice espagnol.", correct: false }
                ]
            },
            {
                question: "Cada mañana, antes de ir al colegio, te pones el uniforme. ¿Cuál es la forma correcta de decir 'Yo me visto' en francés?",
                options: [
                    { text: "Je habille", correct: false },
                    { text: "Tu t'habilles", correct: false },
                    { text: "Je m'habille", correct: true },
                    { text: "Il s'habille", correct: false }
                ]
            },
            {
                question: "Recibes esta invitación: 'Je t'invite à ma fête samedi à 19h. Thème: Super-héros. Adresse: 5, rue de la Liberté'. ¿Qué información NO aparece en la invitación?",
                options: [
                    { text: "La fecha y hora de la fiesta.", correct: false },
                    { text: "El tema de la fiesta.", correct: false },
                    { text: "Qué hay que llevar de regalo.", correct: true },
                    { text: "La dirección del evento.", correct: false }
                ]
            },
            {
                question: "En la clase de música, tu compañero toca el violín y en la clase de deportes, juega al rugby. ¿Cuál de estas frases describe correctamente sus actividades?",
                options: [
                    { text: "Il joue au violon et il joue du rugby.", correct: false },
                    { text: "Il joue du violon et il joue au rugby.", correct: true },
                    { text: "Il joue de violon et il joue de rugby.", correct: false },
                    { text: "Il joue à violon et il joue à rugby.", correct: false }
                ]
            },
            {
                question: "La profesora pregunta: '¿Quién quiere participar en el taller de teatro?'. Si tú quieres participar, ¿cuál es la forma más enfática de responder usando un pronombre tónico?",
                options: [
                    { text: "Je, je veux participer.", correct: false },
                    { text: "Toi, tu veux participer.", correct: false },
                    { text: "Moi, je veux participer.", correct: true },
                    { text: "Lui, il veut participer.", correct: false }
                ]
            },
            {
                question: "En una tienda de antigüedades ves una mesa muy bonita pero que tiene muchos años. Si 'mesa' es 'une table' (femenino), ¿cómo la describirías con el adjetivo 'vieux'?",
                options: [
                    { text: "C'est une vieux table.", correct: false },
                    { text: "C'est une vieille table.", correct: true },
                    { text: "C'est un vieil table.", correct: false },
                    { text: "C'est une vieil table.", correct: false }
                ]
            },
            {
                question: "Según el texto 'L'Afrique, c'est chic!', ¿qué es un 'boubou'?",
                options: [
                    { text: "Un tipo de tela muy colorida.", correct: false },
                    { text: "Una larga túnica tradicional que visten los hombres.", correct: true },
                    { text: "Un accesorio con flecos para bolsos y zapatos.", correct: false },
                    { text: "Un festival internacional de moda en Níger.", correct: false }
                ]
            },
            {
                question: "En el Tour de France, ¿qué significa llevar el 'maillot jaune' (maillot amarillo)?",
                options: [
                    { text: "Que eres el ciclista más joven de la competición.", correct: false },
                    { text: "Que has ganado la etapa de montaña.", correct: false },
                    { text: "Que eres el líder de la clasificación general, el más rápido.", correct: true },
                    { text: "Que vienes del país donde se celebra la carrera.", correct: false }
                ]
            }
        ];

        // DOM Elements
        const questionArea = document.getElementById('question-area');
        const questionCounter = document.getElementById('question-counter');
        const scoreCounter = document.getElementById('score-counter');
        const questionText = document.getElementById('question-text');
        const optionsContainer = document.getElementById('options-container');
        const resultsContainer = document.getElementById('results-container');
        const resultsText = document.getElementById('results-text');
        const resultsFeedback = document.getElementById('results-feedback');
        const restartButton = document.getElementById('restart-button');
        const shareButton = document.getElementById('share-button');

        let currentQuestionIndex = 0;
        let score = 0;

        function startQuiz() {
            currentQuestionIndex = 0;
            score = 0;
            resultsContainer.classList.add('hidden');
            questionArea.classList.remove('hidden');
            optionsContainer.classList.remove('hidden');
            optionsContainer.style.pointerEvents = 'auto';
            showQuestion();
        }

        function showQuestion() {
            resetState();
            const currentQuestion = quizData[currentQuestionIndex];
            questionCounter.innerText = `Pregunta ${currentQuestionIndex + 1} de ${quizData.length}`;
            scoreCounter.innerText = `Aciertos: ${score}`;
            questionText.innerText = currentQuestion.question;

            currentQuestion.options.forEach(option => {
                const button = document.createElement('button');
                button.innerText = option.text;
                button.classList.add('quiz-option', 'w-full', 'bg-white', 'border-2', 'border-gray-300', 'text-gray-700', 'font-semibold', 'p-4', 'rounded-lg', 'text-left', 'hover:bg-indigo-50', 'hover:border-indigo-400');
                if (option.correct) {
                    button.dataset.correct = true;
                }
                button.addEventListener('click', selectAnswer);
                optionsContainer.appendChild(button);
            });
        }
        
        function resetState() {
            while (optionsContainer.firstChild) {
                optionsContainer.removeChild(optionsContainer.firstChild);
            }
        }

        function selectAnswer(e) {
            const selectedButton = e.target;
            const correct = selectedButton.dataset.correct === 'true';

            if (correct) {
                score++;
                selectedButton.classList.add('correct');
            } else {
                selectedButton.classList.add('incorrect');
            }
            
            // Show the correct answer
            Array.from(optionsContainer.children).forEach(button => {
                if (button.dataset.correct) {
                    button.classList.add('correct');
                }
                button.disabled = true; // Disable all buttons
            });
            
            optionsContainer.style.pointerEvents = 'none';

            setTimeout(() => {
                currentQuestionIndex++;
                if (currentQuestionIndex < quizData.length) {
                    showQuestion();
                    optionsContainer.style.pointerEvents = 'auto';
                } else {
                    showResults();
                }
            }, 1500);
        }

        function showResults() {
            questionArea.classList.add('hidden');
            optionsContainer.classList.add('hidden');
            resultsContainer.classList.remove('hidden');

            resultsText.innerText = `Tu resultado final es ${score} de ${quizData.length} aciertos.`;
            
            let feedback = '';
            const percentage = (score / quizData.length) * 100;
            if (percentage >= 80) {
                feedback = '¡Excelente trabajo! Tienes un gran dominio.';
            } else if (percentage >= 50) {
                feedback = '¡Buen trabajo! Sigue repasando para mejorar.';
            } else {
                feedback = 'No te preocupes. ¡Este es un buen punto de partida para repasar!';
            }
            resultsFeedback.innerText = feedback;
        }

        restartButton.addEventListener('click', startQuiz);

        shareButton.addEventListener('click', () => {
            const message = encodeURIComponent(`¡Terminé la prueba diagnóstica de francés! Mi resultado fue ${score} de ${quizData.length}.`);
            const whatsappUrl = `https://wa.me/?text=${message}`;
            window.open(whatsappUrl, '_blank');
        });

        // Start the quiz on page load
        startQuiz();
    </script>
</body>
</html>
