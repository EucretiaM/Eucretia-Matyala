```mermaid
classDiagram
    class User {
        +UUID id
        +String name
        +String email
        +String password
        +String role
        +String profilePicture
        +DateTime createdAt
    }

    class Learner {
        +Integer grade
        +String school
        +UUID parentId
    }

    class Teacher {
        +String school
    }

    class Parent { }

    class ContentModule {
        +UUID id
        +String title
        +String description
        +Integer gradeLevel
        +String topic
        +DateTime createdAt
    }

    class Exercise {
        +UUID id
        +UUID contentModuleId
        +String question
        +String[] options
        +String correctAnswer
        +String explanation
    }

    class Assessment {
        +UUID id
        +String title
        +Integer gradeLevel
        +UUID createdBy
        +DateTime dueDate
    }

    class AssessmentItem {
        +UUID assessmentId
        +String question
        +String[] options
        +String correctAnswer
        +Integer marks
    }

    class AssessmentResult {
        +UUID id
        +UUID learnerId
        +UUID assessmentId
        +Float score
        +DateTime submittedAt
        +JSON answers
    }

    class ProgressRecord {
        +UUID id
        +UUID learnerId
        +Date date
        +Integer modulesCompleted
        +Integer exercisesCompleted
        +Float averageScore
    }

    class Achievement {
        +UUID id
        +UUID learnerId
        +String title
        +String description
        +DateTime earnedAt
    }

    %% Relationships
    User <|-- Learner
    User <|-- Teacher
    User <|-- Parent

    Learner "1" --> "0..1" Parent
    Teacher "1" --> "0..*" Learner
    Parent "1" --> "0..*" Learner

    ContentModule "1" --> "0..*" Exercise
    Assessment "1" --> "1..*" AssessmentItem

    Learner "1" --> "0..*" AssessmentResult
    Learner "1" --> "0..*" ProgressRecord
    Learner "1" --> "0..*" Achievement
