---

#  Math Booster – Domain Model (Tabular Description)

This table summarizes the **key domain entities**, their **attributes**, **methods (responsibilities)**, **relationships**, and some essential **business rules** of the system.

---

##  Domain Entities Overview

| Entity         | Attributes                                                                                       | Methods/Responsibilities                                              | Relationships                                                                 |
|----------------|--------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| **User**       | user_id, name, email, password_hash, role, profile_pic                                           | register(), login(), sendMessage(), receiveMessage()                  | Uploads Assignments (Teacher), Submits Submissions (Learner), Sends/Receives Messages, Receives Recommendations, Appears in Leaderboard |
| **Assignment** | assignment_id, title, description, teacher_id, upload_date, due_date                             | upload(), assignToLearners()                                          | Uploaded by User (Teacher), Has many Submissions, Has one Memo                |
| **Submission** | submission_id, assignment_id, learner_id, file_url, submitted_on, marks, feedback                | submit(), updateMarks(), viewFeedback()                               | Linked to Assignment, Submitted by User (Learner)                             |
| **Message**    | message_id, sender_id, receiver_id, timestamp, content                                           | send(), receive()                                                     | Sent and received between Users                                               |
| **Recommendation** | rec_id, learner_id, recommendation_text, generated_on                                       | generate(), view()                                                    | Given to User (Learner)                                                       |
| **Leaderboard** | learner_id, total_score, ranking                                                                | calculateRank(), updateScore()                                        | One per Learner (User)                                                        |
| **Memo**       | memo_id, assignment_id, file_url, uploaded_by, uploaded_on                                      | upload(), view()                                                      | Linked to one Assignment, Uploaded by User (Teacher)                          |

---

##  Business Rules

1. A **User** can have only one **role**: either `"teacher"` or `"learner"` (`role` is an enumeration).
2. Only **Teachers** can **upload Assignments** and **Memos**.
3. Only **Learners** can **submit Submissions** and **receive Recommendations**.
4. One **Assignment** must have **only one Memo**, but may have many Submissions.
5. A **Learner** can appear **only once on the Leaderboard**.
6. **Messages** must occur **between Users**, but learners and teachers cannot message each other outside the platform (POPIA compliance).
7. The **Leaderboard** is ranked based on total_score across Submissions.
8. **Recommendations** are generated based on performance trends in Submissions.

---

## 🧠 Notes

- Methods are indicative; full implementation logic would depend on controller/service layers.
- This domain model enforces separation of concerns between users, learning materials, and communication.
- AI functionality can be abstracted as part of `Recommendation.generate()` or as an external service linked to Learner interactions.
