# Vibe ADR  
*A modern development rhythm for AI-assisted software creation.*

---

## 🧭 Overview

**Vibe ADR** (Adaptive or Architectural Decision Record) is a lightweight, iterative development method for working with AI coding agents such as **Claude Code** or **GitHub Copilot**.

It bridges the gap between *vibe coding* — the fast, conversational style of AI-driven coding — and *spec-driven development* — the structured, disciplined approach that ensures quality, traceability, and alignment.

Vibe ADR gives you a clear, repeatable loop:
> **Decide → Build → Review → Document → Reset**

Each decision you make (architectural, design, tooling, or process) is captured in a concise **ADR file**, tied directly to commits and used to guide the AI’s future behavior.

---

## 💡 Why Vibe ADR?

AI coding is fast — sometimes too fast.  
Without structure, decisions get lost, architectural drift creeps in, and nobody remembers *why* something was done.

Vibe ADR solves this by:
- Keeping **human intent** explicit and traceable.  
- Letting AI generate and implement code *within defined context*.  
- Ensuring every feature, experiment, or architecture choice has a **documented rationale**.  
- Creating **living documentation** that can regenerate the project’s README or architecture summary at any point in time.  

It’s fast, flexible, and future-proof.

---

## ⚙️ The Vibe ADR Loop

### **1️⃣ Define the Vibe**
Write a high-level `README.md` describing the project’s purpose, goals, and guiding principles — *not* implementation details.  
This is your **north star** and will be used by AI agents for context.

### **2️⃣ Draft a New ADR**
Create a new file (e.g. `/docs/decisions/0001-some-meaningful-name.md`) using the `VIBE_ARD_TEMPLATE.md`.  
Each ADR captures a single meaningful decision:
- **Context:** What problem are we solving?  
- **Decision:** What’s our choice and why?  
- **Alternatives:** What did we reject?  
- **Consequences:** Trade-offs, pros/cons.  
- **Commit Links:** Code that implements it.  
- **Vibe Summary:** The intuitive or emotional principle.  

ADRs aren’t limited to architecture — they can cover **any impactful decision** (language, workflow, library, test approach, infrastructure, etc.).
