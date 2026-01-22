1. Jako administrator, chcę zdalnie aktualizować oprogramowanie biletomatów,
aby zapewnić zgodność z nowymi wymogami i funkcjonalnościami.
2. Jako administrator, chcę mieć dostęp do raportów sprzedaży w czasie
rzeczywistym, aby monitorować wyniki finansowe.
3. Jako administrator, chcę konfigurować dostępne bilety, promocje i taryfy w
systemie centralnym, aby odzwierciedlać zmiany w ofercie.

## Diagramy przypadków użycia
### Aktualizacja oprogramowania
```mermaid
flowchart TD
    Administrator --> uc1[Aktualizacja oprogramowania biletomatów]
    uc1 -.includes.-> uc2[Aktualizacja urządzeń]
    uc1 -.extends.-> uc3[Powiadomienie o błędach aktualizacji]
```
### Zarządzanie dostępnością biletów
```mermaid
flowchart TD
    Administrator --> uc1[Zarządzanie dostępnością biletów]
    uc1 -.includes.-> uc2[Synchronizacja danych]
    uc1 -.extends.-> uc3[Powiadomienie o problemach synchronizacji]
```
## Diagramy sekwencji
### Aktualizacja oprogramowania
```mermaid
sequenceDiagram
    participant AD as Administrator
    participant UI as Platforma administracyjna
    participant SY as System Centralny
    participant BT as Biletomat 

    AD ->> UI : Wybranie menu zarządzania biletomatami
    UI ->> SY : Pobranie listy wersji biletomatów
    SY -->> UI : Lista wersji biletomatów
    UI -->> AD : Wyświetlenie listy biletomatów
    AD ->> UI : Wybranie biletomatu
    UI -->> AD : Wyświetlenie szczegółów biletomatu
    AD ->> UI : Wybranie opcji zaktualizuj
    UI ->> SY : Zaktualizuj_biletomat(id) 
    SY ->> BT : Aktualizacja(obraz)
    opt Aktualizacja zakończona błędem
    BT ->> BT : Rollback
    end
    BT -->> SY : Wynik aktualizacji
    SY -->> UI : Wynik aktualizacji dla biletomatu
    UI -->> AD : Wyświetl powiadomienie o stanie aktualizacji

```