Hospital Management System — C++

This is a console-based Hospital Management System written in C++ to apply File Organization concepts in a practical way without using any database system.

The project shows how real databases manage records inside files using:

Variable-length records
Primary and secondary indexing
Binary search
Space reclamation using an AVAIL list
Record relocation on update
Index persistence between runs

All data is stored and managed manually inside binary files.

What this project is about

Instead of using a DBMS, this system stores Doctors, Patients, and Appointments directly in binary files and builds its own indexing system to access data efficiently.

It simulates how database engines:

Store records
Find records quickly
Reuse deleted space
Handle updates when record size changes
Keep indexes synchronized with files
System roles

Administrator

Add, update, delete doctors and patients
Search by ID or name
View all appointments
Generate reports

Doctor

View and update profile
View appointments
Update availability
Reschedule appointments
View patients

Patient

View and update profile
Search doctors by name or ID
Book appointments
Cancel appointments
Delete own account

Appointment

Connects a patient with a doctor at a specific date and time
How data is stored in files

Each record is stored in this format:

[Record Length][ID][Field Length][Field Data]...

This allows:

Saving only the needed space (variable-length)
Reading records precisely using offsets
Updating records efficiently

The system uses three main data files:

Doctors.bin
Patients.bin
Appointments.bin
Indexing idea

To avoid scanning the whole file every time, the system uses two types of indexes.

Primary Index
Maps: ID → Offset in file

struct PrimaryIndex {
    int id;
    int offset;
};

This allows fast binary search to jump directly to the record inside the file.

Secondary Index
Maps: ID → Name

struct SecondaryIndex {
    int id;
    char name[50];
};

This allows searching by name instead of ID.

Deletion and AVAIL list (space reuse)

When a record is deleted:

It is marked with # inside the file
Its space is stored in the AVAIL list
New records reuse this space instead of appending to the end of the file

This simulates how databases reclaim deleted space.

What happens when the program starts and exits

When the program starts:

All primary and secondary indexes are loaded from files into memory

When the program exits:

All indexes are written back to files

This keeps the system fast and persistent.

Program flow
Start the application
Choose role (Admin / Doctor / Patient)
Login
Credentials are validated
User works inside their dashboard
Logout and exit
How to build and run

Requirements:

Any C++17 compatible compiler

Compile:

g++ main.cpp -o hospital

Run:

./hospital
Main classes in the project
Doctor
Patient
Appointment
PrimaryIndex
SecondaryIndex
What this project proves

This project is a full practical implementation of:

File organization
Indexing techniques
Binary search on files
Space reclamation
Record management without a database

It shows clearly how databases actually work internally.
