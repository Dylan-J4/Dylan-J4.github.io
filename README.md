<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rock-Paper-Scissors</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
        }
        #results {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Rock-Paper-Scissors Game</h1>
    <button onclick="playGame()">Play Game</button>
    <div id="results">
        <p id="playerScore">Player Score: 0</p>
        <p id="cpuScore">Computer Score: 0</p>
        <p id="ties">Ties: 0</p>
        <p id="finalResult"></p>
    </div>

    <script>
        let playerScore = 0;
        let cpuScore = 0;
        let ties = 0;

        function getComputerChoice() {
            const rps_array = ["rock", "paper", "scissors"];
            let choice = Math.floor(Math.random() * 3);
            return rps_array[choice];
        }

        function getHumanChoice() {
            let humanChoice;
            let running = true;

            while (running) {
                humanChoice = prompt("rock, paper, or scissors: ").toLowerCase();

                if (["rock", "paper", "scissors"].includes(humanChoice)) {
                    running = false;
                } else {
                    alert("Invalid choice, please choose again.");
                }
            }
            return humanChoice;
        }

        function playRound(playerChoice, computerChoice) {
            if (playerChoice === computerChoice) {
                ties += 1;
                console.log("Round ended in a tie!");
            } else if (
                (playerChoice === "rock" && computerChoice === "scissors") ||
                (playerChoice === "paper" && computerChoice === "rock") ||
                (playerChoice === "scissors" && computerChoice === "paper")
            ) {
                playerScore += 1;
                console.log("You won this round!");
            } else {
                cpuScore += 1;
                console.log("Computer won this round!");
            }
            updateDisplay();
        }

        function updateDisplay() {
            document.getElementById('playerScore').textContent = `Player Score: ${playerScore}`;
            document.getElementById('cpuScore').textContent = `Computer Score: ${cpuScore}`;
            document.getElementById('ties').textContent = `Ties: ${ties}`;
        }

        function playGame() {
            playerScore = 0;
            cpuScore = 0;
            ties = 0;
            updateDisplay();

            for (let i = 0; i < 5; i++) {
                let playerChoice = getHumanChoice();
                let cpuChoice = getComputerChoice();
                playRound(playerChoice, cpuChoice);
            }

            let finalResult;
            if (cpuScore > playerScore) {
                finalResult = "Computer wins!";
            } else if (playerScore > cpuScore) {
                finalResult = "Congrats, You win!";
            } else {
                finalResult = "The game ended in a draw!";
            }

            document.getElementById('finalResult').textContent = finalResult;
        }
    </script>
</body>
</html>
