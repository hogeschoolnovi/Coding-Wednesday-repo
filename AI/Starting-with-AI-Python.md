## Python - workshop overzicht

<!-- TOC -->
  * [Python - workshop overzicht](#python---workshop-overzicht)
  * [Opzetten van het project](#opzetten-van-het-project)
    * [Doel:](#doel)
    * [Stappenplan:](#stappenplan)
  * [Opdracht: maak een openai client](#opdracht-maak-een-openai-client)
    * [Doel:](#doel-1)
    * [Stappenplan:](#stappenplan-1)
  * [Opdracht: maak een chat app](#opdracht-maak-een-chat-app)
    * [Doel:](#doel-2)
  * [Opdracht: maak een chat with streaming](#opdracht-maak-een-chat-with-streaming)
    * [Doel:](#doel-3)
  * [Bonus opdracht: Van tekst naar spraak met OpenAI](#bonus-opdracht-van-tekst-naar-spraak-met-openai)
    * [Doel:](#doel-4)
  * [Bonus opdracht: maak een audio to tekst app](#bonus-opdracht-maak-een-audio-to-tekst-app)
    * [Doel:](#doel-5)
  * [Bonus opdracht: maak een tekst naar plaatje app](#bonus-opdracht-maak-een-tekst-naar-plaatje-app)
    * [Doel:](#doel-6)
  * [Bonus opdracht: maak een plaatje naar tekst app](#bonus-opdracht-maak-een-plaatje-naar-tekst-app)
  * [Bonus opdracht: Beeldherkenning met OpenAI GPT-4o](#bonus-opdracht-beeldherkenning-met-openai-gpt-4o)
    * [Doel:](#doel-7)
  * [Toelichting op de requests](#toelichting-op-de-requests)
    * [Chatrequest](#chatrequest)
    * [Imagerequest](#imagerequest)
    * [Speechrequest](#speechrequest)
    * [Transcriptionrequest](#transcriptionrequest)
    * [Samenvatting](#samenvatting)
<!-- TOC -->

## Opzetten van het project

### Doel:

Opzetten van een basisproject in PyCharm, en het toevoegen van de Simple OpenAI dependency.

### Stappenplan:

1. **Nieuwe Python Project Aanmaken:**
    - Open PyCharm.
    - Selecteer "Create New Project".
    - Kies links de optie "Pure Python"
    - Geef je project een naam en locatie (bijvoorbeeld `openai-demo`).
    - Vink rechts "New environment using Virualenv" en "Create a main.py welcome script" aan in de project wizard en
      klik op "Next".
    - Klik op "Create".
    - Verwijder de inhoud het bestand `main.py` uit de projectstructuur zodat het leeg is.

2. **Project Structuur Controleren:**
    - Zorg ervoor dat je projectstructuur er als volgt uitziet:
        ```
        openai-demo
        ├── venv
        │   └── (hier staan de virtuele omgevingsbestanden)
        └── main.py
        ```
3. **API Sleutel Configureren:**

- Voeg een bestand toe in de root folder / genaamd `.env`
- Voeg je OpenAI API-sleutel toe aan dit bestand
    - OPENAI_API_KEY=_YOUR_API_KEY_HERE_
- Installeer en importeer de `python-dotenv` package in je project om de API-sleutel te laden.
- Laad de API-sleutel met behulp van `load_dotenv()` en `os.getenv("OPENAI_API_KEY")`.
- Sla de API-sleutel op in een variabele voor later gebruik.

**Hints**
<details>
<summary>Hints</summary>

1. **Dependency Toevoegen:**

- Installeer de `python-dotenv` package om de API-sleutel te laden.
    ```bash
    pip install python-dotenv
    ```
- Importeer `os` en `load_dotenv` in je `main.py` bestand.

</details>

**Oplossing**
<details>
<summary>Oplossing</summary>

```python
    import os
    from dotenv import load_dotenv
    
    load_dotenv()
    api_key = os.getenv("OPENAI_API_KEY")
```

</details>

## Opdracht: maak een openai client

### Doel:

Het initialiseren van de OpenAI-client met een API-sleutel in je project.
Dit stelt je in staat om verbinding te maken met de OpenAI-diensten en
hun functies te gebruiken door de client te authentificeren en
te autoriseren met de unieke API-sleutel.

### Stappenplan:

1. **Installeer OpenAI Bibliotheek:**
    - Installeer de OpenAI-bibliotheek `openai` in je project om verbinding te maken met de OpenAI-diensten.
   
2. **Importeer OpenAI Bibliotheek:**
    - Importeer de OpenAI-bibliotheek in je Python-bestand.

3. **Initialiseer de OpenAI client:**
    - Initialiseer de OpenAI-client met de API-sleutel om verbinding te maken met de OpenAI-diensten.
    - Sla de client op in een variabele voor later gebruik.

**Hints**
<details>
<summary>Hints</summary>

1. **Dependency Toevoegen:**

- Installeer de `openai` package om verbinding te maken met de OpenAI-diensten.
    ```bash
    pip install openai
    ```
- Importeer `OpenAI` in je `main.py` bestand.
- Initialiseer de OpenAI-client `OpenAI()` en gebruik de API-sleutel die we in de vorige stap hebben opgeslagen in een variabele.
- Sla de client op in een variabele `client` voor later gebruik.

</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```Python
# Importeer de OpenAI-bibliotheek
from openai import OpenAI

# Initialiseer de OpenAI-client met de API-sleutel
client = OpenAI(
    api_key=api_key
)
```

</details>

## Opdracht: maak een chat app

### Doel:

In deze stap vraag je de gebruiker om een vraag te stellen via de prompt en verstuur je deze vraag naar de OpenAI API met behulp van de client. De client stuurt de gebruikersvraag als een bericht naar het model "gpt-4" en ontvangt vervolgens de gegenereerde reactie van de API, die je kunt gebruiken of weergeven aan de gebruiker. Bekijk ook de [OpenAI API documentatie](https://platform.openai.com/docs/guides/text-generation/chat-completions-api) voor meer informatie over het chatverzoek. 

_Tip: je in het code blok voorbeeld selecteren dat je het in Python syntax wilt zien._

In dit geval heb je slechts één bericht van de gebruiker nodig om een chatverzoek te maken. Je kunt de gegenereerde reactie van de API weergeven in de console of in een GUI-venster.

**Hints**

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Vraag stellen aan OpenAI:**
    - Vraag je de gebruiker om een vraag in te voeren die naar OpenAI gestuurd zal worden. Gebruik hiervoor de `input()` functie.
    - Sla de gebruikersinput op in een variabele voor later gebruik.

2. **Verstuur de prompt naar OpenAI:**
   - Gebruik de `client.chat.completions.create` functie om de vraag naar OpenAI te sturen en het antwoord te ontvangen.
   - De functie kan meerdere argumenten ontvangen, waaronder een `model`, `messages`, `temperature`, en `max_tokens`.
   - Zorg dat je ten minste de `model` en `messages` argumenten correct instelt.
   - Het model moet "gpt-4" zijn en de messages bestaan uit een `dictionary` die als key "role" en als value de prompt (input) bevat die we van de gebruiker hebben ontvangen.
   - Sla de gegenereerde reactie op in een variabele voor later gebruik.

3. **Toon de response aan de gebruiker:**
    - Gebruik de gegenereerde reactie om de AI-antwoord aan de gebruiker te tonen.
    - Gebruik de `print()` functie om de reactie in de console weer te geven.
    - Print eerst het hele object om te zien welke informatie erin zit en kies dan welke informatie je wilt weergeven. 
    - Haal vervolgens de relevante informatie uit het object om deze aan de gebruiker te tonen.


</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```Python
# Ask a question to OpenAI
prompt = input("Ask a question to OpenAI: ")

# Get the response from OpenAI
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "user", "content": prompt}
    ]
)
```

</details>

## Opdracht: maak een chat with streaming

### Doel:

Het opzetten van een applicatie die gebruikersinput vraagt en de reacties streamt met behulp van de OpenAI API.

We gaan weer eerst een chatverzoek sturen naar de OpenAI API, maar deze keer zullen we de reactie streamen in plaats van te wachten op het volledige antwoord. Dit betekent dat we de reactie in realtime zullen ontvangen en verwerken terwijl deze binnenkomt. Dit kan handig zijn voor toepassingen waarbij realtime interactie met de AI nodig is.

We hergebruiken de code van de vorige opdracht en passen deze aan om de reactie te streamen in plaats van te wachten op het volledige antwoord. Geef als extra argument `stream=True` mee aan de `create` functie om de streaming-modus in te schakelen. De response zal een lijst van `ChatCompletion` objecten zijn die in realtime binnenkomen.

Zorg ervoor dat het antwoord van OpenAI in real-time wordt verwerkt en geprint. Gebruik een for-lus om door de stukjes (chunks) van de binnenkomende data in het stream-object te lopen. Controleer in elke iteratie of er inhoud aanwezig is in `chunk.choices[0].delta.content`. Als er inhoud is, print deze dan direct zonder een nieuwe regel te beginnen, zodat een vloeiende stroom van tekst ontstaat.

**Hints**

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **API-aanroep aanpassen voor streaming:**
    - Vervang de standaard responscreatie door het toevoegen van een stream=True parameter in de API-aanroep. 
    - Pas de client.chat.completions.create functie aan zodat deze het stream object retourneert.

2. **Data verwerken en printen:**
  - Implementeer een for-lus om door de binnenkomende data (chunks) te lopen.
  - Controleer in de for-lus of er inhoud aanwezig is in chunk.choices[0].delta.content.
  - Print de ontvangen inhoud direct, zonder een nieuwe regel te beginnen, om een vloeiende stroom van tekst te creëren.


</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```Python
import os
from dotenv import load_dotenv
from openai import OpenAI

# Load environment variables from .env file
load_dotenv()
api_key = os.getenv('OPENAI_API_KEY')

# Initialize the OpenAI client with the API key
client = OpenAI(
    api_key=api_key
)

# Ask a question to OpenAI
prompt = input("Ask a question to OpenAI: ")

# Get the response from OpenAI with streaming
stream = client.chat.completions.create(
    model="gpt-4",
    messages=[
        {"role": "user", "content": prompt}
    ],
    stream=True,
)

# Print the output as it streams
for chunk in stream:
    if chunk.choices[0].delta.content is not None:
        print(chunk.choices[0].delta.content, end="")

```

</details>

## Bonus opdracht: Van tekst naar spraak met OpenAI

### Doel:

In deze opdracht ga je een text response omzetten naar audio met behulp van een ander taalmodel van OpenAI. Je gebruikt hiervoor de OpenAI API om eerst een tekst response te genereren en vervolgens deze tekst om te zetten naar een spraakbestand. Bekijk ook de [OpenAI API documentatie](https://platform.openai.com/docs/api-reference/audio/createSpeech) voor meer informatie over het genereren van spraak.

**Hints**

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Initialiseer de omgeving:**
   - Installeer de benodigde libraries, zoals `dotenv` en `openai`.
   - Maak een `.env` bestand aan en voeg daarin je OpenAI API key toe.

2. **Laad de omgevingsvariabelen:**
   - Gebruik de `load_dotenv` functie om je API key in te laden.

3. **Initialiseer de OpenAI client:**
   - Gebruik de geladen API key om de OpenAI client te initialiseren.

4. **Vraag input van de gebruiker:**
   - Vraag de gebruiker om een vraag in te voeren die naar OpenAI gestuurd wordt.

5. **Krijg de response van OpenAI:**
   - Stuur de vraag naar OpenAI en vang de response op.

6. **Sla de response op in een variabele:**
   - Bewaar de ontvangen tekst response in een variabele.

7. **Zet de tekst om naar spraak:**
   - Gebruik de OpenAI audio API om de tekst om te zetten naar een spraakbestand.
   - Sla het spraakbestand op in de gewenste directory.

</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```Python
import os
from dotenv import load_dotenv
from openai import OpenAI
from pathlib import Path

# Load environment variables from .env file
load_dotenv()
api_key = os.getenv('OPENAI_API_KEY')

# Initialize the OpenAI client with the API key
client = OpenAI(
    api_key=api_key
)

# Ask a question to OpenAI
prompt = input("Ask a question to OpenAI: ")

# Get the response from OpenAI
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "user", "content": prompt}
    ]
)

# Save the output in a variable
output = response.choices[0].message.content

speech_file_path = Path(__file__).parent / "speech.mp3"
with client.audio.speech.with_streaming_response.create(
  model="tts-1",
  voice="alloy",
  input=output,
) as response:
    response.stream_to_file(speech_file_path)
```
</details>

## Bonus opdracht: maak een audio to tekst app

### Doel:

In deze opdracht ga je een audiobestand transcriberen naar tekst en vervolgens deze tekst vertalen naar een andere taal met behulp van OpenAI. Daarna zet je de vertaalde tekst om naar spraak en sla je deze op als een nieuw audiobestand. Bekijk ook de [OpenAI API documentatie](https://platform.openai.com/docs/guides/speech-to-text) voor meer informatie over het transcriberen van audiobestanden.

**Hints**

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Initialiseer de omgeving:**
   - Installeer de benodigde libraries, zoals `dotenv` en `openai`.
   - Maak een `.env` bestand aan en voeg daarin je OpenAI API key toe.

2. **Laad de omgevingsvariabelen:**
   - Gebruik de `load_dotenv` functie om je API key in te laden.

3. **Initialiseer de OpenAI client:**
   - Gebruik de geladen API key om de OpenAI client te initialiseren.

4. **Open het audiobestand:**
   - Open het audiobestand dat je wilt transcriberen.

5. **Transcribeer het audiobestand:**
   - Gebruik de OpenAI API om het audiobestand te transcriberen naar tekst.

6. **Bewaar de getranscribeerde tekst:**
   - Bewaar de getranscribeerde tekst in een variabele.

7. **Krijg een vertaling van de tekst:**
   - Stuur de getranscribeerde tekst naar OpenAI en vang de response op met de vertaalde tekst.

8. **Zet de vertaalde tekst om naar spraak:**
   - Gebruik de OpenAI audio API om de vertaalde tekst om te zetten naar een spraakbestand.
   - Sla het spraakbestand op in de gewenste directory.

</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```Python
import os
from dotenv import load_dotenv
from openai import OpenAI
from pathlib import Path

# Load environment variables from .env file
load_dotenv()
api_key = os.getenv('OPENAI_API_KEY')

# Initialize the OpenAI client with the API key
client = OpenAI(
    api_key=api_key
)

audio_file = open("speech.mp3", "rb")
transcription_response = client.audio.transcriptions.create(
    model="whisper-1",
    file=audio_file,
)

# Get the transcribed text
prompt = transcription_response.json()

# Get the response from OpenAI
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "user", "content": prompt}
    ],
)

# Save the output in a variable
output = response.choices[0].message.content

speech_file_path = Path(__file__).parent / "speech_out.mp3"
with client.audio.speech.with_streaming_response.create(
        model="tts-1",
        voice="alloy",
        input=output,
) as response:
    response.stream_to_file(speech_file_path)
```
</details>

## Bonus opdracht: maak een tekst naar plaatje app

### Doel:

In deze opdracht ga je een afbeelding genereren met behulp van OpenAI's DALL-E model. Je voert een tekstprompt in en ontvangt een gegenereerde afbeelding die overeenkomt met jouw beschrijving. Bekijk ook de [OpenAI API documentatie](https://platform.openai.com/docs/api-reference/images/create) voor meer informatie over het genereren van afbeeldingen.

**Hints**

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Initialiseer de omgeving:**
   - Installeer de benodigde libraries, zoals `dotenv` en `openai`.
   - Maak een `.env` bestand aan en voeg daarin je OpenAI API key toe.

2. **Laad de omgevingsvariabelen:**
   - Gebruik de `load_dotenv` functie om je API key in te laden.

3. **Initialiseer de OpenAI client:**
   - Gebruik de geladen API key om de OpenAI client te initialiseren.

4. **Vraag input van de gebruiker:**
   - Vraag de gebruiker om een beschrijving van de afbeelding die gegenereerd moet worden.

5. **Genereer de afbeelding:**
   - Stuur de tekstprompt naar OpenAI en ontvang de gegenereerde afbeelding.

6. **Toon de afbeelding:**
   - Print de URL van de gegenereerde afbeelding zodat deze bekeken kan worden.

</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```Python
import os
from dotenv import load_dotenv
from openai import OpenAI

# Load environment variables from .env file
load_dotenv()
api_key = os.getenv('OPENAI_API_KEY')

# Initialize the OpenAI client with the API key
client = OpenAI(
    api_key=api_key
)

# Ask a question to OpenAI
prompt = input("Ask a question to OpenAI: ")

response = client.images.generate(
  model="dall-e-3",
  prompt=prompt,
  n=1,
  size="1024x1024"
)

print(response.data[0].url)
```
</details>

## Bonus opdracht: maak een plaatje naar tekst app

## Bonus opdracht: Beeldherkenning met OpenAI GPT-4o

### Doel:

In deze opdracht ga je een afbeelding analyseren met behulp van OpenAI's GPT-4o Vison model. Je stuurt een afbeelding en een bijbehorende vraag naar het model en ontvangt een beschrijving van wat er in de afbeelding te zien is. Bekijk ook de [OpenAI API documentatie](https://platform.openai.com/docs/guides/vision) voor meer informatie over het analyseren van afbeeldingen.

**Hints**

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Initialiseer de omgeving:**
   - Installeer de benodigde libraries, zoals `dotenv` en `openai`.
   - Maak een `.env` bestand aan en voeg daarin je OpenAI API key toe.

2. **Laad de omgevingsvariabelen:**
   - Gebruik de `load_dotenv` functie om je API key in te laden.

3. **Initialiseer de OpenAI client:**
   - Gebruik de geladen API key om de OpenAI client te initialiseren.

4. **Stel de vraag en voeg de afbeelding toe:**
   - Stel een vraag over de afbeelding en voeg de URL van de afbeelding toe.

5. **Analyseer de afbeelding:**
   - Stuur de vraag en de afbeelding naar OpenAI en ontvang de beschrijving van de afbeelding.

6. **Toon de beschrijving:**
   - Print de ontvangen beschrijving van de afbeelding.

</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```Python
# Load environment variables from .env file
import os
from dotenv import load_dotenv
from openai import OpenAI

load_dotenv()
api_key = os.getenv('OPENAI_API_KEY')

# Initialize the OpenAI client with the API key
client = OpenAI(
    api_key=api_key
)

response = client.chat.completions.create(
  model="gpt-4o",
  messages=[
    {
      "role": "user",
      "content": [
        {"type": "text", "text": "What’s in this image?"},
        {
          "type": "image_url",
          "image_url": {
            "url": "https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg",
          },
        },
      ],
    }
  ],
  max_tokens=300,
)

print(response.choices[0].message.content)
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
