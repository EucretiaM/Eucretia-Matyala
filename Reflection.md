
```markdown
# Reflection: From Domain Model to Class Diagram

## Overview

This reflection outlines how the conceptual domain model for the **Math Booster** system was translated into a concrete **UML Class Diagram**, using principles of object-oriented design. It highlights how key entities, their attributes, and relationships were mapped, and explains the rationale behind structural decisions.

---

## Domain Model to Class Mapping

Each domain entity identified in the model was mapped directly to a class in the class diagram, preserving its core attributes and relationships.

| Domain Entity       | Class Diagram Representation     |
|---------------------|----------------------------------|
| User                | `User` superclass                |
| Learner             | `Learner` subclass               |
| Teacher             | `Teacher` subclass               |
| Parent              | `Parent` subclass                |
| ContentModule       | `ContentModule`                  |
| Exercise            | `Exercise`                       |
| Assessment          | `Assessment`                     |
| AssessmentItem      | `AssessmentItem`                 |
| AssessmentResult    | `AssessmentResult`               |
| ProgressRecord      | `ProgressRecord`                 |
| Achievement         | `Achievement`                    |

---

## Inheritance and Role Modeling

To model system roles (`Learner`, `Teacher`, `Parent`), we used **inheritance** from a common `User` class. This supports shared attributes (e.g., `name`, `email`, `password`) while allowing role-specific logic and attributes (e.g., `grade` for Learner, `school` for Teacher).

This structure promotes reusability and simplifies authentication and authorization logic by treating all actors as users with a role distinction.

---

## Relationships and Associations

### One-to-Many and One-to-One Links

- **Learner to Parent**: Modeled as `Learner --> Parent` (1:1 or 1:many depending on future flexibility).
- **Teacher to Learner**: A one-to-many relationship where a teacher manages multiple learners.
- **Learner to Assessments/Progress**: Learners are associated with multiple assessment results and progress records.
- **ContentModule to Exercise**: A one-to-many relationship is used to group exercises under a content unit.
- **Assessment to AssessmentItem**: Each assessment contains one or more assessment items.

### Composition

Composition-like relationships were implied where entities are strongly dependent (e.g., `AssessmentItem` cannot exist without an `Assessment`). This was visually represented using UML's directional association.

---

## Design Choices

### UUIDs as Primary Keys

Each class uses UUIDs for unique identification, aligning with best practices in distributed systems and ensuring flexibility for future integration.

### Enum for Roles

The `role` attribute in the `User` class is used to distinguish between `Learner`, `Teacher`, `Parent`, and `Admin`, even though class inheritance also exists. This duality supports both polymorphism and simplified querying or access control.

### Data Types and Structures

- Lists and arrays (e.g., `options: String[]`) were used to model multiple-choice options.
- JSON fields (e.g., answers in `AssessmentResult`) provide flexibility for storing dynamic data formats.

---

## Limitations and Improvements

- **Multiple Parents**: The current model assumes a one-to-one link between learner and parent. Real-world applications may require support for multiple parents/guardians.
- **Assessment Submission Rules**: Logic for attempts, retries, and deadlines could be reflected more explicitly through additional fields or subclasses.
- **Content Versioning**: Not currently modeled; future iterations may require tracking updates to content modules and exercises.

---

## Conclusion

The class diagram successfully reflects the structure and logic defined in the domain model. It captures key relationships, enforces role hierarchies, and sets the foundation for scalable implementation. This translation from domain concepts to
object-oriented structure allows the development team to begin building data models, APIs, and features in a clean and maintainable way.
```

---
