<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo da Velha</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 flex flex-col items-center justify-center min-h-screen">
    <h1 class="text-4xl font-bold mb-4">Jogo da Velha</h1>
    <div id="placar" class="text-xl mb-4">Jogador X: 0 | Jogador O: 0</div>

    <!-- Container do Anúncio -->
    <div id="banner-container" class="my-4 p-2 bg-white rounded-lg shadow-md">
        <!-- O script do Adsterra virá aqui -->
        <script type="text/javascript" src="https://www.profitabledisplaynetwork.com/5935670?format=300x250"></script>
    </div>

    <!-- Grid do Jogo -->
    <div id="board" class="grid grid-cols-3 gap-2">
        <button class="w-20 h-20 bg-white border-2 border-gray-300 text-3xl font-bold" onclick="clickCell(0)"></button>
        <button class="w-20 h-20 bg-white border-2 border-gray-300 text-3xl font-bold" onclick="clickCell(1)"></button>
        <button class="w-20 h-20 bg-white border-2 border-gray-300 text-3xl font-bold" onclick="clickCell(2)"></button>
        <button class="w-20 h-20 bg-white border-2 border-gray-300 text-3xl font-bold" onclick="clickCell(3)"></button>
        <button class="w-20 h-20 bg-white border-2 border-gray-300 text-3xl font-bold" onclick="clickCell(4)"></button>
        <button class="w-20 h-20 bg-white border-2 border-gray-300 text-3xl font-bold" onclick="clickCell(5)"></button>
        <button class="w-20 h-20 bg-white border-2 border-gray-300 text-3xl font-bold" onclick="clickCell(6)"></button>
        <button class="w-20 h-20 bg-white border-2 border-gray-300 text-3xl font-bold" onclick="clickCell(7)"></button>
        <button class="w-20 h-20 bg-white border-2 border-gray-300 text-3xl font-bold" onclick="clickCell(8)"></button>
    </div>

    <script>
        let board = ["", "", "", "", "", "", "", "", ""];
        let currentPlayer = "X";
        function clickCell(index) {
            if(board[index] === "") {
                board[index] = currentPlayer;
                event.target.innerText = currentPlayer;
                currentPlayer = currentPlayer === "X" ? "O" : "X";
            }
        }
    </script>
</body>
</html>
