# C#

Je kunt een Galgje-spel maken in C# met behulp van .NET Core (of .NET 5/6/7). Hier is een voorbeeld van een Galgje-spel
in C#:

**Stap 1:** Maak een nieuw consoleproject

```bash
dotnet new console -n GalgjeSpel
cd GalgjeSpel
```

**Stap 2:** Vervang de inhoud van `Program.cs` door de volgende code:

```csharp
using System;
using System.Collections.Generic;

namespace GalgjeSpel
{
    class Program
    {
        // Een lijst met mogelijke woorden
        static readonly string[] WOORDEN = {
            "programmeren", "csharp", "computer", "spel", "internet",
            "galgje", "software", "hardware", "database", "netwerk"
        };

        // Functie om een willekeurig woord te kiezen
        static string KiesWillekeurigWoord()
        {
            Random random = new Random();
            int index = random.Next(WOORDEN.Length);
            return WOORDEN[index];
        }

        // Functie om te controleren of het woord volledig is geraden
        static bool IsGeraden(string woord, bool[] geradenLetters)
        {
            foreach (bool geraden in geradenLetters)
            {
                if (!geraden)
                    return false;
            }
            return true;
        }

        // Functie om de huidige stand van het woord te printen
        static void PrintGalgjeStatus(string woord, bool[] geradenLetters)
        {
            for (int i = 0; i < woord.Length; i++)
            {
                if (geradenLetters[i])
                    Console.Write(woord[i] + " ");
                else
                    Console.Write("_ ");
            }
            Console.WriteLine();
        }

        static void Main(string[] args)
        {
            // Kies een willekeurig woord en initialiseer de variabelen
            string woord = KiesWillekeurigWoord();
            bool[] geradenLetters = new bool[woord.Length];
            int pogingen = 6;
            List<char> fouteLetters = new List<char>();

            Console.WriteLine("Welkom bij het spel Galgje!");

            // Loop totdat het woord volledig is geraden of de pogingen op zijn
            while (pogingen > 0 && !IsGeraden(woord, geradenLetters))
            {
                Console.WriteLine($"\nResterende pogingen: {pogingen}");
                Console.Write("Foute letters: ");
                foreach (char letter in fouteLetters)
                    Console.Write(letter + " ");
                Console.WriteLine();
                PrintGalgjeStatus(woord, geradenLetters);

                Console.Write("Gok een letter: ");
                char gok;
                try
                {
                    gok = char.ToLower(Console.ReadLine()[0]);
                }
                catch (Exception)
                {
                    Console.WriteLine("Voer slechts één letter in.");
                    continue;
                }

                if (!char.IsLetter(gok))
                {
                    Console.WriteLine("Voer slechts één letter in.");
                    continue;
                }

                bool juistGeraden = false;
                for (int i = 0; i < woord.Length; i++)
                {
                    if (woord[i] == gok && !geradenLetters[i])
                    {
                        geradenLetters[i] = true;
                        juistGeraden = true;
                    }
                }

                if (juistGeraden)
                {
                    Console.WriteLine("Juist! De huidige stand:");
                }
                else
                {
                    if (!fouteLetters.Contains(gok))
                    {
                        fouteLetters.Add(gok);
                        pogingen--;
                    }
                    Console.WriteLine("Fout! Probeer opnieuw.");
                }
            }

            // Controleer of de speler heeft gewonnen of verloren
            if (IsGeraden(woord, geradenLetters))
            {
                Console.WriteLine($"Gefeliciteerd! Je hebt het woord geraden: {woord}");
            }
            else
            {
                Console.WriteLine($"Helaas, je hebt verloren. Het woord was: {woord}");
            }
        }
    }
}
```

**Stap 3:** Build en voer het programma uit

```bash
dotnet run
```

## Toelichting

- **WOORDEN**: Een array met een aantal woorden waaruit een willekeurig woord wordt gekozen.
- **KiesWillekeurigWoord**: Methode om willekeurig een woord te kiezen.
- **IsGeraden**: Methode om te controleren of het hele woord is geraden.
- **PrintGalgjeStatus**: Methode om de huidige status van het woord weer te geven.
- **Main**: De hoofdmethod die het spel logic implementeert.
