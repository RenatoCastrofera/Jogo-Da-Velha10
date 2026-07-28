<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo da Velha PRO</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background-color: #111827; font-family: 'Inter', sans-serif; }
        .cell { transition: all 0.2s ease; cursor: pointer; display: flex; align-items: center; justify-content: center; height: 80px; width: 80px; }
        .cell:hover:not(:disabled) { background-color: #374151; }
        .cell:disabled { cursor: not-allowed; opacity: 0.85; }
        .winning-cell { background-color: #1d4ed8 !important; }
    </style>
</head>
<body class="text-white flex flex-col items-center min-h-screen p-4">

    <h1 class="text-3xl font-bold mb-6 text-blue-400 mt-4">Jogo da Velha PRO</h1>

    <label class="flex items-center gap-2 cursor-pointer bg-gray-800 p-3 rounded-lg border border-gray-700 mb-6 w-full max-w-[270px] justify-center">
        <input type="checkbox" id="modeToggle" class="w-5 h-5" onchange="resetGame()">
        <span>Jogar contra Computador</span>
    </label>

    <div id="placar" class="text-lg mb-2 font-semibold text-gray-400">X: 0 | O: 0</div>
    <div id="status" class="text-lg mb-4 font-bold text-yellow-400 h-6 text-center"></div>

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

    <div class="flex gap-3 mt-6">
        <button onclick="resetGame()" class="px-8 py-3 bg-blue-600 rounded-full font-bold hover:bg-blue-500 transition shadow-lg">Reiniciar Partida</button>
        <button onclick="resetScore()" class="px-4 py-3 bg-gray-700 rounded-full text-sm hover:bg-gray-600 transition">Zerar Placar</button>
    </div>

    <!-- Container do Banner -->
    <div id="ad-wrapper" class="mt-8 w-full max-w-[320px] min-h-[250px] flex items-center justify-center bg-gray-900 rounded-xl overflow-hidden border border-gray-700">
        <div id="ad-container"></div>
    </div>

    <script>
        let board = Array(9).fill("");
        let currentPlayer = "X";
        let scoreX = 0, scoreO = 0;
        let gameActive = true;

        function vsComputer() { return document.getElementById('modeToggle').checked; }
        function labelOf(player) { return (player === "O" && vsComputer()) ? "Computador" : player; }

        function play(index) {
            if (!gameActive || board[index] !== "") return;
            if (vsComputer() && currentPlayer === "O") return; // impede clique durante a vez do computador

            board[index] = currentPlayer;
            render();
            if (checkEnd()) return;
            currentPlayer = currentPlayer === "X" ? "O" : "X";
            updateStatus();
            if (vsComputer() && currentPlayer === "O" && gameActive) setTimeout(aiMove, 500);
        }

        function aiMove() {
            if (!gameActive) return;
            let available = board.map((v, i) => v === "" ? i : null).filter(v => v !== null);
            if (available.length === 0) return;
            let move = available[Math.floor(Math.random() * available.length)];
            board[move] = "O";
            render();
            if (checkEnd()) return;
            currentPlayer = "X";
            updateStatus();
        }

        function render() {
            const cells = document.querySelectorAll('.cell');
            board.forEach((val, i) => {
                cells[i].innerText = val;
                cells[i].className = `cell bg-gray-700 rounded-lg text-4xl font-bold ${val === 'X' ? 'text-blue-400' : 'text-red-400'}`;
                cells[i].disabled = val !== "" || !gameActive;
            });
        }

        function checkEnd() {
            const w = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
            const cells = document.querySelectorAll('.cell');
            for (let c of w) {
                if (board[c[0]] && board[c[0]] === board[c[1]] && board[c[0]] === board[c[2]]) {
                    gameActive = false;
                    board[c[0]] === 'X' ? scoreX++ : scoreO++;
                    document.getElementById('placar').innerText = `X: ${scoreX} | O: ${scoreO}`;
                    document.getElementById('status').innerText = `🏆 ${labelOf(board[c[0]])} venceu!`;
                    render();
                    c.forEach(i => cells[i].classList.add('winning-cell'));
                    return true;
                }
            }
            if (!board.includes("")) {
                gameActive = false;
                document.getElementById('status').innerText = "🤝 Empate!";
                render();
                return true;
            }
            return false;
        }

        function updateStatus() {
            if (!gameActive) return;
            document.getElementById('status').innerText = `Vez de: ${labelOf(currentPlayer)}`;
        }

        function resetGame() {
            board = Array(9).fill("");
            gameActive = true;
            currentPlayer = "X";
            render();
            updateStatus();
        }

        function resetScore() {
            scoreX = 0;
            scoreO = 0;
            document.getElementById('placar').innerText = `X: 0 | O: 0`;
        }

        resetGame();

        // Carregamento otimizado do anúncio
        window.onload = () => {
            const container = document.getElementById('ad-container');
            const script = document.createElement('script');
            script.src = 'https://www.profitabledisplaynetwork.com/5935670?format=300x250';
            script.async = true;
            container.appendChild(script);
        };
    </script>
</body>
</html>
