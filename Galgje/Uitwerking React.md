# React
**Let op:** om deze opdracht in React te kunnen maken heb je kennis nodig van state en life cycle methods.

Om een React-app op te zetten met Vite, volg je deze stappen:

## Installeren en uitvoeren van de app

1. **Zorg dat je Node.js geïnstalleerd hebt:**
   Als je Node.js nog niet geïnstalleerd hebt, kun je dat downloaden en installeren
   van [nodejs.org](https://nodejs.org/). Dit installeert ook `npm` (Node Package Manager), wat nodig is voor het
   beheren van de afhankelijkheden.

2. **Maak een Nieuw React-project:**
   Open een terminal en gebruik de volgende commando's om een nieuw project te maken met Vite en erin
   te navigeren (of maak een Vite project aan via de interface van WebStorm):

```bash
npm create vite@latest galgje-react -- --template react
cd galgje-react
```

Installeer eerst de bijbehorende node modules door het volgende commando in de terminal te runnen:

```shell 
npm install
```

Wanneer dit klaar is, kun je de applicatie starten met behulp van:

```shell
npm run dev
```

of gebruik de WebStorm knop (npm run dev). Open http://localhost:5173 om de pagina in de browser te bekijken. Begin met het maken van wijzigingen in src/App.jsx: elke keer als je een bestand opslaat, zullen de wijzigingen te zien zijn op de webpagina.

3. **Vervang de inhoud van `src/App.jsx`:**
   Vervang de inhoud van `src/App.jsx` door de volgende code:

```javascript
// src/App.jsx
import {useState, useEffect, useRef} from 'react';
import './App.css';

const woorden = [
	'programmeren', 'javascript', 'computer', 'spel', 'internet',
	'galgje', 'software', 'hardware', 'database', 'netwerk'
];

function App() {
	const [woord, setWoord] = useState('');
	const [letter, setLetter] = useState('');
	const [geradenLetters, setGeradenLetters] = useState([]);
	const [pogingen, setPogingen] = useState(6);
	const [fouteLetters, setFouteLetters] = useState([]);
	const [geraden, setGeraden] = useState(false);
	const [message, setMessage] = useState('');

	// deze gebruik je om het element in focus te brengen (behandelen we niet in de lesstof)
	const inputFieldReference = useRef();

	useEffect(() => {
		initialiseGame();
	}, []);

	useEffect(() => {
		if (geradenLetters.length > 0 && geradenLetters.every((letter) => letter === true)) {
			console.log(geradenLetters);
			setMessage(`Gefeliciteerd! Je hebt het woord geraden: ${woord}`);
			setGeraden(true);
		}
	}, [geradenLetters]);

	useEffect(() => {
		if (pogingen === 0) {
			setMessage(`Helaas, je hebt verloren. Het woord was: ${woord}`);
			setGeraden(true);
		}
	}, [pogingen]);

	function kiesWillekeurigWoord() {
		const index = Math.floor(Math.random() * woorden.length);
		return woorden[index];
	}

	function initialiseGame() {
		const nieuwWoord = kiesWillekeurigWoord();
		setWoord(nieuwWoord);
		setGeradenLetters(Array(nieuwWoord.length).fill(false));
		setPogingen(6);
		setFouteLetters([]);
		setGeraden(false);
		setMessage('');
	}

	function updateWordDisplay() {
		return woord.split('').map((letter, index) => {
				return geradenLetters[index] ? letter : '_'
			}
		).join(' ');
	}

	function handleGuess(gok) {
		if (!gok || !gok.match(/[a-z]/i) || gok.length !== 1 || geraden) {
			return;
		}

		if (woord.includes(gok)) {
			const nieuweGeradenLetters = geradenLetters.map((waarde, index) =>
				woord[index] === gok ? true : waarde
			);
			setGeradenLetters(nieuweGeradenLetters);
		} else if (!fouteLetters.includes(gok)) {
			setFouteLetters([...fouteLetters, gok]);
			setPogingen(pogingen - 1);
		}
		setLetter('');
		// deze gebruik je om het element in focus te brengen (behandelen we niet in de lesstof)
		inputFieldReference.current.focus();
	}

	function handleSubmit(e) {
		e.preventDefault();
		handleGuess(letter);
	}

	return (
		<div>
			<h1>Galgje Spel</h1>
			<div className="game">
				<p>Resterende pogingen: <span id="remaining">{pogingen}</span></p>
				<p>Foute letters: <span id="wrong-letters">{fouteLetters.join(", ")}</span></p>
				<p className="word-display">{updateWordDisplay()}</p>
				<form onSubmit={handleSubmit}>
					<input
						type="text"
						maxLength="1"
						placeholder="Gok een letter"
						// deze gebruik je om het element in focus te brengen (behandelen we niet in de lesstof)
						ref={inputFieldReference}
						onChange={(e) => setLetter(e.target.value)}
						value={letter}
						disabled={geraden}
					/>
					<button type="submit">Gok</button>
				</form>
				<button type="button" onClick={initialiseGame}>Opnieuw Spelen</button>
			</div>
			{message && <p className="message">{message}</p>}
		</div>
	);
}

export default App;
```

4. **Voeg CSS toe voor styling (optioneel):**
   Voeg deze CSS toe in `src/App.css`:

   ```css
   /* src/App.css */
   body {
     font-family: Arial, sans-serif;
     text-align: center;
     margin-top: 50px;
   }

   h1 {
     font-size: 2em;
     margin-bottom: 20px;
   }

   .game {
     margin-bottom: 20px;
   }

   .word-display {
     font-size: 1.5em;
     margin-bottom: 10px;
   }

   input {
     padding: 5px;
     font-size: 1em;
   }

   button {
     padding: 5px 10px;
     margin-top: 10px;
     font-size: 1em;
     cursor: pointer;
   }

   .message {
     font-size: 1.2em;
     margin-top: 20px;
     color: green;
   }
   ```

