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
