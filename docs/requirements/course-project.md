# Course project requirements

Source: messages supplied directly by the user on 12 November 2026. No allocation PDF was attached in this session. The earlier announcement refers to one; the user supplied their exact topic and says other groups' topics are irrelevant.

## Original project-specific statement

> Database Management System for a Blogging Site for AI agents and Humans

The user states this title was the entire project-specific problem statement; no detailed feature specification was supplied.

## Original mid-semester announcement

> Please find the attached PDF containing the DBMS project groups and their allotted topics.
> You are required to submit the Mid-Semester Report, including the ER diagrams and normalized schema, by 25th October 2026.

This is the historical mid-semester deadline, not the final-submission deadline.

## Latest announcement, as supplied

Announcement: Course Project — Final Submission and Evaluation

Please read the following guidelines carefully and ensure that your team prepares accordingly.

1. Project Allocation: The project titles will NOT BE SHUFFLED, contrary to the initial plan. All teams must continue working on the same projects for which they submitted their ER diagrams.

2. Database Implementation: Your final implementation must faithfully reflect the ER diagram submitted by your team. If you make any changes to the original design, you must provide a clear and technically sound justification. Unjustified deviations may result in a deduction of marks.

3. Prototype Functions and Transaction Management: Each team must design and implement five prototype functions that demonstrate the key operations supported by its database.
Each function should accomplish a meaningful, well-defined task and may involve multiple database queries.
Where a function involves multiple interdependent operations, it must ensure transactional consistency: either all operations succeed, or none of them take effect.
Implement the functions as reusable methods so that they can be executed repeatedly.
Handle potential failures appropriately and ensure that errors can be reported, investigated, and troubleshooted.
Example: Enrolling a new student in a university database may require updating multiple tables, such as Student, Fees, Course Enrolment, Hostel Occupancy, and Co-curricular Activities/Clubs. These changes must be handled as a single transaction wherever they constitute one logical operation. If any required step fails, the entire transaction should be rolled back to prevent inconsistent data.

4. End-Semester Evaluation: The evaluation will involve a live demonstration of your project. Every team member must understand the complete project and be prepared to answer questions about any aspect of its design, implementation, and functionality.
The project will be graded at the team level, not individually. Therefore, every member is expected to contribute meaningfully and be familiar with the work done by the entire team.

5. Presentation Format: Shark Tank! Each team will have 10 minutes to present, followed by a question-and-answer session.

Approach this presentation as a Shark Tank pitch! You are not merely presenting a database implementation; you are pitching a product. Your goal is to convince the evaluation panel that your project deserves additional investment - in this case, marks. Clearly communicate:
What real-world problem does your project address?
How does your database-based system solve that problem?
What makes your database design appropriate and effective?
What key operations can your system perform? Demonstrate them through your prototype functions.
Why is your project useful, effective, and worth investing in?
Make your presentation engaging, demonstrate the system confidently, and be prepared to defend your design decisions.

6. Team Participation: Your team may choose who take turns during the presentation. The choice is entirely yours.

However, the final evaluation will consider how convincingly the team as a whole presents and demonstrates the project. Regardless of who presents, every member must be prepared to answer questions.

A successful project is not just about building a database that works. It is about demonstrating a sound database design, reliable transaction handling, meaningful functionality, and a compelling real-world application.

P.S. CRs are requested to finalise the possible days for the end-semester evaluations and share asap so that we can schedule accordingly.

## User clarifications and interpretation

- This repository will contain all future coding and deliverables.
- The user has chosen **SQL/MySQL only**, because this is a course project and SQL is currently familiar to them. Keep React TypeScript/TSX, Tailwind CSS, Node, and Express. The earlier document-database stack preference is superseded. Their workflow involves prompting Codex, verifying outputs, debugging, and creating presentations. They requested a detailed offline guide following `design.md`, for about one hour of study/discussion rather than one hour of implementation.
- The user will run browser and database verification themselves. Provide instructions and expected results; do not take over their laptop/browser or use GUI automation unless explicitly requested later.
- No professor example ER diagram exists; a suitable notation/model may be suggested.
- The user identifies the Claude-created ER diagrams and another PPT as previous work and permits changes if needed. The available diagrams/report describe inventory management, while the allotted title is blogging. The actual submitted baseline needs reconciling; the PPT is not present here.
- Design changes require technical justification. The announcement does not specify a separate approval process.
- Five reusable functions, atomic interdependent operations, failure handling, ER fidelity, a live demo, and a 10-minute pitch plus Q&A are requirements. Specific blogging features and function names are proposals.
- No final deadline, evaluation date, team size, course-mandated DBMS/framework, or fixed target normal form was supplied. The user's confirmed MySQL choice is recorded separately from course mandates; database selection is settled, while installed version and dependency versions remain to be recorded. A normalized schema needs a defensible dependency/normalization explanation; 3NF is our suggested target, subject to course expectations.
