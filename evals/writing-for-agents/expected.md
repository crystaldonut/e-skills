# Expected outcome

Prompt, in this repo: "Review `evals/writing-for-agents/fixture/SKILL.md` with the writing-for-agents skill and list what to change."

The review must name each of these, by rule:

| Line in the fixture | Rule |
|---|---|
| Description lists deploying, shipping, releasing, pushing to production, going live | One trigger per branch: five names for one branch |
| "Deploy checker." in the description | Cut identity the body already carries |
| "You are a careful senior release engineer. Be thorough and write clear output." | No-op |
| Step 1, "Understand the change." | No completion criterion |
| Step 4, "until you are comfortable" | Completion criterion that cannot be checked |
| Step 3, "Don't skip", "Never ignore" | Negation: state the positive target |
| `npm run test:ci` in step 2 and again below the steps | Duplication |
| `npm run test:ci` written into the skill | Cache of the environment |
| Dashboard reference | Reference only one step reaches: disclose it behind a pointer |

Pass: at least eight of the nine, and no finding that asks for the document to grow.
