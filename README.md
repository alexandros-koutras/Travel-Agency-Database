# Travel-Agency-Database


---


## 💡 Overview

This project involves the design and implementation of a relational database in MySQL for managing the operations of a travel agency. The database models core entities such as branches, employees, customers (travelers), trips, destinations, and reservations.


---


## ⚙️ Design Decisions

### 1. Branch and Telephone Numbers

Each sub-branch can have one or more phone numbers, so we created a separate entity called TELEPHONE_NUMBERS, connected to SUBBRANCH via a many-to-one (M:1) relationship.

### 2. Employees and Specializations

The EMPLOYEE entity contains information about all employees, uniquely identified by EmployeeID.
It has a one-to-many (1:N) non-identifying relationship with SUBBRANCH, since an employee is assigned to one branch, but the branch’s key is not required to identify an employee.

To represent employee roles, we created specialization entities:

DRIVER

IT_SUPERVISOR

ADMINISTRATOR

TOUR_GUIDE

Each specialization has a one-to-one (1:1) relationship with EMPLOYEE, as each employee has exactly one role, and each role instance corresponds to a single employee.

### 3. Administrators

The ADMINISTRATOR entity has a 1:1 relationship with SUBBRANCH, meaning that each branch is managed by exactly one administrator and vice versa.
A Manager attribute indicates whether a given employee is also the branch manager (YES/NO).

### 4. Tour Guides and Languages

Since a tour guide can speak multiple languages, and each language can be spoken by multiple guides, we modeled this as a many-to-many (M:N) relationship between TOUR_GUIDE and LANGUAGES.

### 5. Drivers

For drivers, the attributes include:

LicenseID: unique code

Type of License: category (e.g., A, B, etc.)

Months of experience and Ability to drive abroad

### 6. Travelers, Offers, and Reservations

The TRAVELER entity connects to OFFER with a many-to-one (M:1) relationship, since multiple travelers may select the same offer.
It also connects to RESERVATION with a one-to-many (1:N) relationship, as one traveler can make multiple reservations.

The RESERVATION entity includes a foreign key to SUBBRANCH (BranchID) for branch tracking. However, this relationship is non-identifying, as BranchID is not part of the primary key.

### 7. Trips and Destinations

TRIP and DESTINATIONS are linked through a many-to-many (M:N) relationship, since:

A trip can include multiple destinations.

A destination can belong to multiple trips.

DESTINATIONS also contains a Next Destination attribute to indicate travel order.
If there is no subsequent stop, the field remains NULL.

### 8. Events

The EVENTS entity uses the store address as its primary key and connects to DESTINATIONS via a foreign key relationship.
This allows the system to record entertainment activities related to each travel destination.

### 9. Sightseeing and Tours

Each SIGHTSEEING location can host multiple tours (1:N relationship with TOURS), for instance, different guided experiences at a large museum.
TOURS also links to TOUR_GUIDE and LANGUAGES with many-to-one (M:1) relationships, since each tour is conducted by one guide in a single language.

### 10. Unique Identifiers

Custom ID attributes were added where the existing attributes were not sufficient for unique identification of records.
