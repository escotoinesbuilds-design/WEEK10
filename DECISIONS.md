# Decisions

- **Project:** buyer-first pre-checkout purchase review for shoppers in Mexico; the governing specification is [docs/PACKET.md](docs/PACKET.md).
- **Stack:** dependency-free static HTML, CSS, and JavaScript plus a Vercel Node serverless function. Gemini is called with direct server-side `fetch`; `GEMINI_API_KEY` is read only by the function.
- **Privacy:** no accounts, database, or history. Form criteria are bounded, image type/signature/size and request size are validated, and screenshot bytes are sent only for the active analysis request. The app does not log or persist image contents.
- **Honest status:** without `GEMINI_API_KEY`, the endpoint explicitly returns DEMO mode and does not analyze the screenshot. With a key, Gemini vision can extract visible screenshot text; extracted claims are labeled advertised/unverified, missing fields unknown, and the output is not a recommendation or independent verification.
- **Upload:** PNG/JPEG/WebP only, at most 3 MiB, checked in browser and server; the server also validates file signatures. No original screenshot is saved.
- **Cost handling:** missing delivery remains unknown and the displayed amount is explicitly incomplete; the app does not infer shipping, exclusions, return costs, or protections.
- **Next action:** implement commit 4 only: add dated evidence cards, return/exposure details, and correction/request-review status. Do not claim a human review occurred unless it is actually performed.
