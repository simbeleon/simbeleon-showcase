# AI Agent Use Cases

Concrete examples of agentic workflows and structured AI pipelines I've designed and used. Described at the pattern level — implementation details are internal.

---

## 1. Repository Architecture Audit Agent

**Problem:** As a solo developer, architectural drift is easy to miss — naming conventions slip, signal patterns break, and scene dependencies grow without notice.

**Pipeline:**

```
[Master Plan Document]
        ↓
[Agent: Read architecture rules from plan]
        ↓
[Agent: Scan repo structure and key files]
        ↓
[Agent: Compare actual vs. intended — flag deviations]
        ↓
[Output: Structured deviation report with file + line references]
```

**Output format:** XML-structured report listing each deviation with severity (info / warning / critical), file reference, and recommended action.

**Result:** Catches drift before it becomes technical debt. Runs before any major feature branch is merged.

---

## 2. Smoke Test Generator

**Problem:** Writing smoke tests manually is slow and often skipped. AI can generate a baseline test suite from code structure faster than a human can scaffold it.

**Pipeline:**

```
[Source files / module list]
        ↓
[Agent: Identify public interfaces and entry points]
        ↓
[Agent: Generate smoke test stubs with happy-path + null-input coverage]
        ↓
[Human review: accept / reject / edit per test]
        ↓
[Output: Test file ready for runner]
```

**Key design choice:** AI generates stubs; human approves. The agent doesn't decide what's worth testing — it ensures nothing is forgotten.

---

## 3. Claim Processing Support Pipeline

**Problem:** Warranty claims arrive with inconsistent formatting, missing fields, and varying terminology. Manual triage takes time and introduces human error.

**Pipeline:**

```
[Raw claim input (email / form / document)]
        ↓
[Agent: Extract structured fields — claim type, asset, date, value, description]
        ↓
[Agent: Apply business rules — flag missing fields, detect duplicates, score completeness]
        ↓
[Agent: Generate pre-filled claim summary for human review]
        ↓
[Human decision: approve / request info / reject]
```

**Prompt engineering approach:** System prompt defines the exact output schema in XML. Agent response is validated against schema before being passed downstream. Malformed output triggers a retry with error feedback injected into the next prompt.

**Result:** Faster first-pass triage, fewer back-and-forth emails for missing information.

---

## 4. Documentation Extraction Pipeline

**Problem:** Operational knowledge lives in emails, meeting notes, and informal documents. It needs to be structured to be useful.

**Pipeline:**

```
[Unstructured input: email thread / meeting notes / spec document]
        ↓
[Agent: Identify document type and extract key entities]
        ↓
[Agent: Map entities to target schema (process / owner / deadline / dependency)]
        ↓
[Output: Structured entry ready for knowledge base or tracker]
```

**Used for:** Converting maintenance contract correspondence into structured contract records; extracting action items from operational meeting logs.

---

## 5. Prompt Engineering Pattern: XML Role Framing

For complex multi-step tasks, I structure prompts using XML to define role, context, constraints, and output format explicitly.

**Template pattern:**

```xml
<task>
  <role>You are a warranty claim analyst.</role>
  <context>You will receive a raw claim description in Dutch or English.</context>
  <constraints>
    <item>Extract only information present in the input — do not infer or fill in missing data.</item>
    <item>If a required field cannot be determined, mark it as UNKNOWN.</item>
    <item>Output must be valid XML conforming to the schema below.</item>
  </constraints>
  <output_schema>
    <claim>
      <type></type>
      <asset_id></asset_id>
      <date></date>
      <value></value>
      <description></description>
      <completeness_score></completeness_score>
    </claim>
  </output_schema>
</task>
```

**Why XML over prose:** Hierarchy is explicit. The model doesn't have to infer what "constraints" means relative to "context" — the tags define it. Output validation is straightforward because the expected structure is machine-readable.

---

## Patterns in Common

Across all use cases, the same design choices appear:

- **Defined output schema** — the prompt specifies structure, not just intent
- **Human at the boundary** — AI prepares, human decides on consequential actions
- **Retry logic with feedback** — failed outputs are corrected by injecting the error back into the next call
- **Single-responsibility agents** — each step in a pipeline does one thing; chaining is explicit

---

*These are working patterns, not academic exercises. Each one solved a real problem.*
