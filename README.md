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
        .incorrect {
            background-color: #FFB6C1;
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
            words: {
                across: [
                    { number: 1, word: "NALOXONA", row: 0, col: 0, 
                      clue: "Antídoto para sobredosis de opioides" },
                    { number: 3, word: "OXIGENO", row: 3, col: 0, 
                      clue: "Gas esencial para la vida y antídoto en múltiples intoxicaciones" }
                ],
                down: [
                    { number: 2, word: "FLUMAZENIL", row: 0, col: 3, 
                      clue: "Antídoto para sobredosis de benzodiacepinas" },
                    { number: 4, word: "NAC", row: 3, col: 3, 
                      clue: "N-acetilcisteína (siglas)" }
                ]
            }
        };

        function createGrid() {
            const gridElement = document.getElementById('grid');
            // Crear matriz 10x10 con celdas vacías
            for (let i = 0; i < 10; i++) {
                for (let j = 0; j < 10; j++) {
                    const cell = document.createElement('div');
                    cell.className = 'cell';
                    
                    // Verificar si la celda debe ser parte de una palabra
                    if (shouldCreateInput(i, j)) {
                        const input = document.createElement('input');
                        input.maxLength = 1;
                        input.dataset.row = i;
                        input.dataset.col = j;
                        cell.appendChild(input);
                        
                        // Añadir números a las celdas iniciales de palabras
                        const number = getWordNumber(i, j);
                        if (number) {
                            const numberDiv = document.createElement('div');
                            numberDiv.className = 'number';
                            numberDiv.textContent = number;
                            cell.appendChild(numberDiv);
                        }
                    } else {
                        cell.classList.add('black');
                    }
                    
                    gridElement.appendChild(cell);
                }
            }

            // Añadir event listeners para navegación
            const inputs = document.querySelectorAll('input');
            inputs.forEach(input => {
                input.addEventListener('keyup', (e) => {
                    if (e.key === 'Backspace' || e.key === 'Delete') {
                        input.value = '';
                        navigateToPrevious(input);
                    } else if (input.value) {
                        navigateToNext(input);
                    }
                });
                
                input.addEventListener('focus', () => {
                    input.select();
                });
            });
        }

        function shouldCreateInput(row, col) {
            // Verificar si la celda es parte de alguna palabra
            for (const direction of ['across', 'down']) {
                for (const wordData of puzzle.words[direction]) {
                    if (direction === 'across') {
                        if (row === wordData.row && 
                            col >= wordData.col && 
                            col < wordData.col + wordData.word.length) {
                            return true;
                        }
                    } else { // down
                        if (col === wordData.col && 
                            row >= wordData.row && 
                            row < wordData.row + wordData.word.length) {
                            return true;
                        }
                    }
                }
            }
            return false;
        }

        function getWordNumber(row, col) {
            for (const direction of ['across', 'down']) {
                for (const wordData of puzzle.words[direction]) {
                    if (row === wordData.row && col === wordData.col) {
                        return wordData.number;
                    }
                }
            }
            return null;
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
            let allCorrect = true;
            // Limpiar clases previas
            document.querySelectorAll('.cell').forEach(cell => {
                cell.classList.remove('correct', 'incorrect');
            });

            // Verificar palabras horizontales
            puzzle.words.across.forEach(wordData => {
                let userWord = '';
                for (let i = 0; i < wordData.word.length; i++) {
                    const input = document.querySelector(
                        `input[data-row="${wordData.row}"][data-col="${wordData.col + i}"]`
                    );
                    if (input) {
                        userWord += input.value.toUpperCase();
                        // Marcar celda como correcta o incorrecta
                        const cell = input.parentElement;
                        if (input.value.toUpperCase() === wordData.word[i]) {
                            cell.classList.add('correct');
                        } else {
                            cell.classList.add('incorrect');
                            allCorrect = false;
                        }
                    }
                }
            });

            // Verificar palabras verticales
            puzzle.words.down.forEach(wordData => {
                let userWord = '';
                for (let i = 0; i < wordData.word.length; i++) {
                    const input = document.querySelector(
                        `input[data-row="${wordData.row + i}"][data-col="${wordData.col}"]`
                    );
                    if (input) {
                        userWord += input.value.toUpperCase();
                        // Marcar celda como correcta o incorrecta si no está ya marcada
                        const cell = input.parentElement;
                        if (!cell.classList.contains('correct')) {
                            if (input.value.toUpperCase() === wordData.word[i]) {
                                cell.classList.add('correct');
                            } else {
                                cell.classList.add('incorrect');
                                allCorrect = false;
                            }
                        }
                    }
                }
            });

            if (allCorrect) {
                alert('¡Felicitaciones! Has completado el crucigrama correctamente.');
            }
        }

        function showSolution() {
            puzzle.words.across.forEach(wordData => {
                for (let i = 0; i < wordData.word.length; i++) {
                    const input = document.querySelector(
                        `input[data-row="${wordData.row}"][data-col="${wordData.col + i}"]`
                    );
                    if (input) {
                        input.value = wordData.word[i];
                    }
                }
            });

            puzzle.words.down.forEach(wordData => {
                for (let i = 0; i < wordData.word.length; i++) {
                    const input = document.querySelector(
                        `input[data-row="${wordData.row + i}"][data-col="${wordData.col}"]`
                    );
                    if (input) {
                        input.value = wordData.word[i];
                    }
                }
            });
            
            checkAnswers();
        }

        // Inicializar el juego
        createGrid();
        createClues();
    </script>
</body>
</html>
