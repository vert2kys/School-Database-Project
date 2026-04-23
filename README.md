Temat: System Zarządzania Szkołą Lumina
Autorzy: Bohdan Kliukovskyi, Bohdan Krasovskyi.

**Zakres i krótki opis systemu**

Lumina to zintegrowany system bazy danych, stworzony z myślą o kompleksowej cyfryzacji administracji szkolnej. Projekt koncentruje się na dwóch głównych filarach: precyzyjnym zarządzaniu kapitałem ludzkim oraz optymalizacji infrastruktury edukacyjnej.

W ramach ewidencji osób, system gromadzi nie tylko podstawowe dane, ale również szczegółowe profile zawodowe nauczycieli, w tym ich imiona, nazwiska, stopnie naukowe oraz konkretne specjalizacje przedmiotowe. Pozwala to na inteligentne przypisywanie kadry do odpowiednich kursów. W obszarze logistyki, Lumina zarządza zasobami szkoły, łącząc nazwy przedmiotów z konkretnymi salami lekcyjnymi oraz precyzyjnymi ramami czasowymi w tygodniowym harmonogramie. Dodatkowo, system oferuje zaawansowany moduł oceniania, który gwarantuje pełną przejrzystość procesu dydaktycznego poprzez monitorowanie historii każdej wprowadzonej poprawki.

Wymagania i funkcje systemu

Główne wymagania techniczne i funkcjonalne systemu Lumina obejmują:

Integralność danych osobowych: Każdy rekord w bazie musi być zweryfikowany pod kątem unikalności numeru PESEL. Dotyczy to zarówno uczniów, jak i pracowników, co eliminuje błędy w dokumentacji i dublowanie kont.

Zarządzanie dydaktyką: Każdy przedmiot (np. Informatyka, Język Angielski Poziom B2) musi być powiązany z unikalnym kodem oraz przypisany do konkretnego nauczyciela prowadzącego. System dopuszcza relację, w której jeden przedmiot jest wykładany przez wielu pedagogów w różnych grupach.

Harmonogram i kolizje: Rozkład zajęć musi być tworzony w oparciu o sztywne ramy godzinowe (godzina rozpoczęcia i zakończenia). Algorytm bazy danych musi uniemożliwiać rezerwację tej samej sali lekcyjnej dla dwóch różnych grup w tym samym czasie.

Transparentność ocen: Każda zmiana oceny musi automatycznie generować wpis do logów, zawierający datę modyfikacji oraz dane osoby (imię i nazwisko nauczyciela), która dokonała korekty.

Historyjki użytkownika (User Stories):

Jako uczeń, chcę mieć dostęp do aktualnego planu zajęć, aby w każdej chwili sprawdzić dokładną nazwę przedmiotu, nazwisko prowadzącego oraz numer sali, w której odbywa się lekcja.

Jako nauczyciel, chcę sprawnie zarządzać listami uczniów w moich grupach, mając możliwość wystawiania ocen oraz edytowania błędnych wpisów z automatycznym zachowaniem historii zmian.

Jako dyrektor, chcę kontrolować obciążenie sal lekcyjnych oraz zarządzać przypisaniami nauczycieli do nowo tworzonych przedmiotów w ramach rocznego arkusza organizacyjnego.

Jako administrator, chcę czuwać nad poprawnością wprowadzanych danych, blokując rejestrację błędnych numerów PESEL oraz definiując nowe kategorie przedmiotów w strukturze systemu Lumina.
