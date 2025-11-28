# TicTaeToep
Css/Html/JavaScript

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Tic Tac Toe</h1>
    <div class="game-container">
        <div class="cell" data-index="0"></div>
        <div class="cell" data-index="1"></div>
        <div class="cell" data-index="2"></div>
        <div class="cell" data-index="3"></div>
        <div class="cell" data-index="4"></div>
        <div class="cell" data-index="5"></div>
        <div class="cell" data-index="6"></div>
        <div class="cell" data-index="7"></div>
        <div class="cell" data-index="8"></div>
    </div>
    <p id="status">Player X's turn</p>
    <button id="reset">Reset Game</button>

    <script src="script.js"></script>
</body>
</html>


const cells = document.querySelectorAll('.cell');
const statusText = document.getElementById('status');
const resetButton = document.getElementById('reset');

let currentPlayer = 'X';
let board = Array(9).fill('');

const winConditions = [
    [0,1,2],[3,4,5],[6,7,8], // rows
    [0,3,6],[1,4,7],[2,5,8], // columns
    [0,4,8],[2,4,6]          // diagonals
];

function handleClick(e) {
    const index = e.target.dataset.index;

    if(board[index] !== '' || checkWinner()) return;

    board[index] = currentPlayer;
    e.target.textContent = currentPlayer;
    e.target.style.color = currentPlayer === 'X' ? '#6a11cb' : '#2575fc';

    if(checkWinner()) {
        statusText.textContent = `Player ${currentPlayer} wins! 🎉`;
        return;
    }

    if(board.every(cell => cell !== '')) {
        statusText.textContent = `It's a draw! 🤝`;
        return;
    }

    currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
    statusText.textContent = `Player ${currentPlayer}'s turn`;
}

function checkWinner() {
    return winConditions.some(condition => {
        const [a,b,c] = condition;
        return board[a] && board[a] === board[b] && board[a] === board[c];
    });
}

function resetGame() {
    board = Array(9).fill('');
    cells.forEach(cell => cell.textContent = '');
    currentPlayer = 'X';
    statusText.textContent = `Player ${currentPlayer}'s turn`;
}

// Add event listeners
cells.forEach(cell => cell.addEventListener('click', handleClick));
resetButton.addEventListener('click', resetGame);






body {
    display: flex;
    flex-direction: column;
    align-items: center;
    font-family: 'Arial', sans-serif;
    background: linear-gradient(to right, #6a11cb, #2575fc);
    color: white;
    height: 100vh;
    margin: 0;
    padding: 20px;
}

h1 {
    margin-bottom: 20px;
    text-shadow: 2px 2px 5px #000;
}

.game-container {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-template-rows: repeat(3, 100px);
    gap: 10px;
}

.cell {
    width: 100px;
    height: 100px;
    background-color: #fff;
    border-radius: 15px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 3rem;
    cursor: pointer;
    transition: transform 0.2s;
}

.cell:hover {
    transform: scale(1.1);
    background-color: #f0f0f0;
}

#status {
    margin-top: 20px;
    font-size: 1.5rem;
}

button {
    margin-top: 20px;
    padding: 10px 20px;
    font-size: 1rem;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    background-color: #ff6b6b;
    color: white;
    transition: background-color 0.3s;
}

button:hover {
    background-color: #ff4757;
}







