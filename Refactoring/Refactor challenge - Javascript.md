## Workshop overzicht 

1. **Inleidende Theorie (10 minuten)**
    - **Wat is Refactoring?**
        - Refactoring is het proces van het wijzigen van de interne structuur van software zonder het externe gedrag te veranderen.
    - **Waarom Refactoren?**
        - Verbeter de leesbaarheid, onderhoudbaarheid en prestaties van code.

   **Bronnen voor verdere verdieping:**
    - [Refactoring in IntelliJ IDEA](https://www.jetbrains.com/help/idea/refactoring-source-code.html)
    - [SOLID Principes](https://en.wikipedia.org/wiki/SOLID)
    - [Clean Code Boek door Robert C. Martin](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

2. **Oefening 1: Method Extracting (40 minuten)**
    - **Code Voorbeeld:**
   ```javascript
   class InvoicePrinter {
       printInvoice(customerName, amount) {
           console.log("Invoice");
           console.log("---------");
           console.log("Customer: " + customerName);
           console.log("Amount: " + amount);
           console.log("---------");
           console.log("Thank you for your business!");
       }
   }
   ```
    - **Uitdaging:**
        1. Refactor de `printInvoice` methode door verschillende print-operaties naar afzonderlijke methoden te verplaatsen.
        2. Gebruik *Extract Method* in IntelliJ IDEA.


**Oplossing:**

<details>
<summary>Klik hier</summary>


   ```javascript
   class InvoicePrinter {
       printInvoice(customerName, amount) {
           this.printHeader();
           this.printCustomerDetails(customerName, amount);
           this.printFooter();
       }

       printHeader() {
           console.log("Invoice");
           console.log("---------");
       }

       printCustomerDetails(customerName, amount) {
           console.log("Customer: " + customerName);
           console.log("Amount: " + amount);
           console.log("---------");
       }

       printFooter() {
           console.log("Thank you for your business!");
       }
   }
   ```
</details>

3. **Code Smells (10 minuten)**
    - **Wat zijn Code Smells?**
        - "Indicatoren" van slecht ontworpen code.

   **Bronnen voor verdere verdieping:**
    - [Code Smells](https://refactoring.guru/refactoring/smells)

4. **Oefening 2: Extract Class en Move Method (40 minuten)**
    - **Code Voorbeeld:**
   ```javascript
   class Customer {
       constructor(name, address, phoneNumber, orders) {
           this.name = name;
           this.address = address;
           this.phoneNumber = phoneNumber;
           this.orders = orders;
       }

       getTotalOrderValue() {
           let total = 0;
           for (let order of this.orders) {
               total += order.getValue();
           }
           return total;
       }

       hasLatePayments() {
           for (let order of this.orders) {
               if (order.isLate()) {
                   return true;
               }
           }
           return false;
       }
   }
   ```

    - **Uitdaging:**
        1. Verplaats de logica van `getTotalOrderValue` en `hasLatePayments` naar een nieuwe klasse `OrderHistory`.
        2. Gebruik *Extract Class* en *Move Method* in IntelliJ IDEA.
        3. Refactor de `Customer` klasse om samen te werken met `OrderHistory`.


**Oplossing:**

<details>
<summary>Klik hier</summary>


   ```javascript
   class Customer {
       constructor(name, address, phoneNumber, orders) {
           this.name = name;
           this.address = address;
           this.phoneNumber = phoneNumber;
           this.orderHistory = new OrderHistory(orders);
       }

       getTotalOrderValue() {
           return this.orderHistory.getTotalOrderValue();
       }

       hasLatePayments() {
           return this.orderHistory.hasLatePayments();
       }
   }

   class OrderHistory {
       constructor(orders) {
           this.orders = orders;
       }

       getTotalOrderValue() {
           let total = 0;
           for (let order of this.orders) {
               total += order.getValue();
           }
           return total;
       }

       hasLatePayments() {
           for (let order of this.orders) {
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

6. **Oefening 3: Inline Method en Rename Refactoring (30 minuten)**
    - **Code Voorbeeld:**
   ```javascript
   class Product {
       constructor(price) {
           this.price = price;
       }

       getDiscountedPrice() {
           return this.applyDiscount(this.price);
       }

       applyDiscount(originalPrice) {
           return originalPrice * 0.9;
       }
   }
   ```
    - **Uitdaging:**
        1. Gebruik *Inline Method* om `applyDiscount` samen te voegen met `getDiscountedPrice`.
        2. Gebruik *Rename Refactoring* om `price` te hernoemen naar `originalPrice`.


**Oplossing:**

<details>
<summary>Klik hier</summary>


   ```javascript
   class Product {
       constructor(originalPrice) {
           this.originalPrice = originalPrice;
       }

       getDiscountedPrice() {
           return this.originalPrice * 0.9;
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
   ```javascript
   class Library {
       constructor(books) {
           this.books = books;
       }

       getBooksByAuthor(author) {
           let result = [];
           for (let book of this.books) {
               if (book.getAuthor() === author) {
                   result.push(book);
               }
           }
           return result;
       }

       getBooksPublishedAfter(year) {
           let result = [];
           for (let book of this.books) {
               if (book.getPublicationYear() > year) {
                   result.push(book);
               }
           }
           return result;
       }
   }

   class Book {
       constructor(title, author, publicationYear) {
           this.title = title;
           this.author = author;
           this.publicationYear = publicationYear;
       }

       getAuthor() {
           return this.author;
       }

       getPublicationYear() {
           return this.publicationYear;
       }
   }
   ```
    - **Uitdaging:**
        1. Maak een nieuwe klasse `BookFilter` die filtermethoden bevat.
        2. Verplaats de filtermethoden naar `BookFilter`.
        3. Pas de `Library` klasse aan om `BookFilter` te gebruiken.


**Oplossing:**

<details>
<summary>Klik hier</summary>


   ```javascript
   class Library {
       constructor(books) {
           this.books = books;
           this.bookFilter = new BookFilter();
       }

       getBooksByAuthor(author) {
           return this.bookFilter.getBooksByAuthor(this.books, author);
       }

       getBooksPublishedAfter(year) {
           return this.bookFilter.getBooksPublishedAfter(this.books, year);
       }
   }

   class BookFilter {
       getBooksByAuthor(books, author) {
           let result = [];
           for (let book of books) {
               if (book.getAuthor() === author) {
                   result.push(book);
               }
           }
           return result;
       }

       getBooksPublishedAfter(books, year) {
           let result = [];
           for (let book of books) {
               if (book.getPublicationYear() > year) {
                   result.push(book);
               }
           }
           return result;
       }
   }

   class Book {
       constructor(title, author, publicationYear) {
           this.title = title;
           this.author = author;
           this.publicationYear = publicationYear;
       }

       getAuthor() {
           return this.author;
       }

       getPublicationYear() {
           return this.publicationYear;
       }
   }
   ```
</details>


### Nuttige links en documentatie
- [Refactoring in IntelliJ IDEA](https://www.jetbrains.com/help/idea/refactoring-source-code.html)
- [SOLID Principes](https://en.wikipedia.org/wiki/SOLID)
- [Clean Code Boek door Robert C. Martin](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
- [Code Smells](https://refactoring.guru/refactoring/smells)

Veel succes met het implementeren en verbeteren van je code!