---
name: bill-decoder
description: >
  Use this skill when the user asks about any bill currently moving through the
  U.S. Congress (House or Senate) OR any U.S. state legislature. Retrieves
  current bill information, summarizes it in plain language, and presents
  balanced perspectives from relevant political factions — adapted to the actual
  political landscape of the specific chamber (federal, state, or territory).
  Outputs a formatted Word (.docx) document.
---

# Bill Decoder Skill

## Purpose

Help everyday people understand what their legislature is actually doing. When
given a bill name, number, or topic — at any level of U.S. government — this
skill:

1. Detects whether the bill is **federal** or **state-level**, and which state
2. Researches the bill using web search to get current, accurate information
3. Writes a plain-language summary (2–3 paragraphs max)
4. Explains what the relevant political factions think — and *why* — adapted
   to the actual political makeup of that legislature
5. Produces a clean, readable Word document as the final output

---

## Step 1 — Identify the Bill and Its Level

### Determine: Federal or State?

Look at the bill reference the user provides:

| Clue | Level |
|------|-------|
| "H.R.", "S.", "H.J.Res.", "S.Con.Res." | Federal (U.S. Congress) |
| "Congress", "Senate", "House of Representatives" (no state named) | Federal |
| State name mentioned (e.g., "California AB 123", "Texas SB 44") | State |
| State bill prefixes: AB, SB, HB, HF, SF, LD, etc. | State |
| Topic described with "in [State]" or "my state" | State — ask which state if unclear |

**If unclear**, ask: *"Is this a federal bill or a state-level bill? And if state, which state?"*

### Find the Exact Bill

If the user gives a bill number, use it directly. If they give a topic or
nickname, search for the exact bill name and number first.

**Federal search queries:**
- `"[bill topic] Congress [year] bill"`
- `"congress.gov [bill number]"` — always the authoritative source for federal bills

**State search queries:**
- `"[state] [bill topic] [year] legislature bill"`
- `"[state legislature website] [bill number]"` — use the state's official site (see reference below)
- `"[state] [bill number] [year]"` (e.g., `"California AB 1234 2025"`)

Always confirm you have the right bill. If multiple bills match, list the top
2–3 and ask the user to clarify.

---

## Step 2 — Understand the Political Landscape

This is the most important step that differs between federal and state bills.
**Do not assume every legislature looks like Congress.** Before writing the
perspectives section, assess the actual political makeup of the chamber.

### Federal Bills (U.S. Congress)
The political landscape is always Democrat vs. Republican, with occasional
independents (currently Sens. Bernie Sanders and Angus King caucus with
Democrats). Standard two-party framing applies, but always look for intra-party
divisions (e.g., progressive vs. moderate Democrats; fiscal conservative vs.
mainstream Republicans).

### State Bills — Assess These Factors First

Search for: `"[state] legislature political makeup [year]"` or
`"[state] state senate/house party breakdown"`

**Questions to answer before writing:**

1. **Who controls the chamber(s)?**
   - Is it single-party dominant (e.g., California supermajority Democrats;
     Texas Republican supermajority)?
   - Is it closely divided or split between chambers?

2. **Are there meaningful third parties or caucuses?**
   - Vermont: large Progressive Party caucus
   - Maine: significant independent/unenrolled voters and legislators
   - Alaska: bipartisan majority coalition in the House
   - Nebraska: officially nonpartisan unicameral legislature (see special case below)
   - Some states: active Libertarian, Green, or Independent members

3. **Are regional or ideological factions more meaningful than party lines?**
   - In some one-party-dominant states, the real debate is *within* the
     majority party (e.g., rural vs. urban Democrats in deep-blue states;
     conservative vs. business-wing Republicans in deep-red states)

4. **Is the legislature unicameral?**
   - Nebraska has a single chamber (the Unicameral), officially nonpartisan —
     handle separately (see special cases below)

### Political Landscape Decision Table

Use this to decide how to frame the perspectives section:

| Situation | How to Frame Perspectives |
|-----------|--------------------------|
| Competitive two-party state | Democrat vs. Republican (same as federal) |
| One-party supermajority | Majority party factions + minority party reaction |
| Active third party (e.g., VT Progressives) | Three-way: Dems / Progressives / Republicans |
| Bipartisan coalition majority (e.g., AK House) | Coalition supporters vs. opposition |
| Nebraska Unicameral | Conservative bloc vs. liberal bloc (not party labels) |
| True nonpartisan bill (unanimous or near-unanimous) | Say so — explain the rare consensus |

---

## Step 3 — Research the Bill

Run **at least 4–6 searches** total. For state bills, plan on more — state
coverage is often thinner and requires more digging.

### About the Bill Itself
- What problem is it trying to solve?
- What would it actually do if passed? (Key provisions — be specific)
- Where is it in the legislative process?
- Who sponsored it, what party/faction, and why?

### Political Perspectives Research

**For federal bills:**
- `"[bill name] Democrats support/oppose"`
- `"[bill name] Republicans support/oppose"`
- `"[bill name] progressive criticism"` or `"[bill name] conservative opposition"`
- Look for statements from named members of Congress

**For state bills:**
- `"[state] [bill name or number] [party] support/oppose [year]"`
- `"[state] [bill topic] lawmakers reaction"`
- `"[state legislature] [bill number] vote"`
- Check the state legislature's own website for vote records and floor statements
- Check local and regional newspapers — they often have the best coverage of
  state-level legislative debates

### Prioritized Sources by Level

**Federal:** congress.gov, C-SPAN, congressional press releases, NYT, WSJ,
Washington Post, Politico, The Hill, Roll Call

**State:** State legislature official website (see reference below), state
capitol bureau reporters, local newspapers (e.g., the Sacramento Bee for CA,
Texas Tribune for TX, Boston Globe for MA), state policy nonprofits,
statehouse wire services

---

## Step 4 — Write the Content

Write all sections in full before generating the document.

---

### Section 1: Bill Overview (info box data — not prose)

- Official bill name and number
- **Legislature:** U.S. Congress / [State] Legislature
- **Chamber(s):** House / Senate / Both / Unicameral
- Sponsor name, party/affiliation, district or state
- Current status (e.g., "In Senate Finance Committee"; "Passed Assembly, awaiting Senate floor vote")
- Date of most recent action

---

### Section 2: What This Bill Does (plain-language summary)

Write 2–3 paragraphs. Rules:
- **No jargon.** Imagine explaining to a neighbor who doesn't follow politics.
- Lead with *the problem the bill is trying to solve*, then explain what it does.
- Be specific about real-world effects: who does this affect, what changes, who
  pays or saves money.
- Mention the **level of government** naturally — readers should know if this
  is a state or federal matter and why that distinction matters.
- Do NOT editorialize — this section is factual and neutral.
- Maximum ~200 words.

**Example opening (state bill):** "This bill, moving through the Texas
Legislature, would require all public school districts in the state to provide
at least 30 minutes of daily physical activity for elementary school students.
Currently, Texas law recommends but does not require this — meaning some
districts offer it and others don't..."

---

### Section 3 (and beyond): Political Perspectives

**The number and framing of perspective sections depends on the landscape
you assessed in Step 2.** Here are the templates:

---

#### Template A: Standard Two-Party (federal or competitive state)

Use two sections: **What Democrats Think** and **What Republicans Think**

Each section covers:
- Those who *support* it within the party — what values or priorities does this
  serve? Why does this bill appeal to them philosophically or politically?
- Those who *oppose* it within the party — what is their specific critique?
  Cost? Government overreach? Doesn't go far enough? Political risk?

Be *interpretive*, not just descriptive. Explain the underlying reasoning.
Length per section: 2–4 paragraphs.

---

#### Template B: One-Party Dominant State

Use two sections: **Within the [Majority Party]** and **The [Minority Party]'s
View**

The majority party section is the heart of the document. Explore:
- Which factions within the majority support it and why?
- Which factions within the majority oppose it or have reservations?
  (e.g., urban vs. rural, progressive vs. moderate, labor vs. business wing)
- Is the debate really happening inside the majority caucus?

The minority party section:
- What is the minority's position?
- Do they have any realistic leverage, or are they largely observers?
- Are they united or divided on this?

---

#### Template C: Meaningful Third Party Present

Add a third section for the third party/caucus. Example for Vermont:
- **What Democrats Think**
- **What Progressives Think** (Vermont Progressive Party)
- **What Republicans Think**

Explain each party's distinct angle — don't lump Progressives in with Democrats
even if they sometimes vote together. They often have meaningfully different
reasons for supporting or opposing legislation.

---

#### Template D: Nebraska Unicameral (Nonpartisan Legislature)

Nebraska's legislature has no official party designations on the floor.
Use: **The Conservative Bloc** and **The Liberal Bloc**

- Identify which senators are typically aligned with each bloc
- Explain the factional reasoning, not party-line reasoning
- Note: Nebraska requires a supermajority (33 of 49 votes) to break a filibuster,
  so coalition-building across ideological lines often matters more than pure
  bloc voting

---

#### Template E: Bipartisan or Near-Unanimous Support

If the bill has overwhelming support across party lines:
- **Why There Is Rare Agreement** — explain what makes this bill unusual in
  earning cross-party consensus
- **Remaining Points of Disagreement** — even bipartisan bills usually have
  some dissenting voices; find them and represent them honestly

---

### Final Section: Where Things Stand

One short paragraph (3–5 sentences):
- Current vote count or likelihood of passage
- What happens next procedurally (next committee hearing, floor vote scheduled, etc.)
- Any upcoming deadlines (end of legislative session, veto window, ballot timing)
- For state bills: note if the governor has signaled support or opposition

---

## Step 5 — Generate the Word Document

Use the `docx` npm library. Follow the docx skill guidelines
(see `/mnt/skills/public/docx/SKILL.md`).

**Document design:**

```
Title:    [Bill Name or Short Title] — A Plain-Language Guide
Subtitle: [Federal / State of ___] Legislature  •  [Today's Date]

[Thin colored divider line]

SECTION: Bill at a Glance  (shaded info table)
  - Bill Number:    [e.g., H.R. 1234 / CA AB 567]
  - Legislature:    [U.S. Congress / California Legislature / etc.]
  - Sponsor:        [Name, Party/Affiliation, District]
  - Status:         [Current status with emoji indicator if helpful]
  - Last Action:    [Date]

HEADING 1: What This Bill Does
[Plain-language summary]

HEADING 1: [Perspectives — use appropriate template from Step 4]

HEADING 1: Where Things Stand

[Footer: "Information current as of [date]. For informational purposes only."]
```

**Styling:**
- Font: Arial throughout
- Title: bold, dark navy (#1B2A4A)
- Heading 1: bold, dark blue (#1F4E79)
- Body: 12pt, near-black (#222222)
- "Bill at a Glance" box: light blue shading (#D0E4F7), dark blue label column (#1F4E79 with white text)
- Democrat sections: subtle left border in blue (#1D4ED8)
- Republican sections: subtle left border in red (#B91C1C)
- Third party / nonpartisan sections: subtle left border in purple (#7C3AED) or green (#15803D)
- Page size: US Letter (12240 x 15840 DXA), 1-inch margins
- Never use unicode bullets — use docx numbering config

**File naming:** `[BillID]-decoder.docx`
  - Federal: `HR1234-decoder.docx`, `S456-decoder.docx`
  - State: `CA-AB123-decoder.docx`, `TX-SB44-decoder.docx`

Copy to `/mnt/user-data/outputs/` and present to the user.

---

## Tone & Balance Guidelines

- **Never take a side.** The document should be equally useful to readers
  across the political spectrum.
- **Don't flatten complexity.** If a party is split, show it. If a bill has
  genuine cross-party support, say so.
- **Attribute opinions.** Say "Rep. Smith argued..." not "it is widely believed."
- **Be interpretive, not editorial.** Explaining *why* someone holds a view is
  not the same as endorsing that view.
- **Distinguish facts from positions.** The "What This Bill Does" section is
  facts only. Perspectives sections are clearly framed as such.
- **For state bills:** Avoid applying federal political assumptions to state
  politics. A Republican in Massachusetts is very different from one in
  Alabama. Research the specific legislators and their stated positions.

---

## State Legislature Reference

### Official Legislative Websites (select states)

| State | Website | Bill Format |
|-------|---------|-------------|
| California | leginfo.legislature.ca.gov | AB 123, SB 456 |
| Texas | capitol.texas.gov | HB 123, SB 456 |
| New York | nysenate.gov / assembly.state.ny.us | A1234, S1234 |
| Florida | flsenate.gov / myfloridahouse.gov | HB 123, SB 456 |
| Illinois | ilga.gov | HB 123, SB 456 |
| Pennsylvania | legis.state.pa.us | HB 123, SB 456 |
| Ohio | legislature.ohio.gov | HB 123, SB 456 |
| Georgia | legis.ga.gov | HB 123, SB 456 |
| Michigan | legislature.mi.gov | HB 1234, SB 1234 |
| North Carolina | ncleg.gov | HB 123, SB 123 |
| Virginia | lis.virginia.gov | HB 123, SB 123 |
| Washington | leg.wa.gov | HB 1234, SB 1234 |
| Colorado | leg.colorado.gov | HB 1234, SB 1234 |
| Arizona | azleg.gov | HB 1234, SB 1234 |
| Massachusetts | malegislature.gov | HD 1234, SD 1234 |
| Minnesota | revisor.mn.gov | HF 123, SF 123 |
| Wisconsin | docs.legis.wisconsin.gov | AB 123, SB 123 |
| Nevada | leg.state.nv.us | AB 123, SB 123 |
| Oregon | oregonlegislature.gov | HB 1234, SB 1234 |
| Nebraska | nebraskalegislature.gov | LB 123 (unicameral) |
| Vermont | legislature.vermont.gov | H.123, S.123 |
| Maine | legislature.maine.gov | LD 123 |
| Alaska | akleg.gov | HB 123, SB 123 |

For all other states, search: `"[state name] legislature official website"`

### Special Legislative Structures to Know

- **Nebraska**: Unicameral, officially nonpartisan — 49 senators, no House
- **Alaska**: Legislature sometimes operates under a bipartisan majority coalition
- **Vermont**: Strong Progressive Party presence alongside Democrats and Republicans
- **Maine**: High proportion of independent voters; occasional independent legislators
- **Virginia**: Legislature meets in short annual sessions (60 days in odd years, 30 in even) — bills move fast
- **Texas**: Legislature only meets every two years (odd years) — bills not passed are dead until next session
- **California**: Year-round legislature with powerful committee chairs
- **New York**: Legislature often passes budget as primary vehicle for major policy

---

## Handling Edge Cases

| Situation | What to do |
|-----------|------------|
| Bill is very new, little coverage exists | Note this, summarize what's available, flag information gaps |
| One faction has no notable opposition | Say so honestly — "Republicans have united behind this bill" |
| Bill has been amended significantly | Use the most current version; note major changes from original |
| User gives vague topic with multiple matching bills | List top 2–3 matches with brief description, ask which one |
| Bill failed or was withdrawn | Still decode it — note status clearly, explain why it failed |
| State with unusual structure (NE, AK, VT) | Use the appropriate template from Step 4 |
| Governor has vetoed or threatened veto | Include in "Where Things Stand"; explain override process |
| Local/municipal ordinance (not state) | Note this is a local ordinance, not a state bill; adapt as needed |
| User asks about a ballot initiative | Treat as a bill; note it goes directly to voters, not legislature |

---

## Example Invocations

**Federal:**
- "Decode the SAVE Act"
- "What's in H.R. 22?"
- "Explain the border security bill that's in the Senate right now"
- "Break down S. 1249 for me"

**State:**
- "What's California AB 1955 about?"
- "Explain the Texas school voucher bill"
- "Break down what's happening with the housing bill in my state — I'm in Colorado"
- "What does New York's new climate bill actually do?"
- "Decode LB 388 in Nebraska"
- "What are Vermont legislators saying about the proposed paid leave bill?"

In each case, follow the full workflow: identify level → assess political
landscape → research → write → document.
