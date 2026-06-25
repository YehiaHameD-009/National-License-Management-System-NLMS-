# Relational Schema

## Purpose

This document describes the relational representation of the National License Management System (NLMS) domain model.

The purpose of this document is to translate the logical domain entities into relational database structures before moving to the physical database implementation phase.

This schema is based on the requirements analysis, domain analysis, and design decisions documented during the project.

---

## Status

Relational Schema Design Completed.

Ready for Physical Database Design and SQL Server Implementation.

---

## Person

## Person

PersonID (PK)
NationalNumber (UNIQUE, NULL)
FirstName (NOT NULL)
SecondName (NOT NULL)
ThirdName (NOT NULL)
LastName (NOT NULL)
DateOfBirth (NOT NULL)
Gender (NULL)
Nationality (NOT NULL)
Address (NOT NULL)
Phone (NOT NULL)
Email (NULL)
ImagePath (NOT NULL)

---

## Driver

## Driver

DriverID (PK)
PersonID (FK, UNIQUE, NOT NULL)
DriverNumber (UNIQUE, NOT NULL)

---

## User

## User

UserID (PK)
PersonID (FK, UNIQUE, NOT NULL)
Username (UNIQUE, NOT NULL)
Password (NOT NULL)
IsFrozen (NOT NULL)

---

## Service

## Service

ServiceID (PK)
ServiceName (NOT NULL)

---

## Application

## Application

ApplicationID (PK)
ApplicationNumber (UNIQUE, NOT NULL)
ApplicationPersonID (FK, NOT NULL)
ServiceID (FK, NOT NULL)
ApplicationDate (NOT NULL)
ApplicationStatus (NOT NULL)
PaidAppFee (NOT NULL)
ParentAppID (FK, NULL)

---

## LicenseClass

## LicenseClass

LicenseClassID (PK)
ClassName (UNIQUE, NOT NULL)
ClassDescription (NULL)
MinimumAllowedAge (NOT NULL)
ValidityLength (NOT NULL)
ClassFees (NOT NULL)

Constraints:

* CHECK (MinimumAllowedAge > 0)
* CHECK (ValidityLength > 0)
* CHECK (ClassFees >= 0)

---

## License

## License

LicenseID (PK)
LicenseNumber (UNIQUE, NOT NULL)
DriverID (FK, NOT NULL)
ApplicationID (FK, UNIQUE, NOT NULL)
LicenseClassID (FK, NOT NULL)
IssueDate (NOT NULL)
ExpirationDate (NOT NULL)
Notes (NULL)

Constraints:

* CHECK (ExpirationDate > IssueDate)

---

## TestType

## TestType

TestTypeID (PK)
TestName (UNIQUE, NOT NULL)

---

## LicenseClassTest

## LicenseClassTest

LicenseClassTestID (PK)
LicenseClassID (FK, NOT NULL)
TestTypeID (FK, NOT NULL)
TestFee (NOT NULL)

Constraints:

* UNIQUE (LicenseClassID, TestTypeID)
* CHECK (TestFee >= 0)

---

## TestAppointment

## TestAppointment

TestAppointmentID (PK)
ApplicationID (FK, NOT NULL)
TestTypeID (FK, NOT NULL)
UserID (FK, NOT NULL)
AppointmentDate (NOT NULL)

---

## TestAttempt

## TestAttempt

TestAttemptID (PK)
TestAppointmentID (FK, NOT NULL)
TestDate (NOT NULL)
TestResult (NOT NULL)
Score (NULL)

---

## Permission

## Permission

PermissionID (PK)
PermissionName (UNIQUE, NOT NULL)

---

## UserPermission

## UserPermission

UserID (FK, NOT NULL)
PermissionID (FK, NOT NULL)

Constraints:

* PRIMARY KEY (UserID, PermissionID)

---

## AuditLog

## AuditLog

AuditLogID (PK)
UserID (FK, NOT NULL)
ActionType (NOT NULL)
EntityName (NOT NULL)
RecordID (NOT NULL)
ActionDate (NOT NULL)

---

## LicenseHold

## LicenseHold

LicenseHoldID (PK)
LicenseID (FK, NOT NULL)
HoldDate (NOT NULL)
HoldReason (NOT NULL)
FineAmount (NOT NULL)
ReleaseDate (NULL)

Constraints:

* CHECK (FineAmount >= 0)

---

## ServiceTestRequirement

## ServiceTestRequirement

ServiceID (FK, NOT NULL)
TestTypeID (FK, NOT NULL)
Sequence (NOT NULL)

Constraints:

* PRIMARY KEY (ServiceID, TestTypeID)
* CHECK (Sequence > 0)


---
## Note
To Be Updated.....
