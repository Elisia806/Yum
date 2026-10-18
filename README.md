# Yum
Woahh
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cute Heart Catcher</title>
    <style>
        body {
            background-color: #ffe6f2;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
            font-family: 'Comic Sans MS', cursive, sans-serif;
            color: #d63384;
        }
        #game-container {
            width: 400px;
            height: 400px;
            background-color: #fff0f6;
            border: 4px dashed #ff8fab;
            border-radius: 15px;
            position: relative;
            overflow: hidden;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        #basket {
            width: 60px;
            height: 30px;
            background-color: #ffb5a7;
            border-radius: 0 0 15px 15px;
            position: absolute;
            bottom: 10px;
            left: 170px;
            text-align: center;
            line-height: 30px;
            font-size: 20px;
        }
        .heart {
            position: absolute;
            font-size: 24px;
            top: 0;
            user-select: none;
        }
        #score-board {
            font-size: 24px;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>

    <div id="score-board">Score: <span id="score">0</span> 💖</div>
    <div id="game-container">
        <div id="basket">🧺</div>
    </div>

    <script>
        const container = document.getElementById('game-container');
        const basket = document.getElementById('basket');
        const scoreEl = document.getElementById('score');
        
        let score = 0;
        let basketX = 170;

        document.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowLeft' && basketX > 0) {
                basketX -= 20;
            } else if (e.key === 'ArrowRight' && basketX < 340) {
                basketX += 20;
            }
            basket.style.left = basketX + 'px';
        });

        function createHeart() {
            const heart = document.createElement('div');
            heart.classList.add('heart');
            heart.innerHTML = '❤️';
            heart.style.left = Math.floor(Math.random() * 370) + 'px';
            container.appendChild(heart);

            let heartY = 0;
            const fallInterval = setInterval(() => {
                heartY += 5;
                heart.style.top = heartY + 'px';

                // Check collision with basket
                if (heartY >= 350 && heartY <= 380) {
                    const heartX = parseInt(heart.style.left);
                    if (heartX >= basketX - 20 && heartX <= basketX + 60) {
                        score++;
                        scoreEl.innerText = score;
                        heart.remove();
                        clearInterval(fallInterval);
                    }
                }

                // Remove if it hits the bottom
                if (heartY > 400) {
                    heart.remove();
                    clearInterval(fallInterval);
                }
            }, 30);
        }

        setInterval(createHeart, 800);
    </script>
</body>
</html>
