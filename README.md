<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo da Velha</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .cell { transition: all 0.2s ease; cursor: pointer; }
        .cell:hover { background-color: #374151; }
    </style>
</head>
<body class="bg-gray-900 text-white flex flex-col items-center justify-center min-h-screen font-sans p-4">
    
    <h1 class="text-4xl font-bold mb-4 text-blue-400">Jogo da Velha</h1>
    <div id="placar" class="text-xl mb-4 font-semibold text-gray-300">Jogador X: 0 | Jogador O: 0</div>

    <div id="ad-container" class="my-4 w-[320px] h-[250px] bg-gray-800 rounded-lg shadow-xl flex items-center justify-center border border-gray-700 overflow-hidden">
        <!-- COLE O SEU SCRIPT AQUI -->
        <script type="text/javascript" src="https://www.profitabledisplaynetwork.com/5935670?format=300x250"></script>
    </div>

    <div id="board" class="grid grid-cols-3 gap-3 bg-gray-800 p-4 rounded-xl shadow-2xl">
        <!-- Criando células -->
        <button class="cell w-20 h-20 bg-gray-700 border-2 border-gray-600 text-4xl font-bold rounded-lg" onclick="clickCell(0)"></button>
        <button class="cell w-20 h-20 bg-gray-700 border-2 border-gray-600 text-4xl font-bold rounded-lg" onclick="clickCell(1)"></button>
        <button class="cell w-20 h-20 bg-gray-700 border-2 border-gray-600 text-4xl font-bold rounded-lg" onclick="clickCell(2)"></button>
        <button class="cell w-20 h-20 bg-gray-700 border-2 border-gray-600 text-4xl font-bold rounded-lg" onclick="clickCell(3)"></button>
        <button class="cell w-20 h-20 bg-gray-700 border-2 border-gray-600 text-4xl font-bold rounded-lg" onclick="clickCell(4)"></button>
        <button class="cell w-20 h-20 bg-gray-700 border-2 border-gray-600 text-4xl font-bold rounded-lg" onclick="clickCell(5)"></button>
        <button class="cell w-20 h-20 bg-gray-700 border-2 border-gray-600 text-4xl font-bold rounded-lg" onclick="clickCell(6)"></button>
        <button class="cell w-20 h-20 bg-gray-700 border-2 border-gray-600 text-4xl font-bold rounded-lg" onclick="clickCell(7)"></button>
        <button class="cell w-20 h-20 bg-gray-700 border-2 border-gray-600 text-4xl font-bold rounded-lg" onclick="clickCell(8)"></button>
    </div>
    
    <button onclick="resetGame()" class="mt-8 px-8 py-3 bg-blue-600 text-white font-bold rounded-full hover:bg-blue-500 transition shadow-lg">Reiniciar Partida</button>

    <script>
        let board = ["", "", "", "", "", "", "", "", ""];
        let currentPlayer = "X";
        let scoreX = 0, scoreO = 0;
        let gameActive = true;

        function clickCell(index) {
            if(board[index] === "" && gameActive) {
                board[index] = currentPlayer;
                const buttons = document.querySelectorAll('.cell');
                buttons[index].innerText = currentPlayer;
                buttons[index].classList.add(currentPlayer === 'X' ? 'text-blue-400' : 'text-red-400');
                
                // Lógica de verificação simplificada
                checkWin();
            }
        }

        function checkWin() {
            const winConditions = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
            for (let condition of winConditions) {
                let [a, b, c] = condition;
                if (board[a] && board[a] === board[b] && board[a] === board[c]) {
                    gameActive = false;
                    if (currentPlayer === "X") scoreX++; else scoreO++;
                    document.getElementById('placar').innerText = `Jogador X: ${scoreX} | Jogador O: ${scoreO}`;
                    return;
                }
            }
            if (!board.includes("")) gameActive = false;
            currentPlayer = currentPlayer === "X" ? "O" : "X";
        }

        function resetGame() {
            board = ["", "", "", "", "", "", "", "", ""];
            gameActive = true;
            document.querySelectorAll('.cell').forEach(btn => {
                btn.innerText = "";
                btn.classList.remove('text-blue-400', 'text-red-400');
            });
        }
    </script>
</body>
</html>
