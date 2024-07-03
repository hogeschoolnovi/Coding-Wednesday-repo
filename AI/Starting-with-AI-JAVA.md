## Java - workshop overzicht

<!-- TOC -->
  * [Java - workshop overzicht](#java---workshop-overzicht)
  * [Opzetten van het project](#opzetten-van-het-project)
    * [Doel:](#doel)
    * [Stappenplan:](#stappenplan)
  * [Opdracht: Maak een OpenAI Service](#opdracht-maak-een-openai-service)
    * [Doel:](#doel-1)
    * [Stappenplan:](#stappenplan-1)
  * [Opdracht: Maak een chat app](#opdracht-maak-een-chat-app)
    * [Doel:](#doel-2)
  * [Opdracht: Maak een chat with streaming](#opdracht-maak-een-chat-with-streaming)
    * [Doel:](#doel-3)
  * [Bonus Opdracht: Maak een tekst naar audio app](#bonus-opdracht-maak-een-tekst-naar-audio-app)
    * [Doel:](#doel-4)
  * [Bonus Opdracht: Maak een audio to tekst app](#bonus-opdracht-maak-een-audio-to-tekst-app)
    * [Doel:](#doel-5)
  * [Bonus Opdracht: Maak een tekst naar plaatje app](#bonus-opdracht-maak-een-tekst-naar-plaatje-app)
    * [Doel:](#doel-6)
  * [Bonus Opdracht: Maak een plaatje naar tekst app](#bonus-opdracht-maak-een-plaatje-naar-tekst-app)
    * [Doel:](#doel-7)
  * [Toelichting op de requests](#toelichting-op-de-requests)
    * [ChatRequest](#chatrequest)
    * [ImageRequest](#imagerequest)
    * [SpeechRequest](#speechrequest)
    * [TranscriptionRequest](#transcriptionrequest)
    * [Samenvatting](#samenvatting)
<!-- TOC -->

## Opzetten van het project

### Doel:

Opzetten van een basisproject in IntelliJ IDEA met Maven, en het toevoegen van de Simple OpenAI dependency.

### Stappenplan:

1. **Nieuwe Maven Project Aanmaken:**
    - Open IntelliJ IDEA.
    - Selecteer "Create New Project".
    - Kies "Maven" in de project wizard en klik op "Next".
    - Vul de GroupId en ArtifactId in (bijvoorbeeld `com.example` en `openai-demo`).
    - Klik op "Finish".

2. **Maven Dependency Toevoegen:**
    - Open het `pom.xml` bestand in de root van je project.
    - Voeg de Simple OpenAI dependency toe onder de `<dependencies>` sectie.

    ```xml
    <dependency>
        <groupId>io.github.sashirestela</groupId>
        <artifactId>simple-openai</artifactId>
        <version>3.3.0</version>
    </dependency>
    ```

3. **Project Structuur Controleren:**
    - Zorg ervoor dat je projectstructuur er als volgt uitziet:
        ```
        openai-demo
        ├── src
        │   ├── main
        │   │   ├── java
        │   │   └── resources
        │   └── test
        │       ├── java
        │       └── resources
        └── pom.xml
        ```
4. **API Sleutel Configureren:**

- Voeg een bestand toe aan src/main/resources genaamd ai.config.properties.
- Voeg je OpenAI API-sleutel toe aan dit bestand
    - api.key=YOUR_API_KEY_HERE

<details>
<summary>Hints</summary>

1. **Project Aanmaken:**
    - In IntelliJ, kies "New Project" -> "Maven" -> Vul je groeps- en artefact-ID in.

2. **Dependency Toevoegen:**
    - Voeg de gegeven dependency toe aan je `pom.xml` onder de `<dependencies>` sectie.

</details>

<details>
<summary>Oplossing</summary>

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>openai-demo</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>io.github.sashirestela</groupId>
            <artifactId>simple-openai</artifactId>
            <version>3.3.0</version>
        </dependency>
    </dependencies>
</project>
```

```properties
# Ai.config.properties
api.key=YOUR_API_KEY_HERE
```

</details>

## Opdracht: maak een openai service

### Doel:

Het opzetten van een singleton service klasse voor het gebruik van de Simple OpenAI API in je project. Dit maakt het
mogelijk om de API eenvoudig te hergebruiken zonder elke keer een nieuwe instantie aan te maken.

### Stappenplan:

1. **Service Klasse Aanmaken:**
    - Maak een nieuwe mapstructuur aan onder `src/main/java` voor `codingWednesday.AI.Service`.
    - Maak een nieuwe Java-klasse aan genaamd `OpenAiService.java`.

2. **Singleton Pattern Implementeren:**
    - Zorg ervoor dat de klasse een singleton is, zodat er maar één instantie van `SimpleOpenAI` wordt aangemaakt en
      hergebruikt.

3. **API Sleutel Beveiliging:**
    - Haal de API-sleutel uit een configuratiebestand in plaats van deze hardcoded in de klasse te zetten. Dit verbetert
      de beveiliging en maakt het makkelijker om de sleutel te beheren.

**Hints**

<details>
<summary>Klik hier voor de hints</summary>


4. **Code Voorbeeld van de create service methode:**
   ```java
  
       private static void createService()
       {
           Properties prop = new Properties();
           try {
               prop.load(new FileInputStream("src/main/resources/ai.config.properties"));
           } catch (IOException e) {
               e.printStackTrace();
               throw new RuntimeException("API key file not found");
           }

           String apiKey = prop.getProperty("api.key");
           openAI = SimpleOpenAI.builder()
                   .apiKey(apiKey)
                   .build();
       }
  
   ```

</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```java
package codingWednesday.AI.Service;

import io.github.sashirestela.simpleopenai.SimpleOpenAI;

import java.io.FileInputStream;
import java.io.IOException;
import java.util.Properties;

public class OpenAiService {
    private static SimpleOpenAI openAI = null;

    public static SimpleOpenAI getService() {
        if (openAI == null) {
            createService();
        }
        return openAI;
    }

    private static void createService() {
        Properties prop = new Properties();
        try {
            prop.load(new FileInputStream("src/main/resources/config.properties"));
        } catch (IOException e) {
            e.printStackTrace();
            throw new RuntimeException("API key file not found");
        }

        String apiKey = prop.getProperty("api.key");
        openAI = SimpleOpenAI.builder()
                .apiKey(apiKey)
                .build();
    }
}
```

</details>

## Opdracht: maak een chat app

### Doel:

Het opzetten van een eenvoudige applicatie die gebruikersinput vraagt en een reactie genereert met behulp van de OpenAI
API.

Eerst voeg je de `ScannerService` toe. Deze service zal een methode bevatten om gebruikersinput te vragen en een bericht 
te tonen tijdens het wachten. Vervolgens voeg je de `ChatCompletionApp` toe. Maak hiervoor een nieuwe klasse aan genaamd 
`ChatCompletionApp.java`.
Deze klasse zal de main-methode bevatten om de gebruikersinput te vragen en een chatverzoek naar de OpenAI API te sturen.  
Ten slotte gebruik je de eerder gemaakte `OpenAiService` klasse om verbinding te maken met de OpenAI API en het 
chatverzoek uit te voeren.

**Hints**

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Maak de ScannerService Klasse:**
    - Implementeer een methode die gebruikersinput vraagt en een wachtbericht toont. Gebruik de `Scanner` klasse voor
      het lezen van de gebruikersinput.

2. **Maak de ChatCompletionApp Klasse:**
    - Implementeer de main-methode die:
        - Gebruikersinput vraagt met behulp van `ScannerService`.
        - Een `ChatRequest` object aanmaakt met de juiste parameters zoals model, berichten, temperatuur en maximale
          tokens.
        - Het chatverzoek verstuurt en de respons verwerkt om de AI-reactie weer te geven.

3. **Controleer de OpenAiService Klasse:**
    - Zorg ervoor dat de `OpenAiService` klasse correct geïmplementeerd is en gebruik deze om het chatverzoek te
      versturen.

4. **ChatRequest Object:**
    - Zorg ervoor dat je een `ChatRequest` object correct aanmaakt met de benodigde parameters zoals model, berichten,
      temperatuur, en maximale tokens.

5. **Voer het Verzoek uit:**
    - Gebruik de `OpenAiService` om het chatverzoek uit te voeren en de respons te verwerken.

</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```java
// ScannerService.java

import java.util.Scanner;

public class ScannerService {
    public static String askInput(String question, String waitingMessage) {
        Scanner scanner = new Scanner(System.in);
        System.out.println(question);
        String input = scanner.nextLine();
        System.out.println(waitingMessage);
        return input;
    }
}
```

```java
// ChatCompletionApp.java

import io.github.sashirestela.simpleopenai.models.ChatRequest;
import io.github.sashirestela.simpleopenai.models.ChatMessage;

public class ChatCompletionApp {
    public static void main(String[] args) {
        var input = ScannerService.askInput("Welke tekst wil je vragen aan de AI expert?", "We gaan aan de slag, even geduld");

        var chatRequest = ChatRequest.builder()
                .model("gpt-4")
                .message(ChatMessage.SystemMessage.of("You are an expert in AI."))
                .message(ChatMessage.UserMessage.of(input))
                .temperature(0.0)
                .maxTokens(300)
                .build();
        var futureChat = OpenAiService.getService().chatCompletions().create(chatRequest);
        var chatResponse = futureChat.join();
        System.out.println(chatResponse.firstContent());
    }
}
```
</details>

## Opdracht: maak een chat with streaming

### Doel:

Het opzetten van een applicatie die gebruikersinput vraagt en de reacties streamt met behulp van de OpenAI API.

Eerst voeg je de `ChatCompletionStreamingApp` toe. Maak hiervoor een nieuwe klasse aan genaamd `ChatCompletionStreamingApp.java`. Deze klasse zal de main-methode bevatten om de gebruikersinput te vragen en een streaming chatverzoek naar de OpenAI API te sturen. Ten slotte gebruik je de eerder gemaakte `OpenAiService` klasse om verbinding te maken met de OpenAI API en het streaming chatverzoek uit te voeren.

**Hints**

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Maak de ChatCompletionStreamingApp Klasse:**
   - Implementeer de main-methode die:
      - Gebruikersinput vraagt met behulp van `ScannerService`.
      - Een `ChatRequest` object aanmaakt met de juiste parameters zoals model, berichten, temperatuur en maximale tokens.
      - Het chatverzoek verstuurt en de respons verwerkt om de AI-reactie in realtime weer te geven.

2. **Controleer de OpenAiService Klasse:**
   - Zorg ervoor dat de `OpenAiService` klasse correct geïmplementeerd is en gebruik deze om het streaming chatverzoek te versturen.

3. **ChatRequest Object:**
   - Zorg ervoor dat je een `ChatRequest` object correct aanmaakt met de benodigde parameters zoals model, berichten, temperatuur, en maximale tokens.

4. **Stream het Verzoek:**
   - Gebruik de `OpenAiService` om het streaming chatverzoek uit te voeren en de respons in realtime te verwerken.

</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```java
// ChatCompletionStreamingApp.java

import io.github.sashirestela.simpleopenai.models.ChatRequest;
import io.github.sashirestela.simpleopenai.models.ChatMessage;
import io.github.sashirestela.simpleopenai.models.Chat;

public class ChatCompletionStreamingApp {
    public static void main(String[] args) {
        var input = ScannerService.askInput("Welke tekst wil je vragen aan de AI expert?", "We gaan aan de slag, even geduld");

        var chatRequest = ChatRequest.builder()
                .model("gpt-4")
                .message(ChatMessage.SystemMessage.of("You are an expert in AI."))
                .message(ChatMessage.UserMessage.of(input))
                .temperature(0.0)
                .maxTokens(300)
                .build();
        var futureChat = OpenAiService.getService().chatCompletions().createStream(chatRequest);
        var chatResponse = futureChat.join();
        chatResponse.filter(chatResp -> chatResp.getChoices().size() > 0 && chatResp.firstContent() != null)
                .map(Chat::firstContent)
                .forEach(System.out::print);
        System.out.println();
    }
}
```
</details>

## Bonus opdracht: maak een tekst naar audio app

### Doel:

Het opzetten van een applicatie die gebruikersinput vraagt en deze tekst omzet in een audiobestand met behulp van de OpenAI API.

In deze opdracht maak je een nieuwe klasse genaamd `TextToAudioApp`. Deze klasse zal de main-methode bevatten om de gebruikersinput te vragen, een spraakverzoek naar de OpenAI API te sturen en het resulterende audiobestand op te slaan.

**Hints**

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Maak de TextToAudioApp Klasse:**
   - Implementeer de main-methode die:
      - Gebruikersinput vraagt met behulp van `ScannerService`.
      - Een `SpeechRequest` object aanmaakt met de juiste parameters zoals model, input, stem, responsformaat en snelheid.
      - Het spraakverzoek verstuurt en de respons verwerkt om het audiobestand op te slaan.

2. **Controleer de OpenAiService Klasse:**
   - Zorg ervoor dat de `OpenAiService` klasse correct geïmplementeerd is en gebruik deze om het spraakverzoek te versturen.

3. **SpeechRequest Object:**
   - Zorg ervoor dat je een `SpeechRequest` object correct aanmaakt met de benodigde parameters zoals model, input, stem, responsformaat en snelheid.

4. **Sla het Audiobestand op:**
   - Gebruik de `OpenAiService` om het spraakverzoek uit te voeren en de respons op te slaan als een MP3-bestand.

</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```java
// TextToAudioApp.java

import io.github.sashirestela.simpleopenai.models.SpeechRequest;
import java.io.FileOutputStream;

public class TextToAudioApp {
    public static void main(String[] args) {
        var input = ScannerService.askInput("Welke tekst wil je omzetten?", "We gaan aan de slag, even geduld");

        var speechRequest = SpeechRequest.builder()
                .model("tts-1")
                .input(input)
                .voice(SpeechRequest.Voice.ALLOY)
                .responseFormat(SpeechRequest.SpeechResponseFormat.MP3)
                .speed(1.0)
                .build();
        var futureSpeech = OpenAiService.getService().audios().speak(speechRequest);
        var speechResponse = futureSpeech.join();
        try {
            var audioFile = new FileOutputStream("myAudioOutput.mp3");
            audioFile.write(speechResponse.readAllBytes());
            System.out.println(audioFile.getChannel().size() + " bytes");
            audioFile.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
</details>

## Bonus opdracht: maak een audio to tekst app

### Doel:

Het opzetten van een applicatie die een audiobestand omzet naar tekst met behulp van de OpenAI API.

In deze opdracht maak je een nieuwe klasse genaamd `AudioToTextApp`. Deze klasse zal de main-methode bevatten om het pad naar een audiobestand van de gebruiker te vragen, een transcriptieverzoek naar de OpenAI API te sturen en de getranscribeerde tekst weer te geven.

**Hints**

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Maak de AudioToTextApp Klasse:**
   - Implementeer de main-methode die:
      - Het bestandspad vraagt met behulp van `ScannerService`.
      - Een `TranscriptionRequest` object aanmaakt met de juiste parameters zoals model, bestand, prompt, responsformaat, temperatuur, timestamp-granulariteit, en taal.
      - Het transcriptieverzoek verstuurt en de respons verwerkt om de getranscribeerde tekst weer te geven.

2. **Controleer de OpenAiService Klasse:**
   - Zorg ervoor dat de `OpenAiService` klasse correct geïmplementeerd is en gebruik deze om het transcriptieverzoek te versturen.

3. **TranscriptionRequest Object:**
   - Zorg ervoor dat je een `TranscriptionRequest` object correct aanmaakt met de benodigde parameters zoals model, bestand, prompt, responsformaat, temperatuur, timestamp-granulariteit en taal.

4. **Voer het Verzoek uit:**
   - Gebruik de `OpenAiService` om het transcriptieverzoek uit te voeren en de getranscribeerde tekst weer te geven.

</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```java
// AudioToTextApp.java

import io.github.sashirestela.simpleopenai.models.TranscriptionRequest;
import io.github.sashirestela.simpleopenai.models.AudioResponseFormat;
import java.nio.file.Paths;

public class AudioToTextApp {
    public static void main(String[] args) {
        var filePath = ScannerService.askInput("Wat is het pad naar je bestand met het geluidsfragment?", "We gaan aan de slag");

        var audioRequest = TranscriptionRequest.builder()
                .file(Paths.get(filePath))
                .model("whisper-1")
                .prompt("geef me de tekst")
                .responseFormat(AudioResponseFormat.VERBOSE_JSON)
                .temperature(0.0)
                .timestampGranularity(TranscriptionRequest.TimestampGranularity.WORD)
                .timestampGranularity(TranscriptionRequest.TimestampGranularity.SEGMENT)
                .language("nl")
                .build();
        var audioResponse = OpenAiService.getService().audios().transcribe(audioRequest).join();
        System.out.println(audioResponse.getText());
    }
}
```
</details>

## Bonus opdracht: maak een tekst naar plaatje app

### Doel:

Het opzetten van een applicatie die gebruikersinput vraagt en deze tekst omzet in afbeeldingen met behulp van de OpenAI API.

In deze opdracht maak je een nieuwe klasse genaamd `TextToImageApp`. Deze klasse zal de main-methode bevatten om de gebruikersinput te vragen, een afbeeldingsverzoek naar de OpenAI API te sturen en de resulterende afbeeldings-URL's weer te geven.

**Hints**

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Maak de TextToImageApp Klasse:**
   - Implementeer de main-methode die:
      - Gebruikersinput vraagt met behulp van `ScannerService`.
      - Een `ImageRequest` object aanmaakt met de juiste parameters zoals prompt, aantal afbeeldingen, grootte, responsformaat en model.
      - Het afbeeldingsverzoek verstuurt en de respons verwerkt om de URL's van de gegenereerde afbeeldingen weer te geven.

2. **Controleer de OpenAiService Klasse:**
   - Zorg ervoor dat de `OpenAiService` klasse correct geïmplementeerd is en gebruik deze om het afbeeldingsverzoek te versturen.

3. **ImageRequest Object:**
   - Zorg ervoor dat je een `ImageRequest` object correct aanmaakt met de benodigde parameters zoals prompt, aantal afbeeldingen, grootte, responsformaat en model.

4. **Voer het Verzoek uit:**
   - Gebruik de `OpenAiService` om het afbeeldingsverzoek uit te voeren en de URL's van de gegenereerde afbeeldingen weer te geven.

</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```java
// TextToImageApp.java

import io.github.sashirestela.simpleopenai.models.ImageRequest;
import io.github.sashirestela.simpleopenai.models.ImageResponseFormat;
import io.github.sashirestela.simpleopenai.models.Size;

public class TextToImageApp {
    public static void main(String[] args) {
        var input = ScannerService.askInput("Welke tekst wil je omzetten naar een plaatje?", "We gaan aan de slag, even geduld");

        var imageRequest = ImageRequest.builder()
                .prompt(input)
                .n(2)
                .size(Size.X256)
                .responseFormat(ImageResponseFormat.URL)
                .model("dall-e-2")
                .build();

        var futureImage = OpenAiService.getService().images().create(imageRequest);
        var imageResponse = futureImage.join();
        imageResponse.stream().forEach(img -> System.out.println("\n" + img.getUrl()));
    }
}
```
</details>

## Bonus opdracht: maak een plaatje naar tekst app

### Doel:

Het opzetten van een applicatie die gebruikersinput vraagt, een afbeeldingsbestand inlaadt, en deze informatie naar de OpenAI API stuurt om een antwoord te genereren op basis van de afbeelding en de tekst.

In deze opdracht maak je een nieuwe klasse genaamd `ImageToTextApp`. Deze klasse zal de main-methode bevatten om het pad naar een afbeeldingsbestand van de gebruiker te vragen, aanvullende tekstinput te ontvangen, een chatverzoek naar de OpenAI API te sturen en de resulterende reactie weer te geven.

**Hints**

<details>
<summary>Klik hier voor een stappenplan</summary>

1. **Maak de ImageToTextApp Klasse:**
   - Implementeer de main-methode die:
      - Het bestandspad van de afbeelding vraagt met behulp van `ScannerService`.
      - Aanvullende tekstinput vraagt met behulp van `ScannerService`.
      - Een `ChatRequest` object aanmaakt met de juiste parameters zoals model, berichten (inclusief tekst en afbeelding), temperatuur en maximale tokens.
      - Het chatverzoek verstuurt en de respons verwerkt om de AI-reactie weer te geven.

2. **Controleer de OpenAiService Klasse:**
   - Zorg ervoor dat de `OpenAiService` klasse correct geïmplementeerd is en gebruik deze om het chatverzoek te versturen.

3. **ChatRequest Object:**
   - Zorg ervoor dat je een `ChatRequest` object correct aanmaakt met de benodigde parameters zoals model, berichten (inclusief tekst en afbeelding), temperatuur en maximale tokens.

4. **Laad de Afbeelding als Base64:**
   - Gebruik een service om het afbeeldingsbestand als Base64-gecodeerde string in te laden.

5. **Voer het Verzoek uit:**
   - Gebruik de `OpenAiService` om het chatverzoek uit te voeren en de resulterende reactie weer te geven.

</details>

**Oplossing:**

<details>
<summary>Klik hier</summary>

```java
// ImageToTextApp.java

import io.github.sashirestela.simpleopenai.models.ChatRequest;
import io.github.sashirestela.simpleopenai.models.ChatMessage;
import io.github.sashirestela.simpleopenai.models.ContentPart;

import java.util.List;

public class ImageToTextApp {
    public static void main(String[] args) {
        var filePath = ScannerService.askInput("Wat is het pad naar je bestand met het plaatje?", "");
        var input = ScannerService.askInput("Welke tekst wil je vragen aan de AI expert?", "We gaan aan de slag");

        var chatRequest = ChatRequest.builder()
                .model("gpt-4")
                .messages(List.of(
                        ChatMessage.UserMessage.of(List.of(
                                ContentPart.ContentPartText.of(input),
                                ContentPart.ContentPartImageUrl.of(FileService.loadFileAsBase64(filePath))))))
                .temperature(0.0)
                .maxTokens(500)
                .build();

        var chatResponse = OpenAiService.getService().chatCompletions().createStream(chatRequest).join();
        chatResponse.filter(chatResp -> chatResp.getChoices().size() > 0 && chatResp.firstContent() != null)
                .map(Chat::firstContent)
                .forEach(System.out::print);
        System.out.println();
    }
}
```
**FileService.java**


```java

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.Base64;

public class FileService {
    public static String loadFileAsBase64(String filePath) {
        try {
            byte[] fileContent = Files.readAllBytes(Paths.get(filePath));
            return Base64.getEncoder().encodeToString(fileContent);
        } catch (IOException e) {
            e.printStackTrace();
            throw new RuntimeException("Failed to load file");
        }
    }
}
```

</details>

## Toelichting op de requests

### Chatrequest

**Instellingen:**

1. **Model:**
   - De naam van het AI-model dat je wilt gebruiken. Voorbeelden zijn "gpt-4" en "gpt-3.5".
   - **Invloed:** Het model bepaalt de kwaliteit en het type respons. Nieuwere modellen zoals "gpt-4" zijn vaak beter in het begrijpen en genereren van tekst.

2. **Messages:**
   - Een lijst van berichten die de context en input vormen voor het model. Berichten kunnen systeem-, gebruiker-, of assistent-berichten zijn.
   - **Invloed:** De inhoud van deze berichten bepaalt hoe het model de vraag begrijpt en antwoordt. Een duidelijke context en vraag kunnen de kwaliteit van het antwoord verbeteren.

3. **Temperature:**
   - Een waarde tussen 0 en 1 die bepaalt hoe creatief of conservatief de output moet zijn.
   - **Invloed:** Een lagere waarde (zoals 0.0) zorgt voor meer voorspelbare en consistente antwoorden, terwijl een hogere waarde (zoals 0.7) zorgt voor meer variatie en creativiteit in de antwoorden.

4. **MaxTokens:**
   - Het maximum aantal tokens (woorden en leestekens) in de gegenereerde respons.
   - **Invloed:** Beperkt de lengte van de gegenereerde tekst. Een hogere waarde kan resulteren in langere en meer gedetailleerde antwoorden.

### Imagerequest

**Instellingen:**

1. **Prompt:**
   - De tekstuele beschrijving van wat de afbeelding moet voorstellen.
   - **Invloed:** De nauwkeurigheid en relevantie van de gegenereerde afbeelding hangen sterk af van de duidelijkheid en specificiteit van de prompt.

2. **n:**
   - Het aantal afbeeldingen dat gegenereerd moet worden.
   - **Invloed:** Bepaalt hoeveel verschillende afbeeldingen je als resultaat krijgt. Meerdere afbeeldingen kunnen helpen bij het kiezen van de beste interpretatie van de prompt.

3. **Size:**
   - De grootte van de gegenereerde afbeelding (bijvoorbeeld "256x256").
   - **Invloed:** De resolutie van de gegenereerde afbeelding. Grotere afbeeldingen zijn gedetailleerder maar kunnen langer duren om te genereren.

4. **ResponseFormat:**
   - Het formaat van de gegenereerde afbeelding, zoals URL of base64.
   - **Invloed:** Bepaalt hoe de afbeelding wordt geretourneerd. Een URL is handig voor weergave op het web, terwijl base64 nuttig is voor directe integratie in andere toepassingen.

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
   - **Invloed:** Een lagere snelheid kan de verstaanbaarheid verbeteren, terwijl een hogere snelheid nuttig kan zijn voor snelle informatieoverdracht.

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
   - **Invloed:** Een lagere waarde zorgt voor een meer voorspelbare en consistente transcriptie, terwijl een hogere waarde meer variatie kan introduceren.

6. **TimestampGranularity:**
   - De nauwkeurigheid van de tijdstempels in de transcriptie, zoals WORD of SEGMENT.
   - **Invloed:** Bepaalt hoe gedetailleerd de tijdstempels in de transcriptie zijn. Fijnere granulariteit (zoals WORD) biedt nauwkeurigere tijdsinformatie.

7. **Language:**
   - De taal van het audiobestand.
   - **Invloed:** De taalinstelling helpt het model om de audio correct te interpreteren en nauwkeurige transcripties te produceren.

### Samenvatting

De instellingen van elk verzoek naar de OpenAI API zijn belangrijk voor de kwaliteit en relevantie van de resulterende uitkomsten. Door de juiste parameters te kiezen, kun je de AI-modellen optimaal benutten voor verschillende toepassingen, zoals tekstgeneratie, afbeeldingscreatie, spraaksynthese en transcriptie. Experimenteer met deze instellingen om te zien hoe ze de resultaten beïnvloeden en pas ze aan op basis van je specifieke behoeften en context.
