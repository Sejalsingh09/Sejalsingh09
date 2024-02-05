<!DOCTYPE html>
<html>
<head>
    <title>Snake Game</title>
    <style>
        canvas {
            border: 1px solid black;
        }
    </style>
</head>
<body>
    <canvas id="canvas" width="400" height="400"></canvas>
    <script>
        var canvas = document.getElementById("canvas");
        var ctx = canvas.getContext("2d");

        var snake = [{x: 200, y: 200}];
        var food = {x: 0, y: 0};
        var direction = "right";

        function drawSnake() {
            ctx.fillStyle = "green";
            for (var i = 0; i < snake.length; i++) {
                ctx.fillRect(snake[i].x, snake[i].y, 10, 10);
            }
        }

        function drawFood() {
            ctx.fillStyle = "red";
            ctx.fillRect(food.x, food.y, 10, 10);
        }

        function moveSnake() {
            var head = {x: snake[0].x, y: snake[0].y};
            if (direction == "right") {
                head.x += 10;
            } else if (direction == "left") {
                head.x -= 10;
            } else if (direction == "up") {
                head.y -= 10;
            } else if (direction == "down") {
                head.y += 10;
            }
            snake.unshift(head);
            if (head.x == food.x && head.y == food.y) {
                generateFood();
            } else {
                snake.pop();
            }
        }

        function generateFood() {
            food.x = Math.floor(Math.random() * 40) * 10;
            food.y = Math.floor(Math.random() * 40) * 10;
        }

        function changeDirection(event) {
            if (event.keyCode == 37 && direction != "right") {
                direction = "left";
            } else if (event.keyCode == 38 && direction != "down") {
                direction = "up";
            } else if (event.keyCode == 39 && direction != "left") {
                direction = "right";
            } else if (event.keyCode == 40 && direction != "up") {
                direction = "down";
            }
        }

        function gameLoop() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            moveSnake();
            drawSnake();
            drawFood();
        }

        generateFood();
        setInterval(gameLoop, 100);
        document.addEventListener("keydown", changeDirection);
    </script>
</body>
</html>
