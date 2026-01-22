1. Jako użytkownik, chcę płacić za bilet kartą, gotówką lub telefonem, aby mieć
większą elastyczność w wyborze metody płatności.
2. Jako użytkownik, chcę otrzymać wyraźne instrukcje na ekranie, aby wiedzieć,
jak dokonać zakupu krok po kroku.
3. Jako użytkownik, chcę widzieć czas pozostały na decyzję (np. wyświetlany
licznik czasu), aby móc szybko podjąć działanie.
4. Jako użytkownik, chcę szybko wybrać rodzaj biletu, aby zminimalizować czas
spędzony przy biletomacie.
5. Jako użytkownik, chcę mieć możliwość wyboru języka, aby móc korzystać z
biletomatu bez względu na znajomość języka lokalnego.
6. Jako użytkownik, chcę sprawdzić poprawność transakcji przed jej finalizacją,
aby uniknąć pomyłek.
7. Jako użytkownik, chcę otrzymać potwierdzenie zakupu (np. wydruk biletu lub
elektroniczny bilet), aby móc korzystać z transportu zgodnie z przepisami.

## Diagramy przypadków użycia
### Wybór języka

```mermaid
flowchart TD

U[Użytkownik] --> UC_JZ(Wybranie języka)
UC_POP(Wyranie popularnego języka) -.-> |extend| UC_JZ 
UC_JZ -.-> |include| UC_DEF(Wybranie domyślnego języka)

UC_JZ -.-> |include| UC_CANC(Anulowanie transakcji)
```

### Wyświetlenie instrukcji
```mermaid
flowchart TD

U[Użytkownik] --> U_INT(Rozpoczęcie interakcji z biletomatem) -.-> |include| U_INS(Wyświetl instrukcje)

U_INT -.-> |include| U_CANC(Anulowanie transakcji)

U_INT -.-> |include| U_WYB(Wybranie biletu)

U_SZCZ(Wyświetl szczegółowe instrukcje) -.-> |extend| U_INS
```

## Diagramy sekwencji

### Diagram sekwencji dla przypadku użycia Wybór języka

- Aktor: Użytkownik
- Obiekty: Biletomat
- Kolejność komunikatów:
    * Użytkownik uruchamia biletomat
    * System wyświetla ekran powitalny z opcjami wyboru języka
    * Użytkownik wybiera preferowany język
    * System dostosowywuje interfejs do wybranego języka
- Scenariusz alternatywny 1 (Anulowanie procesu):
    * Użytkownik w każdej chwili może anulować proces
- Scenariusz alternatywny 2 (Lista popularnych języków):
    * Użytkownik uruchamia biletomat
    * System wyświetla ekran powitalny z opcjami wyboru języka
    * Użytkownik wybiera opcję wyświetlenia listy popularnych języków
    * System wyświetla listę popularnych języków
    * Użytkownik wybiera preferowany język
    * System dostosowywuje interfejs do wybranego języka
- Scenariusz alternatywny 3 (Domyślny język):
    * Użytkownik uruchamia biletomat
    * System wyświetla ekran powitalny z opcjami wyboru języka
    * Użytkownik wybiera opcję ustawienia języka domyślnego
    * System dostosowywuje interfejs do wybranego języka

```mermaid
sequenceDiagram
	participant u as Użytkownik
	participant b as Biletomat
	
	activate u
	u ->>+ b: Rozpoczęcie interakcji
	b -->>- u: Wyświetlenie opcji języka
	alt Użytkownik chce zobaczyć listę popularnych języków
		u ->>+ b: Lista popularnych języków
		b -->> u: Wyświetlenie listy popularnych języków
		deactivate b
	else Użytkownik chce ustawić język domyślny
		activate b
		u ->> b: Domyślny język
	else
		u ->> b: Wybór języka
	end
	b ->> b: Dostosowanie interfejsu
	deactivate b
	
	break Użytkownik chce anulować proces
		u ->> b: Anulowanie procesu
	end
	
	deactivate u
```
