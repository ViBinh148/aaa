<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trắc nghiệm: Phương Trình Tiếp Tuyến</title>
    <link rel="stylesheet" href="style.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Be+Vietnam+Pro:wght@400;500;700&display=swap" rel="stylesheet">
</head>
<body>
    <div class="quiz-container" id="quiz">
        <div class="quiz-header">
            <h2 id="question">Câu hỏi được tải ở đây</h2>
            <ul>
                <li>
                    <input type="radio" name="answer" id="a" class="answer">
                    <label for="a" id="a_text">Đáp án A</label>
                </li>
                <li>
                    <input type="radio" name="answer" id="b" class="answer">
                    <label for="b" id="b_text">Đáp án B</label>
                </li>
                <li>
                    <input type="radio" name="answer" id="c" class="answer">
                    <label for="c" id="c_text">Đáp án C</label>
                </li>
                <li>
                    <input type="radio" name="answer" id="d" class="answer">
                    <label for="d" id="d_text">Đáp án D</label>
                </li>
            </ul>
        </div>
        <button id="submit">Nộp bài</button>
    </div>

    <script src="script.js"></script>
</body>
</html>
```

#### **2. File `style.css` (Giao diện 3D đẹp mắt)**
```css
:root {
    --bg-color: #e0e0e0;
    --primary-color: #4a90e2;
    --correct-color: #87d37c;
    --incorrect-color: #e74c3c;
    --text-color: #3d3d3d;
}

* {
    box-sizing: border-box;
}

body {
    background-color: var(--bg-color);
    font-family: 'Be Vietnam Pro', sans-serif;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    overflow: hidden;
    margin: 0;
}

.quiz-container {
    background-color: var(--bg-color);
    border-radius: 20px;
    box-shadow: 20px 20px 60px #bebebe, -20px -20px 60px #ffffff;
    width: 600px;
    max-width: 95vw;
    overflow: hidden;
}

.quiz-header {
    padding: 2rem 3rem;
}

h2 {
    padding: 1rem;
    text-align: center;
    margin: 0;
    color: var(--text-color);
    font-weight: 500;
}

ul {
    list-style-type: none;
    padding: 0;
}

ul li {
    font-size: 1.1rem;
    margin: 1.2rem 0;
    cursor: pointer;
}

ul li label {
    cursor: pointer;
    width: 100%;
    display: block;
    padding: 1rem;
    border-radius: 10px;
    transition: all 0.2s ease-in-out;
}

ul li input[type="radio"] {
    display: none;
}

ul li label {
    box-shadow: 5px 5px 10px #bebebe, -5px -5px 10px #ffffff;
}

ul li label:hover {
    box-shadow: 7px 7px 12px #bebebe, -7px -7px 12px #ffffff;
}

ul li input[type="radio"]:checked + label {
    background-color: var(--primary-color);
    color: white;
    box-shadow: inset 5px 5px 10px #3a72b5, inset -5px -5px 10px #5aaeff;
}

button {
    background-color: var(--primary-color);
    color: #fff;
    border: none;
    display: block;
    width: 100%;
    cursor: pointer;
    font-size: 1.3rem;
    font-family: inherit;
    font-weight: 700;
    padding: 1.3rem;
    transition: background-color 0.2s ease, transform 0.1s ease;
}

button:hover {
    background-color: #3a72b5;
}

button:active {
    transform: scale(0.98);
}

.correct {
    background-color: var(--correct-color);
    color: white !important;
    box-shadow: inset 5px 5px 10px #6faa67, inset -5px -5px 10px #a0fca2 !important;
}

.incorrect {
    background-color: var(--incorrect-color);
    color: white !important;
    box-shadow: inset 5px 5px 10px #b93d30, inset -5px -5px 10px #ff5b4a !important;
}

```

#### **3. File `script.js` (Bộ não của ứng dụng)**
```javascript
// --- NGÂN HÀNG CÂU HỎI ---
const quizData = [
    {
        question: "Hệ số góc của tiếp tuyến với đồ thị hàm số y = x³ - 2x tại điểm có hoành độ x₀ = 1 là bao nhiêu?",
        a: "-1",
        b: "0",
        c: "1",
        d: "2",
        correct: "c",
    },
    {
        question: "Phương trình tiếp tuyến của đồ thị hàm số y = x² - 4x + 3 tại điểm M(1, 0) là:",
        a: "y = 2x - 2",
        b: "y = -2x + 2",
        c: "y = x - 1",
        d: "y = -x + 1",
        correct: "b",
    },
    {
        question: "Viết phương trình tiếp tuyến của đường cong y = (2x+1)/(x-1) tại điểm có hoành độ x₀ = 2.",
        a: "y = -3x + 11",
        b: "y = 3x - 1",
        c: "y = -3x + 1",
        d: "y = -3x + 7",
        correct: "a",
    },
    {
        question: "Tiếp tuyến của đồ thị hàm số y = x³ - 3x² + 1 tại điểm có hoành độ x₀ = 0 có phương trình là:",
        a: "y = 1",
        b: "y = 0",
        c: "y = x + 1",
        d: "y = -x + 1",
        correct: "a",
    },
    {
        question: "Cho hàm số y = x⁴ - 2x². Phương trình tiếp tuyến tại điểm M có hoành độ x₀ = -1 là:",
        a: "y = 4x + 3",
        b: "y = -4x - 5",
        c: "y = -4x - 3",
        d: "y = 4x - 5",
        correct: "c",
    },
     {
        question: "Hệ số góc của tiếp tuyến của đường tròn (C): x² + y² = 25 tại điểm M(3, 4) là:",
        a: "3/4",
        b: "-3/4",
        c: "4/3",
        d: "-4/3",
        correct: "b",
    },
    {
        question: "Tìm phương trình tiếp tuyến của (P): y = -x² + 4x, biết tiếp tuyến song song với đường thẳng y = 2x.",
        a: "y = 2x - 1",
        b: "y = 2x + 1",
        c: "y = 2x + 3",
        d: "y = 2x - 3",
        correct: "b",
    }
];

// --- LOGIC CỦA ỨNG DỤNG ---
const quiz = document.getElementById('quiz');
const answerEls = document.querySelectorAll('.answer');
const questionEl = document.getElementById('question');
const a_text = document.getElementById('a_text');
const b_text = document.getElementById('b_text');
const c_text = document.getElementById('c_text');
const d_text = document.getElementById('d_text');
const submitBtn = document.getElementById('submit');

let currentQuiz = 0;
let score = 0;
let shuffledQuizData = [];

function shuffleArray(array) {
    for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
    }
}

function startQuiz() {
    currentQuiz = 0;
    score = 0;
    submitBtn.innerText = "Nộp bài";
    
    // Tạo một bản sao và xáo trộn nó
    shuffledQuizData = [...quizData];
    shuffleArray(shuffledQuizData);

    loadQuiz();
}

function loadQuiz() {
    deselectAnswers();
    const currentQuizData = shuffledQuizData[currentQuiz];

    questionEl.innerText = currentQuizData.question;
    a_text.innerText = currentQuizData.a;
    b_text.innerText = currentQuizData.b;
    c_text.innerText = currentQuizData.c;
    d_text.innerText = currentQuizData.d;
}

function deselectAnswers() {
    answerEls.forEach(answerEl => {
        answerEl.checked = false;
        // Xóa các lớp màu phản hồi
        document.querySelector(`label[for=${answerEl.id}]`).classList.remove('correct', 'incorrect');
    });
}

function getSelected() {
    let answer;
    answerEls.forEach(answerEl => {
        if (answerEl.checked) {
            answer = answerEl.id;
        }
    });
    return answer;
}

submitBtn.addEventListener('click', () => {
    const answer = getSelected();
    
    if (answer) {
        const currentQuizData = shuffledQuizData[currentQuiz];
        const correctAnswer = currentQuizData.correct;
        const correctLabel = document.querySelector(`label[for=${correctAnswer}]`);

        if (answer === correctAnswer) {
            score++;
            correctLabel.classList.add('correct');
        } else {
            const selectedLabel = document.querySelector(`label[for=${answer}]`);
            selectedLabel.classList.add('incorrect');
            correctLabel.classList.add('correct');
        }

        currentQuiz++;

        setTimeout(() => {
            if (currentQuiz < shuffledQuizData.length) {
                loadQuiz();
            } else {
                quiz.innerHTML = `
                    <h2>Bạn đã trả lời đúng ${score}/${shuffledQuizData.length} câu hỏi.</h2>
                    <button onclick="startQuiz()">Tạo đề mới</button>
                `;
            }
        }, 1500); // Đợi 1.5 giây để người dùng xem kết quả
    } else {
        alert("Vui lòng chọn một đáp án!");
    }
});

// Bắt đầu bài kiểm tra khi tải trang
startQuiz();
