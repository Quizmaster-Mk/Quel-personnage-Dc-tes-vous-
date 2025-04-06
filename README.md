<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quel personnage de DC êtes-vous ?</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #282828;
      color: white;
      padding: 20px;
      text-align: center;
    }

    h1 {
      color: #FF5733;
    }

    .question {
      margin: 20px 0;
      background-color: #444;
      padding: 20px;
      border-radius: 10px;
    }

    .options button {
      background-color: #ff6f61;
      color: white;
      padding: 10px 20px;
      border: none;
      margin: 5px;
      font-size: 16px;
      cursor: pointer;
      border-radius: 5px;
      transition: 0.3s;
    }

    .options button:hover {
      background-color: #ff3b2e;
    }

    .result {
      background-color: #444;
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      display: none;
    }

    .score {
      font-size: 20px;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <h1>Quel personnage de DC êtes-vous ?</h1>

  <div id="quiz-container">
    <div class="question" id="question-container">
      <h2 id="question-text"></h2>
      <div class="options" id="options-container"></div>
    </div>
  </div>

  <div class="result" id="result-container">
    <h2>Vous êtes...</h2>
    <p id="result-text"></p>
    <p class="score">Votre résultat est basé sur vos choix !</p>
    <button onclick="startQuiz()">Recommencer le quiz</button>
  </div>

  <script>
    const questions = [
      {
        question: "Quelle est votre principale motivation ?",
        options: ["Justice", "Vengeance", "Liberté", "Protection des innocents"],
        result: [0, 1, 2, 3]  // Chaque index mène à un personnage différent
      },
      {
        question: "Quel est votre style de combat préféré ?",
        options: ["Tactique et intelligence", "Force brute", "Vitesse", "Stratégie et technologie"],
        result: [3, 1, 2, 0]
      },
      {
        question: "Quel type d'ennemi vous inspire le plus ?",
        options: ["Des criminels", "Des tyrans", "Des ennemis avec des pouvoirs surhumains", "Des extraterrestres"],
        result: [0, 1, 2, 3]
      },
      {
        question: "Quel est votre plus grand défaut ?",
        options: ["Impulsivité", "Colère", "Doute", "Isolement"],
        result: [1, 0, 3, 2]
      },
      {
        question: "Si vous pouviez choisir un super pouvoir, lequel serait-ce ?",
        options: ["Vol", "Invulnérabilité", "Téléportation", "Super-force"],
        result: [2, 3, 0, 1]
      }
    ];

    const characters = [
      { name: "Batman", description: "Le détective et maître tacticien. Préfère la stratégie à la force brute." },
      { name: "Superman", description: "L'homme d'acier. Combattant impitoyable pour la justice et la paix." },
      { name: "Flash", description: "Le scarlet speedster. Vitesse incroyable et optimisme à toute épreuve." },
      { name: "Wonder Woman", description: "Princesse amazone. Combattante sans égal, protectrice des innocents." }
    ];

    let currentQuestion = 0;
    let userAnswers = [];

    function startQuiz() {
      currentQuestion = 0;
      userAnswers = [];
      document.getElementById('result-container').style.display = 'none';
      document.getElementById('quiz-container').style.display = 'block';
      showQuestion();
    }

    function showQuestion() {
      const question = questions[currentQuestion];
      document.getElementById('question-text').innerText = question.question;
      
      const optionsContainer = document.getElementById('options-container');
      optionsContainer.innerHTML = '';  // Clear previous options
      
      question.options.forEach((option, index) => {
        const button = document.createElement('button');
        button.innerText = option;
        button.onclick = () => {
          userAnswers.push(question.result[index]);
          currentQuestion++;
          if (currentQuestion < questions.length) {
            showQuestion();
          } else {
            showResult();
          }
        };
        optionsContainer.appendChild(button);
      });
    }

    function showResult() {
      const resultIndex = userAnswers.reduce((a, b) => a + b, 0) % characters.length;
      const result = characters[resultIndex];
      
      document.getElementById('result-text').innerText = `${result.name} - ${result.description}`;
      document.getElementById('quiz-container').style.display = 'none';
      document.getElementById('result-container').style.display = 'block';
    }

    // Initialisation du quiz
    startQuiz();
  </script>
</body>
</html>
