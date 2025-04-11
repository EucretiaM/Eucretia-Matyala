#  Domain Model Documentation: Math Booster System

##  Purpose

This document defines the **Domain Model** for the **Math Booster System**, ensuring that the model is **complete, clear**, and **covers essential business rules**. The system is designed to support mathematics learning and performance tracking for primary and high school learners.

---

##  Domain Overview

Math Booster is a secure, AI-powered web and mobile platform designed to:
- Improve learners' performance in Mathematics.
- Reduce dropout rates from Grade 10 to 12.
- Support real-time collaboration between teachers and learners.
- Allow content uploading, assignment management, feedback, and performance recommendations.

---

##  Core Domain Entities

### 1. `User`
**Description**: Represents a system user, either a `Learner` or a `Teacher`.

| Field           | Type       | Description                             |
|----------------|------------|-----------------------------------------|
| `user_id`       | UUID       | Unique identifier for the user          |
| `name`          | String     | Full name of the user                   |
| `email`         | String     | Unique email for login                  |
| `password_hash` | String     | Encrypted password                      |
| `role`          | Enum       | `learner` or `teacher`                  |
| `profile_pic`   | URL        | Optional profile picture                |
| `created_at`    | DateTime   | Timestamp of registration               |

**Business Rules**:
- Only teachers can upload assignments and memos.
- Only learners can submit assignments.
- Authentication via a secure third-party API is required for all users.

---

### 2. `Assignment`
**Description**: Tasks or homework created by teachers for learners.

| Field           | Type       | Description                              |
|----------------|------------|------------------------------------------|
| `assignment_id` | UUID       | Unique identifier                        |
| `title`         | String     | Assignment title                         |
| `description`   | Text       | Detailed instructions                    |
| `teacher_id`    | UUID       | Linked to the teacher who created it     |
| `upload_date`   | DateTime   | Date the assignment was uploaded         |
| `due_date`      | DateTime   | Submission deadline                      |

**Business Rules**:
- Assignments must have a due date not earlier than the upload date.
- Assignments are only created by users with the `teacher` role.

---

### 3. `Submission`
**Description**: Learner's response to an assignment.

| Field             | Type       | Description                            |
|------------------|------------|----------------------------------------|
| `submission_id`   | UUID       | Unique identifier                      |
| `assignment_id`   | UUID       | Linked assignment                      |
| `learner_id`      | UUID       | Linked learner                         |
| `file_url`        | URL        | File or document of the submission     |
| `submitted_on`    | DateTime   | Timestamp of submission                |
| `marks`           | Number     | Marks awarded by the teacher           |
| `feedback`        | Text       | Teacher comments and notes             |

**Business Rules**:
- Only learners may submit assignments.
- Submissions cannot occur after the `due_date`.
- Marks are only assigned by teachers.

---

### 4. `Memo`
**Description**: Official solution and explanation to the assignment.

| Field         | Type     | Description                              |
|--------------|----------|------------------------------------------|
| `memo_id`     | UUID     | Unique identifier                        |
| `assignment_id` | UUID   | Associated assignment                    |
| `uploaded_by` | UUID     | Teacher who uploaded the memo            |
| `file_url`    | URL      | Location of the memo document            |
| `uploaded_on` | DateTime | Timestamp of memo upload                 |

**Business Rules**:
- Only teachers may upload memos.
- Memo should be uploaded after the assignment due date.

---

### 5. `Message`
**Description**: Real-time chat between learners and teachers.

| Field         | Type       | Description                             |
|--------------|------------|-----------------------------------------|
| `message_id`  | UUID       | Unique identifier                       |
| `sender_id`   | UUID       | Message sender                          |
| `receiver_id` | UUID       | Message receiver                        |
| `content`     | Text       | Message body                            |
| `timestamp`   | DateTime   | Message send time                       |

**Business Rules**:
- Communication is strictly internal; external tools (e.g., WhatsApp) are disallowed.
- Learner-teacher chats must be logged and POPIA-compliant.

---

### 6. `Recommendation`
**Description**: AI-generated suggestions to improve learner performance.

| Field               | Type       | Description                          |
|--------------------|------------|--------------------------------------|
| `rec_id`            | UUID       | Unique identifier                    |
| `learner_id`        | UUID       | Learner the recommendation is for    |
| `recommendation_text` | Text     | System-generated feedback            |
| `generated_on`      | DateTime   | Timestamp of creation                |

**Business Rules**:
- Recommendations are based on learner performance trends.
- Only available to teachers and the respective learner.

---

### 7. `Leaderboard`
**Description**: Displays top-performing learners based on total score.

| Field         | Type   | Description                              |
|--------------|--------|------------------------------------------|
| `learner_id`  | UUID   | Linked learner                           |
| `total_score` | Number | Aggregated marks                         |
| `ranking`     | Number | Position on leaderboard                  |

**Business Rules**:
- Only top 10 learners displayed.
- Leaderboard is updated after every new graded submission.

---

##  Security & Compliance

- All communication is encrypted.
- Authentication and access control via third-party API.
- No external chat apps used to comply with the **POPIA Act**.
- Only teachers can view and manipulate learner data (admin access).

---

##  Business Logic Summary

- Teachers are the **only admins**: can upload content, view analytics, and communicate directly.
- Learners **cannot communicate with each other** to ensure focus and safety.
- AI powers smart search and **personalized performance recommendations**.
- Every assignment has a lifecycle: upload → submission → marking → feedback/memo.
- System is accessible via secure login only and tracks **audit trails** of all activities.

---

##  Notes on Completeness & Clarity

- All core entities and relationships are defined.
- Business rules are embedded into entity descriptions.
- Domain constraints ensure educational goals are met securely.
- Ready for use in **UML diagrams**, **ERD generation**, or **backend modeling**.


