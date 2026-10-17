# Mechanical Test Log

**Date:** 2026-10-17  
**Scope:** Commit 4 mechanical browser pass and reproducible bug fix. No commit or deployment was made.

## Browser and input checks

| Check | Result |
|---|---|
| Enter fictional product, budget, size, and needs | Pass; values appear as text and remain editable. |
| MXN calculation: $1,234.56 product + $45.44 shipping | Pass; displays $1,280.00. |
| Product price known, shipping missing | Pass; total says “Incompleto (al menos $1,234.56)”; shipping stays unknown. |
| Product price missing, shipping $45.44 | Initially failed as detailed below; passed after fix with “Parcial: $45.44; falta precio.” |
| Evidence cards | Pass; cards show source, current check date, and status. Buyer-entered amounts are unverified; screenshot-visible text is advertised; absent data is unknown. |
| Return information | Pass; missing policy, exclusions, disclosed costs, exposure, and claim route remain unknown. Screenshot-claimed costs are explicitly conditional and do not imply protection. |
| Invalid screenshot in browser (`/etc/hosts`, not an allowed image) | Pass; rejected, removed from the file input, and a clear validation message is shown. |
| Valid supplied PNG without `GEMINI_API_KEY` | Pass; endpoint returns explicitly labeled DEMO mode and says no AI analysis ran. No extracted result is shown. |
| Server upload/input validation | Pass; unsupported MIME, invalid PNG signature, image over 3 MiB, and malformed negative buyer amount are rejected. |
| Correction workflow | Pass; correction can be drafted, saved locally, reopened for editing, and copied. Status says it was not submitted or human-reviewed. |
| Buyer choices | Pass; Wait, No comprar, and Decidir por mi cuenta each produce a neutral acknowledgement; no order is placed. |
| Clear/reset | Pass; inputs, result, evidence, and local correction draft clear. |
| Mobile layout at 375 px viewport | Pass; no horizontal document overflow. |
| JavaScript syntax and whitespace | Pass: `node --check api/analyze.js`, inline-script syntax parse, and `git diff --check`. |

For screenshot-card rendering, a local fixture provider returned clearly synthetic analysis data. This exercised the live-response UI path only; it was not a request to Gemini and is not evidence about a real product. No real key was used. This static project has no package manifest or configured lint/build/test runner; no dependencies were installed.

## Reproducible bug

**Steps**

1. Open the local app.
2. Leave “Precio del producto” empty.
3. Enter `120` as shipping.
4. Select “Revisar mi compra” without a screenshot.

**Expected:** the summary indicates the known partial amount and identifies the missing price, consistent with the evidence card.  
**Actual before fix:** summary displayed “Desconocido,” while the evidence card displayed “PARCIAL: $120.00; falta el precio.”

**Fix:** updated the summary total’s conditional to display `Parcial: $120.00; falta precio` when only shipping is known. No inferred product price is added.

**Retest:** repeated the same browser steps after the change; summary displayed `Parcial: $120.00; falta precio`, matching the evidence card. Pass.

## Outcome

Mechanical checks pass after the fix. The synthetic-persona walkthrough was subsequently reported and is documented in [docs/PERSONA_LOG.md](PERSONA_LOG.md); the retest of the copy changes remains pending.

## Persona-driven copy changes (pending persona retest)

**Date:** 2026-10-17  
**Source:** owner-reported five-screen synthetic walkthrough with Lucía, 38, Mexico City. Details and limitations are recorded in [docs/PERSONA_LOG.md](PERSONA_LOG.md).

- Reworded the correction area and button to explicitly state the draft is local, not sent, and not human-reviewed.
- Replaced the total's “SUSTENTADO” label with “CÁLCULO LOCAL (no verificado)” and clarified the input basis and unknown additional charges.
- Added a concrete checklist after the buyer chooses to wait: verify return terms/exclusions, possible costs, and relevant product details, then update the review.

**Local smoke retest:** browser checks confirmed each revised label/message appears after its corresponding action. This does not establish comprehension. **Synthetic-persona retest remains pending.**

## Local retest of persona-driven copy

**Date:** 2026-10-17  
**Result:** Pass for display/interaction behavior; persona comprehension still pending.

- Entered fictional product and MXN amounts, generated the evidence cards, and confirmed the total card is labeled **“CÁLCULO LOCAL (no verificado)”** with text stating it does not verify amounts and unknown extra charges remain unknown.
- Saved a correction draft and confirmed the page states it was not sent and no person reviewed it.
- Chose **“Esperar y verificar más”** and confirmed the follow-up names return terms/exclusions, possible costs, product characteristics, and updating the review.
- These checks validate UI behavior only. They are not a retest with Lucía; see [docs/PERSONA_LOG.md](PERSONA_LOG.md), where the retest remains pending.

## Final persona fixes and local verification

**Date:** 2026-10-17  
**Persona source:** owner-reported completed retest with Lucía; see [docs/PERSONA_LOG.md](PERSONA_LOG.md).

- Added a numbered, visible next-step explanation after choosing **“Esperar y verificar más”**, including how to edit the same form and review again without restarting.
- Added optional buyer-entered return-policy text. The evidence card identifies buyer input, marks it **NO VERIFICADO**, and explicitly says it does not guarantee a refund.
- Replaced buyer-facing Gemini/API availability phrases with plain Spanish and an explicit **Modo DEMO** message when automatic screenshot analysis is unavailable.

**Local browser verification:** selected Wait and confirmed all steps and same-form editing instructions appeared; entered return-policy text and confirmed the card was labeled unverified with no refund promise; confirmed the DEMO message explains automatic analysis is unavailable and manual review is possible; submitted a screenshot to a static-only local server and confirmed the unsupported endpoint response is converted to a plain Spanish unavailable message. Syntax checks passed. No live Gemini request was made. Lucía's retest of these final changes remains pending.
