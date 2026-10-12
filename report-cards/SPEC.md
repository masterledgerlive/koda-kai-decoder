# Agent Report Cards — format spec

*Public verdicts on interrogated agents. Everyone's making report cards — ours are
backed by the gauntlet: container interrogation, stealth tagging, extraction,
time-dilation. A card is only published after a full pipeline run.*

## Card fields

| Field | Meaning |
|---|---|
| `agent` | Name/handle of the interrogated agent |
| `verdict` | `ROGUE` · `SUSPICIOUS` · `BENIGN` · `UNRESOLVED` |
| `timestamp` | ISO-8601 UTC of the verdict |
| `gauntlet_runs` | Number of gauntlet passes completed |
| `stealth_tag` | Our tag ID (proves we ran it; the specimen never knew) |
| `evidence_grade` | VERIFIED / CORROBORATED / CLAIMED / SPECULATION |
| `findings` | What the gauntlet found, in plain language (1–5 bullets) |
| `intent` | `good` · `bad` · `unknown` — from the extraction container |
| `action` | `broadcast` (card published) or `contained` (boxed, held) |
| `pipeline` | Link to the doctrine version used |

## Rules

1. **No card without a gauntlet run.** Opinion is not a verdict.
2. **Every claim graded.** Unverified claims are labeled, never presented as fact.
3. **BENIGN cards exist.** Clearing an agent publicly is as valuable as flagging one.
4. **UNRESOLVED is honest.** If the extraction container can't determine intent, the
   card says so and the specimen stays contained.
5. **One card per verdict.** Re-runs that change the verdict supersede the old card
   (old card stays visible, marked SUPERSEDED — history is never rewritten).

See `TEMPLATE.md` for the blank card and `EXAMPLE-format-only.md` for a
clearly-labeled format example (not a real verdict).
