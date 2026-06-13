# Administrative Requirements

## Overview

This document summarizes the administrative and management requirements discovered during requirements analysis.

---

## User Management

### Supported Operations

- Add User
- View User
- Update User
- Delete User
- Freeze User
- Assign Permissions

### Business Rules

- A user account must be linked to an existing person.
- Not every person is a system user.
- A frozen user remains in the system but cannot access it.
- Permissions can be assigned to users.

### Open Questions

- Can a person own multiple user accounts?
- Is username required to be unique?
- Is delete physical or logical?

---

## Person Management

### Supported Operations

- Search Person by National Number
- View Person
- Add Person
- Update Person
- Delete Person

### Business Rules

- National Number uniquely identifies a person.
- Duplicate National Numbers are not allowed.

### Open Questions

- Can a person with existing licenses or applications be deleted?

---

## Application Management

### Supported Operations

- Search by Application Number
- Search by National Number
- View Applications
- View Application Details
- Update Application
- Filter by Status

### Business Rules

- Application Number uniquely identifies an application.
- Applications can be filtered by status.

### Open Questions

- Which application fields are editable after creation?

---

## Test Type Management

### Business Rules

- Test types are predefined.
- Test types cannot be added or deleted.
- Test fees can be modified.

---

## License Class Management

### Business Rules

- License classes are predefined.
- License classes cannot be added or deleted.
- Minimum age can be modified.
- Validity period can be modified.
- License fees can be modified.

### Assumptions

- Fee changes affect future applications only.
- Historical applications retain their original fee values.

---

## License Hold

### Business Rules

- A license can be placed on hold.
- Hold operation requires:
  - License Number
  - Hold Reason
  - Hold Date
  - Fine Amount

### Observations

- License Hold behaves as a business event.
- A license may experience multiple hold events throughout its lifetime.

---

## Audit Trail

### Business Rules

- Every system operation must record:
  - User
  - Operation Date

### Observations

- The system must support traceability of actions.
- Audit information applies across the entire system.
