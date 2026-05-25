# AI Mentor Bootcamp — <KUNDRAPU MUTYALA BABU>
## Day 1 — Setup complete

- ✅ Google AI Studio API key provisioned
- ✅ Groq API key provisioned
- ✅ Hello-Gemini call working — see [Day1_Setup.ipynb](Day1_Setup.ipynb)
- 4-tool comparison matrix from Lab 1A: see screenshot below
- # Day 6 — Capstone Sprint 1: PlacementDataProcessor

### Engineer Answer

1. **PROBLEM** — JDs from Naukri / LinkedIn are messy text — placement cells need structured data to filter ("which JDs want Java + CGPA 7+?"). Manual extraction is unscalable for 50+ JDs.

2. **ARCHITECTURE** — JD URL → BeautifulSoup scraper (extract clean text) → Gemini structured-output call (response_schema=JD Pydantic) → JSON Lines file. Validation at each step; retry on schema fail.

3. **TRADE-OFFS** —
   - Cost: free Gemini ~1 JD/sec on average; ~30K tokens/day quota → ~5K JDs/day.
   - Accuracy: Pydantic catches schema violations but not semantic errors (e.g., model says skill is "Python" when source says "Python 3.12 specifically").
   - Latency: ~2-5s per JD (Gemini call dominant).
   - Complexity: scraping fragile (sites block automation). Cached fallback is mandatory.

4. **SCALE** —
   - 10 JDs/day: trivial. Today's lab.
   - 100 JDs/day: still in free quota. Add overnight batch + sleep between calls.
   - 10K JDs/day: free tier breaks. Move to paid Gemini OR self-host an open model.

5. **INTERVIEW ANSWER** — "I built a structured-output pipeline that turns scraped JDs into clean filterable JSON, using free Gemini and Pydantic. Schema-first design with retry-on-failure made it production-shaped on a free-tier API."
## Day 7 Lab 7A — ChromaDB Hello-World

- Embedded 10 CSE Sem 5 paragraphs with all-MiniLM-L6-v2 (384-dim, free)
- Indexed in persistent ChromaDB collection `hello_syllabus`
- Ran 3 semantic queries — observed: top-1 match is relevant when query topic is in corpus, irrelevant when not
- Plotted PCA 2D — visible OS / DBMS clusters

**Reflection:**



