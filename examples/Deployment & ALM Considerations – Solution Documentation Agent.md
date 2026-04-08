# Deployment & ALM Considerations

## Document Metadata

| Field | Value |
|---|---|
| **Solution Name** | Solution Documentaion |
| **Document Type** | Deployment & ALM Considerations |
| **Document Version** | 1.0 |
| **Generated On** | 2026-04-08 |

---

## Solution State

| Property | Value |
|---|---|
| **Managed** | No (Unmanaged) |
| **Version** | 0.0.0.1 |
| **Publisher Prefix** | crc55 |
| **Target Environment** | Dev (current) |

> **Critical:** This solution is unmanaged. It must be exported as a **Managed Solution** before deployment to Test or Production environments.

---

## Environment Promotion Path

```mermaid
flowchart LR
    DEV[Dev Environment\n(Unmanaged)] -->|Export as Managed| TEST[Test Environment\n(Managed)]
    TEST -->|Validate & Approve| PROD[Production Environment\n(Managed)]
```

---

## Pre-Deployment Checklist

### For All Target Environments

- [ ] Export solution from Dev as a **Managed Solution** (version bumped appropriately).
- [ ] Provision target Dataverse environment with sufficient capacity.
- [ ] Ensure the Copilot Studio agent `jenssch_solutiondocumentationagent` is deployed and published in the target environment.
- [ ] Create and configure the following connection references:
  - `shared_commondataserviceforapps` bound to a valid service account connection.
  - `shared_microsoftcopilotstudio` bound to a valid service account connection.
- [ ] Verify DLP policies allow `shared_commondataserviceforapps` and `shared_microsoftcopilotstudio` in the same policy scope.
- [ ] Assign the Power Automate flow owner to a service account (not a named user).
- [ ] Activate the Power Automate flow after import.
- [ ] Publish the Model-Driven App (`Solution Documentation Center`).

---

## ALM Recommendations

### Source Control
- Store the exported managed solution ZIP in a version-controlled repository (e.g., Azure DevOps, GitHub).
- Use **Power Platform Build Tools** (Azure DevOps) or **GitHub Actions for Power Platform** for CI/CD pipelines.

### Versioning
- Increment the solution version (`Major.Minor.Build.Revision`) with each release:
  - Major: breaking changes to data model or architecture.
  - Minor: new features or components.
  - Build/Revision: bug fixes and patch changes.

### Environment Variables (Recommended Enhancement)
- Introduce an environment variable for the target agent logical name (`jenssch_solutiondocumentationagent`) to avoid hard-coded references across environments.

### Connection References
- All connection references must be re-bound in each environment at import time.
- Use a dedicated service principal or service account for production connection bindings.

### Upgrade vs. Overwrite
- Use **Upgrade** (not Overwrite) when promoting managed solution updates to preserve existing data and configuration.

### Rollback Strategy
- Maintain the previous managed solution version in source control.
- Dataverse supports solution uninstallation (managed), but this will delete all custom table data. Ensure data backups exist before uninstalling.

---

## Post-Deployment Validation

1. Create a test row in `crc55_solution`.
2. Confirm the Power Automate flow triggers successfully.
3. Confirm the Copilot Studio agent is invoked and completes processing.
4. Verify documentation records appear in `crc55_solutiondocumentation` linked to the test solution.
5. Open the **Solution Documentation Center** app and confirm the data is visible and correct.
