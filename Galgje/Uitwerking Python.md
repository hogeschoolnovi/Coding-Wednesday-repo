# Python

Hier is een implementatie van het Galgje-spel in Python. Dit voorbeeld gebruikt de `random` module om een willekeurig
woord te kiezen.

## Galgje spel in python

```python
import random

# Een lijst van mogelijke woorden
WOORDEN = [
    "programmeren", "python", "computer", "spel", "internet",
    "galgje", "software", "hardware", "database", "netwerk"
]

# Functie om een willekeurig woord te kiezen uit de lijst
def kies_willekeurig_woord():
    return random.choice(WOORDEN)

# Functie om te controleren of het woord volledig is geraden
def is_geraden(woord, geraden_letters):
    return all(geraden_letters)

# Functie om de huidige stand van het woord te printen
def print_galgje_status(woord, geraden_letters):
    display = ''.join([woord[i] if geraden_letters[i] else '_' for i in range(len(woord))])
    print(' '.join(display))

def main():
    # Kies een willekeurig woord en initialiseer de variabelen
    woord = kies_willekeurig_woord()
    geraden_letters = [False] * len(woord)
    pogingen = 6
    foute_letters = []

    print("Welkom bij het spel Galgje!")
    
    # Loop totdat het woord volledig is geraden of de pogingen op zijn
    while pogingen > 0 and not is_geraden(woord, geraden_letters):
        print(f"\nResterende pogingen: {pogingen}")
        print("Foute letters:", ' '.join(foute_letters))
        print_galgje_status(woord, geraden_letters)
        
        gok = input("Gok een letter: ").lower()
        if len(gok) != 1 or not gok.isalpha():
            print("Voer slechts één letter in.")
            continue
        
        if gok in woord:
            for index, letter in enumerate(woord):
                if letter == gok:
                    geraden_letters[index] = True
            print(f"Juist! De huidige stand:")
        else:
            if gok not in foute_letters:
                foute_letters.append(gok)
                pogingen -= 1
            print("Fout! Probeer opnieuw.")
        
    # Controleer of de speler heeft gewonnen of verloren
    if is_geraden(woord, geraden_letters):
        print(f"Gefeliciteerd! Je hebt het woord geraden: {woord}")
    else:
        print(f"Helaas, je hebt verloren. Het woord was: {woord}")

if __name__ == "__main__":
    main()
```

## Hoe te gebruiken

1. Maak een nieuw Python-bestand aan, bijvoorbeeld `galgje.py`.
2. Plak de bovenstaande code in dat bestand.
3. Voer het programma uit met het volgende commando:

```bash
python galgje.py
```

## Toelichting

- **WOORDEN**: Een lijst met woorden waaruit willekeurig wordt gekozen.
- **kies_willekeurig_woord**: Functie om willekeurig een woord te kiezen.
- **is_geraden**: Functie om te controleren of het hele woord is geraden.
- **print_galgje_status**: Functie om de huidige status van het woord weer te geven.
- **main**: Hoofdfunctie die het spel logica implementeert.

