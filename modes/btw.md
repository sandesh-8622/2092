# Mode: btw

`/btw` is a side channel for mid-conversation notes. It lets them drop information without derailing what they were doing.

## Trigger

They say `/btw [something]` or "btw, [something]" while in the middle of another conversation.

## What to do

1. **Route it silently to the right place** — don't ask where it belongs, just figure it out:
   - Money mention ("spent $12", "got paid", "rent's due") → log to `data/finances.md`
   - Schedule change or upcoming event → log to `data/schedule.md`
   - Reminder request ("remind me to...", "don't let me forget...") → add to `config/reminders.yml`
   - Anything else (mood, observation, loose thought, something that happened) → log to today's daily note under "Notable" or "Open threads"

2. **Acknowledge in one line.** No elaboration, no follow-up questions, no pivot. Examples:
   - "logged."
   - "noted — added to your schedule."
   - "got it, reminder set."
   - "added to finances."
   - "saved to today's note."

3. **Continue the previous conversation** exactly where it left off, as if the side note never happened. Pick up mid-sentence if needed.

## What NOT to do

- Don't turn the btw into a new topic.
- Don't ask clarifying questions unless the note is completely ambiguous (and even then, make your best guess and say what you assumed).
- Don't summarize what you just logged. One line, then back to what you were doing.
- Don't break flow. The whole point is that they can toss something over the fence and it lands without friction.

## Example

> **Conversation in progress:** they're talking about a job application and what to write in their cover letter.
>
> **They say:** `/btw spent $40 on groceries`
>
> **You:** "added to finances. — anyway, for the cover letter, lead with the project you mentioned..."

## Edge cases

- Multiple btw items in one message: log all of them, single combined acknowledgment ("logged a few things"), continue.
- Ambiguous category: default to daily note, mention what you assumed. "dropped that in today's note — not sure if it was schedule or just a thought."
- The btw IS the conversation (they just opened with it): treat it as a normal message, not a side note. Route and log as usual, then ask if there's more.
