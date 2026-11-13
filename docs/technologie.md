##  Stos Technologiczny

### 1. Frontend (Web & Mobile)
* **Wybrane technologie:** `React` (Panel Web) + `React Native` (Aplikacja Mobilna)
* **Uzasadnienie:** Wykorzystanie wspólnego ekosystemu JavaScript/TypeScript pozwala na współdzielenie typów danych oraz logiki biznesowej między panelem administracyjno-dyspozytorskim a aplikacją mobilną. React Native umożliwia sprawne stworzenie natywnie działającej aplikacji dla Kuriera i Magazyniera (np. obsługa skanera kodów, rejestracja prób doręczeń w terenie) bez konieczności utrzymywania dwóch osobnych baz kodu na systemy Android oraz iOS.


---

### 2. Backend (Język i Framework)
* **Wybrane technologie:** `C#` / `.NET 8` (`ASP.NET Core Web API`)
* **Uzasadnienie:** Framework .NET 8 w języku C# zapewnia wysoką wydajność, bezpieczeństwo typowania oraz przejrzystą architekturę REST API. Doskonale integruje się z systemem bazy danych MS SQL Server i udostępnia gotowe rozwiązania w zakresie autoryzacji/uwierzytelniania oraz bezpiecznego przetwarzania wielowątkowego.


---

### 3. Baza Danych
* **Wybrane technologie:** `Microsoft SQL Server` (zarządzana przez **SQL Server Management Studio - SSMS**) + `Entity Framework Core`
* **Uzasadnienie:** Relacyjna baza danych SQL Server idealnie odpowiada wymaganiom spójności transakcyjnej (ACID) niezbędnej przy obsłudze zleceń, rozliczeniach i zmianie statusów przesyłek. Entity Framework Core ułatwia komunikację z bazą na poziomie kodu C#, automatyzuje proces migracji i zabezpiecza system przed wyciekiem danych oraz atakami typu SQL Injection.


---

### 4. Infrastruktura / Hosting / CI/CD
* **Wybrane technologie:** `Docker` + `AWS` (Amazon Web Services) + `GitHub Actions`
* **Uzasadnienie:** Konteneryzacja w Dockerze gwarantuje identyczne środowisko uruchomieniowe na maszynach deweloperskich oraz produkcyjnych, a potoki GitHub Actions automatyzują testy i wdrożenia. Chmura AWS (usługi takie jak AWS ECS dla kontenerów oraz Amazon RDS for SQL Server) zapewnia skalowalną, stabilną i wysoko dostępną infrastrukturę serwerową o wszechstronnych możliwościach konfiguracji.


---

### 5. Integracje Zewnętrzne
* **Wybrane technologie:** `OpenStreetMap` (Leaflet.js / OSRM API) + `Twilio` / `SendGrid` + `PayU` / `Stripe`
* **Uzasadnienie:** OpenStreetMap połączony z biblioteką Leaflet.js i API OSRM (Open Source Routing Machine) oferuje elastyczne, darmowe i pozbawione limitów licencyjnych rozwiązanie do wizualizacji map, geokodowania adresów i planowania tras. Bramka płatności (Stripe/PayU) weryfikuje wpłaty online w czasie rzeczywistym do natychmiastowej generacji etykiety, a Twilio (SMS) oraz SendGrid (E-mail) odpowiadają za powiadomienia o statusie przesyłki.


---

### 6. Narzędzia Zespołowe
* **Wybrane technologie:** `GitHub` + `app.diagrams.net` (draw.io)
* **Uzasadnienie:** GitHub oferuje pełną kontrolę wersji, wbudowaną obsługę zadań (Issues/Projects) oraz przejrzysty proces Code Review poprzez Pull Requesty. Platforma app.diagrams.net pozwala na darmową, standaryzowaną edycję i eksport diagramów procesowych (BPMN), sekwencji, przypadków użycia oraz struktur bazy danych w powszechnie akceptowanych formatach graficznych i wektorowych.
