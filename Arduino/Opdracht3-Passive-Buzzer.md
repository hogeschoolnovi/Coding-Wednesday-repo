# Opdracht 3: Passive Buzzer

Voor deze opdracht heb je nodig: 

- 1x Arduino
- 1x Passive Buzzer
- 2x F-M draad

De buzzer heeft 2 pinnen. Bij elke pin staat aangegeven of het de + of de - pin is. 

Sluit de positieve pin aan op pin 8 van de Arduino en sluit de negatieve pin aan op gnd.

Vervolgens kun je onderstaande voorbeeld code inladen om je buzzer geluid te laten maken: 

```
const int buzzer = 8; // Pin where the buzzer is connected

// Frequencies for the notes
const int C = 261;
const int D = 294;
const int E = 329;
const int F = 349;
const int G = 392;
const int A = 440;
const int B = 493;
const int highC = 523;

// Length of the note
const int noteDuration = 500;

void setup() {
  pinMode(buzzer, OUTPUT);
}

void loop() {
  // Play the melody
  playTone(C, noteDuration);
  playTone(D, noteDuration);
  playTone(E, noteDuration);
  playTone(F, noteDuration);
  playTone(G, noteDuration);
  playTone(A, noteDuration);
  playTone(B, noteDuration);
  playTone(highC, noteDuration);

  delay(2000); // Wait 2 seconds before the melody starts again
}

void playTone(int frequency, int duration) {
  tone(buzzer, frequency, duration);
  delay(duration);
  noTone(buzzer);
}

```

De `tone(pin, frequentie, duur)` methode is een methode van de Arduino library. Met deze methode kun je een toon van een bepaalde frequentie laten klinken voor een bepaalde duur op een bepaalde pin.

De `noTone(pin)` methode stopt juist de toon die op een bepaalde pin wordt verstuurd.

## Je eigen lied

Schrijf nu je eigen lied met de 8 noten die je in de voorbeeldcode hebt gezien. Je kunt gebruik een van deze kinder liedjes gebruiken voor de xylofoon: 
![](images/XylofoonKinderLiedjes.jpg)

Of google eens naar "popular 8 note songs" of maak iets na wat je leuk lijkt, zoals de titelsongs van je favoriete film of serie. Ken je deze bijvoorbeeld nog: https://www.youtube.com/watch?v=1Sz7ww7aBJ0
