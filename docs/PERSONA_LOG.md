# Synthetic Persona Log

**Project:** CompraConInfo, buyer-first pre-checkout review  
**Test date:** 2026-10-17  
**Persona:** Lucía, 38, online shopper in Mexico City  
**Format:** Five-screen synthetic-persona walkthrough, as reported by the project owner. This is not a real-user study or evidence of market outcomes.

## Walkthrough record

The project owner reports that Lucía tested five screens. The notes provided do not identify the exact names/order of the screens, map each confusion to a screen number, or preserve a click-by-click transcript. To avoid inventing observations, the table records the walkthrough coverage limit and the findings are summarized separately.

| Screen | What Lucía understood, clicked, questioned, or trusted |
|---|---|
| Screen 1 | Included in the reported five-screen walkthrough; screen-specific actions and statements were not recorded in the notes provided. |
| Screen 2 | Included in the reported five-screen walkthrough; screen-specific actions and statements were not recorded in the notes provided. |
| Screen 3 | Included in the reported five-screen walkthrough; screen-specific actions and statements were not recorded in the notes provided. |
| Screen 4 | Included in the reported five-screen walkthrough; screen-specific actions and statements were not recorded in the notes provided. |
| Screen 5 | Included in the reported five-screen walkthrough; screen-specific actions and statements were not recorded in the notes provided. |

**Reported trust/understanding:** Lucía questioned whether **“Solicitar corrección”** would reach a human; she interpreted **“SUSTENTADO”** on the total as possibly meaning the price was verified; and **“Esperar y verificar más”** did not make the next step clear. The supplied summary does not say whether she clicked each control, what other details she understood, or what evidence she trusted. No additional behavior or quotation is inferred.

## Main confusions and UI response

1. **Correction route implied a human submission.** The section is now titled **“Borrador local de corrección”**, explains that it is temporary, not sent, and not reviewed by a person, and labels the action **“Guardar borrador local (no enviado)”**.
2. **“SUSTENTADO” implied verified prices.** The total card now says **“CÁLCULO LOCAL (no verificado)”** and explains that it is calculated from entered or screenshot-visible amounts, does not verify price/shipping, and leaves additional unknown charges unknown.
3. **Waiting did not explain a next step.** Choosing **“Esperar y verificar más”** now tells the buyer to check return terms/exclusions, possible costs, and relevant product characteristics, then update the review. It does not make the decision for them.

## Synthetic-persona retest

**Completed, as reported by the project owner.** Lucía confirmed that the calculated-versus-verified distinction is clearer and that she understands correction drafts are not submitted. She still could not identify what to do after selecting **“Esperar y verificar más”**, could not find where to enter return-policy information, and found Gemini/API availability terminology confusing.

### Remaining limitations reported

- Live AI is unavailable to Lucía in the current environment. No live Gemini request or live-model result is claimed.
- Product verification remains incomplete. A screenshot claim is not independently verified; missing return terms, costs, and product details remain unknown.

### Final UI fixes after the retest

- The **Wait** response now gives numbered next steps: check return terms and exclusions, find who pays return shipping and other possible costs, confirm needed product characteristics, then edit the same form and select **“Revisar mi compra”** again. It says there is no need to start over and unknowns should remain unknown. This copy change is intended to address the reported confusion; no new response from Lucía is claimed.
- Added an optional return-policy text field. Its evidence card attributes the text to the buyer, labels it **NO VERIFICADO**, and states that it does not establish compliance or guarantee a refund.
- Replaced Gemini/API availability wording in buyer-facing states with plain Spanish explaining whether automatic screenshot analysis is available and what manual review means. DEMO remains explicitly labeled.

**Retest of these final UI fixes:** pending. Local browser verification is recorded in [docs/TEST_LOG.md](TEST_LOG.md), but is not a synthetic-persona retest.
