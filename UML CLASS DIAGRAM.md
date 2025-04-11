# 📐 UML Class Diagram: Math Booster System

```mermaid
classDiagram
    class User {
        +String user_id
        +String name
        +String email
        +String password_hash
        +String role  <<enumeration>> // teacher or learner
        +String profile_pic
    }

    class Assignment {
        +String assignment_id
        +String title
        +String description
        +String teacher_id
        +Date upload_date
        +Date due_date
    }

    class Submission {
        +String submission_id
        +String assignment_id
        +String learner_id
        +String file_url
        +Date submitted_on
        +Float marks
        +String feedback
    }

    class Message {
        +String message_id
        +String sender_id
        +String receiver_id
        +Date timestamp
        +String content
    }

    class Recommendation {
        +String rec_id
        +String learner_id
        +String recommendation_text
        +Date generated_on
    }

    class Leaderboard {
        +String learner_id
        +Float total_score
        +int ranking
    }

    class Memo {
        +String memo_id
        +String assignment_id
        +String file_url
        +String uploaded_by
        +Date uploaded_on
    }

    User "1" --> "*" Assignment : uploads
    User "1" --> "*" Submission : submits
    User "1" --> "*" Message : sends
    User "1" <-- "*" Message : receives
    User "1" --> "*" Recommendation : receives
    User "1" --> "1" Leaderboard : has
    Assignment "1" --> "*" Submission : receives
    Assignment "1" --> "1" Memo : has
