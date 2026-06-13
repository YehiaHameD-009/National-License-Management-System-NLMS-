#Core Entities

Entity Name:
Person

Purpose:
Represents any individual stored in the system.

Important Attributes:
- NationalNo
- FullName
- DateOfBirth
- Address
- Phone
- Email
- Nationality
- ImagePath

Relationships:
- Person can submit many Applications.
- Person may become a Driver.
- Person may be a SystemUser.

Important Notes:
- Acts as a Generalization (Parent Entity).
- Personal information must not be duplicated in the system.

***************************
***************************

Entity Name:
Driver

Purpose:
Represents a person who has been officially licensed by the system.

Important Attributes:
- DriverID
- DriverNumber

Relationships:
- Driver can submit many applications.
- Driver can have many license but not in same class.

Important Notes:
- Acts as a specialization (child entity from Person).
- A person becomes a driver only after the first license is issued
- Driver Number is assingned once
- All future licenses issued to the same person
must be associated with the existing Driver record.

***************************
***************************
Entity Name:
SystemUser

Purpose:
Represents a person who is authorized to access and operate the system.

Important Attributes
- Username
- Password
- IsActive / IsFrozen

RelationShips:
- One Person can be linked to one SystemUser.
- One SystemUser can perform many system operations

Important Notes:
Not every Person is a SystemUser.
User account must be linked to an existing Person.
User account can be frozen without deletion

***************************
***************************

Entity Name:
service

Purpose:
Represents a licensing service offered by the system.

Important Attributes:
- ServiceID
- ServiceName
- ServiceFee

RelationShips:
- One Service can be associated with many Applications.

Important Notes:
- Services define the type of licensing operation requested by applicants.
- Each service may have its own business rules and workflow.

***************************
***************************

Entity Name:
Application.

Purpose:
Represents the formal request submitted by an applicant to obtain a specific licensing service provided by the system.

Important Attributes:
- ApplicationID
- ApplicationNumber
- ApplicationDate
- ApplicationStatus ==> {New-Completed-cancelled}
- PaidFees

RelationShips:
- First issue application must reference one license class.
- one application MAY result one license.
- the application has a recursive relationship with itself.    "Self Referencing Relationship"

Important Notes:
- Applications act as the entry point for all licensing services.
- Every service requires a new application.
- A person may have multiple applications.
- A person cannot have more than one incomplete application of the same service type.

***************************
***************************

Entity Name:
License Class

Purpose:
Represents the classification of driving licenses and defines the requirements,
fees, validity period, and restrictions associated with each class.

Important Attributes:
- LicenseClassID
- ClassName
- MinimumAge
- LicenseFees
- ValidPeriod
- ClassDescription
- PracticalFee

Important Notes:
- Each license class defines its own eligibility requirements, fees, and validity period.

***************************
***************************

Entity Name:
License.

Purpose:
Represents a driving license issued by the system after all required 
conditions and examinations have been successfully completed.

Important Attributes:
- LicenseID
- LicenseNumber
- IssueDate
- ExpiryDate
- IssueType
- Notes
- LicenseStatus
- Photo

Important Notes:
- A driver can't own more than one license in same class.
- A driver can own multiple licenses of different classes.
- License status may change during its lifecycle.
- License can become Held.

***************************
***************************

Entity Name:
TestType

Purpose:
Represents a category of examination required during the licensing process.

Important Attributes:
- TestTypeID
- TestTypeName
- Description
- TestFee

Relationships:
- One TestType can be associated with many TestAttempts.
- One TestType can be associated with many TestAppointments.

Important Notes:
- Vision Test, Theory Test, and Practical Test are predefined test types.

***************************
***************************

Entity Name:
LicenseHold

Purpose:
Represents a hold event applied to a license including the reason, fine amount, and hold date.

Important Attributes:
- HoldID
- HoldDate
- HoldReason
- FineAmount

Relationships:
- One License can have many Hold events.
- Each Hold event belongs to one License.

Important Notes:
- Hold behaves as a business event.
- Hold history should be retained.
- A license may be held multiple times during its lifetime.

***************************
***************************

Entity Name:
TestAttempt

Purpose:
Represents a single attempt made by an applicant to complete a specific test.

Important Attributes:
- attemptID
- Result
- AttemptDate
- Score

Relationships:
- one person can have many testattempt.
- one testType can have many testattempt.
- one testappointment can have one or zero testattempt.

Important Notes:
- The system must retain all test attempts and their outcomes.
- Applicants may perform multiple attempts for the same test type.
- A failed attempt allows the applicant to retake the test.
- Test attempts must follow the required examination sequence.
- Progression to the next test requires successful completion of the current test.

***************************
***************************

Entity Name:
TestAppointment

Purpose:
Represents the scheduling of a test for an applicant.

Important Attributes:
- AppointmentID
- AppointmentDate

Relationships:
- one testtype can have many testappointment.
- one application for many testoppointment.

Important Notes:
- Appointments are assigned manually by a system user.
- Test fees must be paid before scheduling an appointment.
- An applicant cannot have multiple active appointments for the same test.

***************************
***************************

Pending Analysis:
- SystemUser
