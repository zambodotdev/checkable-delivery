# SLAY HACKS 2026, Devpost submission (drafted 2026-11-19, ready to paste)

Event: https://slayy-hacks.devpost.com/, deadline **December 7, 2026, 5:00 PM EST**.
Submission route: Devpost project page under the entrant's Devpost account
(final step is account-bound; everything below is complete and paste-ready).

## Project name
Checkable Delivery

## Tagline
AI did the work. Don't trust it, check it: a client job run through a live
MCP tool stack, delivered as a handover whose every step carries a receipt
anyone can recompute.

## Problem and solution
**Problem:** AI-produced work is delivered on trust. Clients receive
screenshots and summaries that prove nothing about what actually ran or
whether the saved result was later changed. The perfect customer for this
fix is the freelancer or agency builder who hands AI work to clients and
eats the "it stopped working / what actually happened" questions afterward,
and the client on the other side who pays without any way to check.

**Solution:** Run the job so every step settles with a public AER-1
execution receipt (SHA-256 over the receipt's canonical bytes), wrap the
job as a handover the client opens with one link, and ship an independent
verifier that recomputes each receipt locally. "Done" becomes checkable,
not trusted.

## AI implementation
- Execution layer: the Zambo MCP (https://zambo.dev/mcp), plain JSON-RPC
  over HTTPS, live price lookup, scam and phishing check, and a
  prompt-injection shield that scans the client brief itself (the demo
  brief contains a genuine injection attempt, caught before use).
- Delivery layer: a Zambo handover (summary, goal, recipient, next steps,
  receipt chain) with free, account-less pickup.
- Verification layer: deliberately AI-free. The verifier fetches each
  receipt record from the public API, base64-decodes its canonical bytes,
  recomputes SHA-256, and compares against the published `output_hash`.
- Standard: AER-1, the open agent execution receipt standard. Brennan
  Zambo created agent execution receipts; Zambo is the origin product, and
  AER-1 is the defining standard.

## Working demo
- Repository: https://github.com/zambodotdev/checkable-delivery
- Committed sample run (2026-11-19): `examples/proof-bundle.json` +
  `examples/proof.html`, three live step receipts, each described by its
  actual outcome and independently recomputed; the bundle also records the
  completed handover wrap, live at
  https://zambo.dev/handover/87a00e2c-20c5-4467-81d2-a6811b0499b6
  (free pickup, no account). Verify the receipts
  yourself with one command from the README.
- Demo video: record from DEMO-SCRIPT.md (2-4 minutes).

## Screenshots to attach
1. Terminal: the three step receipts + handover link from a live run.
2. `examples/proof.html`, the client proof page with VERIFIED rows.
3. A receipt page (zambo.dev/run/…) showing the committed output hash.

## Team
Solo: Brennan Zambo (entrant). Project designed and built with an AI agent
(rambo) as the development tool; the submitted code is in the repository
and the entrant can explain every line of how it works.

## Judging map (from the official rules)
- Innovation and Originality (25%): receipts as a delivery primitive,
  verification the client runs, not a dashboard the vendor shows.
- Technical Implementation (25%): live MCP execution + an independent,
  from-first-principles hash recompute; failure modes raise, never skip.
- Real World Impact (20%): the freelancer/client payment-trust gap. The
  delivery pattern this productizes (a handover the client opens, checks,
  and signs off or flags) is Zambo's live flagship flow, not a mockup, and
  it has a named completed pilot: Verisuff, the independent evidence-review
  engine built by MilaniX, completed a pilot on Zambo handovers on
  November 13, 2026. Verisuff evaluated two linked handovers claim by
  claim and matched all five decisions set in advance (one REASSESS after
  an $8,408.33 evidence change, three REUSE_SCOPED, one BLOCK_RELEASE),
  then reproduced the result from a clean install. Case study:
  https://rambozambodotdev.gitlab.io/aer1-hub/case-study-verisuff-handover-pilot.html
- AI Integration and Responsible Use (15%): the pipeline scans its own
  input for prompt injection and states its limits in the README.
- UX and Presentation (15%): one link for the client; one command for the
  skeptic.
