Temat: System Zarządzania Szkołą "Lumina"

Autorzy: Bohdan Krasovskyi, Bohdan Kliukovskyi.


1. Zakres i krótki opis systemu
Projekt dotyczy relacyjnej bazy danych "Lumina", która służy do zarządzania procesami w placówce oświatowej. System został zaprojektowany z myślą o pełnej kontroli nad danymi uczniów, nauczycieli oraz historią oceniania.

Główne funkcjonalności:
Ewidencja osób:** Przechowywanie danych osobowych z unikalną identyfikacją PESEL.
Zarządzanie strukturą:** Obsługa klas, przedmiotów oraz elastyczne przypisywanie nauczycieli do zajęć.
Historia ocen:** Możliwość korekty ocen z automatycznym śledzeniem daty modyfikacji.


2. Wymagania i funkcje systemu

Wymagania systemowe:
Integralność danych: Każdy rekord ucznia musi posiadać unikalny numer PESEL (brak możliwości dublowania).
Elastyczność dydaktyczna: Jeden przedmiot może być prowadzony przez wielu nauczycieli (np. w różnych grupach).
Edycja ocen System musi pozwalać nauczycielom na poprawę ocen, rejestrując przy tym czas zmiany.

Historyjki użytkownika (User Stories):
Jako administrator, chcę mieć pewność, że w bazie nie pojawią się dwa te same numery PESEL.
Jako nauczyciel, chcę móc edytować ocenę w przypadku pomyłki, aby w systemie widniała aktualna data korekty.
Jako dyrektor, chcę przypisać kilku nauczycieli do tego samego przedmiotu (np. Język angielski) dla różnych grup uczniów.
Jako wychowawca, chcę wygenerować listę wszystkich uczniów mojej klasy wraz z ich danymi.
