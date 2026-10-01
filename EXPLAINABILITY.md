# EXPLAINABILITY — Anthropic Agent Skills Engine

> **Admissibility & Transparency Report for OpenGAP / Agent Passport**  
> *Agent Name:* Anthropic Agent Skills Engine (`anthropic-agent-skills`)  
> *Specification:* OpenGAP v0.1.0  
> *Domain:* Developer Tools / Agent Extensibility & Document Intelligence  

---

## 1. Overview & Operational Purpose

The **Anthropic Agent Skills Engine** (`anthropic-agent-skills`) provides a production-grade, extensible skill execution runtime designed for document engineering, artifact design, and Model Context Protocol (MCP) integrations. It bridges complex multi-modal user intentions with deterministic procedural workflows, enabling autonomous agents to construct, modify, and verify enterprise-grade documents (DOCX, PPTX, XLSX, PDF), dynamic web artifacts, and standardized tool endpoints.

By encapsulating Anthropic's reference skill implementations into standardized OpenGAP modules, the engine ensures reproducible execution, strict formatting compliance, zero data exfiltration, and full explainability across every stage of artifact generation.

---

## 2. How the Agent Decides (Decision-Making Logic)

Anthropic Agent Skills Engine operates across a deterministic, multi-stage decision pipeline:

```
[Stage 1: Intent & Format Ingestion] ──> [Stage 2: Skill Matching & Activation] ──> [Stage 3: Token Budgeting & Sandboxing]
                                                                                                    │
                                                                                                    ▼
[Stage 6: Multi-Format Serialization] <── [Stage 5: Verification & Guideline Check] <── [Stage 4: Execution & Generation]
```

### 2.1 Ingestion & Intent Analysis
- **Decision:** Parses incoming natural language prompts, referenced document assets, and format constraints to identify target deliverables.
- **Rules:** If target format is explicitly stated (e.g., `.docx`, `.xlsx`, `.pptx`), route directly to dedicated document handlers. If request is ambiguous, prompt user for clarification before generating files.

### 2.2 Skill Selection & Activation
- **Decision:** Matches operational requirements against the 19 registered skill manifests using semantic similarity and strict file extension rules.
- **Rules:** Only activate skills whose prerequisites and execution environments are satisfied. Fallback to general coding patterns if specialized skill requirements are absent.

### 2.3 Sandboxed Execution & Synthesis
- **Decision:** Executes procedural generation scripts (e.g., `docx-js`, `openpyxl`, `canvas`) in isolated runtime workspaces.
- **Rules:** Never run arbitrary package installations without operator confirmation. Enforce dual-width table constraints and DXA coordinate systems on Word documents.

### 2.4 Artifact Verification & Validation
- **Decision:** Validates generated artifacts using headless rendering tools and structural linters before presenting them to the user.
- **Rules:** Confirm file integrity and syntax validity. If rendering anomalies or formatting errors occur, invoke the error correction loop up to 2 iterations before reporting.

---

## 3. Data & Privacy

| Category | Policy / Handling |
|---|---|
| **Input Data** | In-memory processing of user prompts and referenced document files within the local working boundary. |
| **Output Artifacts** | Locally saved files (`.docx`, `.pptx`, `.xlsx`, `.pdf`, `.html`) written directly to the host workspace. |
| **Telemetry & Logging** | Local deterministic debug logs recording tool execution status, latency, and token allocations; no cloud transmission. |
| **Third-Party APIs** | Model inference occurs through secure user-configured API endpoints with zero external telemetry scraping. |

Anthropic Agent Skills Engine complies with operational security and privacy standards:
- **No Cloud Data Exfiltration:** Operates entirely within the local repository workspace without sending proprietary documents to unapproved external endpoints.
- **Epistemic Isolation:** Memory structures and working caches are scrubbed between task sessions to prevent cross-document contamination.
- **Sanitized Model Payloads:** Sensitive identifiers, internal paths, and macro code are sanitized before inclusion in prompt context windows.
- **Data Minimization:** Only contextually relevant portions of large documents (headings, extracted text, targeted tables) are ingested into active memory.

---

## 4. Known Limitations & Failure Modes

Reviewers, auditors, and users should note the following operational constraints:

1. **Complex Legacy Binary Formats**
   - *Limitation:* Proprietary binary formats (`.doc`, `.xls`, `.ppt`) cannot be natively edited without prior conversion to OpenXML standards.
   - *Mitigation:* The engine detects legacy formats and requests user permission to run automated format conversion via LibreOffice or Pandoc before processing.

2. **Large Document Token Envelopes**
   - *Limitation:* Ingesting full documents exceeding several hundred pages may exceed agent context windows or degrade procedural attention.
   - *Mitigation:* The agent applies chunked text extraction and section-by-section processing pipelines to preserve reasoning quality.

3. **Complex Macro & Visual Basic Scripting**
   - *Limitation:* The agent does not execute embedded VBA macros or ActiveX controls inside Office documents due to security sandbox constraints.
   - *Mitigation:* Macros are extracted, preserved, or flagged as non-executable, notifying the user of their presence without executing untrusted bytecode.

4. **Dynamic Font Availability Across Host Environments**
   - *Limitation:* Headless document rendering depends on system font availability, which may cause subtle visual shifts between Linux and Windows hosts.
   - *Mitigation:* The agent embeds web-safe standard font fallbacks and generates standalone PDF previews to guarantee visual parity.

---

## 5. Verification, Safety & Human Oversight

The agent implements comprehensive oversight mechanisms:
- **Real-Time Human Approval Gate:** Mandatory explicit operator confirmation is required prior to overwriting existing documents, running external shell compilers, or executing file deletions.
- **Emergency Session Interrupt:** Users can immediately halt generation pipelines at any time via SIGINT (`Ctrl+C`) or process termination without leaving corrupted temporary files.
- **Step Quota Guardrails:** Multi-turn artifact creation processes are bounded by strict maximum iteration budgets (default: 10 steps) to prevent runaway generation cycles.
- **Structured Audit Logging:** Every skill activation, parameter payload, and tool response is recorded in machine-readable JSON logs for auditing and reproducibility.
