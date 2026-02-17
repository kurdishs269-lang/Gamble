<!DOCTYPE html>
<html>
<head>
    <title>Fake Money Slot Machine</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #222;
            color: white;
        }
        .slot-container {
            font-size: 50px;
            margin: 20px;
        }
        button {
            padding: 10px 20px;
            font-size: 18px;
            cursor: pointer;
            background-color: gold;
            border: none;
            border-radius: 5px;
        }
        input {
            padding: 5px;
            font-size: 16px;
            width: 80px;
            text-align: center;
        }
        .money {
            font-size: 22px;
            margin: 15px;
        }
    </style>
</head>
<body>

    <h1>🎰 Fake Money Slot Machine</h1>

    <div class="money">
        Balance: $<span id="balance">1000</span>
    </div>

    <div>
        Bet: $<input type="number" id="bet" value="50" min="1">
    </div>

    <div class="slot-container">
        <span id="slot1">❓</span>
        <span id="slot2">❓</span>
        <span id="slot3">❓</span>
    </div>

    <button onclick="spin()">Spin</button>
    <button onclick="resetGame()">Restart Game</button>

    <p id="result"></p>

    <script>
        let balance = 1000;
        const symbols = ["🍒", "🍋", "🍉", "⭐", "💎"];

        function spin() {
            let bet = parseInt(document.getElementById("bet").value);

            if (balance <= 0) {
                alert("Game Over! Restart the game to play again.");
                return;
            }

            if (bet > balance || bet <= 0) {
                alert("Invalid bet amount!");
                return;
            }

            // Deduct the bet amount
            balance -= bet;

            // Generate random slot symbols
            let slot1 = symbols[Math.floor(Math.random() * symbols.length)];
            let slot2 = symbols[Math.floor(Math.random() * symbols.length)];
            let slot3 = symbols[Math.floor(Math.random() * symbols.length)];

            // Display slots after the "spin"
            document.getElementById("slot1").textContent = slot1;
            document.getElementById("slot2").textContent = slot2;
            document.getElementById("slot3").textContent = slot3;

            let resultText = "";

            // Check results
            if (slot1 === slot2 && slot2 === slot3) {
                let winAmount = bet * 5;
                balance += winAmount;
                resultText = "🎉 JACKPOT! You won $" + winAmount;
            } else if (slot1 === slot2 || slot2 === slot3 || slot1 === slot3) {
                let winAmount = bet * 2;
                balance += winAmount;
                resultText = "✨ Nice! You won $" + winAmount;
            } else {
                resultText = "😢 You lost $" + bet;
            }

            // Update results and balance
            document.getElementById("balance").textContent = balance;
            document.getElementById("result").textContent = resultText;

            // Check for game over
            if (balance <= 0) {
                alert("Game Over! Restart the game to play again.");
            }
        }

        function resetGame() {
            balance = 1000;
            document.getElementById("balance").textContent = balance;
            document.getElementById("result").textContent = "";
            document.getElementById("slot1").textContent = "❓";
            document.getElementById("slot2").textContent = "❓";
            document.getElementById("slot3").textContent = "❓";
            document.getElementById("bet").value = 50;
        }
    </script>

</body>
</html>