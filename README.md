# 🎓 College Enrollment Database

A relational database schema for managing student enrollment, courses, staff, and results at a college — designed from scratch, normalized, and backed by sample data.

![SQL](https://img.shields.io/badge/SQL-MySQL-blue?logo=mysql&logoColor=white)
![Status](https://img.shields.io/badge/status-active-brightgreen)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## 📌 About

Every semester, students enroll in courses, each conducted by an instructor and carrying a fixed number of credits. At the end of the term, students receive marks/grades for every course they took. This project models that entire flow — from staff and department structure down to per-student, per-semester results — as a normalized relational schema.

**[📊 View the full ER Diagram on DrawSQL →](https://drawsql.app/teams/sagar-santosh/diagrams/college)**

<details>
<summary>🖼️ Click to preview schema overview</summary>

```
Staff ──1:N── Department        (via faculty_id)
Staff ──1:N── Subjects          (via faculty_id)
Department ──1:N── Subjects
Student ──1:N── Enrollment
Subjects ──1:N── Enrollment
Semester ──1:N── Enrollment
Enrollment ──1:1── Results
```

</details>

---

## 🗂️ Entities

| Table | Purpose |
|---|---|
| **Staff** | Instructors, HODs, Dean, and Principal |
| **Department** | Academic departments (CE, AIDS, IT, ENTC, ME) |
| **Students** | Enrolled student records |
| **Subjects** | Courses offered, tied to a department and instructor |
| **Semester** | Academic term (semester no. + year) |
| **Enrollment** | Junction table — which student took which subject, in which semester |
| **Results** | Marks and pass/fail status for a completed enrollment |

---

## 📁 Project Structure

```
college-enrollment-db/
├── README.md
└── DATABASE.SQL      # Schema (CREATE TABLE), sample data (INSERT), and queries — all in one file
```

---

## ⚙️ Setup

1. Clone this repo:
   ```bash
   git clone https://github.com/<your-username>/college-enrollment-db.git
   cd college-enrollment-db
   ```

2. Run the schema, then the sample data, in order (foreign keys depend on it):
   ```bash
   mysql -u root -p your_database < schema/create_tables.sql
   mysql -u root -p your_database < data/sample_data.sql
   ```

3. (Optional) Run the sample queries:
   ```bash
   mysql -u root -p your_database < queries/sample_queries.sql
   ```

---

## 🔑 Key Design Decisions

- **`Enrollment` as a junction table** — resolves the many-to-many relationship between `Students` and `Subjects`, while also carrying the `Semester` context.
- **`Results` split from `Enrollment` (1:1)** — lets an enrollment exist with a pending result, rather than forcing every registration to have a grade immediately.
- **Constraints enforced at the schema level** — `CHECK` constraints validate gender, roles, email domains, and mark ranges; `UNIQUE` constraints prevent duplicate semesters and duplicate enrollments (`student_id`, `subject_id`, `semester_id`).

---

## 🛠️ Built With

- MySQL 8.0+ (for `CHECK` constraint support)
- [DrawSQL](https://drawsql.app/) for ER diagram design

---

## 📄 License

This project is open-sourced under the [MIT License](LICENSE).

---

## 👤 Author

**Sagar Santosh**
Feel free to open an issue or pull request if you spot something to improve.
