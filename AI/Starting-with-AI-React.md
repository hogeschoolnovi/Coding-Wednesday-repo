## Webstorm - workshop overzicht

<!-- TOC -->
  * [Webstorm - workshop overzicht](#webstorm---workshop-overzicht)
  * [Opdracht: maak een chat app](#opdracht-maak-een-chat-app)
    * [Doel:](#doel)
    * [Stappenplan:](#stappenplan)
    * [Hints:](#hints)
    * [Oplossing:](#oplossing)
  * [Opdracht: maak een chat app met streaming](#opdracht-maak-een-chat-app-met-streaming)
    * [Doel:](#doel-1)
    * [Stappenplan:](#stappenplan-1)
    * [Hints:](#hints-1)
    * [Oplossing:](#oplossing-1)
    * [Helper Functie: `processStream`](#helper-functie-processstream)
  * [Bonus opdracht: Van tekst naar spraak met OpenAI](#bonus-opdracht-van-tekst-naar-spraak-met-openai)
    * [Doel:](#doel-2)
    * [Stappenplan:](#stappenplan-2)
    * [Hints:](#hints-2)
    * [Oplossing:](#oplossing-2)
  * [Bonus opdracht: maak een audio to tekst app](#bonus-opdracht-maak-een-audio-to-tekst-app)
    * [Doel:](#doel-3)
    * [Stappenplan:](#stappenplan-3)
    * [Hints:](#hints-3)
    * [Oplossing:](#oplossing-3)
  * [Bonus opdracht: maak een tekst naar plaatje app](#bonus-opdracht-maak-een-tekst-naar-plaatje-app)
    * [Doel:](#doel-4)
    * [Stappenplan:](#stappenplan-4)
    * [Hints:](#hints-4)
    * [Oplossing:](#oplossing-4)
  * [Bonus opdracht: maak een plaatje naar tekst app](#bonus-opdracht-maak-een-plaatje-naar-tekst-app)
    * [Doel:](#doel-5)
    * [Stappenplan:](#stappenplan-5)
    * [Hints:](#hints-5)
    * [Oplossing:](#oplossing-5)
  * [Toelichting op de requests](#toelichting-op-de-requests)
    * [Chatrequest](#chatrequest)
    * [Imagerequest](#imagerequest)
    * [Speechrequest](#speechrequest)
    * [Transcriptionrequest](#transcriptionrequest)
    * [Samenvatting](#samenvatting)
<!-- TOC -->

## Opdracht: maak een chat app

### Doel:

Opzetten van een basisproject in WebStorm, en het toevoegen van de Simple OpenAI dependency.

In deze opdracht ga je een React-component maken die communiceert met de OpenAI API om tekst completions te genereren. Je zult de `useState` hook gebruiken om de status van de invoer en de respons bij te houden, en de Axios bibliotheek om HTTP-verzoeken naar de API te sturen. De component bevat een formulier waarin je een prompt kunt invoeren, deze prompt wordt vervolgens naar de OpenAI API gestuurd, en de respons wordt weergegeven op de pagina. Het is belangrijk dat je begrijpt hoe je API-sleutels gebruikt, hoe je gebruik maakt van asynchrone functies, en hoe je de state van een component bijwerkt in React. Bekijk ook de [OpenAI API documentatie](https://platform.openai.com/docs/guides/completion) voor meer informatie over tekst completions.


### Stappenplan:

1. **Nieuwe React Project Aanmaken:**
   - Open WebStorm.
   - Selecteer "New Project".
   - Kies links de optie "Vite"
   - Geef je project een naam en locatie (bijvoorbeeld `openai-demo`).
   - Selecteer rechts het template "React"
   - Klik op "Create".

2. **Project Structuur Controleren:**
   - Zorg ervoor dat je projectstructuur er als volgt uitziet:
       ```
       openai-demo
       ├── src
       │   ├── components
       │   │   └── Completion.jsx
       │   │   └── CompletionStream.jsx
       │   │   └── Etc..
       │   └── App.css
       │   └── App.jsx
       │   └── index.css
       │   └── main.jsx
       └── index.html
       ```
3. **API Sleutel Configureren:**

   - Voeg een bestand toe in de root folder genaamd `.env`
   - Voeg je OpenAI API-sleutel toe aan dit bestand
      - OPENAI_API_KEY=_YOUR_API_KEY_HERE_
   - Laad de API-sleutel met behulp van `import.meta.env.OPENAI_API_KEY`
   - Sla de API-sleutel op in een variabele voor later gebruik.

4. **Component Structuur:**
   - Maak een nieuwe React-component genaamd `Completion`.
   - Gebruik de `useState` hook om twee stukjes state te maken: één voor de prompt en één voor de respons.

5. **Formulier en Invoer:**
   - Voeg een formulier toe aan je component met een invoerveld voor de prompt en een submit-knop.
   - Gebruik de `onChange` handler om de waarde van de prompt bij te werken in de state.

6. **Asynchrone Functie voor API-verzoek:**
   - Open de terminal en installeer Axios in je project met `npm install axios`.
   - Maak een asynchrone functie genaamd `handleSubmit` die wordt aangeroepen wanneer het formulier wordt ingediend.
   - Voorkom dat de pagina opnieuw laadt bij het indienen van het formulier door `e.preventDefault()` te gebruiken.
   - Verstuur een POST-verzoek naar de OpenAI API met behulp van Axios. Vergeet niet om de juiste headers en payload mee te geven.
   - Werk de state bij met de respons van de API.

7. **Weergave van de Respons:**
   - Voeg een voorwaardelijke rendering toe om de respons weer te geven zodra deze beschikbaar is.

### Hints:

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Project Voorbereiding:**
   - Zorg ervoor dat je een Vite project hebt met React en Axios geïnstalleerd.
   - Importeer de API-sleutel met `import.meta.env.VITE_OPENAI_API_KEY`.

2. **Component Structuur:**
   - Maak een nieuwe file `Completion.jsx` en voeg de basis structuur van een functionele component toe.
   - Importeer `useState` van React.

3. **Formulier en Invoer:**
   - Voeg een formulier toe in de JSX van je component.
   - Gebruik een `input` element voor de prompt en een `button` voor het indienen.

4. **Asynchrone Functie voor API-verzoek:**
   - Definieer een `handleSubmit` functie die het formulier indienen afhandelt.
   - Gebruik `axios.post` om een POST-verzoek te sturen naar de OpenAI API.
   - Werk de state bij met de respons data.

5. **Weergave van de Respons:**
   - Voeg conditionele logica toe om de respons weer te geven zodra deze beschikbaar is (`response && <div>{response}</div>`).

</details>

### Oplossing:

<details>
<summary>Klik hier</summary>

```jsx
import { useState } from "react";
import axios from "axios";

const apiKey = import.meta.env.VITE_OPENAI_API_KEY;

const Completion = () => {
  const [prompt, setPrompt] = useState("");
  const [response, setResponse] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();
    setResponse("");
    try {
      const res = await axios.post(
        "https://api.openai.com/v1/chat/completions",
        {
          model: "gpt-4",
          messages: [{ role: "user", content: prompt }],
        },
        {
          headers: {
            Authorization: `Bearer ${apiKey}`,
            "Content-Type": "application/json",
          },
        }
      );

      const output = res.data.choices[0].message.content;
      setResponse(output);
    } catch (error) {
      console.error("Error communicating with OpenAI:", error);
    }
    setPrompt("");
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <label htmlFor="prompt">
          Ask a question to OpenAI:
          <input
            id="prompt"
            type="text"
            value={prompt}
            onChange={(e) => setPrompt(e.target.value)}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
      {response && (
        <div>
          <p>{response}</p>
        </div>
      )}
    </div>
  );
};

export default Completion;
```

</details>

## Opdracht: maak een chat app met streaming
### Doel:

In deze opdracht ga je een React-component maken die communiceert met de OpenAI API om tekst te genereren via een streaming verbinding. Dit betekent dat je de respons in realtime zult ontvangen en weergeven terwijl deze binnenkomt. Je zult de `useState` hook gebruiken om de status van de invoer en de respons bij te houden, en de Fetch API om HTTP-verzoeken naar de API te sturen. Daarnaast maak je gebruik van een helperfunctie om de gestreamde data te verwerken. Het is belangrijk dat je begrijpt hoe je API-sleutels gebruikt, hoe je gebruik maakt van asynchrone functies, en hoe je de state van een component bijwerkt in React. Bekijk ook de [OpenAI API documentatie](https://platform.openai.com/docs/guides/completion/streaming) voor meer informatie over het streamen van tekst completions.


### Stappenplan:

1. **Voorbereiding:**
   - Zorg ervoor dat je project is opgezet met Vite en dat je React hebt geïnstalleerd.
   - Zorg dat je een geldige OpenAI API-sleutel hebt en deze op de juiste manier in je project hebt geïmporteerd via de `import.meta.env` functie.
   - Zorg dat de helperfunctie `processStream` beschikbaar is in je project.

2. **Component Structuur:**
   - Maak een nieuwe React-component genaamd `CompletionWithStream`.
   - Gebruik de `useState` hook om twee stukjes state te maken: één voor de prompt en één voor de respons.

3. **Formulier en Invoer:**
   - Voeg een formulier toe aan je component met een invoerveld voor de prompt en een submit-knop.
   - Gebruik de `onChange` handler om de waarde van de prompt bij te werken in de state.

4. **Asynchrone Functie voor API-verzoek met Streaming:**
   - Maak een asynchrone functie genaamd `handleSubmit` die wordt aangeroepen wanneer het formulier wordt ingediend.
   - Voorkom dat de pagina opnieuw laadt bij het indienen van het formulier door `e.preventDefault()` te gebruiken.
   - Verstuur een POST-verzoek naar de OpenAI API met behulp van de Fetch API. Vergeet niet om de juiste headers en payload mee te geven, inclusief de stream parameter.
   - Verwerk de gestreamde respons met de `processStream` helperfunctie.

5. **Weergave van de Respons:**
   - Voeg een voorwaardelijke rendering toe om de respons weer te geven zodra deze beschikbaar is.

### Hints:

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Project Voorbereiding:**
   - Zorg ervoor dat je een Vite project hebt met React geïnstalleerd.
   - Importeer de API-sleutel met `import.meta.env.VITE_OPENAI_API_KEY`.
   - Zorg dat je de helperfunctie `processStream` beschikbaar hebt in je project.

2. **Component Structuur:**
   - Maak een nieuwe file `CompletionWithStream.jsx` en voeg de basis structuur van een functionele component toe.
   - Importeer `useState` van React en de `processStream` functie.

3. **Formulier en Invoer:**
   - Voeg een formulier toe in de JSX van je component.
   - Gebruik een `input` element voor de prompt en een `button` voor het indienen.

4. **Asynchrone Functie voor API-verzoek met Streaming:**
   - Definieer een `handleSubmit` functie die het formulier indienen afhandelt.
   - Gebruik de Fetch API om een POST-verzoek te sturen naar de OpenAI API.
   - Verwerk de gestreamde respons met `processStream`.

5. **Weergave van de Respons:**
   - Voeg conditionele logica toe om de respons weer te geven zodra deze beschikbaar is (`response && <div>{response}</div>`).

</details>

### Oplossing:

<details>
<summary>Klik hier</summary>

```jsx
import { useState } from "react";
import processStream from "../helper/processStream.js";

const apiKey = import.meta.env.VITE_OPENAI_API_KEY;

const CompletionWithStream = () => {
  const [prompt, setPrompt] = useState("");
  const [response, setResponse] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();

    setResponse("");

    try {
      const res = await fetch("https://api.openai.com/v1/chat/completions", {
        method: "POST",
        headers: {
          Authorization: `Bearer ${apiKey}`,
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          model: "gpt-4",
          messages: [{ role: "user", content: prompt }],
          stream: true,
        }),
      });

      await processStream(res.body, setResponse);
    } catch (error) {
      console.error("Error communicating with OpenAI:", error);
    }

    setPrompt("");
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <label htmlFor="prompt">
          Ask a question to OpenAI (stream):
          <input
            id="prompt"
            type="text"
            value={prompt}
            onChange={(e) => setPrompt(e.target.value)}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
      {response && (
        <div>
          <p>{response}</p>
        </div>
      )}
    </div>
  );
};

export default CompletionWithStream;
```

</details>

### Helper Functie: `processStream`

```javascript
const processStream = async (responseBody, setResponse) => {
  const reader = responseBody.getReader();
  const decoder = new TextDecoder();
  let done = false;

  while (!done) {
    const { value, done: readerDone } = await reader.read();
    done = readerDone;
    const chunk = decoder.decode(value);
    const lines = chunk.split("\n").filter((line) => line.trim() !== "");

    for (const line of lines) {
      if (line.startsWith("data: ")) {
        const data = line.substring(6).trim();
        if (data === "[DONE]") {
          done = true;
          break;
        }

        try {
          const message = JSON.parse(data).choices[0].delta?.content;
          if (message) {
            setResponse((prev) => prev + message);
          }
        } catch (e) {
          console.error("Error parsing JSON:", e);
        }
      }
    }
  }
};

export default processStream;
```


## Bonus opdracht: Van tekst naar spraak met OpenAI

### Doel:

In deze opdracht ga je een React-component maken die communiceert met de OpenAI API om tekst te genereren en deze vervolgens om te zetten naar audio. Je zult de `useState` hook gebruiken om de status van de invoer, de respons en de audio-URL bij te houden, en de Axios bibliotheek om HTTP-verzoeken naar de API te sturen. De component bevat een formulier waarin je een prompt kunt invoeren, deze prompt wordt vervolgens naar de OpenAI API gestuurd, de respons wordt weergegeven en omgezet naar audio, die dan afgespeeld kan worden op de pagina. Het is belangrijk dat je begrijpt hoe je API-sleutels gebruikt, hoe je gebruik maakt van asynchrone functies, en hoe je de state van een component bijwerkt in React. Bekijk ook de [OpenAI API documentatie](https://platform.openai.com/docs/api-reference/audio/create) voor meer informatie over het genereren van spraak.


### Stappenplan:

1. **Voorbereiding:**
   - Zorg ervoor dat je project is opgezet met Vite en dat je React en Axios hebt geïnstalleerd.
   - Zorg dat je een geldige OpenAI API-sleutel hebt en deze op de juiste manier in je project hebt geïmporteerd via de `import.meta.env` functie.

2. **Component Structuur:**
   - Maak een nieuwe React-component genaamd `Completion`.
   - Gebruik de `useState` hook om drie stukjes state te maken: één voor de prompt, één voor de tekstrespons, en één voor de audio-URL.

3. **Formulier en Invoer:**
   - Voeg een formulier toe aan je component met een invoerveld voor de prompt en een submit-knop.
   - Gebruik de `onChange` handler om de waarde van de prompt bij te werken in de state.

4. **Asynchrone Functie voor API-verzoek en Tekst naar Audio:**
   - Maak een asynchrone functie genaamd `handleSubmit` die wordt aangeroepen wanneer het formulier wordt ingediend.
   - Voorkom dat de pagina opnieuw laadt bij het indienen van het formulier door `e.preventDefault()` te gebruiken.
   - Verstuur een POST-verzoek naar de OpenAI API met behulp van Axios om de tekstrespons te verkrijgen.
   - Verstuur een tweede POST-verzoek naar de OpenAI API om de tekst om te zetten naar audio.
   - Verwerk de respons en update de state met de verkregen data.

5. **Weergave van de Respons en Audio:**
   - Voeg voorwaardelijke rendering toe om de tekstrespons en de audio-URL weer te geven zodra deze beschikbaar zijn.

### Hints:

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Project Voorbereiding:**
   - Zorg ervoor dat je een Vite project hebt met React en Axios geïnstalleerd.
   - Importeer de API-sleutel met `import.meta.env.VITE_OPENAI_API_KEY`.

2. **Component Structuur:**
   - Maak een nieuwe file `Completion.jsx` en voeg de basis structuur van een functionele component toe.
   - Importeer `useState` van React.

3. **Formulier en Invoer:**
   - Voeg een formulier toe in de JSX van je component.
   - Gebruik een `input` element voor de prompt en een `button` voor het indienen.

4. **Asynchrone Functie voor API-verzoek en Tekst naar Audio:**
   - Definieer een `handleSubmit` functie die het formulier indienen afhandelt.
   - Gebruik `axios.post` om een POST-verzoek te sturen naar de OpenAI API voor de tekstrespons.
   - Verstuur een tweede POST-verzoek om de tekst om te zetten naar audio.
   - Verwerk de respons en update de state.

5. **Weergave van de Respons en Audio:**
   - Voeg conditionele logica toe om de tekstrespons en audio-URL weer te geven zodra deze beschikbaar zijn (`response && <div>{response}</div>` en `audioUrl && <audio controls src={audioUrl}></audio>`).

</details>

### Oplossing:

<details>
<summary>Klik hier</summary>

```jsx
import { useState } from "react";
import axios from "axios";

const apiKey = import.meta.env.VITE_OPENAI_API_KEY;

const Completion = () => {
  const [prompt, setPrompt] = useState("");
  const [response, setResponse] = useState("");
  const [audioUrl, setAudioUrl] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();
    setResponse("");
    setAudioUrl("");
    try {
      const res = await axios.post(
        "https://api.openai.com/v1/chat/completions",
        {
          model: "gpt-4",
          messages: [{ role: "user", content: prompt }],
        },
        {
          headers: {
            Authorization: `Bearer ${apiKey}`,
            "Content-Type": "application/json",
          },
        }
      );

      const output = res.data.choices[0].message.content;
      setResponse(output);

      // Now convert the response to speech
      const audioRes = await axios.post(
        "https://api.openai.com/v1/audio/speech",
        {
          model: "tts-1",
          voice: "alloy",
          input: output,
        },
        {
          headers: {
            Authorization: `Bearer ${apiKey}`,
            "Content-Type": "application/json",
          },
          responseType: "arraybuffer",
        }
      );

      const audioBlob = new Blob([audioRes.data], { type: "audio/mpeg" });
      const audioUrl = URL.createObjectURL(audioBlob);
      setAudioUrl(audioUrl);
    } catch (error) {
      console.error("Error communicating with OpenAI:", error);
    }
    setPrompt("");
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <label htmlFor="prompt">
          Ask a question to OpenAI (text to audio):
          <input
            id="prompt"
            type="text"
            value={prompt}
            onChange={(e) => setPrompt(e.target.value)}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
      {response && (
        <div>
          <p>{response}</p>
        </div>
      )}
      {audioUrl && (
        <div>
          <audio controls>
            <source src={audioUrl} type="audio/mpeg" />
            Your browser does not support the audio element.
          </audio>
        </div>
      )}
    </div>
  );
};

export default Completion;
```

</details>

## Bonus opdracht: maak een audio to tekst app

### Doel:

In deze opdracht ga je een React-component maken die zowel spraak naar tekst als tekst naar spraak omzettingen kan uitvoeren met behulp van de OpenAI API. Je zult de `useState` en `useRef` hooks gebruiken om de status van de invoer, de respons, de audio-URL en de opname bij te houden. Daarnaast maak je gebruik van de MediaRecorder API om audio op te nemen en deze te versturen naar de OpenAI API voor transcriptie. Vervolgens gebruik je de OpenAI API om de getranscribeerde tekst om te zetten naar audio. Het is belangrijk dat je begrijpt hoe je API-sleutels gebruikt, hoe je gebruik maakt van asynchrone functies, en hoe je de state van een component bijwerkt in React. Bekijk ook de [OpenAI API documentatie](https://platform.openai.com/docs/guides/speech-to-text) voor meer informatie over transcriptie en spraaksynthese.


### Stappenplan:

1. **Voorbereiding:**
   - Zorg ervoor dat je project is opgezet met Vite en dat je React en Axios hebt geïnstalleerd.
   - Zorg dat je een geldige OpenAI API-sleutel hebt en deze op de juiste manier in je project hebt geïmporteerd via de `import.meta.env` functie.

2. **Component Structuur:**
   - Maak een nieuwe React-component genaamd `Completion`.
   - Gebruik de `useState` hook om vier stukjes state te maken: één voor de prompt, één voor de tekstrespons, één voor de audio-URL, en één voor de opname status.
   - Gebruik de `useRef` hook om de `MediaRecorder` en de audio chunks bij te houden.

3. **Formulier en Invoer:**
   - Voeg een formulier toe aan je component met een invoerveld voor de prompt en een submit-knop.
   - Gebruik de `onChange` handler om de waarde van de prompt bij te werken in de state.
   - Voeg een knop toe om de opname te starten en te stoppen, en wijzig het uiterlijk van de knop afhankelijk van de opname status.

4. **Functies voor Opname en Transcriptie:**
   - Maak functies voor het starten en stoppen van de audio-opname.
   - Verwerk de opgenomen audio om deze te transcriberen naar tekst met behulp van de OpenAI API.

5. **Asynchrone Functie voor API-verzoek en Tekst naar Audio:**
   - Maak een asynchrone functie genaamd `handleSubmit` die wordt aangeroepen wanneer het formulier wordt ingediend of wanneer de transcriptie beschikbaar is.
   - Verstuur een POST-verzoek naar de OpenAI API met behulp van Axios om de tekstrespons te verkrijgen.
   - Verstuur een tweede POST-verzoek naar de OpenAI API om de tekst om te zetten naar audio.
   - Verwerk de respons en update de state met de verkregen data.

6. **Weergave van de Respons en Audio:**
   - Voeg voorwaardelijke rendering toe om de tekstrespons en de audio-URL weer te geven zodra deze beschikbaar zijn.

### Hints:

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Project Voorbereiding:**
   - Zorg ervoor dat je een Vite project hebt met React en Axios geïnstalleerd.
   - Importeer de API-sleutel met `import.meta.env.VITE_OPENAI_API_KEY`.

2. **Component Structuur:**
   - Maak een nieuwe file `Completion.jsx` en voeg de basis structuur van een functionele component toe.
   - Importeer `useState` en `useRef` van React.

3. **Formulier en Invoer:**
   - Voeg een formulier toe in de JSX van je component.
   - Gebruik een `input` element voor de prompt en een `button` voor het indienen.
   - Voeg een knop toe voor het starten en stoppen van de opname.

4. **Functies voor Opname en Transcriptie:**
   - Definieer functies voor het starten en stoppen van de audio-opname.
   - Gebruik de `MediaRecorder` API om audio op te nemen en verstuur de audio voor transcriptie.

5. **Asynchrone Functie voor API-verzoek en Tekst naar Audio:**
   - Definieer een `handleSubmit` functie die het formulier indienen afhandelt en de transcriptie verwerkt.
   - Gebruik `axios.post` om POST-verzoeken te sturen naar de OpenAI API voor de tekstrespons en de tekst naar audio conversie.
   - Verwerk de respons en update de state.

6. **Weergave van de Respons en Audio:**
   - Voeg conditionele logica toe om de tekstrespons en audio-URL weer te geven zodra deze beschikbaar zijn (`response && <div>{response}</div>` en `audioUrl && <audio controls src={audioUrl}></audio>`).

</details>

### Oplossing:

<details>
<summary>Klik hier</summary>

```jsx
import { useRef, useState } from "react";
import axios from "axios";
import { MicIcon, MicOffIcon } from "lucide-react";

const apiKey = import.meta.env.VITE_OPENAI_API_KEY;

const Completion = () => {
  const [prompt, setPrompt] = useState("");
  const [response, setResponse] = useState("");
  const [audioUrl, setAudioUrl] = useState("");
  const [recording, setRecording] = useState(false);
  const mediaRecorderRef = useRef(null);
  const audioChunksRef = useRef([]);

  const startRecording = () => {
    setRecording(true);
    audioChunksRef.current = [];
    navigator.mediaDevices.getUserMedia({ audio: true }).then((stream) => {
      mediaRecorderRef.current = new MediaRecorder(stream);
      mediaRecorderRef.current.ondataavailable = (event) => {
        audioChunksRef.current.push(event.data);
      };
      mediaRecorderRef.current.start();
    });
  };

  const stopRecording = () => {
    setRecording(false);
    mediaRecorderRef.current.stop();
    mediaRecorderRef.current.onstop = async () => {
      const audioBlob = new Blob(audioChunksRef.current, { type: "audio/mp3" });
      const audioFile = new File([audioBlob], "audio.mp3", {
        type: "audio/mp3",
      });

      const formData = new FormData();
      formData.append("file", audioFile);
      formData.append("model", "whisper-1");

      try {
        const transcriptionRes = await axios.post(
          "https://api.openai.com/v1/audio/transcriptions", // Replace with actual transcription endpoint
          formData,
          {
            headers: {
              Authorization: `Bearer ${apiKey}`,
              "Content-Type": "multipart/form-data",
            },
          }
        );

        const transcription = transcriptionRes.data.text;
        setPrompt(transcription);
        handleSubmit(null, transcription);
      } catch (error) {
        console.error("Error transcribing audio:", error);
      }
    };
  };

  const handleSubmit = async (e, text) => {
    if (e) e.preventDefault();
    setResponse("");
    setAudioUrl("");
    try {
      const res = await axios.post(
        "https://api.openai.com/v1/chat/completions",
        {
          model: "gpt-4",
          messages: [{ role: "user", content: text || prompt }],
        },
        {
          headers: {
            Authorization: `Bearer ${apiKey}`,
            "Content-Type": "application/json",
          },
        }
      );

      const output = res.data.choices[0].message.content;
      setResponse(output);

      // Now convert the response to speech
      const audioRes = await axios.post(
        "https://api.openai.com/v1/audio/speech",
        {
          model: "tts-1",
          voice: "alloy",
          input: output,
        },
        {
          headers: {
            Authorization: `Bearer ${apiKey}`,
            "Content-Type": "application/json",
          },
          responseType: "arraybuffer",
        }
      );

      const audioBlob = new Blob([audioRes.data], { type: "audio/mpeg" });
      const audioUrl = URL.createObjectURL(audioBlob);
      setAudioUrl(audioUrl);
    } catch (error) {
      console.error("Error communicating with OpenAI:", error);
    }
    setPrompt("");
  };

  return (
    <div>
      <div className="flex">
        <form onSubmit={handleSubmit}>
          <label htmlFor="prompt">
            Ask a question to OpenAI (audio to text):
            <input
              id="prompt"
              type="text"
              value={prompt}
              onChange={(e) => setPrompt(e.target.value)}
            />
          </label>
        </form>
        <button
          className="btn"
          onClick={recording ? stopRecording : startRecording}
        >
          {recording ? <MicOffIcon size={16} /> : <MicIcon size={16} />}
        </button>
      </div>
      {response && (
        <div>
          <p>{response}</p>
        </div>
      )}
      {audioUrl && (
        <div>
          <audio controls>
            <source src={audioUrl} type="audio/mpeg" />
            Your browser does not support the audio element.
          </audio>
        </div>
      )}
    </div>
  );
};

export default Completion;
```

</details>

## Bonus opdracht: maak een tekst naar plaatje app

### Doel:

In deze opdracht ga je een React-component maken die communiceert met de OpenAI API om afbeeldingen te genereren op basis van een tekstprompt. Je zult de `useState` hook gebruiken om de status van de invoer en de gegenereerde afbeelding bij te houden, en de Axios bibliotheek om HTTP-verzoeken naar de API te sturen. De component bevat een formulier waarin je een prompt kunt invoeren, deze prompt wordt vervolgens naar de OpenAI API gestuurd, en de gegenereerde afbeelding wordt weergegeven op de pagina. Het is belangrijk dat je begrijpt hoe je API-sleutels gebruikt, hoe je gebruik maakt van asynchrone functies, en hoe je de state van een component bijwerkt in React. Bekijk ook de [OpenAI API documentatie](https://platform.openai.com/docs/guides/images/generations) voor meer informatie over het genereren van afbeeldingen.


### Stappenplan:

1. **Voorbereiding:**
   - Zorg ervoor dat je project is opgezet met Vite en dat je React en Axios hebt geïnstalleerd.
   - Zorg dat je een geldige OpenAI API-sleutel hebt en deze op de juiste manier in je project hebt geïmporteerd via de `import.meta.env` functie.

2. **Component Structuur:**
   - Maak een nieuwe React-component genaamd `Completion`.
   - Gebruik de `useState` hook om twee stukjes state te maken: één voor de prompt en één voor de gegenereerde afbeelding URL.

3. **Formulier en Invoer:**
   - Voeg een formulier toe aan je component met een invoerveld voor de prompt en een submit-knop.
   - Gebruik de `onChange` handler om de waarde van de prompt bij te werken in de state.

4. **Asynchrone Functie voor API-verzoek:**
   - Maak een asynchrone functie genaamd `handleSubmit` die wordt aangeroepen wanneer het formulier wordt ingediend.
   - Voorkom dat de pagina opnieuw laadt bij het indienen van het formulier door `e.preventDefault()` te gebruiken.
   - Verstuur een POST-verzoek naar de OpenAI API met behulp van Axios om de afbeelding te genereren.
   - Verwerk de respons en update de state met de URL van de gegenereerde afbeelding.

5. **Weergave van de Afbeelding:**
   - Voeg voorwaardelijke rendering toe om de gegenereerde afbeelding weer te geven zodra deze beschikbaar is.

### Hints:

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Project Voorbereiding:**
   - Zorg ervoor dat je een Vite project hebt met React en Axios geïnstalleerd.
   - Importeer de API-sleutel met `import.meta.env.VITE_OPENAI_API_KEY`.

2. **Component Structuur:**
   - Maak een nieuwe file `Completion.jsx` en voeg de basis structuur van een functionele component toe.
   - Importeer `useState` van React.

3. **Formulier en Invoer:**
   - Voeg een formulier toe in de JSX van je component.
   - Gebruik een `input` element voor de prompt en een `button` voor het indienen.

4. **Asynchrone Functie voor API-verzoek:**
   - Definieer een `handleSubmit` functie die het formulier indienen afhandelt.
   - Gebruik `axios.post` om een POST-verzoek te sturen naar de OpenAI API voor het genereren van de afbeelding.
   - Verwerk de respons en update de state met de gegenereerde afbeelding URL.

5. **Weergave van de Afbeelding:**
   - Voeg conditionele logica toe om de gegenereerde afbeelding weer te geven zodra deze beschikbaar is (`imageUrl && <img src={imageUrl} alt="Generated by OpenAI" />`).

</details>

### Oplossing:

<details>
<summary>Klik hier</summary>

```jsx
import { useState } from "react";
import axios from "axios";

const apiKey = import.meta.env.VITE_OPENAI_API_KEY;

const Completion = () => {
  const [prompt, setPrompt] = useState("");
  const [imageUrl, setImageUrl] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();
    setImageUrl("");
    try {
      const res = await axios.post(
        "https://api.openai.com/v1/images/generations",
        {
          model: "dall-e-3",
          prompt,
        },
        {
          headers: {
            Authorization: `Bearer ${apiKey}`,
            "Content-Type": "application/json",
          },
        }
      );

      const imageUrl = res.data.data[0].url;
      setImageUrl(imageUrl);
    } catch (error) {
      console.error("Error generating image with OpenAI:", error);
    }
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <label htmlFor="prompt">
          Ask a question to OpenAI (text to image):
          <input
            id="prompt"
            type="text"
            value={prompt}
            onChange={(e) => setPrompt(e.target.value)}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
      {imageUrl && (
        <div>
          <img src={imageUrl} alt="Generated by OpenAI" />
        </div>
      )}
    </div>
  );
};

export default Completion;
```

</details>

## Bonus opdracht: maak een plaatje naar tekst app

### Doel:

In deze opdracht ga je een React-component maken die communiceert met de OpenAI API om een afbeelding te analyseren en een beschrijving ervan te genereren op basis van een ingevoerde URL. Je zult de `useState` hook gebruiken om de status van de invoer en de gegenereerde tekst bij te houden, en de Fetch API om HTTP-verzoeken naar de API te sturen. De component bevat een formulier waarin je een URL van een afbeelding kunt invoeren, deze URL wordt vervolgens naar de OpenAI API gestuurd, en de beschrijving van de afbeelding wordt weergegeven op de pagina. Het is belangrijk dat je begrijpt hoe je API-sleutels gebruikt, hoe je gebruik maakt van asynchrone functies, en hoe je de state van een component bijwerkt in React. Bekijk ook de [OpenAI API documentatie](https://platform.openai.com/docs/guides/images/description) voor meer informatie over beeldbeschrijving.

### Stappenplan:

1. **Voorbereiding:**
   - Zorg ervoor dat je project is opgezet met Vite en dat je React hebt geïnstalleerd.
   - Zorg dat je een geldige OpenAI API-sleutel hebt en deze op de juiste manier in je project hebt geïmporteerd via de `import.meta.env` functie.

2. **Component Structuur:**
   - Maak een nieuwe React-component genaamd `CompletionImageToText`.
   - Gebruik de `useState` hook om twee stukjes state te maken: één voor de prompt (de afbeelding URL) en één voor de gegenereerde tekstbeschrijving van de afbeelding.

3. **Formulier en Invoer:**
   - Voeg een formulier toe aan je component met een invoerveld voor de afbeelding URL en een submit-knop.
   - Gebruik de `onChange` handler om de waarde van de prompt bij te werken in de state.

4. **Asynchrone Functie voor API-verzoek:**
   - Maak een asynchrone functie genaamd `handleSubmit` die wordt aangeroepen wanneer het formulier wordt ingediend.
   - Voorkom dat de pagina opnieuw laadt bij het indienen van het formulier door `e.preventDefault()` te gebruiken.
   - Verstuur een POST-verzoek naar de OpenAI API met behulp van de Fetch API om de afbeelding te analyseren.
   - Verwerk de respons en update de state met de gegenereerde tekstbeschrijving.

5. **Weergave van de Analyse:**
   - Voeg voorwaardelijke rendering toe om de gegenereerde tekstbeschrijving weer te geven zodra deze beschikbaar is.

### Hints:

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Project Voorbereiding:**
   - Zorg ervoor dat je een Vite project hebt met React geïnstalleerd.
   - Importeer de API-sleutel met `import.meta.env.VITE_OPENAI_API_KEY`.

2. **Component Structuur:**
   - Maak een nieuwe file `CompletionImageToText.jsx` en voeg de basis structuur van een functionele component toe.
   - Importeer `useState` van React.

3. **Formulier en Invoer:**
   - Voeg een formulier toe in de JSX van je component.
   - Gebruik een `input` element voor de prompt (de afbeelding URL) en een `button` voor het indienen.

4. **Asynchrone Functie voor API-verzoek:**
   - Definieer een `handleSubmit` functie die het formulier indienen afhandelt.
   - Gebruik de Fetch API om een POST-verzoek te sturen naar de OpenAI API voor het analyseren van de afbeelding.
   - Verwerk de respons en update de state met de gegenereerde tekstbeschrijving.

5. **Weergave van de Analyse:**
   - Voeg conditionele logica toe om de gegenereerde tekstbeschrijving weer te geven zodra deze beschikbaar is (`imageAnalysis && <div>{imageAnalysis}</div>`).

</details>

### Oplossing:

<details>
<summary>Klik hier</summary>

```jsx
import { useState } from "react";

const apiKey = import.meta.env.VITE_OPENAI_API_KEY;

const CompletionImageToText = () => {
  const [prompt, setPrompt] = useState("");
  const [imageAnalysis, setImageAnalysis] = useState("");

  const handleSubmit = async (event) => {
    event.preventDefault();
    setImageAnalysis("");

    const requestBody = {
      model: "gpt-4",
      messages: [
        {
          role: "user",
          content: `What’s in this image? ${prompt}`,
        },
      ],
    };

    try {
      const response = await fetch(
        "https://api.openai.com/v1/chat/completions",
        {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            Authorization: `Bearer ${apiKey}`,
          },
          body: JSON.stringify(requestBody),
        }
      );

      if (!response.ok) {
        throw new Error(`Error: ${response.statusText}`);
      }

      const data = await response.json();
      const analysis = data.choices[0].message.content;
      setImageAnalysis(analysis);
    } catch (error) {
      console.error("Error analyzing image with OpenAI:", error);
    }
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <label htmlFor="prompt">
          Ask a question to OpenAI (image to text):
          <input
            id="prompt"
            type="text"
            placeholder="Enter an image URL"
            value={prompt}
            onChange={(e) => setPrompt(e.target.value)}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
      {imageAnalysis && (
        <div>
          <p>{imageAnalysis}</p>
        </div>
      )}
    </div>
  );
};

export default CompletionImageToText;
```

</details>

## Toelichting op de requests

### Chatrequest

**Instellingen:**

1. **Model:**
    - De naam van het AI-model dat je wilt gebruiken. Voorbeelden zijn "gpt-4" en "gpt-3.5".
    - **Invloed:** Het model bepaalt de kwaliteit en het type respons. Nieuwere modellen zoals "gpt-4" zijn vaak beter
      in het begrijpen en genereren van tekst.

2. **Messages:**
    - Een lijst van berichten die de context en input vormen voor het model. Berichten kunnen systeem-, gebruiker-, of
      assistent-berichten zijn.
    - **Invloed:** De inhoud van deze berichten bepaalt hoe het model de vraag begrijpt en antwoordt. Een duidelijke
      context en vraag kunnen de kwaliteit van het antwoord verbeteren.

3. **Temperature:**
    - Een waarde tussen 0 en 1 die bepaalt hoe creatief of conservatief de output moet zijn.
    - **Invloed:** Een lagere waarde (zoals 0.0) zorgt voor meer voorspelbare en consistente antwoorden, terwijl een
      hogere waarde (zoals 0.7) zorgt voor meer variatie en creativiteit in de antwoorden.

4. **MaxTokens:**
    - Het maximum aantal tokens (woorden en leestekens) in de gegenereerde respons.
    - **Invloed:** Beperkt de lengte van de gegenereerde tekst. Een hogere waarde kan resulteren in langere en meer
      gedetailleerde antwoorden.

### Imagerequest

**Instellingen:**

1. **Prompt:**
    - De tekstuele beschrijving van wat de afbeelding moet voorstellen.
    - **Invloed:** De nauwkeurigheid en relevantie van de gegenereerde afbeelding hangen sterk af van de duidelijkheid
      en specificiteit van de prompt.

2. **n:**
    - Het aantal afbeeldingen dat gegenereerd moet worden.
    - **Invloed:** Bepaalt hoeveel verschillende afbeeldingen je als resultaat krijgt. Meerdere afbeeldingen kunnen
      helpen bij het kiezen van de beste interpretatie van de prompt.

3. **Size:**
    - De grootte van de gegenereerde afbeelding (bijvoorbeeld "256x256").
    - **Invloed:** De resolutie van de gegenereerde afbeelding. Grotere afbeeldingen zijn gedetailleerder maar kunnen
      langer duren om te genereren.

4. **ResponseFormat:**
    - Het formaat van de gegenereerde afbeelding, zoals URL of base64.
    - **Invloed:** Bepaalt hoe de afbeelding wordt geretourneerd. Een URL is handig voor weergave op het web, terwijl
      base64 nuttig is voor directe integratie in andere toepassingen.

5. **Model:**
    - De naam van het model dat wordt gebruikt om de afbeeldingen te genereren, zoals "dall-e-2".
    - **Invloed:** Verschillende modellen kunnen variëren in stijl en kwaliteit van de gegenereerde afbeeldingen.

### Speechrequest

**Instellingen:**

1. **Model:**
    - De naam van het AI-model dat wordt gebruikt voor spraaksynthese, zoals "tts-1".
    - **Invloed:** Het model bepaalt de stemkwaliteit en de natuurlijkheid van de gegenereerde spraak.

2. **Input:**
    - De tekst die moet worden omgezet in spraak.
    - **Invloed:** De inhoud en lengte van de tekst bepalen de resulterende spraak.

3. **Voice:**
    - De specifieke stem die moet worden gebruikt voor de spraaksynthese.
    - **Invloed:** Verschillende stemmen kunnen variëren in toonhoogte, snelheid en expressie.

4. **ResponseFormat:**
    - Het formaat van de gegenereerde spraak, zoals MP3.
    - **Invloed:** Bepaalt hoe de spraak wordt geretourneerd en opgeslagen.

5. **Speed:**
    - De snelheid waarmee de tekst wordt uitgesproken.
    - **Invloed:** Een lagere snelheid kan de verstaanbaarheid verbeteren, terwijl een hogere snelheid nuttig kan zijn
      voor snelle informatieoverdracht.

### Transcriptionrequest

**Instellingen:**

1. **File:**
    - Het pad naar het audiobestand dat moet worden getranscribeerd.
    - **Invloed:** De kwaliteit en duidelijkheid van de audio beïnvloeden de nauwkeurigheid van de transcriptie.

2. **Model:**
    - De naam van het AI-model dat wordt gebruikt voor transcriptie, zoals "whisper-1".
    - **Invloed:** Het model bepaalt de nauwkeurigheid en snelheid van de transcriptie.

3. **Prompt:**
    - Extra tekstinstructies om het model te helpen bij de transcriptie.
    - **Invloed:** Helpt het model om de context beter te begrijpen, wat kan leiden tot nauwkeurigere transcripties.

4. **ResponseFormat:**
    - Het formaat van de geretourneerde transcriptie, zoals JSON.
    - **Invloed:** Bepaalt hoe de transcriptiegegevens worden geretourneerd en verwerkt.

5. **Temperature:**
    - Een waarde tussen 0 en 1 die bepaalt hoe creatief of conservatief de transcriptie moet zijn.
    - **Invloed:** Een lagere waarde zorgt voor een meer voorspelbare en consistente transcriptie, terwijl een hogere
      waarde meer variatie kan introduceren.

6. **TimestampGranularity:**
    - De nauwkeurigheid van de tijdstempels in de transcriptie, zoals WORD of SEGMENT.
    - **Invloed:** Bepaalt hoe gedetailleerd de tijdstempels in de transcriptie zijn. Fijnere granulariteit (zoals WORD)
      biedt nauwkeurigere tijdsinformatie.

7. **Language:**
    - De taal van het audiobestand.
    - **Invloed:** De taalinstelling helpt het model om de audio correct te interpreteren en nauwkeurige transcripties
      te produceren.

### Samenvatting

De instellingen van elk verzoek naar de OpenAI API zijn belangrijk voor de kwaliteit en relevantie van de resulterende
uitkomsten. Door de juiste parameters te kiezen, kun je de AI-modellen optimaal benutten voor verschillende
toepassingen, zoals tekstgeneratie, afbeeldingscreatie, spraaksynthese en transcriptie. Experimenteer met deze
instellingen om te zien hoe ze de resultaten beïnvloeden en pas ze aan op basis van je specifieke behoeften en context.
