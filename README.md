# Travel-Agency-Database


---


## 💡 Overview

This project involves the design and implementation of a relational database in MySQL for managing the operations of a travel agency. The database models core entities such as branches, employees, customers (travelers), trips, destinations, and bookings.


---


## ⚙️ Design Decisions

### 1. Employee Model (Generalization / Specialization)
- A central EMPLOYEE entity contains the common attributes for all employees (Name, Address, VAT Number, etc.), with EmployeeID as the primary key.
- Each employee belongs to one and only one sub-branch (a 1:N Relationship with the SUBBRANCH entity).
- For each employee specialty, a separate entity was created (DRIVER, IT_SUPERVISOR, ADMINISTRATOR, TOUR_GUIDE).
- Each of these specialized entities is connected with a 1:1 relationship to the EMPLOYEE entity, as each employee has only one specialty. This approach ensures
  that each type of employee only has the attributes relevant to them.

### 2. Management of Sub-branches & Staff
- Each sub-branch (SUBBRANCH) can have one or more telephone numbers. This was modeled using a separate TELEPHONE_NUMBERS entity and a 1:N relationship.
- Each sub-branch is managed by one and only one ADMINISTRATOR. This is implemented with a 1:1 relationship between the ADMINISTRATOR and SUBBRANCH entities. The
  Manager attribute in the ADMINISTRATOR entity can be used to indicate if the employee also has managerial duties.

### 3. Trips and Destinations Model
- A trip (TRIP) can include many destinations (DESTINATIONS), and a destination can be part of many different trips. This was implemented with an intermediate
  entity TRIP_has_DESTINATIONS (an M:N Relationship).
- The DESTINATIONS entity includes a Next_Destination attribute that refers to the next destination on the route. This field can be NULL if it is the final
  estination, allowing for the creation of chained routes.

### 4. Tour Management
- A tour guide (TOUR_GUIDE) can speak multiple languages (LANGUAGES). This was modeled with an M:N relationship through the TOUR_GUIDE_has_LANGUAGES entity.
- A tour (TOUR) is conducted by a specific tour guide in a specific language (an M:1 Relationship with TOUR_GUIDE and LANGUAGES).
- At a single attraction (SIGHTSEEING), multiple, different tours can be conducted (a 1:N Relationship with the TOURS entity).

### 5. Reservations and Travelers
- The RESERVATION entity is linked to the SUBBRANCH to record the branch where the booking was made. This relationship is non-identifying, as the BranchID is not
  required to uniquely identify a reservation.
- A traveler (TRAVELER) can make many reservations, but each reservation belongs to a single traveler (a 1:N Relationship).
- A traveler can take advantage of special offers (OFFER), with an M:1 relationship from TRAVELER to OFFER.

6. Primary Keys
- Natural keys were used where feasible (e.g., Company Name in the COMPANY entity).
- In entities where there was no obvious natural key or to simplify relationships, surrogate keys were added, such as TripID, OfferID, ReservationID, etc.
