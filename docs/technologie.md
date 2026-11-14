
##  Stos Technologiczny

### 1. Frontend (Web & Mobile)

* **Wybrane technologie:** `React` (Aplikacja Webowa / RWA) + `React Native` (Aplikacje Mobilne)
* **Uzasadnienie:** Wykorzystanie wspólnego ekosystemu JavaScript/TypeScript w oparciu o React pozwala na łatwe współdzielenie kodu i logiki biznesowej. Panel webowy obsługuje Klienta (składanie zleceń, opłacanie, śledzenie paczki), Odbiorcę oraz Dyspozytora i Administratora. Z kolei dedykowane aplikacje mobilne w React Native zapewniają płynne działanie w terenie dla Kuriera (skanowanie przesyłek, obsługa prób doręczenia) oraz Magazyniera (przyjmowanie, sortowanie i zwroty).


### 2. Backend (Język, Framework i Komunikacja Live)

* **Wybrane technologie:** `C#` / `.NET 10 (LTS)` (`ASP.NET Core Web API`), `SignalR` (WebSocket), `ASP.NET Core Identity` + `JWT`
* **Uzasadnienie:** Framework .NET 10 (LTS) zapewnia najwyższą wydajność, bezpieczeństwo typowania oraz przejrzystą architekturę REST API. Dodatkowo oferuje wbudowany mechanizm uwierzytelniania i autoryzacji (`ASP.NET Core Identity` z tokenami `JWT`) oraz bibliotekę `SignalR` wykorzystującą protokół WebSocket do śledzenia pozycji kuriera i statusu przesyłek w czasie rzeczywistym.


### 3. Baza Danych

* **Wybrane technologie:** `Microsoft SQL Server` + `Entity Framework Core 10 (LTS)`
* **Uzasadnienie:** Relacyjna baza danych SQL Server idealnie odpowiada wymaganiom spójności transakcyjnej (ACID) niezbędnej przy obsłudze zleceń, rozliczeniach i zmianie statusów przesyłek. Entity Framework Core 10 ułatwia komunikację z bazą na poziomie kodu C#, automatyzuje proces migracji bazy oraz chroni przed atakami typu SQL Injection dzięki parametryzowanym zapytaniom.


### 4. Infrastruktura / Hosting / CI/CD

* **Wybrane technologie:** `Docker` + `AWS` (`AWS ECS`, `AWS RDS for SQL Server`, `AWS ALB`) + `GitHub Actions`
* **Uzasadnienie:** Konteneryzacja w Dockerze gwarantuje identyczne środowisko uruchomieniowe na maszynach deweloperskich oraz produkcyjnych, a potoki GitHub Actions automatyzują testy i wdrożenia. Chmura AWS oferuje skalowalną i wysoko dostępną infrastrukturę: usługi `AWS ECS` do uruchamiania kontenerów backendowych, `AWS RDS` do obsługi relacyjnej bazy MS SQL Server oraz `AWS Application Load Balancer (ALB)` do równoważenia ruchu.


### 5. Integracje Zewnętrzne

* **Wybrane technologie:** `OpenStreetMap` (Leaflet.js / OSRM) + `PayU` + `Twilio` (SMS) + `SendGrid` (e-mail)
* **Uzasadnienie:** 
  * **OpenStreetMap:** Dane OpenStreetMap są dostępne bez opłat licencyjnych (licencja ODbL, wymagane podanie źródła). Na produkcji planujemy własny serwer OSRM i kafelków (self-hosting), żeby nie wpaść na limity publicznych serwerów.
  * **PayU:** Wybrany ze względu na pełne wsparcie dla najpopularniejszych polskich metod płatności (BLIK, natychmiastowe przelewy online / Pay-by-link), co jest kluczowe dla szybkiej weryfikacji wpłaty i natychmiastowego generowania etykiety.
  * **Twilio + SendGrid:** Dwaj niezależni, dedykowani dostawcy używani wspólnie: Twilio odpowiada za wysyłkę powiadomień SMS z kodem odbioru, a SendGrid obsługuje wiadomości e-mail o zmianie statusu przesyłki.


### 6. Narzędzia Zespołowe i Deweloperskie

* **Wybrane technologie:** `GitHub` + `app.diagrams.net` (draw.io) + `SQL Server Management Studio (SSMS)`
* **Uzasadnienie:** GitHub zapewnia kontrolę wersji, zarządzanie zadaniami oraz Code Review poprzez Pull Requesty. Narzędzie `app.diagrams.net` służy do wygenerowania i utrzymywania źródeł diagramów w plikach `docs/architektura.drawio` oraz eksportu do `docs/architektura.png`. Środowisko `SSMS` służy deweloperom jako opcjonalne narzędzie do podglądu bazy danych i lokalnego wykonywania zapytań T-SQL.
