# Software Requirements Specification and Design Document
**Project Name:** Vehicle Rental System (VRS)  

---

## 1. Functional Requirements

### 1.1 Overview
This section lists the functional requirements of the Vehicle Rental System (VRS), grouped by actor.

**Actors**
* **Guest:** A visitor who accesses the system but has not logged in.
* **Customer:** A registered member who has logged in successfully and uploaded a Driver's License. A Customer inherits all Guest functions.
* **Rental Staff:** Showroom staff responsible for physical fleet management, license verification, vehicle handover (pick-up), return inspection, and fine collection.
* **Administrator:** The user with the highest authority, responsible for configuring rental/fine policies, managing staff accounts, and overseeing the whole system.
* **System:** The automatic actor that performs programmed tasks on a schedule or on an event, without direct human action.

**Conventions**
* The word **"shall"** indicates a mandatory requirement.
* Requirement IDs use the format `FR-<ACTOR>-<NN>`.

---

### 1.2 Guest
| ID | Requirement |
| :--- | :--- |
| **FR-GST-01** | The system **shall** allow a Guest to register a Customer account by entering personal information (full name, email, phone number, national ID, and password). The system **shall** validate input data and check for duplicate email, phone number, or national ID before creating the account. |
| **FR-GST-02** | The system **shall** allow a Guest to search and filter public vehicles by brand, category (Car, Motorbike, SUV, Van), transmission type, price range, and pick-up/return dates to see whether a vehicle is available. A Guest **shall not** be able to book or reserve a vehicle without logging in. |
| **FR-GST-03** | The system **shall** allow a Guest to view the showroom's rental terms and conditions, deposit policies, insurance packages, opening hours, and branch locations. |
| **FR-GST-04** | The system **shall** allow a Guest to log in by entering an registered email and password, and **shall** then redirect the user to the role of Customer, Rental Staff, or Administrator according to the account. If the credentials are invalid or the account is locked, the system **shall** display an appropriate error message. |

### 1.3 Customer
| ID | Requirement |
| :--- | :--- |
| **FR-CUS-01** | The system **shall** give a Customer all functions of a Guest (searching vehicles and viewing rental policies). |
| **FR-CUS-02** | The system **shall** allow a Customer to view and update personal information (password, avatar, phone number, address) and upload photos of their Driver's License for staff verification. |
| **FR-CUS-03** | The system **shall** allow a Customer with a verified Driver's License to book an available vehicle online by selecting the pick-up date, expected return date, and optional insurance. The system **shall** prevent booking if the vehicle is already reserved for overlapping dates. |
| **FR-CUS-04** | The system **shall** allow a Customer to send a rental extension request, asking for more rental days, for an active rental contract before its due date. |
| **FR-CUS-05** | The system **shall** approve a rental extension request only if the contract is not currently overdue, the maximum rental duration has not been exceeded, and the vehicle has not been pre-booked by another Customer for the requested extension dates. |
| **FR-CUS-06** | The system **shall** allow a Customer to view their rental history, including currently rented vehicles, completed contracts, scheduled return dates, and the status of their online bookings. |
| **FR-CUS-07** | The system **shall** allow a Customer to view detailed invoices and fine records caused by late returns, fuel shortage, or vehicle damages. |
| **FR-CUS-08** | If the system integrates a bank or e-wallet payment gateway, the system **shall** allow a Customer to pay reservation deposits, rental invoices, and penalty fines online. |
| **FR-CUS-09** | The system **shall** allow a Customer to view and download their signed digital rental contract and payment receipts in PDF format. |

### 1.4 Rental Staff
| ID | Requirement |
| :--- | :--- |
| **FR-STF-01** | The system **shall** allow Rental Staff to add a new vehicle to the fleet catalog (License Plate, Brand, Model, Category, Publish Year, Transmission, Seats, Daily Rate, and Odometer). |
| **FR-STF-02** | The system **shall** allow Rental Staff to edit vehicle information and update daily rental prices. |
| **FR-STF-03** | The system **shall** allow Rental Staff to classify a vehicle by category (Sedan, SUV, Motorbike, Van) and assign its required security deposit rate. |
| **FR-STF-04** | The system **shall** allow Rental Staff to assign the parking bay or showroom branch location of a vehicle. |
| **FR-STF-05** | The system **shall** allow Rental Staff to retire a vehicle or send it to maintenance by updating its status to `MAINTENANCE` or `RETIRED`, temporarily or permanently removing it from public booking. |
| **FR-STF-06** | The system **shall** allow Rental Staff to process a vehicle handover (pick-up) at the showroom by scanning the booking QR/code, recording initial odometer mileage and fuel level, and changing the vehicle status to `RENTED`. |
| **FR-STF-07** | The system **shall** allow Rental Staff to record a returned vehicle by entering its license plate or contract ID, recording final odometer mileage, and updating its status to `AVAILABLE` (or `MAINTENANCE` if damaged). |
| **FR-STF-08** | The system **shall** allow Rental Staff to inspect and record the physical condition of a returned vehicle (`INTACT`, `SCRATCHED`, or `DAMAGED`) and fuel level. |
| **FR-STF-09** | The system **shall** allow Rental Staff to create a violation/damage record with a penalty fine when a Customer returns a vehicle late, returns it with insufficient fuel, or causes exterior/interior damage. |
| **FR-STF-10** | The system **shall** allow Rental Staff to record that an invoice or fine has been settled (or deducted from the security deposit) when the Customer pays at the showroom counter. |
| **FR-STF-11** | The system **shall** allow Rental Staff to review and approve or reject Customer Driver's License verification requests. |
| **FR-STF-12** | The system **shall** allow Rental Staff to lock or unlock a Customer's account according to severe violations of rental regulations or unpaid damages. |
| **FR-STF-13** | The system **shall** allow Rental Staff to perform periodic fleet audits to compare the actual physical vehicles parked in the showroom with the status shown in the software. |

### 1.5 Administrator
| ID | Requirement |
| :--- | :--- |
| **FR-ADM-01** | The system **shall** allow an Administrator to add new Rental Staff accounts, edit their information, or lock them. |
| **FR-ADM-02** | The system **shall** allow an Administrator to define roles and assign specific permissions to them (Role-Based Access Control - RBAC). |
| **FR-ADM-03** | The system **shall** allow an Administrator to configure system parameters: required deposit percentage, maximum rental days, overdue hourly/daily penalty rates, and unpaid booking expiration time. |
| **FR-ADM-04** | The system **shall** allow an Administrator to view and export charts and statistical reports on fleet utilization, monthly rental revenue, new Customers, and total fines collected, by month or by year. |
| **FR-ADM-05** | The system **shall** allow an Administrator to back up the database. |
| **FR-ADM-06** | The system **shall** allow an Administrator to restore the system from a backup when a technical failure occurs. |
| **FR-ADM-07** | The system **shall** allow an Administrator to view system audit logs (recording user login history, vehicle price/status modifications, and configuration changes) for security and auditing purposes. |

### 1.6 System (Automatic Functions)
| ID | Requirement |
| :--- | :--- |
| **FR-SYS-01** | The system **shall** scan all active rental contracts periodically every hour and, for each overdue contract, automatically mark its status as `OVERDUE` and calculate the accrued late fee. |
| **FR-SYS-02** | The system **shall** automatically send reminders to Customers by email, SMS, or in-app notification when a rental contract is due soon (24 hours before the return due time), when a contract becomes overdue, or when a booking is confirmed. |
| **FR-SYS-03** | The system **shall** automatically cancel a `PENDING_PAYMENT` booking if the Customer does not pay the required reservation deposit within 30 minutes of booking creation, and **shall** return the vehicle to the `AVAILABLE` state. |
| **FR-SYS-04** | The system **shall** automatically log critical actions of Rental Staff and Administrators (for example, who approved a license, edited daily rates, or closed a contract) for security and error-tracing purposes. |

---

## 2. Non-Functional Requirements

### 2.1 Overview
This section describes the quality requirements of the Vehicle Rental System (VRS): how well the system shall perform, not what functions it provides. Each requirement is written to be measurable where possible.

**Conventions**
* The word **"shall"** indicates a mandatory requirement.
* Requirement IDs use the format `NFR-<CATEGORY>-<NN>`.
* The numeric values (response times, number of users, and so on) are **proposed targets**.
* The "Related FR" column links a requirement to the functional requirements in Section 1.

---

### 2.2 Performance
| ID | Requirement | Related FR |
| :--- | :--- | :--- |
| **NFR-PER-01** | The system **shall** return available vehicle search and filter results within **2.0 seconds** under normal load for a database containing up to 10,000 vehicle records and 100,000 booking records. | FR-GST-02 |
| **NFR-PER-02** | The system **shall** save a vehicle handover (pick-up) or return transaction and calculate final settlement for Rental Staff within **2.0 seconds** after submission. | FR-STF-06, FR-STF-07 |
| **NFR-PER-03** | The system **shall** support at least **200 concurrent active users** browsing and booking vehicles without more than 10% degradation in average response time. | All |
| **NFR-PER-04** | The periodic background scan of active rental contracts (overdue fee calculation and reminder dispatch) **shall** complete within **5 minutes** without degrading online booking performance. | FR-SYS-01, FR-SYS-02 |
| **NFR-PER-05** | The web application **shall** load its initial catalog interface within **2.5 seconds** for at least 95% of user requests under standard network conditions. | All |

### 2.3 Security
| ID | Requirement | Related FR |
| :--- | :--- | :--- |
| **NFR-SEC-01** | The system **shall** store user passwords using a strong, salted hashing algorithm (e.g., **Bcrypt** with cost factor >= 12 or Argon2) and **shall** never store passwords in plain text. | FR-GST-01, FR-GST-04 |
| **NFR-SEC-02** | The system **shall** encrypt all communication between the user's client browser and the server using **HTTPS over TLS v1.2 or TLS v1.3**. | All |
| **NFR-SEC-03** | The system **shall** enforce Role-Based Access Control (**RBAC**). A user **shall not** be able to access functions or data outside their assigned role permissions, including direct URL manipulation. | FR-ADM-02 |
| **NFR-SEC-04** | A Customer **shall** be restricted to viewing only their own personal profile, uploaded Driver's License, rental contracts, and invoice/fine details. | FR-CUS-02, FR-CUS-06, FR-CUS-07 |
| **NFR-SEC-05** | The system **shall** automatically terminate an idle user session after **30 minutes** of inactivity. | FR-GST-04 |
| **NFR-SEC-06** | The system **shall** temporarily lock an account for **15 minutes** after **5 consecutive failed login attempts** to prevent brute-force attacks. | FR-GST-04 |
| **NFR-SEC-07** | The system **shall** sanitize and validate all user inputs to protect against common web vulnerabilities, including SQL Injection, Cross-Site Scripting (XSS), and CSRF. | All |
| **NFR-SEC-08** | The system audit logs of Rental Staff and Administrator actions **shall** be write-once/read-only (immutable via the application), and **shall** only be viewable by an Administrator. | FR-SYS-04, FR-ADM-07 |
| **NFR-SEC-09** | The system **shall not** store any raw credit card, bank, or e-wallet credentials. All online deposit and fine payments **shall** be delegated securely to third-party payment gateways. | FR-CUS-08 |
| **NFR-SEC-10** | Uploaded sensitive identity documents (National ID and Driver's License images) **shall** be stored in private storage buckets accessible only to authenticated Rental Staff and Administrators. | FR-CUS-02, FR-STF-11 |

### 2.4 Reliability, Availability, and Data Integrity
| ID | Requirement | Related FR |
| :--- | :--- | :--- |
| **NFR-REL-01** | The system **shall** maintain an uptime availability of at least **99.5%** during operational hours, excluding scheduled maintenance windows. | All |
| **NFR-REL-02** | The system **shall** enforce transactional **ACID** properties. If a booking payment, handover, or return transaction fails midway, the system **shall** perform an automatic rollback to prevent inconsistent vehicle statuses. | FR-CUS-03, FR-STF-06, FR-STF-07 |
| **NFR-REL-03** | The system **shall** implement database concurrency control (e.g., **pessimistic row-level locking**) to prevent race conditions and ensure **zero double-bookings** when two Customers attempt to book the exact same vehicle for overlapping dates simultaneously. | FR-CUS-03 |
| **NFR-REL-04** | The system **shall** perform automated daily database backups at **00:00** and store copies in two physically isolated locations (local backup server and cloud storage). | FR-ADM-05 |
| **NFR-REL-05** | Following a hardware or system failure, the system **shall** achieve a Recovery Time Objective (**RTO**) of <= 4 hours and a Recovery Point Objective (**RPO**) of <= 24 hours. | FR-ADM-06 |
| **NFR-REL-06** | The system **shall** handle email/SMS notification dispatching asynchronously with automated retry mechanisms, ensuring that notification delivery failures do not block core booking transactions. | FR-SYS-02 |

### 2.5 Usability
| ID | Requirement | Related FR |
| :--- | :--- | :--- |
| **NFR-USA-01** | The primary user interface language **shall** be Vietnamese (with English support), using **UTF-8** character encoding across all displays, forms, and database transactions. | All |
| **NFR-USA-02** | A newly recruited Rental Staff member **shall** be able to perform standard vehicle handover and return inspections without supervision after at most **4 hours** of system training. | FR-STF-06, FR-STF-07 |
| **NFR-USA-03** | The system **shall** display clear, actionable, and non-technical error messages (e.g., *"This vehicle is already booked from 10/11 to 12/11"*) rather than raw system exceptions. | All |
| **NFR-USA-04** | The public portal (Guest and Customer interfaces) **shall** feature a responsive design that displays correctly across major desktop and mobile browsers down to a viewport width of **360px**. | FR-GST-02, FR-CUS-03, FR-CUS-06 |
| **NFR-USA-05** | The system **shall** require explicit user confirmation via modal dialogs before executing non-reversible or destructive actions (e.g., retiring a vehicle, locking a customer account, or modifying penalty rates). | FR-STF-05, FR-STF-12, FR-ADM-01, FR-ADM-03 |

### 2.6 Compatibility and Localization
| ID | Requirement | Related FR |
| :--- | :--- | :--- |
| **NFR-COM-01** | The web application **shall** be fully compatible with the latest two major stable versions of Google Chrome, Microsoft Edge, Mozilla Firefox, and Apple Safari on both desktop and mobile platforms. | All |
| **NFR-COM-02** | The system **shall** interface seamlessly with standard optical/USB QR and barcode scanners for scanning booking codes and Customer IDs at the showroom counter. | FR-STF-06, FR-STF-13 |
| **NFR-COM-03** | The system **shall** fully support Vietnamese localization (L10n), formatting dates as `DD/MM/YYYY`, displaying currency in `VND`, and synchronizing timestamps with Indochina Time (`UTC+7`). | All |
| **NFR-COM-04** | The contract management component **shall** support generating and downloading rental contracts and invoices in standard **PDF** file format. | FR-CUS-09 |

### 2.7 Maintainability and Scalability
| ID | Requirement | Related FR |
| :--- | :--- | :--- |
| **NFR-MNT-01** | The system architecture **shall** follow a modular design (**3-Tier / MVC Architecture**) ensuring low coupling and high cohesion, so that modifications in one module (e.g., Auth, Fleet, Booking, Billing) do not impact others. | All |
| **NFR-MNT-02** | Global business parameters (deposit percentage, maximum rental duration, overdue fine rates) **shall** be dynamically configurable via the Administrator interface without requiring source code modifications or system redeployment. | FR-ADM-03 |
| **NFR-MNT-03** | The codebase **shall** adhere strictly to established coding standards, maintain inline documentation, and provide clean API specifications to facilitate onboarding for team members. | All |
| **NFR-MNT-04** | The database schema and indexing strategy **shall** be designed to scale seamlessly, supporting at least **10,000 vehicles**, **50,000 Customer accounts**, and up to **500,000 booking/contract logs** without architectural redesign. | All |

---

## 3. Data Flow Diagram (DFD)
*(To be updated in the next step)*

## 4. Use Case Diagram
*(To be updated)*

## 5. Class Diagram
*(To be updated)*

## 6. Data Model
*(To be updated)*

## 7. Interface Design Description
*(To be updated)*
