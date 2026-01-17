\#  FestiCore - Festival Management System



\*\*FestiCore\*\* is a command-line Java application designed to simulate the complete management of an international music festival. This project was developed as part of the ESIEA Technical Challenge.



The application handles ticketing (Tickets, VIP Passes, Activities), scheduling (Artists, Stages, Concerts), user management, and data persistence.



---



\##  Implemented Features



The project covers all the functional requirements of the core curriculum:



\### 1. Festival \& Ticketing Management

\* \*\*Scheduling:\*\* Management of stages, artists, and concerts (dates/times).

\* \*\*Varied Offers:\*\*

&nbsp; \* Standard Tickets (Day Pass).

&nbsp; \* VIP Passes (Camping access, Backstage/Lounge access).

&nbsp; \* Activities (Meet \& Greet with Artists).

\* \*\*Stock Management:\*\* Strict quota management with real-time locking.



\### 2. User Management

\* \*\*Registration/Login:\*\* Secure account creation (Name, Email, Phone).

\* \*\*History:\*\* Complete tracking of past orders for the connected user.



\### 3. Technical System

\* \*\*JSON Persistence:\*\* Automatic saving and loading of all data (Users, Catalog, Stocks) via the Gson library.

\* \*\*Logging:\*\* Traceability of actions (logins, purchases, errors) via `java.util.logging` configured through an external file.

\* \*\*Search:\*\* Filtering of concerts and activities by date.



---



\##  Architecture \& Technical Choices



This project respects a layered architecture (\*Separation of Concerns\*) and implements advanced OOP concepts:



\### 1. Modeling (Inheritance \& Polymorphism)

\* Usage of an abstract class \*\*`Offre`\*\* extended by `Billet` (Ticket), `Pass`, and `Activite` (Activity).

\* Allows polymorphic manipulation of the catalog (`List<Offre>`) and generic purchase processing.



\### 2. Data Access (Generics)

\* Implementation of a \*\*Generic Repository\*\*: `JsonRepository<T>`.

\* This single component is capable of serializing/deserializing any type of object (`User`, `Offer`, etc.), reducing code duplication.

\* Usage of \*\*Gson Adapters\*\* (`OffreAdapter`, `LocalDateTimeAdapter`) to handle JSON polymorphism and Java 8 dates.



\### 3. Robustness (Exceptions)

\* Fine-grained error management via a hierarchy of custom exceptions (`FestiException`, `StockEpuiseException`).



---



\##  Project Structure



```text

src/

├── cli/                          # User Interface (View)

│   ├── Main.java                 # Entry Point

│   └── MenuPrincipal.java        # Command handling and display

│

├── service/                      # Business Logic (Controller)

│   ├── AuthService.java          # Registration/Login management

│   ├── BilletterieService.java   # Stock, catalog, and festival management

│   └── LogService.java           # Logger configuration

│

├── model/                        # Data Model

│   ├── offre/                    # Offer Hierarchy (Ticket, Pass...)

│   ├── festival/                 # Structure (Stage, Concert, Artist)

│   ├── acteur/                   # User

│   └── transaction/              # Order/Command

│

├── dao/                          # Data Access Object

│   ├── JsonRepository.java       # Generic saving engine <T>

│   └── \*Adapter.java             # Adapters for Gson

│

└── exception/                    # Business Exceptions

