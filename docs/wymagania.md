# Wymagania systemu dla firmy kurierskiej

## 1. Założenia

- Płatność za zlecenie jest dokonywana z góry, przed odbiorem paczki.
- Po dwóch nieudanych próbach doręczenia paczka jest zwracana do nadawcy.
- Po pierwszej nieudanej próbie paczka wraca do ponownego przydziału na trasę.
- Kurier i Magazynier korzystają z aplikacji mobilnych, pozostali aktorzy z panelu webowego.
- Odbiorca nie musi mieć konta: status przesyłki sprawdza po numerze przesyłki lub linku z powiadomienia.

## 2. Wymagania funkcjonalne

### 2.1 Zestawienie historyjek

| ID | Aktor | Tytuł | Priorytet |
|----|-------|-------|-----------|
| US-01 | Klient (nadawca) | Rejestracja i logowanie | Must |
| US-02 | Klient (nadawca) | Złożenie zlecenia z wyceną | Must |
| US-03 | Klient (nadawca) | Płatność online za zlecenie | Must |
| US-04 | Klient (nadawca) | Anulowanie zlecenia przed odbiorem | Should |
| US-05 | Klient (nadawca), Odbiorca | Śledzenie statusu przesyłki | Must |
| US-06 | Dyspozytor | Przydział kuriera i planowanie tras | Must |
| US-07 | Kurier | Odbiór paczki od klienta | Must |
| US-08 | Magazynier | Przyjęcie i sortowanie paczki w magazynie | Must |
| US-09 | Kurier | Rejestracja próby doręczenia | Must |
| US-10 | Odbiorca | Potwierdzenie odbioru przesyłki | Must |
| US-11 | Dyspozytor | Zlecenie zwrotu po dwóch nieudanych próbach | Must |
| US-12 | Odbiorca | Ustalenie nowego terminu doręczenia | Could |
| US-13 | Administrator | Zarządzanie kontami i cennikiem | Should |
| US-14 | Administrator | Raporty o przesyłkach i terminowości | Could |
| US-15 | Systemy zewnętrzne | Przekazanie wyniku płatności i wysyłka powiadomień | Must |
| US-16 | Klient (nadawca) | Płatność przy odbiorze paczki | Won't |
| US-17 | Klient (nadawca) | Przesyłki międzynarodowe | Won't |

### 2.2 Szczegóły historyjek

### US-01: Rejestracja i logowanie
**Jako** Klient (nadawca) **chcę** założyć konto i się zalogować, **aby** składać zlecenia i widzieć ich historię.

**Kryteria akceptacji:**
- **Given** nie mam konta, **When** podaję poprawny e-mail i hasło spełniające wymagania, **Then** system tworzy konto i umożliwia logowanie.
- **Given** mam konto, **When** podaję poprawne dane logowania, **Then** system mnie loguje i otwiera panel klienta.
- **Given** podaję błędne hasło, **When** próbuję się zalogować, **Then** system odrzuca logowanie bez ujawniania, które pole było błędne.

**Priorytet:** Must

### US-02: Złożenie zlecenia z wyceną
**Jako** Klient (nadawca) **chcę** złożyć zlecenie, podając adres odbioru, adres doręczenia, wymiary i wagę paczki, **aby** nadać przesyłkę bez wizyty w oddziale.

**Kryteria akceptacji:**
- **Given** jestem zalogowany, **When** podaję poprawne adresy, wymiary i wagę, **Then** system wylicza i wyświetla cenę zgodną z aktualnym cennikiem.
- **Given** brakuje pola obowiązkowego lub wartość jest niepoprawna, **When** zatwierdzam formularz, **Then** system wskazuje błędne pola i nie tworzy zlecenia.
- **Given** cena została wyświetlona, **When** ją akceptuję, **Then** system przechodzi do płatności.

**Priorytet:** Must

### US-03: Płatność online za zlecenie
**Jako** Klient (nadawca) **chcę** zapłacić za zlecenie online (m.in. BLIK, przelew), **aby** zlecenie zostało przyjęte do realizacji.

**Kryteria akceptacji:**
- **Given** zaakceptowałem cenę, **When** płatność zakończy się powodzeniem, **Then** system nadaje numer przesyłki i generuje etykietę.
- **Given** płatność zakończyła się niepowodzeniem, **When** system otrzymuje taką informację, **Then** system anuluje zlecenie i kończy proces („Zlecenie anulowane”).
- **Given** płatność nie została potwierdzona, **When** zlecenie czeka na wynik płatności, **Then** zlecenie nie jest przekazywane do realizacji.

**Priorytet:** Must

### US-04: Anulowanie zlecenia przed odbiorem
**Jako** Klient (nadawca) **chcę** anulować zlecenie przed odbiorem paczki, **aby** nie nadawać przesyłki, której już nie potrzebuję.

**Kryteria akceptacji:**
- **Given** paczka nie została jeszcze odebrana przez kuriera, **When** anuluję zlecenie, **Then** system zmienia status zlecenia na „anulowane”.
- **Given** kurier odebrał już paczkę, **When** próbuję anulować zlecenie, **Then** system odmawia i informuje, że anulowanie nie jest już możliwe.

**Uwaga:** Możliwość anulowania przez Klienta wynika z tabeli aktorów w `kontekst.md`. Model procesu pokazuje na razie tylko anulowanie przez System po nieudanej płatności (opisane w US-03).

**Priorytet:** Should

### US-05: Śledzenie statusu przesyłki
**Jako** Klient (nadawca) lub Odbiorca **chcę** sprawdzać aktualny status przesyłki, **aby** wiedzieć, kiedy mogę się jej spodziewać.

**Kryteria akceptacji:**
- **Given** znam numer przesyłki, **When** wpisuję go w panelu webowym, **Then** widzę aktualny status i historię zmian statusu.
- **Given** paczka jest w drodze do odbiorcy, **When** zmienia się pozycja kuriera lub status przesyłki, **Then** widok na żywo odświeża się bez ręcznego przeładowania strony.
- **Given** podaję nieistniejący numer przesyłki, **When** wyszukuję, **Then** system informuje, że przesyłka nie została znaleziona.

**Priorytet:** Must

### US-06: Przydział kuriera i planowanie tras
**Jako** Dyspozytor **chcę** przydzielać kurierów do odbiorów oraz paczki do tras doręczeń, **aby** zorganizować pracę kurierów i skrócić czas obsługi.

**Kryteria akceptacji:**
- **Given** zlecenie zostało opłacone i ma numer przesyłki, **When** przydzielam kuriera do odbioru paczki, **Then** kurier widzi to zlecenie w swojej aplikacji mobilnej.
- **Given** paczka została przyjęta i posortowana w magazynie, **When** przypisuję ją do trasy doręczenia, **Then** system dodaje ją do uporządkowanej listy adresów kuriera na dany dzień.
- **Given** kurier zarejestrował pierwszą nieudaną próbę doręczenia, **When** Dyspozytor ponownie przypisuje paczkę do trasy, **Then** paczka trafia na kolejną trasę doręczenia.

**Priorytet:** Must

### US-07: Odbiór paczki od klienta
**Jako** Kurier **chcę** zarejestrować odbiór paczki od klienta w aplikacji mobilnej, **aby** system wiedział, że przesyłka jest w drodze do magazynu.

**Kryteria akceptacji:**
- **Given** mam przydzielone zlecenie odbioru, **When** skanuję etykietę paczki w aplikacji mobilnej, **Then** system zmienia status przesyłki na „odebrana od nadawcy”.
- **Given** zeskanowana etykieta nie odpowiada zleceniu z mojej listy, **When** próbuję zatwierdzić odbiór, **Then** system odrzuca operację i wyświetla komunikat o błędzie.

**Priorytet:** Must

### US-08: Przyjęcie i sortowanie paczki w magazynie
**Jako** Magazynier **chcę** przyjąć i posortować paczkę w aplikacji mobilnej, **aby** była gotowa do przypisania do trasy doręczenia.

**Kryteria akceptacji:**
- **Given** paczka dotarła do magazynu, **When** skanuję jej etykietę, **Then** system zmienia status na „w magazynie” i zapisuje czas przyjęcia.
- **Given** paczka została posortowana, **When** zatwierdzam sortowanie, **Then** system udostępnia ją Dyspozytorowi do przypisania do trasy.

**Priorytet:** Must

### US-09: Rejestracja próby doręczenia
**Jako** Kurier **chcę** zarejestrować wynik próby doręczenia (udaną lub nieudaną), **aby** system miał aktualny stan przesyłki.

**Kryteria akceptacji:**
- **Given** jestem pod adresem doręczenia, **When** odbiorca odbiera paczkę, **Then** system zapisuje udaną próbę i przechodzi do potwierdzenia odbioru.
- **Given** odbiorca jest nieobecny, **When** rejestruję nieudaną próbę z powodem, **Then** system zapisuje próbę, zwiększa licznik prób i powiadamia odbiorcę o nieudanej próbie.
- **Given** zarejestrowana została pierwsza nieudana próba, **When** system ją zapisuje, **Then** Dyspozytor ponownie przydziela paczkę do trasy doręczenia.

**Priorytet:** Must

### US-10: Potwierdzenie odbioru przesyłki
**Jako** Odbiorca **chcę** potwierdzić odbiór paczki kodem lub podpisem, **aby** doręczenie było udokumentowane.

**Kryteria akceptacji:**
- **Given** kurier jest pod adresem doręczenia, **When** odbieram paczkę i potwierdzam odbiór kodem lub podpisem, **Then** system rejestruje potwierdzenie i zmienia status na „doręczona”.
- **Given** doręczenie zostało potwierdzone, **When** system zapisuje potwierdzenie, **Then** system powiadamia Klienta (nadawcę) o doręczeniu i kończy proces („Przesyłka doręczona”).

**Priorytet:** Must

### US-11: Zlecenie zwrotu po dwóch nieudanych próbach
**Jako** Dyspozytor **chcę** zlecić zwrot paczki do nadawcy po dwóch nieudanych próbach doręczenia, **aby** nie blokować paczki w obiegu.

**Kryteria akceptacji:**
- **Given** Kurier zarejestrował nieudaną próbę, a Odbiorca został powiadomiony, **When** Dyspozytor stwierdza, że to była 2. próba, **Then** Dyspozytor zleca zwrot paczki do nadawcy.
- **Given** zwrot został zlecony, **When** Magazynier przyjmuje paczkę i odsyła ją do nadawcy, **Then** system zmienia status na „zwrócona do nadawcy” i kończy proces („Paczka zwrócona”).
- **Given** to była dopiero 1. próba, **When** Dyspozytor sprawdza liczbę prób, **Then** zwrot nie jest zlecany, a paczka wraca do ponownego przydziału.

**Priorytet:** Must

### US-12: Ustalenie nowego terminu doręczenia
**Jako** Odbiorca **chcę** ustalić nowy termin doręczenia po nieudanej próbie, **aby** odebrać paczkę, kiedy będę w domu.

**Kryteria akceptacji:**
- **Given** otrzymałem powiadomienie o nieudanej próbie, **When** wybieram nowy dostępny termin, **Then** system zapisuje go i przekazuje Dyspozytorowi do planowania trasy.
- **Given** paczka ma już dwie nieudane próby, **When** próbuję wybrać nowy termin, **Then** system informuje, że paczka zostanie zwrócona do nadawcy.

**Uwaga:** Funkcja wynika z kontekstu (Odbiorca „może ustalić nowy termin doręczenia”). Model procesu jej nie pokazuje, dlatego jest to rozszerzenie o priorytecie Could.

**Priorytet:** Could

### US-13: Zarządzanie kontami i cennikiem
**Jako** Administrator **chcę** zarządzać kontami użytkowników i cennikiem, **aby** system odzwierciedlał aktualną strukturę firmy i ofertę.

**Kryteria akceptacji:**
- **Given** jestem zalogowany jako Administrator, **When** dodaję, edytuję lub blokuję konto pracownika, **Then** zmiana jest zapisana i obowiązuje od następnego logowania.
- **Given** zmieniam cennik, **When** zapisuję nowe stawki, **Then** obowiązują one tylko dla zleceń złożonych po zmianie.
- **Given** jestem użytkownikiem bez roli Administratora, **When** próbuję otworzyć panel administracyjny, **Then** system odmawia dostępu.

**Priorytet:** Should

### US-14: Raporty o przesyłkach i terminowości
**Jako** Administrator **chcę** generować raporty (liczba przesyłek, terminowość, odsetek nieudanych doręczeń), **aby** oceniać skuteczność pracy firmy.

**Kryteria akceptacji:**
- **Given** wybieram zakres dat, **When** generuję raport, **Then** system pokazuje liczbę przesyłek, terminowość i odsetek nieudanych doręczeń w tym okresie.
- **Given** w wybranym okresie nie ma danych, **When** generuję raport, **Then** system informuje o braku danych zamiast pokazywać puste wartości.

**Priorytet:** Could

### US-15: Przekazanie wyniku płatności i wysyłka powiadomień
**Jako** Systemy zewnętrzne (bramka płatności, bramka SMS/e-mail) **chcę** przekazywać wyniki płatności oraz dostarczać powiadomienia, **aby** system mógł aktualizować statusy zleceń i informować klientów oraz odbiorców.

**Kryteria akceptacji:**
- **Given** płatność została rozliczona w bramce płatności, **When** bramka przesyła wynik do systemu, **Then** system przechodzi do nadania numeru przesyłki (płatność udana) albo anuluje zlecenie (płatność nieudana).
- **Given** Kurier zarejestrował nieudaną próbę doręczenia, **When** system zleca powiadomienie, **Then** bramka SMS/e-mail dostarcza wiadomość do Odbiorcy.
- **Given** doręczenie zostało potwierdzone, **When** system zleca powiadomienie, **Then** bramka SMS/e-mail dostarcza wiadomość do Klienta (nadawcy).
- **Given** bramka powiadomień jest niedostępna, **When** system próbuje wysłać wiadomość, **Then** ponawia próbę i zapisuje błąd w logach.

**Priorytet:** Must

### US-16: Płatność przy odbiorze paczki
**Jako** Klient (nadawca) **chcę** płacić za zlecenie przy odbiorze paczki przez kuriera, **aby** nie płacić z góry.

**Uzasadnienie priorytetu:** W założeniach projektu płatność jest dokonywana z góry, dlatego funkcja nie wchodzi w zakres tej wersji systemu.

**Priorytet:** Won't

### US-17: Przesyłki międzynarodowe
**Jako** Klient (nadawca) **chcę** nadawać przesyłki za granicę, **aby** korzystać z jednej firmy kurierskiej do wszystkich wysyłek.

**Uzasadnienie priorytetu:** Firma działa na terenie jednego kraju, więc obsługa przesyłek zagranicznych (cła, dokumenty, partnerzy) nie wchodzi w zakres tej wersji.

**Priorytet:** Won't

## 3. Zgodność z modelem procesu

| Krok procesu „Realizacja zlecenia kurierskiego” | Historyjka |
|---|---|
| Klient składa zlecenie, System wylicza cenę | US-02 |
| Klient płaci, decyzja „Płatność udana?” | US-03, US-15 |
| Nadanie numeru przesyłki i generowanie etykiety | US-03 |
| Anulowanie zlecenia po nieudanej płatności | US-03 |
| Dyspozytor przydziela kuriera do odbioru | US-06 |
| Kurier odbiera paczkę od klienta | US-07 |
| Magazynier przyjmuje i sortuje paczkę | US-08 |
| Dyspozytor przypisuje paczkę do trasy doręczenia | US-06 |
| Kurier jedzie do odbiorcy i próbuje doręczyć | US-09 |
| Odbiorca odbiera paczkę i potwierdza odbiór | US-10 |
| System powiadamia klienta o doręczeniu | US-10, US-15 |
| Kurier rejestruje nieudaną próbę, System powiadamia odbiorcę | US-09, US-15 |
| Decyzja „To była 2. próba?” (NIE: ponowny przydział) | US-06, US-09, US-11 |
| Dyspozytor zleca zwrot, Magazynier przyjmuje zwrot i odsyła | US-11 |

Historyjki spoza procesu (wynikają z `kontekst.md`): US-01, US-04, US-05, US-12, US-13, US-14.

## 4. Wymagania niefunkcjonalne

| ID | Kategoria | Wymaganie |
|----|-----------|-----------|
| NFR-01 | Wydajność | Wyświetlenie statusu przesyłki trwa maksymalnie 2 s dla 95% żądań przy 500 jednocześnie działających użytkownikach. |
| NFR-02 | Dostępność | System jest dostępny co najmniej 99,5% czasu w skali miesiąca (z wyłączeniem zaplanowanych okien serwisowych). |
| NFR-03 | Bezpieczeństwo | Uwierzytelnianie opiera się na ASP.NET Core Identity i tokenach JWT; hasła są przechowywane jako hashe z solą; cała komunikacja odbywa się po HTTPS; dostęp jest ograniczony rolami (np. Kurier widzi wyłącznie paczki ze swojej trasy). |
| NFR-04 | Bezpieczeństwo płatności | System nie przechowuje danych kart płatniczych; płatności obsługuje zewnętrzna bramka płatności. |
| NFR-05 | Skalowalność | Backend działa w kontenerach Docker i skaluje się poziomo (AWS ECS za AWS ALB) bez zmian w kodzie; system obsługuje co najmniej 10 000 przesyłek dziennie. |
| NFR-06 | Użyteczność | Nowy użytkownik składa pierwsze zlecenie w maksymalnie 5 minut bez instrukcji; aplikacje mobilne Kuriera i Magazyniera pozwalają zarejestrować skan paczki w maksymalnie 3 interakcjach. |
| NFR-07 | Zgodność z RODO | Dane osobowe klientów i odbiorców są usuwane lub anonimizowane w ciągu 30 dni od zgłoszenia żądania; dostęp do nich jest rejestrowany. |
| NFR-08 | Czas rzeczywisty | Zmiana pozycji kuriera lub statusu przesyłki jest widoczna dla klienta w ciągu 5 s (komunikacja SignalR / WebSocket). |
| NFR-09 | Spójność danych | Operacje na zleceniach, płatnościach i statusach przesyłek są transakcyjne (ACID); przy awarii w trakcie operacji dane nie pozostają w stanie niespójnym. |
| NFR-10 | Niezawodność | Kopia zapasowa bazy danych jest wykonywana codziennie; odtworzenie danych po awarii trwa maksymalnie 4 godziny. |
| NFR-11 | Zgodność platform | Panel webowy działa w aktualnych wersjach Chrome, Firefox i Edge; aplikacje mobilne działają na Androidzie i iOS. |
| NFR-12 | Utrzymywalność | Backend jest napisany w C# (.NET 10 LTS); logika biznesowa jest pokryta testami jednostkowymi w co najmniej 70%. |
| NFR-13 | Licencje | Dane map OpenStreetMap są wyświetlane z podaniem źródła zgodnie z licencją ODbL. |