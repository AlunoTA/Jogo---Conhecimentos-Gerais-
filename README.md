<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Quiz Divertido e Colorido</title>
  <style>
    body {
      font-family: 'Comic Sans MS', sans-serif;
      background: linear-gradient(120deg, #f6d365, #fda085);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .quiz-container {
      background-color: #fff;
      border-radius: 20px;
      box-shadow: 0 10px 20px rgba(0,0,0,0.3);
      width: 90%;
      max-width: 550px;
      padding: 30px;
      text-align: center;
      animation: popIn 0.5s ease;
    }
    @keyframes popIn {
      0% { transform: scale(0.8); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }
    h2 {
      font-size: 24px;
      margin-bottom: 15px;
      color: #ff4b5c;
      text-shadow: 1px 1px 2px #fff;
    }
    p {
      font-size: 18px;
      margin-bottom: 25px;
      color: #333;
    }
    .option {
      display: block;
      width: 100%;
      background-color: #ffecd2;
      border: 2px solid #ff4b5c;
      color: #333;
      border-radius: 12px;
      padding: 14px;
      margin-bottom: 15px;
      cursor: pointer;
      font-size: 16px;
      transition: transform 0.2s, background-color 0.2s;
      box-shadow: 2px 2px 5px rgba(0,0,0,0.2);
    }
    .option:hover {
      transform: scale(1.05);
      background-color: #ffe0b3;
    }
    .btn {
      background-color: #ff4b5c;
      color: white;
      border: none;
      padding: 12px 20px;
      border-radius: 12px;
      font-size: 16px;
      cursor: pointer;
      margin-top: 15px;
      transition: background-color 0.2s, transform 0.2s;
    }
    .btn:hover {
      background-color: #ff1c3d;
      transform: scale(1.05);
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <h2 id="question-number">Pergunta 1 de 10</h2>
    <p id="question-text">Carregando pergunta...</p>
    <div id="options"></div>
  </div>

  <script>
    const questions = [
      { question: "Qual é o país com a maior população do mundo?", options: ["Índia","China","Estados Unidos","Indonésia"], answer: "Índia" },
      { question: "Quem pintou a Mona Lisa?", options: ["Van Gogh","Leonardo da Vinci","Michelangelo","Picasso"], answer: "Leonardo da Vinci" },
      { question: "Qual é o menor país do mundo?", options: ["Mônaco","Vaticano","Malta","San Marino"], answer: "Vaticano" },
      { question: "Em que continente fica o Egito?", options: ["Ásia","Europa","África","América"], answer: "África" },
      { question: "Quem escreveu 'Dom Quixote'?", options: ["William Shakespeare","Miguel de Cervantes","José Saramago","Machado de Assis"], answer: "Miguel de Cervantes" },
      { question: "Qual é o elemento químico representado por 'O'?", options: ["Ouro","Ósmio","Oxigênio","Oxalato"], answer: "Oxigênio" },
      { question: "Quantos planetas há no Sistema Solar?", options: ["7","8","9","10"], answer: "8" },
      { question: "Qual é a capital do Canadá?", options: ["Toronto","Ottawa","Vancouver","Montreal"], answer: "Ottawa" },
      { question: "Quem foi o primeiro homem a pisar na Lua?", options: ["Buzz Aldrin","Neil Armstrong","Yuri Gagarin","Michael Collins"], answer: "Neil Armstrong" },
      { question: "Qual é o maior oceano do planeta?", options: ["Atlântico","Índico","Pacífico","Antártico"], answer: "Pacífico" }
    ];

    let current = 0;
    let score = 0;

    const questionNumber = document.getElementById("question-number");
    const questionText = document.getElementById("question-text");
    const optionsDiv = document.getElementById("options");
    const container = document.querySelector(".quiz-container");

    function showQuestion() {
      const q = questions[current];
      questionNumber.textContent = `Pergunta ${current + 1} de ${questions.length}`;
      questionText.textContent = q.question;
      optionsDiv.innerHTML = "";

      q.options.forEach(option => {
        const btn = document.createElement("button");
        btn.classList.add("option");
        btn.textContent = option;
        btn.onclick = () => handleAnswer(option);
        optionsDiv.appendChild(btn);
      });
    }

    function handleAnswer(selected) {
      if(selected === questions[current].answer) score++;
      current++;
      if(current < questions.length) {
        showQuestion();
      } else {
        showResult();
      }
    }

    function showResult() {
      container.innerHTML = `<h2>Resultado 🎉</h2><p>Você acertou ${score} de ${questions.length} perguntas!</p><button class='btn' onclick='restartQuiz()'>Jogar novamente</button>`;
    }

    function restartQuiz() {
      current = 0;
      score = 0;
      container.innerHTML = `<h2 id='question-number'></h2><p id='question-text'></p><div id='options'></div>`;
      showQuestion();
    }

    showQuestion();
  </script>
</body>
</html>
