# 🏫 System Zarządzania Szkołą "Lumina"

**Autorzy:** Bohdan Kliukovskyi, Bohdan Krasovskyi  
**Data projektu:** 2026-04-23  
**Status:** Dokumentacja Techniczna (Zadanie 1 i 2)

---

## 1. Opis Systemu
**Lumina** to zintegrowany system bazy danych służący do automatyzacji procesów administracyjnych i dydaktycznych. System opiera się na relacyjnym modelu danych, który łączy ewidencję osób (uczniów i nauczycieli) z logistyką zajęć (plan lekcji, sale) oraz wynikami nauczania.

---

## 2. Architektura Danych (Struktura Tabel)

Na podstawie diagramu ERD, system składa się z następujących kluczowych komponentów:

### 👤 Zarządzanie Osobami
* **Students**: Przechowuje dane uczniów. Kluczowym elementem jest unikalny numer **PESEL** oraz przypisanie do konkretnej klasy (`classId`).
* **Teachers**: Ewidencja kadry pedagogicznej (imię, nazwisko, email, numer telefonu).
* **Classes**: Definiuje grupy uczniów (nazwa klasy i poziom, np. "1A", "Liceum").

### 📚 Program Nauczania i Logistyka
* **Subjects**: Katalog przedmiotów nauczanych w szkole.
* **Teacher_Subjects**: Tabela łącząca, realizująca relację wiele-do-wielu (jeden nauczyciel może uczyć wielu przedmiotów, a jeden przedmiot może być prowadzony przez wielu nauczycieli).
* **Rooms**: Wykaz sal lekcyjnych, w których odbywają się zajęcia.

### 📅 Proces Dydaktyczny
* **Schedules**: Centralna tabela systemu. Łączy nauczyciela, klasę, przedmiot i salę w konkretnym czasie (`startTime`, `endTime`).
* **Attendance**: Moduł śledzenia obecności uczniów na konkretnych lekcjach.
* **Grades**: Ewidencja ocen uczniów. Każda ocena jest powiązana z konkretnym uczniem oraz jednostką lekcyjną (`lessonId`), co pozwala określić jej wagę i wartość.

---

## 3. Wymagania i Integralność Systemu

System implementuje szereg reguł biznesowych zapewniających spójność danych:

1.  **Integralność Tożsamości**: Tabela `Students` wymusza unikalność pola `pesel` (Unique Key), uniemożliwiając dublowanie rekordów.
2.  **Spójność Relacyjna**: Wykorzystanie kluczy obcych (FK) gwarantuje, że np. ocena nie może zostać wystawiona nieistniejącemu uczniowi, a lekcja nie może odbyć się bez przypisanego przedmiotu.
3.  **Logistyka Zajęć**: Tabela `Schedules` pozwala na precyzyjne zarządzanie czasem pracy szkoły, unikając nakładania się terminów dla klas i nauczycieli.
4.  **Wielopoziomowość**: Dzięki tabeli `Teacher_Subjects`, system elastycznie zarządza specjalizacjami kadry.

---

## 4. Historyjki Użytkownika (User Stories)

| Rola | Potrzeba (Cel) | Powiązane Tabele |
| :--- | :--- | :--- |
| **Uczeń** | Chcę sprawdzić w jakiej sali i z jakim nauczycielem mam lekcję o danej godzinie. | `Schedules`, `Rooms`, `Teachers` |
| **Nauczyciel** | Chcę wystawić ocenę uczniowi za konkretną lekcję i określić jej wagę. | `Grades`, `Students`, `Schedules` |
| **Wychowawca** | Chcę zobaczyć listę wszystkich uczniów przypisanych do mojej klasy. | `Classes`, `Students` |
| **Dyrektor** | Chcę sprawdzić, jakie przedmioty są przypisane do danego nauczyciela. | `Teachers`, `Teacher_Subjects`, `Subjects` |
| **Administrator** | Chcę dodać nową salę lekcyjną do systemu, aby móc planować w niej zajęcia. | `Rooms` |

---

## 5. Kluczowe Relacje (Techniczne)

* **One-to-Many (1:N)**: 
    * `Classes` -> `Students` (Jedna klasa ma wielu uczniów).
    * `Schedules` -> `Grades` (Z jednej lekcji może wynikać wiele ocen).
* **Many-to-Many (M:N)**:
    * `Teachers` <-> `Subjects` (poprzez `Teacher_Subjects`).
    * `Students` <-> `Schedules` (poprzez `Attendance`).

---

### Uwagi do implementacji:
* Wszystkie tabele posiadają klucze główne (PK) typu `int` dla zapewnienia wydajności indeksowania.
* Dane kontaktowe (`email`, `phoneNumber`) są przechowywane jako `varchar` dla zachowania elastyczności formatowania.

```mermaid

erDiagram
    direction TB

    Classes ||--o{ Students : "contains"
    Classes ||--o{ Schedules : "attends"
    
    Teachers ||--o{ Teacher_Subjects : "specializes_in"
    Subjects ||--o{ Teacher_Subjects : "is_assigned_to"
    
    Rooms ||--o{ Schedules : "hosts"
    Subjects ||--o{ Schedules : "taught_as"
    Teachers ||--o{ Schedules : "conducts"
    
    Schedules ||--o{ Grades : "resulted_in"
    Students ||--o{ Grades : "earns"
    
    Schedules ||--o{ Attendance : "tracks"
    Students ||--o{ Attendance : "attends"

    Classes {
        int classId PK
        varchar className
        varchar classLevel
    }

    Students {
        int studentId PK
        varchar firstName
        varchar lastName
        varchar(11) pesel UK "Unique"
        varchar email
        int classId FK
    }

    Teachers {
        int teacherId PK
        varchar firstName
        varchar lastName
        varchar email
        varchar phoneNumber
    }

    Subjects {
        int subjectId PK
        varchar subjectName
    }

    Grades {
        int gradeId PK
        decimal gradeValue
        int weight
        int studentId FK
        int lessonId FK 
    }

    Schedules {
        int lessonId PK
        int roomId FK
        int classId FK
        int subjectId FK
        int teacherId FK
        datetime startTime
        datetime endTime
    }

 
