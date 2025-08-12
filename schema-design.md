## MySQL Database Design

### Table: appointments
- appointment_id: INT, Primary Key, Auto Increment
- doctor_id: INT, Foreign Key → doctors(id)
- patient_id: INT, Foreign Key → patients(id)
- appointment_time: DATETIME, Not Null
- status: INT (0 = Scheduled, 1 = Completed, 2 = Cancelled)

### Table: admin
- admin_id: INT, Primary Key, Auto Increment
- username: VARCHAR(20), Unique, Not Null
- password_hash: VARCHAR(255), Not Null
- email: VARCHAR(55), Unique, Not Null
- last_login: DATETIME, Nullable

### Table: doctors
- doctor_id: INT, Primary Key, Auto Increment
- first_name: VARCHAR(15), Not Null
- last_name: VARCHAR(15), Not Null
- email: VARCHAR(55), Unique, Not Null
- phone_number: VARCHAR(11), Nullable
- specialization: VARCHAR(15), Not Null
- license_number: VARCHAR(20), Unique, Nullable
- status: INT (0 = Inactive, 1 = Active)
- available_start_time: TIME, Nullable
- available_end_time: TIME, Nullable

### Table: patients
- patient_id: INT, Primary Key, Auto Increment
- first_name: VARCHAR(15), Not Null
- last_name: VARCHAR(15), Not Null
- email: VARCHAR(55), Unique, Nullable
- phone_number: VARCHAR(11), Nullable
- date_of_birth: DATE, Nullable
- gender: ENUM('male', 'female', 'N/A'), Nullable
- address: VARCHAR(100), Nullable

## MongoDB Collection Design

### Collection: prescriptions
```json
{
  "_id": "ObjectId('64abc123456')",
  "patientName": "Albert Williams",
  "appointmentId": 51,
  "medication": "Paracetamol",
  "dosage": "500mg",
  "doctorNotes": "Take 1 tablet every 6 hours.",
  "refillCount": 2,
  "pharmacy": {
    "name": "Walgreens SF",
    "location": "Market Street"
  }
}
### Collection: feedback
```json
{
  "_id": "ObjectId('64def456789')",
  "patientId": 123,
  "doctorId": 45,
  "appointmentId": 51,
  "rating": 4,                    // Integer rating, e.g., 1 to 5
  "comments": "Doctor was very attentive and helpful.",
  "submittedAt": "2025-08-11T14:30:00Z",
  "followUpRequested": false
}
### Collection: logs
{
  "_id": "ObjectId('64f01234567')",
  "timestamp": "2025-08-11T15:00:00Z",
  "level": "INFO",                // e.g., INFO, WARN, ERROR
  "message": "User login successful",
  "userId": 123,                 // Optional, if related to a user
  "ipAddress": "192.168.1.10",  // Optional
  "metadata": {
    "browser": "Chrome",
    "version": "113.0.5678.24"
  }
}
### Collection: messages
{
  "_id": "ObjectId('64f1a234567')",
  "senderId": 45,                // Could be doctor or patient user ID
  "receiverId": 123,             // Recipient user ID
  "appointmentId": 51,           // Optional, if related to appointment
  "content": "Please take your medication after meals.",
  "sentAt": "2025-08-11T16:00:00Z",
  "read": false,                 // Message read status
  "attachments": [               // Optional array of attached files
    {
      "fileName": "personalprescription.pdf",
      "fileUrl": "https://smartclinic.com/files/prescription.pdf"
    }
  ]
}
