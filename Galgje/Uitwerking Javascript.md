# Javascript - html

Hier is een implementatie van Galgje met HTML en JavaScript:

**HTML** (`index.html`):

```html
<!DOCTYPE html>
<html lang="nl">
<head>
    <meta charset="UTF-8">
    <title>Galgje Spel</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
<h1>Galgje Spel</h1>
<div id="game">
    <p>Resterende pogingen: <span id="remaining">6</span></p>
    <p>Foute letters: <span id="wrong-letters"></span></p>
    <p id="word-display"></p>
    <form id="guess-form">
        <input type="text" id="guess-input" maxlength="1" placeholder="Gok een letter" autofocus/>
        <button type="submit">Gok</button>
    </form>
</div>
<p id="message"></p>
<button type="button" id="restart-button">Opnieuw Spelen</button>
<script src="main.js"></script>
</body>
</html>
```

**CSS** (`style.css`):

```css
body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin-top: 50px;
}

h1 {
    font-size: 2em;
    margin-bottom: 20px;
}

#game {
    margin-bottom: 20px;
}

#word-display {
    font-size: 1.5em;
    margin-bottom: 10px;
}

#guess-input {
    padding: 5px;
    font-size: 1em;
}

button {
    padding: 5px 10px;
    margin-top: 10px;
    font-size: 1em;
    cursor: pointer;
}

#message {
    font-size: 1.2em;
    margin-top: 20px;
    color: green;
}
```

**JavaScript** (`script.js`):

```javascript
const woorden = [
	"programmeren", "javascript", "computer", "spel", "internet",
	"galgje", "software", "hardware", "database", "netwerk"
];

let woord, geradenLetters, pogingen, fouteLetters, geraden;
const remainingElement = document.getElementById("remaining");
const wordDisplayElement = document.getElementById("word-display");
const wrongLettersElement = document.getElementById("wrong-letters");
const messageElement = document.getElementById("message");
const guessInputElement = document.getElementById("guess-input");
const guessButtonElement = document.getElementById("guess-button");
const guessFormElement = document.getElementById("guess-form");
const restartButtonElement = document.getElementById("restart-button");

function kiesWillekeurigWoord() {
	const index = Math.floor(Math.random() * woorden.length);
	return woorden[index];
}

function initialiseGame() {
	woord = kiesWillekeurigWoord();
	geradenLetters = Array(woord.length).fill(false);
	pogingen = 6;
	fouteLetters = [];
	geraden = false;
	remainingElement.textContent = pogingen;
	wrongLettersElement.textContent = "";
	messageElement.textContent = "";
	updateWordDisplay();
}

function updateWordDisplay() {
	let display = "";
	for (let i = 0; i < woord.length; i++) {
		display += geradenLetters[i] ? woord[i] + " " : "_ ";
	}
	wordDisplayElement.textContent = display.trim();
}

function isGeraden() {
	return geradenLetters.every(Boolean);
}

function handleGuess() {
	const gok = guessInputElement.value.toLowerCase();
	guessInputElement.value = "";

	if (!gok || !gok.match(/[a-z]/i) || gok.length !== 1) {
		return;
	}

	if (woord.includes(gok)) {
		for (let i = 0; i < woord.length; i++) {
			if (woord[i] === gok) {
				geradenLetters[i] = true;
			}
		}
	} else if (!fouteLetters.includes(gok)) {
		fouteLetters.push(gok);
		pogingen--;
		remainingElement.textContent = pogingen;
		wrongLettersElement.textContent = fouteLetters.join(", ");
	}

	updateWordDisplay();

	if (isGeraden()) {
		messageElement.textContent = "Gefeliciteerd! Je hebt het woord geraden: " + woord;
		geraden = true;
	} else if (pogingen === 0) {
		messageElement.textContent = "Helaas, je hebt verloren. Het woord was: " + woord;
		geraden = true;
	}
}

guessFormElement.addEventListener("submit", (e) => {
	e.preventDefault();
	!geraden && handleGuess();
})

restartButtonElement.addEventListener("click", initialiseGame);

initialiseGame();
```

## Toelichting

- **HTML**: De basisstructuur van de pagina met een eenvoudig formulier voor het raden van een letter en knoppen voor
  gokken en opnieuw starten.
- **CSS**: Een eenvoudige stijl voor het Galgje-spel.
- **JavaScript**:
    - **kiesWillekeurigWoord**: Functie om een willekeurig woord te kiezen.
    - **initialiseGame**: Initialiseert het spel.
    - **updateWordDisplay**: Toont de huidige status van het woord.
    - **isGeraden**: Controleert of het woord volledig is geraden.
    - **handleGuess**: Behandelt de gok van de speler.

## Hoe te gebruiken

1. Maak een map voor je project, bijv. `galgje`.
2. Maak drie bestanden: `index.html`, `style.css`, `script.js`.
3. Plaats de respectievelijke code in deze bestanden.
4. Open `index.html` in je webbrowser om het Galgje-spel te spelen.

