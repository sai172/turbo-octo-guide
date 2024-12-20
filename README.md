<!DOCTYPE html>
<html>
<head>
  <title>Turbo Octo Guide - Quiz App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 20px;
    }
    .quiz-container {
      max-width: 600px;
      margin: auto;
      text-align: left;
    }
    .question {
      font-size: 1.2em;
      margin-bottom: 20px;
    }
    .option {
      margin: 10px 0;
    }
    .result {
      font-size: 1.5em;
      margin-top: 20px;
      color: green;
    }
  </style>
</head>
<body>
  <h1>Turbo Octo Guide - Quiz App</h1>
  <div class="quiz-container">
    <div id="quiz-content">
      <!-- Dynamic content will be loaded here -->
    </div>
    <button id="submit" style="display:none;">Submit</button>
    <div id="result" class="result"></div>
  </div>

  <script>
    const quizData = [
      {
        question: "What does HTML stand for?",
        options: ["Hyper Text Markup Language", "High Text Machine Language", "Hyperlink and Text Markup Language"],
        correct: 0,
      },
      {
        question: "Which programming language is used for web apps?",
        options: ["Python", "JavaScript", "C++"],
        correct: 1,
      },
      {
        question: "What is the capital of France?",
        options: ["Berlin", "Madrid", "Paris"],
        correct: 2,
      },
    ];

    let currentQuestion = 0;
    let score = 0;

    function loadQuestion() {
      const quizContent = document.getElementById("quiz-content");
      quizContent.innerHTML = `
        <div class="question">${quizData[currentQuestion].question}</div>
        ${quizData[currentQuestion].options
          .map(
            (option, index) =>
              `<div class="option">
                <input type="radio" name="option" value="${index}" id="option${index}">
                <label for="option${index}">${option}</label>
              </div>`
          )
          .join("")}
      `;
      document.getElementById("submit").style.display = "block";
    }

    function handleSubmission() {
      const selectedOption = document.querySelector("input[name='option']:checked");
      if (!selectedOption) {
        alert("Please select an answer!");
        return;
      }

      const selectedValue = parseInt(selectedOption.value);
      if (selectedValue === quizData[currentQuestion].correct) {
        score++;
      }

      currentQuestion++;
      if (currentQuestion < quizData.length) {
        loadQuestion();
      } else {
        showResult();
      }
    }

    function showResult() {
      const resultDiv = document.getElementById("result");
      resultDiv.textContent = `You scored ${score} out of ${quizData.length}!`;
      document.getElementById("quiz-content").style.display = "none";
      document.getElementById("submit").style.display = "none";
    }

    document.getElementById("submit").addEventListener("click", handleSubmission);
    loadQuestion();
  </script>
</body>
</html>
