## Java - workshop overzicht 

1. **Inleidende Theorie (10 minuten)**
    - **Wat is Refactoring?**
        - Refactoring is het proces van het wijzigen van de interne structuur van software zonder het externe gedrag te
          veranderen.
    - **Waarom Refactoren?**
        - Verbeter de leesbaarheid, onderhoudbaarheid en prestaties van code.

   **Bronnen voor verdere verdieping:**
    - [Refactoring in IntelliJ IDEA](https://www.jetbrains.com/help/idea/refactoring-source-code.html)
    - [SOLID Principes](https://en.wikipedia.org/wiki/SOLID)
    - [Clean Code Boek door Robert C. Martin](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

2. **Oefening 1: Method Extracting (40 minuten)**
    - **Code Voorbeeld:**
   ```java
   public class InvoicePrinter {
       public void printInvoice(String customerName, double amount) {
           System.out.println("Invoice");
           System.out.println("---------");
           System.out.println("Customer: " + customerName);
           System.out.println("Amount: " + amount);
           System.out.println("---------");
           System.out.println("Thank you for your business!");
       }
   }
   ```
    - **Uitdaging:**
        - Refactor de `printInvoice` methode door verschillende print-operaties naar afzonderlijke methoden te
          verplaatsen.
        - Gebruik *Extract Method* (*Ctrl + Alt + M* of *Cmd + Option + M* op macOS) in IntelliJ IDEA.
        - Zorg dat er minimaal aantal duplicate code is.
        - Zorg dat je makkelijk de System.out.println kan vervangen door een andere print mogelijkheid.
            - tip: er mag maar 1 keer System.out.println in de code staan
          
**Oplossing:**
   
<details>
<summary>Klik hier</summary>

```java
   public class InvoicePrinter {
      public void printInvoice(String customerName, double amount) {
          printHeader();
          printCustomerDetails(customerName, amount);
          printFooter();
      }

      private void printHeader() {
          print("Invoice");
          printHorizontalLine();
      }

      private void printHorizontalLine()
      {
          print("----------------------");
      }

      private void printCustomerDetails(String customerName, double amount) {
          print("Customer: " + customerName);
          print("Amount: " + amount);
          printHorizontalLine();
      }

      private void printFooter() {
          print("Thank you for your business!");
      }

      private void print(String text){
          System.out.println(text);
      }
  }
```

</details>


3. **Code Smells (10 minuten)**
    - **Wat zijn Code Smells?**
        - "Indicatoren" van slecht ontworpen code.

   **Bronnen voor verdere verdieping:**
    - [Code Smells](https://refactoring.guru/refactoring/smells)

De methoden getTotalOrderValue() en hasLatePayments() zijn mogelijk een voorbeeld van de 'Feature Envy' smell. Beide
methoden zijn sterk afhankelijk van de interne details van de Order klasse. Ze gebruiken voornamelijk data van de Order
objecten (zoals het ophalen van waarden en de status van de betalingen), wat suggereert dat deze functionaliteit
misschien beter in de Order klasse of een klasse die Order collecties beheert, geplaatst kan worden.

4. **Oefening 2: Extract Class en Move Method (40 minuten)**
    - **Code Voorbeeld:**
   ```java
   public class Customer {
       private String name;
       private String address;
       private String phoneNumber;
       private List<Order> orders;

       public double getTotalOrderValue() {
           double total = 0;
           for (Order order : orders) {
               total += order.getValue();
           }
           return total;
       }

       public boolean hasLatePayments() {
           for (Order order : orders) {
               if (order.isLate()) {
                   return true;
               }
           }
           return false;
       }

       // Getters en Setters
   }
   ```

    - **Uitdaging:**
        1. Verplaats de logica van `getTotalOrderValue` en `hasLatePayments` naar een nieuwe klasse `OrderHistory`.
        2. Gebruik *Extract Class* en *Move Method* in IntelliJ IDEA. Ctrl+Alt+Shift+T (Windows/Linux) of Ctrl+T (Mac)
        3. Refactor de `Customer` klasse om samen te werken met `OrderHistory`.


**Oplossing:**

<details>
<summary>Klik hier</summary>

   ```java
   public class Customer {
       private String name;
       private String address;
       private String phoneNumber;
       private OrderHistory orderHistory;

       public double getTotalOrderValue() {
           return orderHistory.getTotalOrderValue();
       }

       public boolean hasLatePayments() {
           return orderHistory.hasLatePayments();
       }

       // Getters en Setters
   }

   public class OrderHistory {
       private List<Order> orders;

       public double getTotalOrderValue() {
           double total = 0;
           for (Order order : orders) {
               total += order.getValue();
           }
           return total;
       }

       public boolean hasLatePayments() {
           for (Order order : orders) {
               if (order.isLate()) {
                   return true;
               }
           }
           return false;
       }
   }
   ```

</details>

5. **Break (10 minuten)**

6. **Oefening 3: Remove Indentations (30 minuten)**
    - **Code Voorbeeld:**
   ```java
   public static void main(String[] args) {
        var config = new Config("user", "mySecret" , "http://localhost:8080");
        var validationResult = new ConfigurationValidator().validateConfiguration(config);
        System.out.println("Config validation resulted in:" + validationResult);
    }

    public class ConfigurationValidator {
        public boolean validateConfiguration(Config config) {
            if (config != null) {
                if (config.getUsername() != null) {
                    if (!config.getUsername().isEmpty()) {
                        if (config.getPassword() != null) {
                            if (!config.getPassword().isEmpty()) {
                                if (config.getUrl() != null) {
                                    if (!config.getUrl().isEmpty()) {
                                        if (config.getUrl().startsWith("http")) {
                                            // Valid configuration
                                            return true;
                                        } else {
                                            System.out.println("Invalid URL: must start with http");
                                            return false;
                                        }
                                    } else {
                                        System.out.println("URL cannot be empty");
                                        return false;
                                    }
                                } else {
                                    System.out.println("URL cannot be null");
                                    return false;
                                }
                            } else {
                                System.out.println("Password cannot be empty");
                                return false;
                            }
                        } else {
                            System.out.println("Password cannot be null");
                            return false;
                        }
                    } else {
                        System.out.println("Username cannot be empty");
                        return false;
                    }
                } else {
                    System.out.println("Username cannot be null");
                    return false;
                }
            } else {
                System.out.println("Config object cannot be null");
                return false;
            }
        }
    }


    public class Config {
        private String username;
        private String password;
        private String url;

        public Config(String username, String password, String url) {
            this.username = username;
            this.password = password;
            this.url = url;
        }

        public String getUsername() {
            return username;
        }

        public String getPassword() {
            return password;
        }

        public String getUrl() {
            return url;
        }
    }

   ```
    - **Uitdaging:**
        1. maak unit testen indien ze nog niet bestaan.
        2. gebruik early return, zodra je weet dat het niet goed is return het resultaat.
        3. Gebruik *Extract methods* om de if conditie in een methode te zetten. Ctrl+Alt+Shift+T (Windows/Linux) of
           Ctrl+T (Mac)


**Oplossing:**

<details>
<summary>Klik hier</summary>


```java
 
   public class ConfigurationValidator {
        public boolean validateConfiguration(Config config) {
            if (!isValidNotNull(config)) {
                System.out.println("Config object cannot be null");
                return false;
            }
            if (!isValidUsername(config.getUsername())) {
                System.out.println("Username cannot be null or empty");
                return false;
            }
            if (!isValidPassword(config.getPassword())) {
                System.out.println("Password cannot be null or empty");
                return false;
            }
            if (!isValidUrl(config.getUrl())) {
                System.out.println("URL cannot be null or empty");
                return false;
            }
            if (!isValidUrlProtocol(config.getUrl())) {
                System.out.println("Invalid URL: must start with http");
                return false;
            }
            // All checks passed, configuration is valid
            return true;
        }

        private boolean isValidNotNull(Object obj) {
            return obj != null;
        }

        private boolean isValidUsername(String username) {
            return username != null && !username.isEmpty();
        }

        private boolean isValidPassword(String password) {
            return password != null && !password.isEmpty();
        }

        private boolean isValidUrl(String url) {
            return url != null && !url.isEmpty();
        }

        private boolean isValidUrlProtocol(String url) {
            return url.startsWith("http");
        }
    }
   
   
```
</details>

7. **Theorie: Refactoring Tools in IntelliJ IDEA (10 minuten)**
    - **Overzicht van Refactoring Tools:**
        - *Extract Method / Class / Interface*
        - *Inline Method / Variable*
        - *Rename*
        - *Move Method / Class*
        - *Change Signature*

   **Bronnen voor verdere verdieping:**
    - [Refactoring Tools in IntelliJ IDEA](https://www.jetbrains.com/help/idea/refactoring-source-code.html)

8. **Eindopdracht (40 minuten): Verbeter een Project met Refactoring Tools**
    - **Doel:** Verbeter een bestaande codebase met behulp van refactoring tools in IntelliJ IDEA.
    - **Code Voorbeeld:**
   ```java
   public class Library {
       private List<Book> books;

       public Library(List<Book> books) {
           this.books = books;
       }

       public List<Book> getBooksByAuthor(String author) {
           List<Book> result = new ArrayList<>();
           for (Book book : books) {
               if (book.getAuthor().equals(author)) {
                   result.add(book);
               }
           }
           return result;
       }

       public List<Book> getBooksPublishedAfter(int year) {
           List<Book> result = new ArrayList<>();
           for (Book book : books) {
               if (book.getPublicationYear() > year) {
                   result.add(book);
               }
           }
           return result;
       }
   }

   public class Book {
       private String title;
       private String author;
       private int publicationYear;

       // Constructor, Getters en Setters
   }
   ```
    - **Uitdaging:**
        1. Maak een nieuwe klasse `BookFilter` die filtermethoden bevat.
        2. Verplaats de filtermethoden naar `BookFilter`.
        3. Pas de `Library` klasse aan om `BookFilter` te gebruiken.


**Oplossing:**

<details>
<summary>Klik hier</summary>


   ```java
   public class Library {
       private List<Book> books;
       private BookFilter bookFilter;

       public Library(List<Book> books) {
           this.books = books;
           this.bookFilter = new BookFilter();
       }

       public List<Book> getBooksByAuthor(String author) {
           return bookFilter.getBooksByAuthor(books, author);
       }

       public List<Book> getBooksPublishedAfter(int year) {
           return bookFilter.getBooksPublishedAfter(books, year);
       }
   }

   public class BookFilter {
       public List<Book> getBooksByAuthor(List<Book> books, String author) {
           List<Book> result = new ArrayList<>();
           for (Book book : books) {
               if (book.getAuthor().equals(author)) {
                   result.add(book);
               }
           }
           return result;
       }

       public List<Book> getBooksPublishedAfter(List<Book> books, int year) {
           List<Book> result = new ArrayList<>();
           for (Book book : books) {
               if (book.getPublicationYear() > year) {
                   result.add(book);
               }
           }
           return result;
       }
   }

   public class Book {
       private String title;
       private String author;
       private int publicationYear;

       // Constructor, Getters en Setters
   }
   ```
</details>

### Nuttige links en documentatie

- [Refactoring in IntelliJ IDEA](https://www.jetbrains.com/help/idea/refactoring-source-code.html)
- [SOLID Principes](https://en.wikipedia.org/wiki/SOLID)
- [Clean Code Boek door Robert C. Martin](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
- [Code Smells](https://refactoring.guru/refactoring/smells)

Veel succes met het implementeren en verbeteren van je code!