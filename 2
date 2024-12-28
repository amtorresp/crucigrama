<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crucigrama - Antídotos</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            background-color: #f0f0f0;
            padding: 20px;
        }
        .game-container {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            max-width: 800px;
            width: 100%;
        }
        .grid {
            display: grid;
            grid-template-columns: repeat(10, 40px);
            gap: 2px;
            margin: 20px auto;
        }
        .cell {
            width: 40px;
            height: 40px;
            border: 1px solid #ccc;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            background-color: white;
        }
        .cell.black {
            background-color: black;
        }
        .cell input {
            width: 90%;
            height: 90%;
            border: none;
            text-align: center;
            font-size: 20px;
            text-transform: uppercase;
        }
        .cell .number {
            position: absolute;
            top: 2px;
            left: 2px;
            font-size: 12px;
            color: #666;
        }
        .clues {
            margin-top: 20px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }
        .clue-section {
            background-color: #f8f8f8;
            padding: 15px;
            border-radius: 5px;
        }
        .correct {
            background-color: #90EE90;
        }
        button {
            margin: 10px;
            padding: 10px 20px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h2>Crucigrama - Antídotos</h2>
        <div id="grid" class="grid"></div>
        <div class="clues">
            <div class="clue-section">
                <h3>Horizontales:</h3>
                <div id="across-clues"></div>
            </div>
            <div class="clue-section">
                <h3>Verticales:</h3>
                <div id="down-clues"></div>
            </div>
        </div>
        <button onclick="checkAnswers()">Verificar respuestas</button>
        <button onclick="showSolution()">Ver solución</button>
    </div>

    <script>
        const puzzle = {
            width: 10,
            height: 10,
            grid: [
                [1,1,1,1,1,1,1,1,0,0],
                [0,0,0,2,0,0,0,0,0,0],
                [0,0,0,1,0,0,0,0,0,0],
                [3,1,1,1,1,1,1,1,0,0],
                [0,0,0,1,0,0,0,0,0,0],
                [0,0,0,1,0,0,0,0,0,0],
                [0,0,0,1,0,0,0,0,0,0],
                [0,0,0,0,0,0,0,0,0,0],
                [0,0,0,0,0,0,0,0,0,0],
                [0,0,0,0,0,0,0,0,0,0]
            ],
            words: {
                across: [
                    { number: 1, clue: "Antídoto para sobredosis de opioides", answer: "NALOXONA" },
                    { number: 3, clue: "Gas esencial para la vida y antídoto en múltiples intoxicaciones", answer: "OXIGENO" }
                ],
                down: [
                    { number: 2, clue: "Antídoto para sobredosis de benzodiacepinas", answer: "FLUMAZENIL" },
                    { number: 4, clue: "N-acetilcisteína (siglas)", answer: "NAC" }
                ]
            }
        };

        function createGrid() {
            const gridElement = document.getElementById('grid');
            let cellNumber = 1;

            for (let i = 0; i < puzzle.height; i++) {
                for (let j = 0; j < puzzle.width; j++) {
                    const cell = document.createElement('div');
                    cell.className = 'cell';
                    
                    if (puzzle.grid[i][j] === 0) {
                        cell.classList.add('black');
                    } else {
                        const input = document.createElement('input');
                        input.maxLength = 1;
                        input.dataset.row = i;
                        input.dataset.col = j;
                        cell.appendChild(input);

                        if (puzzle.grid[i][j] === 1) {
                            const number = document.createElement('div');
                            number.className = 'number';
                            number.textContent = cellNumber++;
                            cell.appendChild(number);
                        }
                    }
                    
                    gridElement.appendChild(cell);
                }
            }

            // Añadir event listeners para navegación
            const inputs = document.querySelectorAll('input');
            inputs.forEach(input => {
                input.addEventListener('keyup', (e) => {
                    if (e.key === 'Backspace' || e.key === 'Delete') {
                        navigateToPrevious(input);
                    } else if (input.value) {
                        navigateToNext(input);
                    }
                });
            });
        }

        function createClues() {
            const acrossClues = document.getElementById('across-clues');
            const downClues = document.getElementById('down-clues');

            puzzle.words.across.forEach(word => {
                const div = document.createElement('div');
                div.textContent = `${word.number}. ${word.clue}`;
                acrossClues.appendChild(div);
            });

            puzzle.words.down.forEach(word => {
                const div = document.createElement('div');
                div.textContent = `${word.number}. ${word.clue}`;
                downClues.appendChild(div);
            });
        }

        function navigateToNext(currentInput) {
            const nextInput = findNextInput(currentInput);
            if (nextInput) {
                nextInput.focus();
            }
        }

        function navigateToPrevious(currentInput) {
            const prevInput = findPreviousInput(currentInput);
            if (prevInput) {
                prevInput.focus();
            }
        }

        function findNextInput(currentInput) {
            const inputs = Array.from(document.querySelectorAll('input'));
            const currentIndex = inputs.indexOf(currentInput);
            return inputs[currentIndex + 1];
        }

        function findPreviousInput(currentInput) {
            const inputs = Array.from(document.querySelectorAll('input'));
            const currentIndex = inputs.indexOf(currentInput);
            return inputs[currentIndex - 1];
        }

        function checkAnswers() {
            const inputs = document.querySelectorAll('input');
            let allCorrect = true;

            inputs.forEach(input => {
                const row = parseInt(input.dataset.row);
                const col = parseInt(input.dataset.col);
                const cell = input.parentElement;

                // Verificar horizontales
                for (let word of puzzle.words.across) {
                    if (puzzle.grid[row][col] === 1) {
                        const userAnswer = getUserAnswer(row, col, 'across');
                        if (userAnswer === word.answer) {
                            cell.classList.add('correct');
                        } else {
                            cell.classList.remove('correct');
                            allCorrect = false;
                        }
                    }
                }

                // Verificar verticales
                for (let word of puzzle.words.down) {
                    if (puzzle.grid[row][col] === 1) {
                        const userAnswer = getUserAnswer(row, col, 'down');
                        if (userAnswer === word.answer) {
                            cell.classList.add('correct');
                        } else {
                            cell.classList.remove('correct');
                            allCorrect = false;
                        }
                    }
                }
            });

            if (allCorrect) {
                alert('¡Felicitaciones! Has completado el crucigrama correctamente.');
            }
        }

        function getUserAnswer(row, col, direction) {
            let answer = '';
            const inputs = document.querySelectorAll('input');
            
            if (direction === 'across') {
                for (let i = 0; i < puzzle.width; i++) {
                    const input = Array.from(inputs).find(
                        input => parseInt(input.dataset.row) === row && 
                                parseInt(input.dataset.col) === i
                    );
                    if (input) {
                        answer += input.value.toUpperCase();
                    }
                }
            } else {
                for (let i = 0; i < puzzle.height; i++) {
                    const input = Array.from(inputs).find(
                        input => parseInt(input.dataset.row) === i && 
                                parseInt(input.dataset.col) === col
                    );
                    if (input) {
                        answer += input.value.toUpperCase();
                    }
                }
            }
            
            return answer;
        }

        function showSolution() {
            const inputs = document.querySelectorAll('input');
            
            puzzle.words.across.forEach(word => {
                let row, col;
                // Encontrar la posición inicial de la palabra
                for (let i = 0; i < puzzle.height; i++) {
                    for (let j = 0; j < puzzle.width; j++) {
                        if (puzzle.grid[i][j] === 1) {
                            row = i;
                            col = j;
                            break;
                        }
                    }
                    if (row !== undefined) break;
                }
                
                // Rellenar la palabra
                for (let i = 0; i < word.answer.length; i++) {
                    const input = Array.from(inputs).find(
                        input => parseInt(input.dataset.row) === row && 
                                parseInt(input.dataset.col) === (col + i)
                    );
                    if (input) {
                        input.value = word.answer[i];
                    }
                }
            });

            puzzle.words.down.forEach(word => {
                let row = 0, col;
                // Encontrar la columna de la palabra vertical
                for (let j = 0; j < puzzle.width; j++) {
                    if (puzzle.grid[row][j] === 1) {
                        col = j;
                        break;
                    }
                }
                
                // Rellenar la palabra
                for (let i = 0; i < word.answer.length; i++) {
                    const input = Array.from(inputs).find(
                        input => parseInt(input.dataset.row) === (row + i) && 
                                parseInt(input.dataset.col) === col
                    );
                    if (input) {
                        input.value = word.answer[i];
                    }
                }
            });
        }

        // Inicializar el juego
        createGrid();
        createClues();
    </script>
</body>
</html>
