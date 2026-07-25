<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo da Velha Pro</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background-color: #111827; font-family: 'Inter', sans-serif; }
        .cell { transition: all 0.2s ease; cursor: pointer; display: flex; align-items: center; justify-content: center; }
        .cell:hover { background-color: #374151; }
        .board-grid { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 12px; }
    </style>
</head>
<body class="text-white flex flex-col items-center justify-center min-h-screen p-4">

    <div id="ad-container" class="mb-6 w-full max-w-[320px] h-[250px] bg-gray-800 rounded-lg flex items-center justify-center border border-gray-700">
        <script type="text/javascript" src="https://www.profitabledisplaynetwork.com/5935670?format=300x250"></script>
    </div>

    <h1 class="text-3xl font-bold mb-2 text-blue-400">Jogo da Velha</h1>
    
    <div class="flex gap-4 mb-4">
        <input type="text" id="p1" placeholder="Nome Jogador" class="bg-gray-700 p-2 rounded text-white w-32">
        <input type="text" id="p2" placeholder="Computador" value="Computador" class="bg-gray-700 p-2 rounded text-white w-32" disabled>
    </div>

    <div id="placar" class="text-lg mb-6 font-semibold text-gray-400">X: 0 | O: 0</div>

    <div id="board" class="board-grid bg-gray-800 p-4 rounded-xl shadow-2xl w-full max-w-[320px]">
        <button class="cell w-20 h-20 bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(0)"></button>
        <button class="cell w-20 h-20 bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(1)"></button>
        <button class="cell w-20 h-20 bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(2)"></button>
        <button class="cell w-20 h-20 bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(3)"></button>
        <button class="cell w-20 h-20 bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(4)"></button>
        <button class="cell w-20 h-20 bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(5)"></button>
        <button class="cell w-20 h-20 bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(6)"></button>
        <button class="cell w-20 h-20 bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(7)"></button>
        <button class="cell w-20 h-20 bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(8)"></button>
    </div>
    
    <button onclick="resetGame()" class="mt-8 px-8 py-3 bg-blue-600 rounded-full font-bold hover:bg-blue-500 transition">Reiniciar Partida</button>

    <script>
        let board = ["", "", "", "", "", "", "", "", ""];
        let human = "X";
        let ai = "O";
        let scoreX = 0, scoreO = 0;
        let gameActive = true;

        function play(index) {
            if (board[index] === "" && gameActive) {
                board[index] = human;
                updateBoard();
                if (checkWinner()) return;
                gameActive = false;
                setTimeout(aiMove, 500);
            }
        }

        function aiMove() {
            let available = board.map((v, i) => v === "" ? i : null).filter(v => v !== null);
            if (available.length > 0) {
                let move = available[Math.floor(Math.random() * available.length)];
                board[move] = ai;
                updateBoard();
                checkWinner();
                gameActive = true;
            }
        }

        function updateBoard() {
            const cells = document.querySelectorAll('.cell');
            board.forEach((val, i) => {
                cells[i].innerText = val;
                cells[i].className = `cell w-20 h-20 bg-gray-700 rounded-lg text-4xl font-bold ${val === 'X' ? 'text-blue-400' : 'text-red-400'}`;
            });
        }

        function checkWinner() {
            const wins = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
            for (let w of wins) {
                if (board[w[0]] && board[w[0]] === board[w[1]] && board[w[0]] === board[w[2]]) {
                    gameActive = false;
                    board[w[0]] === human ? scoreX++ : scoreO++;
                    document.getElementById('placar').innerText = `X: ${scoreX} | O: ${scoreO}`;
                    return true;
                }
            }
            if (!board.includes("")) { gameActive = false; return true; }
            return false;
        }

        function resetGame() {
            board = ["", "", "", "", "", "", "", "", ""];
            gameActive = true;
            updateBoard();
        }
    </script>
</body>
</html>
