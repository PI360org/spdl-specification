# SPDL – Semantic Process Definition Language

**Version:** 0.1 (Initial Specification)  
**Created:** June 2026  
**Maintained by:** Jean-Marc Erieau, PI360 gUG  
**License:** Dual Licensed
- Non-Commercial: CC BY-SA 4.0 (Free)
- Commercial: Custom Commercial License (Fee Required)

---

## What is SPDL?

SPDL is a semantic framework that makes business process knowledge machine-readable for AI agents.

**The Problem:**
Traditional process documentation (BPMN) describes *what* happens.
But AI agents need to understand *what it means*, *why it matters*, and *how to decide*.

**The Solution:**
SPDL is a 4-layer semantic model:

### Layer 1: Process Model
- Activities, decisions, variants, cycle times
- Who does what, when, where

### Layer 2: Semantic Layer
- Business concepts and their definitions
- Synonyms, relationships, hierarchies
- What things actually *mean* in the business

### Layer 3: Knowledge Layer
- Business rules (decision logic)
- Risks and controls
- Context dependencies
- Where knowledge comes from

### Layer 4: Agent Layer
- AI agent blueprints
- Execution specifications
- Escalation rules
- KPI definitions

---

## Why SPDL?

**AI without context is scalable randomness.**

When you give an AI agent a BPMN diagram alone:
- ❌ It doesn't understand when to escalate
- ❌ It makes decisions without business context
- ❌ It can't explain its logic
- ❌ It fails on edge cases

When you give it SPDL:
- ✅ It understands business meaning
- ✅ It knows when to escalate and to whom
- ✅ It can explain its decisions
- ✅ It handles edge cases with context

---

## SPDL in Action: Example

### Goods Receipt Process (SAP MM)

**Without SPDL:**
```
Activity: "Post Goods Receipt"
System: SAP MM
Duration: 5 minutes
```

**With SPDL:**
```json
{
  "activity": "Post Goods Receipt",
  "semanticType": "AccountingRelevantInventoryPosting",
  "businessMeaning": "Record inventory received in accounting system",
  "role": "Warehouse Lead",
  "duration": "5 minutes",
  "inputObjects": ["GoodsReceipt", "PurchaseOrder"],
  "outputObjects": ["AccountingEntry"],
  "decision": "Quality acceptable?",
  "businessRule": "IF received_condition = 'Acceptable' AND variance < 2% THEN post ELSE escalate",
  "risk": "Damaged goods undetected",
  "control": "Quality inspection before posting",
  "kpisAffected": ["inventory_accuracy", "cycle_time"],
  "systemsInvolved": ["SAP MM (MIGO)"],
  "escalationTrigger": "IF variance > 2% OR condition != 'Acceptable' THEN escalate_to_QualityEngineer"
}
```

Now an AI agent can:
- ✅ Understand when to post automatically
- ✅ Know when to escalate to Quality
- ✅ Explain its decision
- ✅ Reduce manual work by 80%

---

## Quick Start

### 1. Understand SPDL Structure

See `/specification/spdl-schema-v0.1.json` for the complete schema.

### 2. See Examples

Browse `/examples/` for real process models in SPDL format:
- `goods-receipt.spdl.json` – SAP MM process
- `invoice-processing.spdl.json` – Finance process
- `sponsorship-process.spdl.json` – Business development

### 3. Create Your Own

Use the schema to model your own processes:

```bash
# Copy example
cp examples/goods-receipt.spdl.json my-process.spdl.json

# Edit with your process data
# Validate against schema
```

---

## SPDL Schema

### Layer 1: Process Model

```json
{
  "processId": "unique_identifier",
  "processName": "Process Name",
  "purpose": "Why does this process exist?",
  "trigger": "What starts the process?",
  "outcome": "What is the desired outcome?",
  "frequency": "How often does it run?",
  "volume": "How many cases per period?",
  "roles": ["Role 1", "Role 2"],
  "activities": [
    {
      "id": "activity_1",
      "name": "Activity Name",
      "performer": "Role",
      "duration": "Time estimate",
      "sequence": 1
    }
  ],
  "decisions": [
    {
      "id": "decision_1",
      "question": "What is being decided?",
      "outcomes": ["Yes", "No"],
      "frequency": "How often each path?"
    }
  ]
}
```

### Layer 2: Semantic Layer

```json
{
  "semanticConcepts": [
    {
      "id": "concept_1",
      "name": "Concept Name",
      "definition": "Clear business definition",
      "synonyms": ["Synonym 1", "Synonym 2"],
      "relatedConcepts": ["concept_2", "concept_3"],
      "hierarchy": {
        "parent": "ParentConcept",
        "children": ["ChildConcept"]
      }
    }
  ],
  "businessObjects": [
    {
      "id": "object_1",
      "name": "Business Object Name",
      "attributes": ["attr1", "attr2"],
      "lifecycle": ["Created", "Processed", "Archived"],
      "owner": "Responsible Role"
    }
  ]
}
```

### Layer 3: Knowledge Layer

```json
{
  "businessRules": [
    {
      "id": "rule_1",
      "name": "Rule Name",
      "rule": "IF condition THEN action",
      "businessImpact": "Why does this matter?",
      "owner": "Who enforces this?"
    }
  ],
  "risks": [
    {
      "id": "risk_1",
      "name": "Risk Name",
      "likelihood": "Low|Medium|High",
      "impact": "Low|Medium|High",
      "triggers": ["What causes this risk?"],
      "mitigations": ["How is it controlled?"]
    }
  ]
}
```

### Layer 4: Agent Layer

```json
{
  "agentBlueprints": [
    {
      "agentId": "agent_1",
      "purpose": "What should the agent do?",
      "trigger": "When should it activate?",
      "inputData": ["What data does it need?"],
      "decisions": ["What can it decide?"],
      "actions": ["What can it do?"],
      "escalationTriggers": ["When should it ask for help?"],
      "systems": ["Which systems does it access?"],
      "kpis": ["How do we measure success?"],
      "readinessScore": "0-100 (Is it ready for AI?)"
    }
  ]
}
```

---

## How to Use This Repository

### For Process Modelers:
1. Copy `/examples/goods-receipt.spdl.json`
2. Edit with your process data
3. Validate against `/specification/spdl-schema-v0.1.json`
4. Submit pull request to share

### For Developers:
1. See `/specification/spdl-schema-v0.1.json` for JSON Schema
2. Implement SPDL parser in your language
3. Validate SPDL documents programmatically

### For AI Teams:
1. Export SPDL documents
2. Parse into agent blueprints
3. Generate agent execution specifications
4. Deploy autonomous agents with business context

---

## Governance

**Who can contribute?**
- SPDL specification: Pull requests welcome (Jean-Marc reviews)
- Examples: Open contributions encouraged
- Issues: Report problems, suggest improvements

**License:**
- Specification: CC BY-SA 4.0 (attribute PI360, share-alike)
- Examples: CC BY-SA 4.0
- Code: Your choice

---

## Roadmap

**v0.1 (June 2026):**
- ✅ Core 4-layer model
- ✅ JSON Schema specification
- ✅ 3 working examples
- ✅ Basic documentation

**v0.2 (Q3 2026):**
- [ ] YAML format support
- [ ] XML export
- [ ] Validation tooling
- [ ] More examples (10+)

**v1.0 (Q4 2026):**
- [ ] Official specification
- [ ] Multiple language support
- [ ] Industry standards alignment
- [ ] Toolkit release

---

## Questions?

**About SPDL:**
- See `/specification/spdl-spec.md` for detailed docs
- Check `/examples/` for how it works

**About PI360:**
- Web: https://pi360.org (Coming 2026)
- Email: hello@pi360.org
- LinkedIn: @pi360network

**About this Repository:**
- Issues: Questions, suggestions, bug reports
- Pull Requests: Contributions welcome
- Discussions: Community chat

---

## Citation

If you reference SPDL in academic work:

```
@article{erieau2026spdl,
  title={SPDL: Semantic Process Definition Language for AI-Ready Business Processes},
  author={Erieau, Jean-Marc},
  organization={PI360 – The Process Intelligence Network},
  year={2026}
}
```

---

## License

Dual Licensed:
- Non-Commercial: CC BY-SA 4.0 (Free)
- Commercial: Custom Commercial License (Fee Required)
---

**Created by:** Jean-Marc Erieau  
**Organization:** PI360 – The Process Intelligence Network  
**Date:** June 2026  
**Status:** Open Source (CC BY-SA 4.0)

For the latest version, visit: https://github.com/pi360/spdl-specification
