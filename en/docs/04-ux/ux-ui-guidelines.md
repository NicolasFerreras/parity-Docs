---
title: "UX/UI Guidelines"
---

# UX/UI Guidelines — Parity

> Parity's tone, identity and principles guide. Reference for all of `04-ux`.

## 1. General identity

| Field | Final definition (universal sales tone, citing no case) |
|---|---|
| **Name** | **Parity** (product as persona) / **parity** (software, e.g. "upload file to parity") / **PARITY** (all-caps variant) — preserve the distinction. Usage: *"Parity is simplicity, quality and precision"* vs *"upload file to parity"* |
| **Short description** | Platform turning messy orders —WhatsApp, mail, PDF, Excel or photo— into validated data ready to export in one click, with no re-typing. |
| **Value proposition** | Messy order in, validated order out. No re-typing, no hidden doubts, with human control to the end. Saves hours, cuts errors, keeps your judgment. |
| **Purpose** | **Parity exists to turn order chaos into operational clarity and give hours back to whoever moves the business forward. Messy order in, validated order out. No re-typing, no hidden doubts.** |
| **Vision** | **To be the invisible standard behind every sale. Orders that understand, load and flow by themselves — with any customer, in any format, at any product-selling company.** |
| **Mission** | **Today we turn scattered messages, spreadsheets and PDFs into one clear, validated, exportable view. We automate the repetitive, assist the critical and respect your judgment to the end.** |

## 2. Brand essence

**Concepts we want to convey:**
Simplicity · Trust · Precision · Efficiency · Transparency · Control · Technology serving people · Order · Fluency · Automation · Validation · Clarity

**Values (4):**
1. **Precision** — Every code recognized, every product found. We don't guess, we flag.
2. **Control** — The person decides. Technology assists. The user has the last word.
3. **Fluency** — From chaotic order to ready spreadsheet in seconds, without switching tools.
4. **Trust** — Visible, traceable, one-click-exportable validation.

## 3. Personality

**If Parity were a person, it would be:**
Professional · Precise · Reliable · Simple · Modern · Direct

**We do NOT want it perceived as:**
Complex · Cold · Replacing · Artificial · Bureaucratic

> Test: does it sound like an efficient colleague lifting work off you, not a robot replacing you?

## 4. Communication tone

**How we speak:**
Clear · Direct · Professional · Simple · Warm

**How we do NOT speak:**
Overly technical · Corporate · Confusing · Exaggeratedly informal

**Examples:**
- ❌ "Our ETL solution with heuristic parsers normalizes heterogeneous SKU ontologies"
- ✅ "Upload the order as it arrives. parity sorts it and you validate in seconds."
- ❌ "End-to-end disruptive automation replacing your management"
- ✅ "We automate the repetitive. You keep control."

## 5. Associated words

**Use:** Precision · Order · Fluency · Trust · Clarity · Efficiency · Control · Automation · Validation · Simplicity

**Avoid:** Replacement · Automagic · Complex · Bureaucratic · "AI deciding for you" — they signal loss of control.

## 6. Product principles (guide design and dev)

1. **Technology assists, the person decides.** Automate the repetitive, flag the ambiguous, never guess.
2. **Flag, don't hide.** Every doubtful match is marked (yellow/red), with visible alternative and editable field.
3. **Don't displace the usual system.** Excel-like grid, 1-click export to the internal format — no forcing ERP/flow changes.
4. **Standardize before sophisticating.** Validated single format first; per-customer rules (units, packs) in v2.

## 7. Criteria for future decisions

Before every design/communication/product decision, ask:
- Does this represent who we are? (precision, control, warmth)
- Does it simplify the experience or add complexity?
- Does it convey trust and control?
- Does it help the user or just sound "innovative"?

## 8. Naming convention (operating rule)

| Context | Form | Example |
|---|---|---|
| Code, technical docs, load CTAs | `parity` lowercase | "Drag file to parity", `api.parity.*` |
| Brand communication, hero, pitch | `Parity` Capitalized | "Parity is operational clarity" |
| Logotype / claim lockup | `PARITY` all-caps if the lockup requires it | `PARITY — Order in, order out` |

---
*Visual reference and detailed copy: `design-system.md` (palette/typography/logos) + `user-flows.md` (8-node flow + user journey).*
