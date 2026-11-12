# Kontekst projektu: system dla firmy kurierskiej

## 1. Wizja systemu

System wspiera firmę kurierską w obsłudze pełnego cyklu życia przesyłki: od złożenia zlecenia przez klienta, przez odbiór, sortowanie w magazynie i transport, aż po doręczenie odbiorcy lub zwrot do nadawcy. Klienci mogą w jednym miejscu zamówić wysyłkę, zapłacić i śledzić status paczki na bieżąco. Pracownicy firmy (dyspozytorzy, magazynierzy, kurierzy) otrzymują narzędzia do planowania tras, zarządzania magazynem i rejestrowania przebiegu doręczeń. Celem jest skrócenie czasu obsługi, ograniczenie liczby zagubionych lub niedoręczonych paczek oraz pełna przejrzystość procesu dla klienta.

## 2. Cele systemu

- Umożliwić klientom samodzielne składanie zleceń i płatności online.
- Zapewnić śledzenie statusu przesyłki w czasie zbliżonym do rzeczywistego.
- Usprawnić przydział kurierów i planowanie tras doręczeń.
- Uporządkować obsługę magazynu (przyjęcie, sortowanie, wydanie paczek).
- Standaryzować obsługę sytuacji nietypowych (nieobecny odbiorca, uszkodzona paczka, zwrot).
- Dostarczyć kierownictwu podstawowe raporty (liczba przesyłek, terminowość, odsetek nieudanych doręczeń).

## 3. Zakres systemu

**W zakresie:**
- rejestracja i obsługa kont użytkowników,
- składanie zleceń, wycena i płatność online,
- generowanie numeru przesyłki i etykiety,
- przydział kurierów do odbiorów i doręczeń oraz planowanie tras,
- obsługa magazynu (przyjęcie, sortowanie, zwroty),
- rejestrowanie prób doręczenia i potwierdzeń odbioru,
- powiadomienia dla klientów i odbiorców (e-mail / SMS),
- śledzenie przesyłek i raporty.

## 4. Aktorzy

| Aktor | Typ | Rola w systemie |
|---|---|---|
| Klient (nadawca) | osoba zewnętrzna | Składa zlecenie wysyłki, płaci, śledzi status przesyłki, może anulować zlecenie przed odbiorem. |
| Odbiorca | osoba zewnętrzna | Odbiera przesyłkę, potwierdza odbiór, otrzymuje powiadomienia o statusie, może ustalić nowy termin doręczenia. |
| Kurier | pracownik | Odbiera paczki od klientów, doręcza je odbiorcom, rejestruje próby doręczenia i problemy. |
| Dyspozytor | pracownik | Przydziela kurierów do odbiorów i tras doręczeń, reaguje na nieudane doręczenia, decyduje o zwrocie. |
| Magazynier | pracownik | Przyjmuje, sortuje i wydaje paczki w magazynie, obsługuje zwroty. |
| Administrator | pracownik | Zarządza kontami użytkowników, cennikiem i konfiguracją systemu. |
| Systemy zewnętrzne | system | Bramka płatności, usługa map i geolokalizacji, bramka SMS / e-mail. |

## 5. Słowniczek pojęć

| Pojęcie | Znaczenie |
|---|---|
| Zlecenie | Zamówienie usługi kurierskiej złożone przez klienta (adres odbioru, adres doręczenia, wymiary i waga paczki). |
| Przesyłka | Fizyczna paczka objęta zleceniem, identyfikowana unikalnym numerem. |
| Etykieta | Dokument z numerem przesyłki i kodem kreskowym naklejany na paczkę. |
| Trasa | Uporządkowana lista adresów doręczeń lub odbiorów przypisana kurierowi na dany dzień. |
| Próba doręczenia | Pojedyncza wizyta kuriera u odbiorcy w celu wydania paczki. |
| Zwrot | Odesłanie niedoręczonej paczki do nadawcy po wyczerpaniu prób doręczenia. |
| Potwierdzenie odbioru | Zarejestrowany w systemie dowód wydania paczki odbiorcy (np. podpis lub kod). |

## 6. Założenia

- Firma działa na terenie jednego kraju i obsługuje klientów indywidualnych oraz biznesowych.
- Po dwóch nieudanych próbach doręczenia paczka jest zwracana do nadawcy.
- Płatność za zlecenie jest dokonywana z góry, przed odbiorem paczki.
- Nazwy aktorów z tego dokumentu obowiązują we wszystkich pozostałych dokumentach projektu.
