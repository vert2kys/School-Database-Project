# Temat: System Zarządzania Szkołą "Lumina"

**Autorzy:** (Bohdan Kliukovskyi, Bohdan Krasovskyi)  
**Data projektu:** 2026-04-23  
**Status:** Zadanie 1 i 2 (Projektowanie i Wymagania)

---

## 1. Zakres i krótki opis systemu

**Lumina** to zintegrowany system bazy danych zaprojektowany do kompleksowej obsługi procesów administracyjnych i dydaktycznych w nowoczesnej placówce oświatowej. System ma na celu zastąpienie rozproszonych arkuszy danych jedną, spójną strukturą relacyjną, która gwarantuje bezpieczeństwo i szybkość dostępu do informacji.

### Kluczowe obszary funkcjonalne:
* **Zarządzanie kadrą pedagogiczną:** System przechowuje szczegółowe profile nauczycieli, w tym **imiona, nazwiska, stopnie naukowe** oraz specjalizacje przedmiotowe, co pozwala na precyzyjne dopasowanie kadry do planu zajęć.
* **Ewidencja uczniów:** Centralna baza danych z unikalną identyfikacją osób, umożliwiająca śledzenie przynależności do klas oraz historii nauczania.
* **Logistyka i infrastruktura:** Moduł zarządzania zasobami, który łączy **nazwy przedmiotów** z konkretnymi numerami sal lekcyjnych oraz precyzyjnymi godzinami w harmonogramie.
* **Transparentność oceniania:** Zaawansowana ewidencja wyników nauczania, która kładzie nacisk na historię zmian — każda korekta oceny jest monitorowana wraz z datą modyfikacji.

---

## 2. Wymagania i funkcje systemu

System Lumina został zaprojektowany w oparciu o rygorystyczne wymagania dotyczące spójności i wygody użytkowania.

### 🛠 Wymagania techniczne i integralność
1.  **Unikalność tożsamości:** Każdy rekord w tabelach uczniów i nauczycieli musi posiadać unikalny numer **PESEL**. System automatycznie blokuje próby wprowadzenia duplikatów.
2.  **Relacje przedmiotowe:** System obsługuje relacje wiele-do-wielu, co pozwala na przypisanie wielu nauczycieli do jednej **nazwy przedmiotu** (np. Język angielski prowadzony przez różnych lektorów w różnych grupach).
3.  **Bezpieczeństwo harmonogramu:** Baza danych posiada mechanizmy kontroli kolizji, uniemożliwiające przypisanie dwóch różnych lekcji do tej samej sali w tym samym czasie.
4.  **Audyt ocen:** Każda ocena w systemie przechowuje informację o dacie ostatniej zmiany, co pozwala na weryfikację ewentualnych błędów lub korekt.

### 👤 Historyjki użytkownika (User Stories)

| Rola | Potrzeba użytkownika |
| :--- | :--- |
| **Uczeń** | Chcę sprawdzić mój **plan zajęć**, aby widzieć dokładną godzinę, nazwę przedmiotu oraz nazwisko nauczyciela prowadzącego lekcję w danej sali. |
| **Nauczyciel** | Chcę zarządzać listą uczniów w moich grupach oraz mieć możliwość poprawy oceny z automatycznym zapisem daty modyfikacji. |
| **Dyrektor** | Chcę mieć możliwość przypisania imienia i nazwiska konkretnego nauczyciela do przedmiotów w ramach nowego arkusza organizacyjnego. |
| **Wychowawca** | Chcę wygenerować raport zawierający imiona i nazwiska uczniów mojej klasy wraz z ich średnią ocen ze wszystkich przedmiotów. |
| **Administrator** | Chcę definiować nowe nazwy przedmiotów (np. Fizyka Kwantowa) i kontrolować poprawność numerów PESEL podczas dodawania nowych osób do bazy Lumina. |


```mermaid

erDiagram
    Classes ||--o{ Students : "contains"
    Students ||--o{ Grades : "receive"
    Teachers ||--o{ Grades : "assign"
    Subjects ||--o{ Grades : "relate_to"
    Teachers ||--o{ Teacher_Subjects : "teaches"
    Subjects ||--o{ Teacher_Subjects : "is_taught_by"
    Classes ||--o{ Schedules : "attends"
    Subjects ||--o{ Schedules : "includes"
    Teachers ||--o{ Schedules : "conducts"
    
    %% Новые связи без изменения старых
    Rooms ||--o{ Schedules : "hosts"
    Schedules ||--o{ Attendance : "records"
    Students ||--o{ Attendance : "marked_in"

    Classes {
        int classId PK
        varchar className
        varchar classLevel
    }

    Students {
        int studentId PK
        varchar firstName
        varchar lastName
        char(11) pesel
        varchar email
        int classId FK
    }

    Teachers {
        int teacherId PK
        varchar firstName
        varchar lastName
        char(11) pesel
        varchar email
        varchar phoneNumber
        varchar specialization
    }

    Subjects {
        int subjectId PK
        varchar subjectName
        varchar description
    }

    Rooms {
        int roomId PK
        varchar roomNumber
        int capacity
        varchar roomType
    }

    Teacher_Subjects {
        int assignmentId PK
        int teacherId FK
        int subjectId FK
    }

    Grades {
        int gradeId PK
        decimal gradeValue
        int weight
        varchar comment
        timestamp lastModified
        int studentId FK
        int subjectId FK
        int teacherId FK
    }

    Schedules {
        int lessonId PK
        int roomId FK
        datetime startTime
        datetime endTime
        int classId FK
        int subjectId FK
        int teacherId FK
    }

    Attendance {
        int attendanceId PK
        int studentId FK
        int lessonId FK
        varchar status
    }
