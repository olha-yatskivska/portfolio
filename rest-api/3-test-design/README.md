# Test Design Workbook

## The detailed test design and mapping are maintained in the project spreadsheet.

*  **Interactive View (Google Sheets):** [View Test Analysis Online](https://docs.google.com/spreadsheets/d/1JyiP7P8-y5kIP1tJ0QuwbAnAP90Btph4AVkKAvTaxKc/edit?usp=sharing)


---

### Workbook Structure and Testing Layers

| Tab                     | Test object                       | Level              | Validates                 | Test Type  |
| ----------------------- | --------------------------------- | ------------------ | ------------------------- | ---------- |
| Parsing                 | JSON string                       | unit               | valid syntax              | functional |
| Schema/Contract testing | agreed JSON Schema                | integration        | shape matches agreement   | functional |
| Business Rules          | value semantics/logic             | unit/integration   | value is valid for domain | functional |
| CRUD                    | doc+operation                     | integration        | operation correct         | functional |
| OWASP for API           | Endpoints, HTTP Methods, Payloads | system/integration | risk mitigation           | security   |

