# Call-Long
<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Payoff Long Call</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }
        canvas {
            border: 1px solid black;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Payoff di una Call Long</h1>
    <canvas id="payoffCanvas" width="600" height="400"></canvas>
    <script>
        function drawPayoff(){
            const canvas = document.getElementById("payoffCanvas");
            const ctx = canvas.getContext("2d");

            // Pulizia del canvas
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Definizione del payoff
            const width = canvas.width;
            const height = canvas.height;
            const strikePrice = width / 2;
            const profitHeight = height * 2 / 3;
            const lossHeight = height * 3 / 4;

            // Disegno degli assi
            ctx.beginPath();
            // Asse Y
            ctx.moveTo(width/4, 0);
            ctx.lineTo(width/4, height);
            // Asse X
            ctx.moveTo(0, profitHeight);
            ctx.lineTo(width, profitHeight);
            ctx.strokeStyle = "black";
            ctx.stroke();

            // Disegno del payoff
            ctx.beginPath();
            ctx.moveTo(width/8, lossHeight);
            ctx.lineTo(strikePrice-(lossHeight-profitHeight), lossHeight);
            ctx.lineTo(strikePrice-(lossHeight-profitHeight) + 200, lossHeight - 200);
            ctx.strokeStyle = "blue";
            ctx.lineWidth = 2;
            ctx.stroke();

            // Disegno della retta dello Strike
            ctx.beginPath();
            ctx.moveTo(strikePrice, 0);
            ctx.lineTo(strikePrice, height);
            ctx.strokeStyle = "red";
            ctx.setLineDash([5, 5]); // Linea tratteggiata
            ctx.stroke();
            ctx.setLineDash([]); //Ripristina lo stile normale

            // Aggiunta etichette sugli assi
            ctx.font = "14px Arial";
            ctx.fillStyle = "black";
            // Asse X
            ctx.fillText("Prezzo",width - 50, profitHeight - 10);
            ctx.fillText("Strike", strikePrice - 40, profitHeight - 5);
            ctx.fillText("0", width/4 - 10, profitHeight - 5);
            // Asse Y
            ctx.fillText("Profitto", width/4 + 5, 20);
            ctx.fillText("Perdita", width/4 + 5, height - 10);


        }
    </script>
    <br>
    <button onclick="drawPayoff()">Disegna Payoff</button>
</body>
</html>
