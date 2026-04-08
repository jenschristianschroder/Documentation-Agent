# Security & Governance

## Document Metadata

| Field | Value |
|---|---|
| **Solution Name** | Solution Documentaion |
| **Document Type** | Security & Governance |
| **Document Version** | 1.0 |
| **Generated On** | 2026-04-08 |

---

## Authentication & Authorization

### Dataverse Security
- All custom tables (`crc55_solution`, `crc55_solutiondocumentation`, `crc55_solutionmetadata`, `crc55_solutioncategory`, `crc55_solutionattachment`) use standard Dataverse role-based access control (RBAC).
- Table-level access must be granted to:
  - **Platform admins** – full create/read/update/delete (CRUD) on all tables.
  - **Solution owners** – create/read on `crc55_solution`, read-only on `crc55_solutiondocumentation`.
  - **Copilot Studio Agent runtime** – read on `crc55_solution` and `crc55_solutionmetadata`; create/write on `crc55_solutiondocumentation`.
  - **Power Automate Flow** – runs as **Calling User** (`runas = 1`); the triggering user must have sufficient Dataverse privileges.

### Connection Reference Security
- Connection references bind to named user connections at import time.
- `shared_commondataserviceforapps` must be authenticated with a user or service account that has Dataverse read access on `crc55_solution`.
- `shared_microsoftcopilotstudio` must be authenticated with an account that can invoke the target agent (`jenssch_solutiondocumentationagent`).

### Copilot Studio Agent
- Agent invocation is secured by the Copilot Studio connector; the connection requires a valid Microsoft Entra ID authentication.
- The agent must be configured with appropriate Dataverse table permissions for read/write operations.

---

## Data Governance

| Concern | Implementation |
|---|---|
| **Data ownership** | All records have `ownerid` (user or team). Records created by the agent will be owned by the service connection user. |
| **Soft deletion** | `crc55_solution` supports archiving via `crc55_isarchived` flag. All tables support deactivation via `statecode`. |
| **Audit trail** | Standard Dataverse `createdon`, `modifiedon`, `createdby`, `modifiedby` columns are present on all tables. |
| **Data residency** | Data is stored in the Dataverse environment. Ensure environment region aligns with organizational data residency policies. |
| **PII / sensitive data** | No PII-specific columns identified. Solution names and documentation content should be treated as internal information. |

---

## Access Control Recommendations

- Create a dedicated **Security Role** for "Solution Documentation Contributor" with:
  - Read/Write on `crc55_solution`
  - Read/Write on `crc55_solutiondocumentation`
  - Read on `crc55_solutionmetadata` and `crc55_solutioncategory`
  - Read/Write on `crc55_solutionattachment`
- Create a separate "Solution Documentation Viewer" role with Read-only access to all tables.
- Apply the **Principle of Least Privilege** to connection reference accounts.

---

## Governance Considerations

- **Solution is unmanaged** in the current environment. Promote to managed before deploying to Test or Production environments.
- **No Data Loss Prevention (DLP) policy** configuration was observed in the solution definition. Ensure the environment DLP policy permits the use of `shared_commondataserviceforapps` and `shared_microsoftcopilotstudio` connectors together.
- **Environment Variables:** No environment variables were detected in this solution. Consider introducing environment variables for the agent name (`jenssch_solutiondocumentationagent`) to improve portability across environments.
- **Co-ownership:** The flow owner is currently **Alex Baker** (a named user). For production deployments, flows should be owned by a service account or team to prevent orphaned flows.
