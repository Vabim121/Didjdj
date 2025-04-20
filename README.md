<!DOCTYPE html>
<html>
<head>
    <title>Mines Signals</title>
    <meta charset="UTF-8">
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        body {
            background: #000;
            color: #fff;
            font-family: Arial, sans-serif;
            padding: 20px;
            text-align: center;
        }
        
        .header {
            font-size: 24px;
            margin: 15px 0;
            letter-spacing: 2px;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 10px;
            margin: 20px auto;
            width: 200px;
        }

        .cell {
            width: 40px;
            height: 40px;
            background: #222;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
        }

        button {
            background: #444;
            color: #fff;
            border: none;
            padding: 12px 24px;
            margin: 10px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
        }

        .counter {
            font-size: 32px;
            margin: 15px 0;
            color: #FFD700;
        }
    </style>
</head>
<body>
    <div class="header">MINES ABYZ</div>
    <div class="header">MINES</div>
    
    <div id="grid" class="grid"></div>
    
    <div class="counter">3</div>
    
    <button onclick="generateSignal()">ПОЛУЧИТЬ СИГНАЛ</button>
    <button onclick="Telegram.WebApp.close()">ВЕРНУТЬСЯ</button>

    <script>
        function createGrid() {
            const grid = document.getElementById('grid');
            grid.innerHTML = '';
            
            for(let i = 0; i < 25; i++) {
                const cell = document.createElement('div');
                cell.className = 'cell';
                grid.appendChild(cell);
            }
        }

        function generateSignal() {
            const cells = document.getElementsByClassName('cell');
            
            // Очистка предыдущих сигналов
            Array.from(cells).forEach(cell => cell.innerHTML = '');
            
            // Генерация 3 случайных мин
            const mines = new Set();
            while(mines.size < 3) {
                mines.add(Math.floor(Math.random() * 25));
            }
            
            // Отметить мины
            mines.forEach(position => {
                cells[position].innerHTML = 'X';
                cells[position].style.color = '#ff0000';
            });
        }

        // Инициализация при загрузке
        Telegram.WebApp.ready();
        createGrid();
    </script>
</body>
</html>
