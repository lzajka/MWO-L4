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
### Zarządzanie dostępnością biletu
```mermaid
sequenceDiagram
    participant AD as Administrator
    participant UI as Platforma administracyjna
    participant SY as System Centralny
    participant BT as Biletomaty

    AD ->> UI : Wybranie menu zarządzania dostępnością biletów
    UI ->> SY : Pobranie listy biletów
    SY -->> UI : Lista biletów
    UI -->> AD : Wyświetlenie listy biletów
    alt Administrator chce dodać bilet
    AD ->> UI : Wybranie opcji dodaj bilet
    UI -->> AD : Formularz dodania biletu
    AD ->> UI : Administrator wypełnia formularz dodania biletu
    UI ->> SY : dodaj_bilet(bilet_info)
    else Administrator chce edytować bilet
    AD ->> UI : Wybranie opcji edycji biletu z listy
    UI ->> SY : Pobranie danych biletu
    SY -->> UI : Dane biletu
    UI -->> AD : Wyświetlenie szczegółów biletu
    AD ->> UI : Modyfikacja danych w polach
    UI ->> SY : zaktualizuj_bilet(bilet_id, bilet_info) 
    else Administrator chce usunąć bilet
    AD ->> UI : Wybranie opcji usunięcia biletu z listy
    UI ->> SY : usun_bilet(id)
    end
    SY ->> BT : zaktualizuj listę biletów
    BT -->> SY : 
    SY -->> UI : Aktualna lista biletów
    UI -->> AD : Aktualna lista biletów
```    
### Aktualizacja oprogramowania
```mermaid
sequenceDiagram
    participant AD as Administrator
    participant UI as Platforma administracyjna
    participant SY as System Centraln
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

## Diagram klas

### Zarządzanie dostępnością biletu

```mermaid
classDiagram
	class Admin {
	}
	
	class AdminPlatform {
		-Ticket[] ticketList
		+Ticket[] showTicketList()
		+void addTicket()
		+Ticket[] postTicket(TicketInfo ticketInfo)
		+TicketInfo editTicket(id)
		+Ticket[] updateTicket(id, TicketInfo ticketInfo)
		+Ticket[] deleteTicket(id)
	}
	
	class CentralSystem {
		-Ticket[] ticketList
		-TicketInfo[] ticketInfoList
		+Ticket[] downloadTicketList()
		+TicketInfo downloadTicketInfo(id)
		+void addTicket(TicketInfo ticketInfo)
		+void updateTicket(id, TicketInfo ticketInfo)
		+void deleteTicket(id)
	}
	
	class TicketMachine {
		-Ticket[] ticketList
		+void updateTicketList()
	}

	Admin --> AdminPlatform : interacts with
	AdminPlatform --> CentralSystem : modifies
	CentralSystem --> TicketMachine : updates
```
