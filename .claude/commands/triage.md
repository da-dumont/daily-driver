Process everything in `inbox.md`. Run silently, then show a summary.

## Steps

1. **Read** `inbox.md` — parse every item (lines, bullets, checkboxes, raw text)

2. **Categorize** each item:
   - **Action** — requires a follow-up step by me or someone else
   - **Reference** — information worth keeping but no action needed
   - **Done** — already resolved or no longer relevant
   - **Unclear** — needs clarification before categorizing (flag these, don't guess)

3. **For Actions:**
   - Create a Jira ticket in my personal CTCT board
   - Title: concise action label
   - Description: context from the inbox item
   - Priority: infer from language (words like "urgent", "blocking", "by Friday" → P1/P2; everything else → P3)
   - Link the Jira ticket back in the summary

4. **For Reference:**
   - If it belongs in `context/`: append to the relevant context file
   - If it's a decision: create a new file in `decisions/YYYY-MM-DD-[topic].md`
   - If it's a win: append to today's bragdoc entry

5. **For Done/Unclear:**
   - Done: remove from inbox, no further action
   - Unclear: leave in inbox with a `[?]` prefix and a note on what's unclear

6. **Update `inbox.md`** — remove processed items, keep only unresolved ones (Unclear items stay)

## Output Format

```
## Triage complete — [Date]

### Created in Jira
- [CTCT-XXX] [title] (P[N])
- ...

### Filed as reference
- "[item]" → context/[file] or decisions/[file]

### Logged as wins
- "[item]" → bragdoc/[date]

### Needs clarification (left in inbox)
- [?] [item] — [what's unclear]

### Cleared as done
- [N] items removed
```
