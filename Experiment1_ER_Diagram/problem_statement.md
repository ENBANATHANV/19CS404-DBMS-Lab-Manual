# ER Diagram Workshop – Submission Template



## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

*Business Context:*  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

*Requirements:*  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="2481" height="3508" alt="vijay1 drawio (4)" src="https://github.com/user-attachments/assets/1411d0fc-6175-4cfa-bb30-ab96dce8f934" />



### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Member | MemberID (PK), Name, Phone, Email | Stores details of gym members |
| Program | ProgramID (PK), ProgramName, Description | Represents fitness programs (Yoga, Zumba, etc.) |
| Trainer | TrainerID (PK), Name, Specialization | Trainers who conduct programs and sessions |
| Session | SessionID (PK), SessionDate, StartTime, EndTime, TrainerID (FK) | Individual training sessions |
| Attendance | AttendanceID (PK), SessionID (FK), Status | Attendance recorded for sessions |
| MembershipPlan | MembershipPlanID (PK), PlanName, DurationMonths, Price | Membership plans offered |
| Payment | PaymentID (PK), Amount, PaymentType | Records payments for memberships or sessions |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Member – MembershipPlan (SUBSCRIBES TO) | N:1 | Mandatory for Member | Each member subscribes to one plan |
| Member – Program (JOINS) | M:N | Optional for Member | Members may join multiple programs |
| Trainer – Program (CONDUCTS) | M:N | Optional | Trainers conduct programs |
| Member – Session (BOOKS) | 1:N | Optional | Member may book sessions |
| Trainer – Session (CONDUCTS) | 1:N | Mandatory for Session | Each session has one trainer |
| Session – Attendance (HAS) | 1:N | Mandatory for Attendance | Attendance linked to sessions |
| Member – Payment (MAKES) | 1:N | Mandatory for Payment | Payments belong to members |
| Session – Payment (FOR) | 1:N | Optional | Payment may be for a session |

### Assumptions

- Members subscribe to a membership plan.
- Members may join multiple programs.
- Trainers may conduct multiple programs and sessions.
- Members may book personal training sessions.
- Attendance is recorded for each session.
- Payments are made by members and may relate to sessions.

---

# Scenario B: City Library Event & Book Lending System

*Business Context:*  
The Central Library wants to manage book lending and cultural events.

*Requirements:*  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="3319" height="2349" alt="enbavedi drawio (3)" src="https://github.com/user-attachments/assets/5f6187ee-6356-43be-8ad6-b167b8f1b16e" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Member | MemberID (PK), Name, Phone, Email, Address | Library members who borrow books and attend events |
| Book | BookID (PK), Title, Publisher, Year_of_Publication, CategoryID (FK) | Books available in library |
| Author | AuthorID (PK), AuthorName, Nationality | Authors of books |
| Category | CategoryID (PK), CategoryName | Book categories |
| Loan | LoanID (PK), LoanDate, DueDate, ReturnDate, MemberID (FK), BookID (FK) | Records borrowing details |
| Fine | FineID (PK), FineAmount, PaidStatus, LoanID (FK) | Fines generated for overdue loans |
| Event | EventID (PK), EventName, EventDate, StartTime, EndTime | Library events |
| Speaker | SpeakerID (PK), SpeakerName, Specialization, ContactInfo | Event speakers |
| Room | RoomID (PK), RoomName, Capacity | Rooms used for events |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Member – Loan (BORROWS) | 1:N | Mandatory for Loan | Member borrows books via loans |
| Loan – Book (IS LOANED IN) | N:1 | Mandatory for Loan | Each loan involves one book |
| Loan – Fine (GENERATES) | 1:0..1 | Optional | Fine generated only if overdue |
| Book – Author (WRITTEN BY) | M:N | Mandatory for Book | Books can have multiple authors |
| Book – Category (BELONGS TO) | N:1 | Mandatory for Book | Each book belongs to one category |
| Member – Event (REGISTERS FOR) | M:N | Optional | Members may attend events |
| Event – Speaker (FEATURES) | M:N | Mandatory for Event | Events include speakers |
| Event – Room (HELD IN) | N:1 | Mandatory for Event | Each event occurs in one room |

### Assumptions

- A member can borrow multiple books, but each loan record refers to one book.
- Fines are generated only when a book is returned late.
- A book belongs to one category but may have multiple authors.
- Events are held in one room but may feature multiple speakers.
- Members can register for events but registration is optional.

---

# Scenario C: Restaurant Table Reservation & Ordering

*Business Context:*  
A popular restaurant wants to manage reservations, orders, and billing.

*Requirements:*  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="3308" height="2338" alt="Untitled Diagram drawio (2)" src="https://github.com/user-attachments/assets/923a3a54-ec45-4c86-b614-1b754fb54e00" />





### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Customer | CustomerID (PK), Name, Phone | Customers who make reservations |
| Reservation | ReservationID (PK), Date, Time, Number_of_Guests, CustomerID (FK), WaiterID (FK) | Table reservations made by customers |
| Waiter | WaiterID (PK), Name, Shift | Waiters who serve reservations |
| Order | OrderID (PK), OrderTime, ReservationID (FK) | Orders placed under a reservation |
| Dish | DishID (PK), DishName, Price, CategoryID (FK) | Food items available for order |
| Category | CategoryID (PK), CategoryName | Dish categories (Starter, Main, Dessert) |
| Bill | BillID (PK), FoodCharges, ServiceCharges | Bill generated for a reservation |


### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Customer – Reservation (MAKES) | 1:N | Mandatory for Reservation | One customer can make many reservations |
| Reservation – Waiter (SERVED BY) | N:1 | Mandatory for Reservation | Each reservation served by one waiter |
| Reservation – Order (HAS) | 1:N | Optional | A reservation may have multiple orders |
| Order – Dish (CONTAINS) | M:N | Mandatory for Order | Orders contain multiple dishes |
| Dish – Category (BELONGS TO) | N:1 | Mandatory for Dish | Each dish belongs to one category |
| Reservation – Bill (GENERATES) | 1:1 | Mandatory for Bill | Each reservation generates one bill |

### Assumptions

- Customers must create a reservation before placing orders.
- Each reservation is handled by one waiter.
- A reservation can include multiple orders.
- Each order can include multiple dishes.
- Bills are generated per reservation including food and service charges.

---

## Instructions for Students

1. Complete *all three scenarios* (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using *draw.io / diagrams.net* or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as *a single PDF*
