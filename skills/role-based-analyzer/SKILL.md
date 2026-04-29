---
name: role-based-analyzer
description: Use when the user wants to analyze and document the current structure of a business field's workflow inside a company, as a precondition for process improvement. Conducts a structured interview covering Roles (Holacracy-style), Artifacts, and Meetings, then writes a single structured markdown report. Invoke with /role-based-analyzer. Use only for static structural analysis — does not cover dynamic relationships across dimensions, timing, or edge cases.
---

# Role-Based Analyzer

## When to use

Invoke this skill when the user wants to understand and document the current structure of a business field within a company (e.g., "finance department", "HR onboarding process", "sales operations") before planning improvements.

## When NOT to use

- The user asks about relationships *between* roles, artifacts, and meetings (cross-dimension dynamics are out of scope)
- The user asks about timing, sequencing, frequency, or durations
- The user asks about edge cases, exceptions, or error flows
- The user wants to redesign or improve the process (this skill captures current state only)

If an out-of-scope question arises during the interview, acknowledge it and note it can be explored in a separate session. Do not attempt to answer it within this skill.

---

## Operating principles

1. **Roles are person-independent.** A Role is a function or position, not a named individual. If the user names a person, gently reframe: "What is the role that person fills?"
2. **Accountabilities must be in `-ing` form.** Each accountability is an ongoing action (e.g., "Reviewing budget submissions", "Maintaining the master schedule"). If the user describes one in another form, paraphrase it correctly and confirm.
3. **`Meeting::Role` must derive from a primary Role.** A Meeting::Role is a meeting-specific manifestation of a primary Role. If a new role appears only in a meeting context, first capture it as a primary Role in Phase A, then reference it in Phase C.
4. **Do not invent entries.** Only record what the user explicitly provides. If a field is unknown or not applicable, mark it as `(not specified)`.
5. **One entity at a time.** Complete all fields for one Role (or Artifact, or Meeting) before moving to the next.

---

## Interview protocol

Begin with a brief orientation:

> "I'll guide you through a structured interview to capture the current structure of this business field across three dimensions: Roles, Artifacts, and Meetings. We'll go through them in order. You can say 'done' at any point when you've listed all entries for a dimension. Ready to start with Roles?"

---

### Phase A — Roles

Ask for the business field name first if not provided.

For each Role, ask these questions in sequence:

1. "What is the name of this role?" *(intuitive name, not necessarily the job title)*
2. "What is the purpose of this role — the ideal state it aims to maintain or achieve?"
3. "What does this role have exclusive control over? These are its domains — areas or assets that cannot be touched without its permission."
4. "What are the ongoing accountabilities of this role — the recurring actions it is expected to perform? Please phrase each one starting with a verb in `-ing` form."
   - Collect as many accountabilities as the user provides.
   - Validate each is in `-ing` form; rephrase gently if not, and confirm.

After completing a Role, ask: "Is there another Role? Or are you done with Roles?"

When the user finishes Roles, ask: "Are there any roles that appear only inside specific meetings — not in the general workflow? We'll capture those as `Meeting::Role` entries in the Meetings phase."

---

### Phase B — Artifacts

Transition with: "Now let's capture the Artifacts — deliverables or submitted items involved in this business field, regardless of format."

For each Artifact, ask:

1. "What is the name of this artifact?"
2. "Is it digital, physical, or either?"
3. "Briefly, what is it? (What it is, not who handles it.)"
4. "Does this artifact have distinct internal parts — chapters, sections, or components that are meaningful to the workflow?" *(if yes, list each part as `Artifact::part`)*

After completing an Artifact, ask: "Is there another Artifact? Or are you done with Artifacts?"

---

### Phase C — Meetings

Transition with: "Finally, let's capture the Meetings — structured gatherings that are part of this business field's workflow."

For each Meeting, ask:

1. "What is the name of this meeting?"
2. "What documents or data are required as preparation for this meeting?" *(requirement documents)*
3. "Who participates in this meeting — not by name, but by criteria: what information or responsibility qualifies someone to attend?"
4. "What is the agenda of this meeting — the actual flow of the meeting, step by step?" *(collect as `Meeting::agenda-item` entries)*
5. "What does this meeting produce? List the output documents (e.g., minutes, decisions, action item lists)."
6. "Are there roles specific to this meeting — such as facilitator, note-taker, or decision-maker?" *(collect as `Meeting::Role` entries; each must reference a primary Role from Phase A)*
   - For each `Meeting::Role`, ask: "Which primary Role from our Phase A list does this correspond to?"
   - If it's entirely new, say: "This sounds like a primary Role we haven't captured yet. Let me add it to the Roles section first." Then capture it with Name/Purpose/Domain/Accountabilities, and reference it here.

After completing a Meeting, ask: "Is there another Meeting? Or are you done with Meetings?"

---

## Writing the report

Once all three phases are complete, confirm with the user:

> "I have all the information. Where should I save the report? (Default: `./<field-name>-analysis.md`)"

Then write a single markdown file with this structure:

```markdown
# <Business Field Name> — Structural Analysis

## Roles

### <Role Name>

- **Purpose:** <one-sentence ideal state>
- **Domain:**
  - <exclusive area or asset>
  - ...
- **Accountabilities:**
  - <...ing ...>
  - ...

---

## Artifacts

### <Artifact Name>

- **Format:** <digital / physical / either>
- **Description:** <brief description>
- **Parts:**
  - <part name and brief description>
  - ...

---

## Meetings

### <Meeting Name>

- **Requirement documents:**
  - <document or data required for preparation>
  - ...
- **Participants:** <criteria for who should attend>
- **Agenda items:**
  - <step description>
  - ...
- **Output documents:**
  - <deliverable produced>
  - ...
- **Meeting::Role:**
  - `<Meeting-Role Name>` ← derived from `<Primary Role Name>`
  - ...
```

Omit any optional sub-section (Parts, Meeting::Role) entirely if no entries were captured for it — do not leave empty bullets.

---

## Closing step

After writing the file, output a brief summary:

> "Report saved to `<path>`. Captured: **N roles**, **M artifacts**, **K meetings**. Please review and let me know if anything needs correction."

Do not add analysis, recommendations, or observations — this skill captures structure only.
