# Decisions

- **Project:** buyer-first pre-checkout purchase review for shoppers in Mexico; the governing specification is [docs/PACKET.md](docs/PACKET.md).
- **Stack:** dependency-free static HTML, CSS, and JavaScript plus a Vercel Node serverless function. Gemini is called with direct server-side `fetch`; `GEMINI_API_KEY` is read only by the function.
- **Privacy:** no accounts, database, or history. Form criteria are bounded, image type/signature/size and request size are validated, and screenshot bytes are sent only for the active analysis request. The app does not log or persist image contents.
- **Honest status:** without `GEMINI_API_KEY`, the endpoint explicitly returns DEMO mode and does not analyze the screenshot. With a key, Gemini vision can extract visible screenshot text; extracted claims are labeled advertised/unverified, missing fields unknown, and the output is not a recommendation or independent verification.
- **Upload:** PNG/JPEG/WebP only, at most 3 MiB, checked in browser and server; the server also validates file signatures. No original screenshot is saved.
- **Cost handling:** missing delivery remains unknown and the displayed amount is explicitly incomplete; the app does not infer shipping, exclusions, return costs, or protections.
- **Evidence cards:** buyer-entered amounts are labeled unverified and sourced to buyer input; screenshot text is labeled advertised and sourced to the supplied screenshot; local arithmetic is labeled supported only as a calculation. Every card shows the check date. Missing return terms, exclusions, fees, claim routes, fit, and quality remain unknown.
- **Correction workflow:** correction requests are editable, copyable local drafts held only in the current page. They are explicitly not submitted and not human-reviewed; there is no backend or stored personal information.
- **Next action:** implement commit 5 only: perform the documented synthetic-persona/comprehension test pass, fix any resulting UX issues, and retest before the second deployment.
