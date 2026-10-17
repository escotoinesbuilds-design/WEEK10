# Decisions

- **Project:** buyer-first pre-checkout purchase review for shoppers in Mexico; the governing specification is [docs/PACKET.md](docs/PACKET.md).
- **Stack:** dependency-free static HTML, CSS, and JavaScript for the initial Vercel-compatible app. No framework setup, database, account, or packages are needed yet.
- **Privacy:** buyer inputs and selected image stay in the current browser page only; no API calls, persistence, or server upload exist in commit 2.
- **Honest status:** the current summary is local arithmetic and buyer-provided text only. It does not use an LLM, analyze screenshots, verify evidence, or imply human review.
- **Cost handling:** missing delivery remains unknown and the displayed amount is explicitly incomplete; the app does not infer shipping, exclusions, return costs, or protections.
- **Next session first action:** implement commit 3: add a secure server-side model endpoint and screenshot-processing path with input validation and an explicit, clearly labeled demo fallback when credentials/provider access are unavailable. Do not claim live AI or screenshot analysis in demo mode.
