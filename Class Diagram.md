
# Math Booster - Class Diagram

This diagram models the core structure of the Math Booster platform. It captures the primary entities, their attributes and methods, and the relationships between them.
---
```mermaid
classDiagram
class User {
  +UUID id
  +String name
  +String email
  +String passwordHash
  +String role
  +DateTime lastLogin
  +login()
  +logout()
  +updateProfile()
}

class Learner {
  +String gradeLevel
  +submitAssessment()
  +editSubmission()
  +viewMarks()
  +chatWithEducator()
}

class Educator {
  +uploadAssessment()
  +markSubmission()
  +generateReport()
  +sendNotification()
}

class Assessment {
  +UUID id
  +String title
  +String instructions
  +DateTime deadline
  +UUID educatorId
  +DateTime createdAt
  +isDeadlinePassed()
  +notifyLearners()
}

class Submission {
  +UUID id
  +UUID learnerId
  +UUID assessmentId
  +Text content
  +DateTime timestamp
  +String status
  +Int marks
  +verifyOTP()
  +updateStatus()
}

class Report {
  +UUID id
  +UUID educatorId
  +String criteria
  +DateTime generatedAt
  +JSON reportData
  +generate()
  +download()
}

class OTP {
  +String code
  +UUID userId
  +DateTime expiresAt
  +Boolean verified
  +generate()
  +validate()
}

class Notification {
  +UUID id
  +UUID recipientId
  +String message
  +DateTime timestamp
  +send()
  +markAsRead()
}

User <|-- Learner
User <|-- Educator

Educator "1" --> "0..*" Assessment : creates
Assessment "1" --> "0..*" Submission : receives
Learner "1" --> "0..*" Submission : submits
Submission "1" --> "1" OTP : uses
Educator "1" --> "0..*" Report : generates
User "1" --> "0..*" Notification : receives
