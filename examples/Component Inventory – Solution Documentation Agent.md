# Component Inventory

## Document Metadata

| Field | Value |
|---|---|
| **Solution Name** | Solution Documentaion |
| **Unique Name** | SolutionDocumentaion |
| **Solution ID** | 4b98ff8f-fc24-f111-88b3-7ced8d3c72c7 |
| **Document Type** | Component Inventory |
| **Document Version** | 1.0 |
| **Generated On** | 2026-04-08 |

---

## Power Automate Cloud Flow

| Attribute | Value |
|---|---|
| **Name** | When a Solution row is added |
| **ID** | 1dcddf0e-7e26-f111-88b3-7ced8d3c7dc6 |
| **Type** | Modern Flow (Power Automate) |
| **Category** | 5 (Automated Flow) |
| **State** | Activated |
| **Trigger** | Dataverse – Row Added on `crc55_solution` (Organization scope) |
| **Owner** | Alex Baker |
| **Created** | 2026-03-23 |
| **Modified** | 2026-03-23 |
| **Creation Source** | Copilot Studio |
| **Scope** | Organization |

**Actions:**
- `Sends_a_prompt_to_the_specified_copilot_for_processing` — Calls `ExecuteCopilot` on agent `jenssch_solutiondocumentationagent` with message: `"Document the {crc55_solutionname} solution"`.

---

## Copilot Studio Agent

| Attribute | Value |
|---|---|
| **Name** | Solution Documentation Agent |
| **ID** | 0c5b2c9c-fc24-f111-88b3-7ced8d3c72c7 |
| **Component Type** | Bot (10207) |
| **State** | Active |
| **Component State** | Published |

**Bot Components (Topics / Nodes) – 12 registered:**

| Component Object ID | Type |
|---|---|
| 92094f69-7c39-4632-8bce-203862255beb | Bot Component (10208) |
| 7a917688-5a0e-46a7-ae20-24d05b46defc | Bot Component (10208) |
| 243970e1-cd88-4cc7-92fa-3b01f370ddcc | Bot Component (10208) |
| 5c01e3fc-9273-43c5-804c-3c0d6087f4b5 | Bot Component (10208) |
| 60b4714f-4354-41b8-855a-4d78707bbd36 | Bot Component (10208) |
| b3e46ef7-ff32-4265-af34-555f5011f867 | Bot Component (10208) |
| 3a0b7476-aabe-4773-8457-61438203c3d6 | Bot Component (10208) |
| 3f1f7057-e8b2-4db4-9645-73df3d6a148d | Bot Component (10208) |
| 604c14ed-28d2-465a-8401-91b0a9ed2874 | Bot Component (10208) |
| 2d308e91-6cb6-41df-aad0-a9a3aa320a2f | Bot Component (10208) |
| 66e2df04-3af6-4afb-a641-cfa4fc3829db | Bot Component (10208) |
| 23daec24-b722-46c2-af46-d39544845773 | Bot Component (10208) |
| 7ae9905f-0248-4419-a6b3-d99f26d6bd81 | Bot Component (10208) |
| d5e2d2e8-5d7b-48e6-aac5-e4a04ab5b2e2 | Bot Component (10208) |
| 386abe68-fcae-41d9-8a0c-ed6c244776a5 | Bot Component (10208) |
| aa54a4b1-76e8-47eb-badb-fa4a7f0828a7 | Bot Component (10208) |

> **Note:** Individual bot component names and topic details are not exposed via the solution component query. Full topic names require inspection inside Copilot Studio.

---

## Model-Driven App

| Attribute | Value |
|---|---|
| **Name** | Solution Documentation Center |
| **App Module ID** | afe928b0-b525-f111-88b3-7ced8d6ecb14 |
| **Unique Name** | crc55_SolutionDocumentatia6f844fa |
| **Description** | A centralized app for solution owners and platform admins to create, update, and organize all solution documentation and metadata efficiently. |

---

## Connection References

| Logical Name | Connector | Purpose |
|---|---|---|
| `jenssch_AdverseMediaQueryAgent.shared_commondataserviceforapps.d883130156a64d53a16b6134d7f25316` | shared_commondataserviceforapps | Dataverse trigger connection for the Power Automate flow |
| `jenssch_sharedmicrosoftcopilotstudio_6d463` | shared_microsoftcopilotstudio | Copilot Studio agent invocation from the flow |

---

## Dataverse Tables (Custom)

| Logical Name | Display Name |
|---|---|
| `crc55_solution` | Solution |
| `crc55_solutiondocumentation` | Solution Documentation |
| `crc55_solutionmetadata` | Solution Metadata |
| `crc55_solutioncategory` | Solution Category |
| `crc55_solutionattachment` | Solution Attachment |
