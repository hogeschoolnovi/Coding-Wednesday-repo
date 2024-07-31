# Opdracht 1: SOS

Nu we de test led van pin 13 kunnen laten knipperen, kunnen we dat ook in een ritme. Pas je "hello world" code zo aan, dat het S-O-S knippert in morse. Dit kunt je bereiken door met de `digitWrite` en de `delay` te spelen.

SOS in morse is: `...---...`, dus `kort-kort-kort lang-lang-lang kort-kort-kort`

<details>
<summary>Tip</summary>
Maak een "dot" methode en een "dash" methode en definieer constanten voor de tijden. Hoelang de LED aan moet zijn of uit moet zijn en ook hoelang de LED moet wachten tussen signalen, tussen letters of tussen loop iteraties.
</details>

<details>
<summary>Tip: start code</summary>

```
// Definieer constanten om te bepalen hoe lang alles duurt
const int dotDuration = ...     // Duur van een punt in milliseconden
const int dashDuration = ...    // Duur van een streepje (3x een punt)
const int shortGap = ...        // Korte pauze tussen signalen (duur van een punt)
const int mediumGap = ...       // Middellange pauze tussen letters (duur van drie punten)
const int longGap = ...         // Lange pauze tussen woorden (duur van zeven punten)

void setup(){
// Zet de pin modus op OUTPUT
}

void loop(){
// code om S, O en nog eens S te knipperen met de LED (en dan een korte pauze voor je de volgende loop start)
}

void blinkDot() {
  digitalWrite(TEST, HIGH); // Zet LED aan
  delay(dotDuration);         // Wacht de duur van een punt
  digitalWrite(TEST, LOW);  // Zet LED uit
  delay(shortGap);            // Korte pauze tussen signalen
}

void blinkDash() {
  digitalWrite(TEST, HIGH); // Zet LED aan
  delay(dashDuration);        // Wacht de duur van een streepje
  digitalWrite(TEST, LOW);  // Zet LED uit
  delay(shortGap);            // Korte pauze tussen signalen
}

```
</details>


## Uitwerking

<details>
<summary>Klik hier om de uitwerking te bekijken</summary>

```
const int ledPin = 13; // Pin waar de LED op is aangesloten

// Tijdinstellingen
const int dotDuration = 250; // Duur van een punt in milliseconden
const int dashDuration = dotDuration * 3; // Duur van een streepje (3x een punt)
const int shortGap = dotDuration; // Korte pauze tussen signalen (duur van een punt)
const int mediumGap = dotDuration * 3; // Middellange pauze tussen letters (duur van drie punten)
const int longGap = dotDuration * 7; // Lange pauze tussen woorden (duur van zeven punten)

void setup() {
  pinMode(ledPin, OUTPUT); // Stel de LED-pin in als output
}

void loop() {
  // Code voor 'S' (3 x een punt)
  blinkDot();
  blinkDot();
  blinkDot();
  
  // Korte pauze tussen letters
  delay(mediumGap);

  // Code voor 'O' (3 x een streepje)
  blinkDash();
  blinkDash();
  blinkDash();
  
  delay(mediumGap);

  // Code voor 'S' (3 x een punt)
  blinkDot();
  blinkDot();
  blinkDot();
  
  // Lange pauze voor dat de loop zich herhaalt en opnieuw SOS gaat zenden
  delay(longGap);
}

void blinkDot() {
  digitalWrite(ledPin, HIGH); // Zet LED aan
  delay(dotDuration);         // Wacht de duur van een punt
  digitalWrite(ledPin, LOW);  // Zet LED uit
  delay(shortGap);            // Korte pauze tussen signalen
}

void blinkDash() {
  digitalWrite(ledPin, HIGH); // LED aan
  delay(dashDuration);        // Wacht de duur van een streepje
  digitalWrite(ledPin, LOW);  // LED uit
  delay(shortGap);            // Korte pauze tussen signalen
}


```

</details>