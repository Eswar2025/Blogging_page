# Project handoff

> Historical inventory-project record, superseded by [the current blogging-project handoff](handoff.md). Scope, instructions, and next steps below describe the earlier interpretation and are not current project requirements.

Last updated: 2026-11-12.

## Current goal and state

The user moved an Inventory and Warehouse Management System DBMS assignment from Claude into this repository and wants agents to help finish the project, including the report, EER diagrams, database, and code where required.

The current task was to read the saved conversation, organize files, update the README, and add agent instructions. That repository setup is complete. The existing design has not been redesigned or certified against the original assignment. There is no executable implementation or selected DBMS.

Start future work with the latest user request, this note, and newly supplied assignment files. Do not restart the design merely because this is a new session.

## Sources and limitations

| Source | What it provides | Limitation |
| --- | --- | --- |
| [Claude chat PDF](claude-chat.pdf) | Four-page conversation, with small previews of the example diagram and case study | Original attachments, tool outputs, and any unexported conversation are not independently available |
| [Extracted conversation](claude-chat.txt) | Searchable page-marked text from all four pages | Extraction includes interface text and may change reading order; images and formatting remain in the PDF |
| [Part 1 PDF](../report/part1.pdf) | Existing 11-page report, table structures, and a landscape EER diagram on page 6 | Generated draft, not verified against the full assignment |
| [Part 1 Markdown](../report/part1.md) | Editable report text | Flattened tables, incomplete key formatting, no embedded diagram; not publication-ready |
| [Draw.io source](../../diagrams/er_diagram.drawio) and [PNG](../../diagrams/er_diagram.png) | Editable EER diagram and image export | Future changes must synchronize the source, image, and report |

The original prompt, full rubric, and professor's example are missing as standalone files. Chat previews show attachments were supplied previously; their complete contents have not been recovered.

## Confirmed decisions in the saved conversation

- The assignment was for one person.
- The user explicitly requested **Part 1 only**. Part 2 began below the original screenshot and was not developed in the saved conversation.
- The professor's instruction was to produce simplified relations/tables and a proper ER diagram matching the database.
- The selected presentation used an EER style with a weak entity, specialization, aggregation, and `(min,max)` labels. Table structures were to contain no sample rows.
- Claude produced the report and later an editable document. The user requested a shareable editable document and a Draw.io diagram so a friend could edit them.
- The conversation ends with discussion of exporting a Word document. No `.docx` or accessible cloud document is present here. That suggestion is historical context, not an outstanding instruction to create a Word file now.
- Old claims about Claude plan access and sharing have not been reverified; they are not project requirements.

## Inherited design

The draft contains 14 functional requirements (FR1-FR14), 16 business rules (BR1-BR16), and 13 relations:

```text
CATEGORY(Category_ID, Category_Name, Description)
PRODUCT(Product_ID, Product_Name, SKU, Unit_Price, Reorder_Level, Category_ID)
WAREHOUSE(Warehouse_ID, Warehouse_Name, City, Country, Capacity)
INVENTORY(Product_ID, Warehouse_ID, Qty_On_Hand, Last_Updated)
SUPPLIER(Supplier_ID, Supplier_Name, Contact_Person, Email)
SUPPLIER_PHONE(Supplier_ID, Phone_No)
PURCHASE_ORDER(PO_ID, Order_Date, Expected_Date, Status, Supplier_ID)
PURCHASE_ITEM(PO_ID, Line_No, Product_ID, Qty_Ordered, Unit_Cost)
STOCK_MOVEMENT(Movement_ID, Movement_Date, Quantity, Movement_Type, Product_ID, Warehouse_ID)
GOODS_RECEIPT(Movement_ID, PO_ID, Line_No, Qty_Rejected)
DISPATCH(Movement_ID, Customer_Name, Destination)
STOCK_ADJUSTMENT(Movement_ID, Reason, Adjust_Type)
STOCK_TRANSFER(Movement_ID, To_Warehouse_ID, Transfer_Status)
```

These column lists are for orientation, not executable DDL or a replacement for the report's PK/FK definitions.

Important modeling choices:

- `PURCHASE_ITEM` is weak, with composite PK `(PO_ID, Line_No)`.
- `STOCKED_IN` relates products to warehouses, carries quantity/update time, and maps to `INVENTORY(Product_ID, Warehouse_ID, ...)`. Its aggregation connects to movements through `AFFECTS`.
- `STOCK_MOVEMENT` has a composite FK to INVENTORY. Its four subclasses share `Movement_ID` as their PK and FK to the superclass.
- Specialization is intended to be total/disjoint; discriminator values are RECEIPT, DISPATCH, ADJUSTMENT, TRANSFER.
- `SUPPLIER_PHONE` maps a multivalued attribute. Location becomes City/Country. Order total is calculated from item quantity times unit cost.
- Reporting covers stock levels/reorder alerts, procurement, warehouse utilization, movement history, and management summaries.

## Open design questions

These are review findings, not approved schema changes. Resolve them before the affected implementation or final submission.

1. **Receipt quantity:** The stock-effect table increases inventory by `Quantity`, with rejected quantity separate. Clarify whether Quantity is accepted or total delivered, whether order limits count rejected units, and how a fully rejected delivery is represented when movement Quantity must be positive. Reports must use the same definition.
2. **Transfer timing:** Transfers have `In transit` and `Completed` statuses, but the draft describes subtracting/adding stock together. Define when each balance changes, how in-transit stock is represented, and how to prevent applying a transfer twice.
3. **Rule enforcement:** The table structures do not alone enforce exactly one matching subtype, orders having at least one item, cumulative receipt limits, receipt-product agreement, available stock, aggregate capacity, or distinct transfer warehouses. Plan enforcement appropriate to the chosen DBMS.
4. **Capacity and inventory setup:** The report assumes capacity is comparable to a sum of item counts. Confirm units and treatment of mixed products. Define creation of zero-balance inventory pairs before movements and destination inventory creation during transfers.
5. **Report correctness:** The draft calls nullable unique supplier Email a candidate key; review nullability before making that claim. Its literal one-to-one diagram/table wording needs qualification: the multivalued phone attribute creates a table and the derived total is not stored.
6. **Editable report and identity:** Repair Markdown tables and key styling before regenerating exports; Section 6 has no embedded diagram. The PDF says Dinesh with blank roll number, while Markdown identity fields are incomplete. Confirm intended submission details.
7. **Assignment compliance:** Validate notation, cardinalities, exact deliverables, and normalization requirements against the original source. A draft PDF does not establish professor approval or project completion.

## Next useful steps

1. Obtain original problem statement, example diagram, and rubric under `docs/requirements/`. Establish whether Part 1 remains the scope or Part 2 is now required.
2. Compare sources against the draft and resolve applicable questions. Record decisions here and synchronize report and diagram.
3. Restore Markdown tables and explicit PK/FK notation, embed the diagram, and prepare a reproducible export workflow if report editing is requested.
4. For implementation, establish DBMS/version and required stack, then add SQL, sample data, operations, reporting queries, and required application code, with meaningful validation and setup instructions.

Continue work independent of missing inputs under the current request. Do not repeatedly ask for information supplied in later files/messages.

## Repository setup and verification

- Read all four chat pages and the text of the 11-page report. Visually reviewed all chat pages and the report's landscape diagram page.
- Moved five existing artifacts without content edits. Imported Markdown remains unchanged; repairing it is a separate report-editing task.
- Added README, root `AGENTS.md`, this handoff, requirements intake notes, searchable chat extraction, and a temporary-files ignore rule.
- Setup checks cover preserved file hashes, local Markdown links, PDF page counts, and Draw.io XML parsing. No database/application tests apply because no implementation exists.

## Original file locations

| Original root filename | Current path |
| --- | --- |
| `Simplified ER diagram and tables PDF - Claude.pdf` | `docs/context/claude-chat.pdf` |
| `Case Study 7 Inventory and Warehouse Management SystemPart 1.md` | `docs/report/part1.md` |
| `Case_Study_7_Inventory_Warehouse_Part1.pdf` | `docs/report/part1.pdf` |
| `er_diagram.drawio` | `diagrams/er_diagram.drawio` |
| `er_diagram.png` | `diagrams/er_diagram.png` |
