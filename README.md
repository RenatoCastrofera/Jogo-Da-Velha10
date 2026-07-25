<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo da Velha Pro</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background-color: #111827; font-family: 'Inter', sans-serif; }
        .cell { transition: all 0.2s ease; cursor: pointer; display: flex; align-items: center; justify-content: center; height: 80px; width: 80px; }
        .cell:hover { background-color: #374151; }
    </style>
</head>
<body class="text-white flex flex-col items-center min-h-screen p-4">

    <h1 class="text-3xl font-bold mb-6 text-blue-400 mt-4">Jogo da Velha Pro</h1>
    
    <div class="flex flex-col gap-3 mb-6 w-full max-w-[320px]">
        <div class="flex gap-2">
            <input type="text" id="p1" placeholder="Jogador 1" class="bg-gray-700 p-2 rounded text-white flex-1 border border-gray-600">
            <input type="text" id="p2" placeholder="Jogador 2" class="bg-gray-700 p-2 rounded text-white flex-1 border border-gray-600">
        </div>
        <label class="flex items-center gap-2 cursor-pointer bg-gray-800 p-3 rounded-lg border border-gray-700">
            <input type="checkbox" id="modeToggle" class="w-5 h-5">
            <span>Jogar contra Computador</span>
        </label>
    </div>

    <div id="placar" class="text-lg mb-4 font-semibold text-gray-400">X: 0 | O: 0</div>

    <div id="board" class="grid grid-cols-3 gap-2 bg-gray-800 p-3 rounded-xl shadow-2xl w-full max-w-[270px]">
        <button class="cell bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(0)"></button>
        <button class="cell bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(1)"></button>
        <button class="cell bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(2)"></button>
        <button class="cell bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(3)"></button>
        <button class="cell bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(4)"></button>
        <button class="cell bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(5)"></button>
        <button class="cell bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(6)"></button>
        <button class="cell bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(7)"></button>
        <button class="cell bg-gray-700 rounded-lg text-4xl font-bold" onclick="play(8)"></button>
    </div>
    
    <button onclick="resetGame()" class="mt-6 px-8 py-3 bg-blue-600 rounded-full font-bold hover:bg-blue-500 transition shadow-lg">Reiniciar Partida</button>

    <div id="ad-container" class="mt-8 w-full max-w-[320px] min-h-[250px] flex items-center justify-center"></div>

    <script>
        let board = ["", "", "", "", "", "", "", "", ""];
        let currentPlayer = "X";
        let scoreX = 0, scoreO = 0;
        let gameActive = true;

        function play(index) {
            if (board[index] === "" && gameActive) {
                board[index] = currentPlayer;
                render();
                if (checkWinner()) return;
                currentPlayer = currentPlayer === "X" ? "O" : "X";
                if (document.getElementById('modeToggle').checked && currentPlayer === "O") {
                    gameActive = false;
                    setTimeout(aiMove, 500);
                }
            }
        }

        function aiMove() {
            let available = board.map((v, i) => v === "" ? i : null).filter(v => v !== null);
            if (available.length > 0) {
                let move = available[Math.floor(Math.random() * available.length)];
                board[move] = "O";
                render();
                if (!checkWinner()) { currentPlayer = "X"; gameActive = true; }
            }
        }

        function render() {
            const cells = document.querySelectorAll('.cell');
            board.forEach((val, i) => {
                cells[i].innerText = val;
                cells[i].className = `cell bg-gray-700 rounded-lg text-4xl font-bold ${val === 'X' ? 'text-blue-400' : 'text-red-400'}`;
            });
        }

        function checkWinner() {
            const w = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
            for (let c of w) {
                if (board[c[0]] && board[c[0]] === board[c[1]] && board[c[0]] === board[c[2]]) {
                    gameActive = false;
                    board[c[0]] === 'X' ? scoreX++ : scoreO++;
                    document.getElementById('placar').innerText = `X: ${scoreX} | O: ${scoreO}`;
                    return true;
                }
            }
            if (!board.includes("")) { gameActive = false; return true; }
            return false;
        }

        function resetGame() {
            board = Array(9).fill("");
            gameActive = true;
            currentPlayer = "X";
            render();
        }

        const adContainer = document.getElementById('ad-container');
        const s = document.createElement('script');
        s.src = 'https://www.profitabledisplaynetwork.com/5935670?format=300x250';
        adContainer.appendChild(s);
    </script>
</body>
</html>
