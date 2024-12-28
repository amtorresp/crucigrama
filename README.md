# Estructura del repositorio

## index.html
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crucigrama - Antídotos</title>
    <link rel="stylesheet" href="styles.css">
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
    <script src="script.js"></script>
</body>
</html>

## styles.css
```css
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

## script.js
```javascript
const puzzle = {
    words: {
        across: [
            { number: 1, word: "NALOXONA", row: 4, col: 0, 
              clue: "Antídoto para sobredosis de opioides" },
            { number: 3, word: "NAC", row: 6, col: 1, 
              clue: "N-acetilcisteína (siglas)" }
        ],
        down: [
            { number: 2, word: "FLUMAZENIL", row: 0, col: 0, 
              clue: "Antídoto para sobredosis de benzodiacepinas" },
            { number: 4, word: "OXIGENO", row: 4, col: 6, 
              clue: "Gas esencial para la vida y antídoto en múltiples intoxicaciones" }
        ]
    }
};

[El resto del código JavaScript del crucigrama va aquí]

## README.md
```markdown
# Crucigrama de Antídotos

Un crucigrama interactivo sobre antídotos comunes en toxicología, creado con HTML, CSS y JavaScript puro.

## Características

- Crucigrama interactivo con validación en tiempo real
- Indicadores visuales de respuestas correctas e incorrectas
- Pistas horizontales y verticales
- Botón para verificar respuestas
- Botón para ver la solución
- Diseño responsivo

## Cómo usar

1. Clona este repositorio
2. Abre `index.html` en tu navegador
3. ¡Comienza a resolver el crucigrama!

## Palabras incluidas

- NALOXONA (Antídoto para sobredosis de opioides)
- FLUMAZENIL (Antídoto para sobredosis de benzodiacepinas)
- NAC (N-acetilcisteína)
- OXIGENO (Gas esencial y antídoto en múltiples intoxicaciones)

## Tecnologías utilizadas

- HTML5
- CSS3
- JavaScript vanilla
```

## .gitignore
```
.DS_Store
node_modules/
.env
*.log
```
