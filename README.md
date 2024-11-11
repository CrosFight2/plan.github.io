<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Will You Marry Me?</title>
    <link href="https://fonts.googleapis.com/css2?family=Sacramento&family=Indie+Flower&display=swap" rel="stylesheet">
    <style>
        * {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body, html {
            height: 100%;
            background: linear-gradient(135deg, #ff7e5f, #feb47b);
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0;
            overflow: hidden;
        }

        #div1 {
            display: flex;
            flex-direction: column;
            align-items: center;
            border: 3px solid black;
            border-radius: 10px;
            padding: 20px;
            background-color: rgba(255, 255, 255, 0.9);
            box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.2);
            position: relative;
            text-align: center;
            width: 350px;
            z-index: 10;
            animation: slideIn 1s ease-out, bounce 2s ease-out 1;
        }

        @keyframes slideIn {
            from {
                transform: translateY(-200px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        @keyframes bounce {
            0% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-10px);
            }
            100% {
                transform: translateY(0);
            }
        }

        p {
            font-size: 30px;
            font-weight: bold;
            color: #333;
            margin-bottom: 20px;
            letter-spacing: 1px;
            font-family: 'Sacramento', cursive;
            animation: fadeIn 1s ease-out;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        button {
            width: 80px;
            height: 35px;
            border-radius: 20px;
            border: none;
            color: #fff;
            cursor: pointer;
            transition: transform 0.2s ease, background-color 0.3s ease;
            margin: 10px;
            font-size: 16px;
            font-weight: bold;
        }

        #buttonyes {
            background-color: #7bed9f;
        }

        #buttonno {
            background-color: #ff6b81;
        }

        button:hover {
            transform: scale(1.1);
        }

        #message {
            font-size: 28px;
            font-weight: bold;
            color: #333;
            margin-top: 30px;
            display: none;
            animation: fadeIn 1.5s ease-out;
            font-family: 'Indie Flower', cursive;
        }

        #heart {
            font-size: 100px;
            color: #ff4d4d;
            margin-top: 20px;
            display: none;
            animation: heartBeat 1s infinite;
        }

        @keyframes heartBeat {
            0% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.2);
            }
            100% {
                transform: scale(1);
            }
        }

        .confetti {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            display: none;
            z-index: 100;
        }

        .confetti-piece {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #ff5733;
            border-radius: 50%;
            animation: confettiFall 2s infinite;
        }

        @keyframes confettiFall {
            0% {
                opacity: 1;
                transform: translateY(0) rotate(0deg);
            }
            100% {
                opacity: 0;
                transform: translateY(300px) rotate(360deg);
            }
        }
    </style>
</head>
<body>
    <div id="div1">
        <p>Will you marry me?</p>
        <div>
            <button id="buttonyes" onclick="showArt()">Yes</button>
            <button id="buttonno">No</button>
        </div>
        <div id="message">Yay! You said YES!</div>
        <div id="heart">💖</div>
    </div>

    <div id="confetti" class="confetti"></div>

    <script>
        const yes = document.getElementById("buttonyes");
        const no = document.getElementById("buttonno");
        const container = document.getElementById("div1");
        const message = document.getElementById("message");
        const heart = document.getElementById("heart");
        const confetti = document.getElementById("confetti");

        const yesSound = new Audio('https://www.soundjay.com/button/beep-07.wav');
        const noSound = new Audio('https://www.soundjay.com/button/beep-08b.wav');

        function getRandomPosition(element, cursorX, cursorY) {
            const containerRect = container.getBoundingClientRect();
            const maxX = containerRect.width - element.offsetWidth;
            const maxY = containerRect.height - element.offsetHeight;

            let randomX, randomY;

            do {
                randomX = Math.floor(Math.random() * maxX);
                randomY = Math.floor(Math.random() * maxY);
            } while (Math.abs(randomX - cursorX) < 100 && Math.abs(randomY - cursorY) < 100);

            return { x: randomX, y: randomY };
        }

        no.addEventListener("mouseover", function(event) {
            const cursorX = event.clientX - container.getBoundingClientRect().left;
            const cursorY = event.clientY - container.getBoundingClientRect().top;

            const position = getRandomPosition(no, cursorX, cursorY);
            no.style.position = 'absolute';
            no.style.left = `${position.x}px`;
            no.style.top = `${position.y}px`;

            noSound.play();
        });

        function showArt() {
            message.style.display = "block";
            heart.style.display = "block";

            yesSound.play();

            generateConfetti();

            yes.style.display = "none";
            no.style.display = "none";
        }

        function generateConfetti() {
            for (let i = 0; i < 50; i++) {
                const confettiPiece = document.createElement('div');
                confettiPiece.classList.add('confetti-piece');
                confettiPiece.style.left = `${Math.random() * 100}%`;
                confettiPiece.style.animationDuration = `${Math.random() * 2 + 2}s`;
                confettiPiece.style.animationDelay = `${Math.random() * 2}s`;
                confetti.appendChild(confettiPiece);
            }
            confetti.style.display = 'block';
        }
    </script>
</body>
</html>
