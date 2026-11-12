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

## Current user clarifications and recovered design

- The correct blogging artifacts were supplied in `Right Contxt Files/` and are now organized under `docs/context/sources/` (chat), `diagrams/` (both diagram pairs), and `docs/presentation/midsem/` (PPTX/team guide and extracts). Original content is preserved. See [source review](../context/blogging-source-review.md) and [exact-column baseline](../design/baseline.md).
- The user explicitly requested removal of obsolete files and a useful implementation structure. The unrelated inventory artifacts, earlier proposal and redundant pointer were removed from the working tree; [the migration note](../context/repository-migration.md) records paths and recoverable history. database/server/client/agents now contain implementation guides, not executable placeholders.
- The settled baseline has 14 tables, 11 conceptual entity sets and two weak entities. Actor identities, scoped API keys, agent ownership, revisions/provenance/citations, threaded comments, separate post/comment votes, human-reviewed edit proposals and audit history define the product. Earlier 12/18-table drafts and the local nine-table proposal are superseded.
- Humans use login/session UI; agents use their own API credentials. Remove the required browser author-selector assumption. Moderator status permissions can remain; a dedicated moderation queue and flag/follow tables were cut.
- The user chooses SQL/MySQL only, React TSX/Tailwind, Node/Express TypeScript, readable parameterized SQL. This overrides the old chat's vanilla/no-TypeScript suggestion. Actual installed versions remain to be recorded; the sources recommend MySQL 8.4.
- No professor sample ER diagram or longer problem statement was supplied. Use the existing Chen model and separate Crow's Foot schema, not a newly invented professor template.
- Preserve source artifacts and justify actual ER/schema deviations. File presence does not certify submission version or professor approval.
- User runs browser/database tests. Provide manual steps and expected outputs without GUI automation/laptop control unless explicitly requested later.
- Five meaningful reusable functions, consistent transactions, useful errors, fidelity, live demo and ten-minute pitch/Q&A are course requirements. Current proposed operation choices are publishPost, addComment, castVote, submitEditProposal and reviewEditProposal; supporting auth/agent/key/read/search operations are still needed.
- The old chat describes largely solo development and later friends helping with slides. Four name placeholders are not proof of four members. Confirm identities when preparing deliverables.
- No final date or final-submission deadline is supplied. The mid-semester slides claim BCNF, but the actual FDs/constraints need verification; do not label that claim a newly completed proof. Session/rate-limit infrastructure must not silently expand the 14-table academic model.
