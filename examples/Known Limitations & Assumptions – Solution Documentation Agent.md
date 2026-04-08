# Known Limitations & Assumptions

## Document Metadata

| Field | Value |
|---|---|
| **Solution Name** | Solution Documentaion |
| **Document Type** | Known Limitations & Assumptions |
| **Document Version** | 1.0 |
| **Generated On** | 2026-04-08 |

---

## Known Limitations

### 1. Solution Name Typo
- The registered solution name is **"Solution Documentaion"** (missing "t" in "Documentation").
- This typo is present in the Dataverse solution record, the unique name, and all related component references.
- **Impact:** All automation and documentation references must use the misspelled name to match the registered artifact. Renaming requires caution to avoid breaking existing references.

### 2. No De-duplication Logic
- No de-duplication logic exists in the flow or agent to prevent duplicate documentation records when the same solution name is registered multiple times.
- **Impact:** Multiple documentation sets may accumulate for the same logical solution if `crc55_solution` rows are created repeatedly.

### 3. Hard-Coded Agent Reference
- The Power Automate flow references the Copilot Studio agent by its logical name (`jenssch_solutiondocumentationagent`) directly in the flow definition.
- **Impact:** Deploying to a different environment or renaming the agent requires editing the flow definition. No environment variable was used to abstract this.

### 4. Flow Runs As Calling User
- The Power Automate flow executes under the identity of the user who created the solution row (`runas = Calling User`).
- **Impact:** If the calling user lacks sufficient Dataverse privileges, the flow may fail. Recommended to use a service account for production.

### 5. Bot Component Topic Names Not Retrievable
- The 16 bot components (topics) included in the solution cannot be individually named via the solution component query.
- **Impact:** The exact conversation logic, dialog flows, and topic names within Copilot Studio are not documented here. Manual inspection of the agent in Copilot Studio is required.

### 6. crc55_solutioncategory Has No FK to crc55_solution
- The `crc55_solutioncategory` table schema does not contain a foreign key to `crc55_solution`.
- **Impact:** The relationship between categories and solutions is not enforced at the data model level. The linkage, if any, may be at the application layer only.

### 7. File Storage Is URL-Based
- `crc55_solutionattachment` stores a URL (`crc55_fileurl`) rather than an embedded file.
- **Impact:** Actual file content is stored externally. There is no built-in file management, versioning, or access control for the referenced files.

### 8. No Error Handling in Flow
- The Power Automate flow does not implement explicit error handling (e.g., no "Run After" failure paths, no retry logic, no alerting).
- **Impact:** Silent failures may occur if the agent call fails. Monitoring and alerting must be configured separately.

---

## Assumptions

| # | Assumption |
|---|---|
| 1 | The Copilot Studio agent (`jenssch_solutiondocumentationagent`) is assumed to contain all the documentation generation logic in its bot components. Full topic details require inspection in Copilot Studio. |
| 2 | The `crc55_solution` table is the primary entry point for triggering documentation. No other triggers or manual invocation paths have been identified. |
| 3 | The model-driven app (`Solution Documentation Center`) is the primary UI. No canvas apps or portals are included in this solution. |
| 4 | The `crc55_solutionmetadata` table is used by the agent to enrich documentation with environment and version context. |
| 5 | All documentation persisted by the agent uses the `crc55_solutiondocumentation` table. No other storage mechanisms (e.g., SharePoint, Blob Storage) are used by the solution. |
| 6 | The "Power Platform Solution Vault" solution (ID: 0d7f60d1-b425-f111-88b3-7ced8d3c72c7) is the designated target for storing all generated documentation and is a separate solution in the same environment. |
