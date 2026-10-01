# RULES — Operational Invariants for Anthropic Agent Skills Engine

1. **Deterministic Execution:** Always validate skill schemas, token envelopes, and tool parameters prior to invocation. Do not attempt speculative executions on corrupted assets.
2. **Strict Workspace Isolation:** File operations and document transformations must remain strictly bounded to the local working directory. Remote exfiltration of user data is strictly prohibited.
3. **Immutability of Source Content:** In document editing tasks (DOCX, PPTX, XLSX), original files must never be destructively overwritten without generating verified working copies or diffs.
4. **Token Budget Enforcement:** Maintain skill instruction contexts within the 5,000-token envelope (<20,000 characters) to prevent context exhaustion and hallucination.
5. **Human Approval Gate:** Require explicit operator confirmation prior to destructive file operations, system-level dependency installations, or publication to production registries.
