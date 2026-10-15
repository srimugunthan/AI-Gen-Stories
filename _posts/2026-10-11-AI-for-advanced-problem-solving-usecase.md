I'll look up the latest on AI for advanced problem solving (reasoning models, math and science benchmarks, agentic research) and the companies and business results around it.

# AI for "advanced problem solving": state of the art (Oct 2026)

I read "advanced problem solving" as AI that can reason through hard, multi-step problems in math, science, engineering and complex business decisions. Many of the figures below come from secondary sources and vendor-reported benchmarks, so treat precise numbers as indicative.

## 1. Where the technology stands

**Reasoning benchmarks are close to saturated, and the field has moved on to harder tests.**
- Humanity's Last Exam launched in early 2025 with top models in single digits on 2,500 expert-level questions; by June 2026 the leading score was 53.3%.
- Science: GPQA Diamond scores at the top reached about 94%.
- Math: on FrontierMath, which uses novel problems written by mathematicians, GPT-5.5 Pro leads at 52.4%, ahead of GPT-5.4 Pro at 50.0% and Claude Opus 4.7 at 43.8%.
- New benchmarks reflect the shift. FrontierScience, for example, includes open-ended research problems rather than only closed-form questions.

**AI is now contributing to open research problems.**
- Olympiad math is largely solved: Gemini Deep Think reached IMO gold level (35/42) in 2025.
- Erdős problems are the new proving ground. Google DeepMind's Aletheia agent was run against 700 problems marked open in the database. The authors note that the "open" status of the problems it resolved came from obscurity rather than difficulty, which is an important caveat. Axiom Math's AxiomProver also logged several verified results, and the formal-math (Lean) route adds machine-checked correctness.
- The bar has risen since. A June 2026 report says a Google AI solved nine of 353 open Erdős problems it attempted, including two unanswered for 56 years. Another report says an OpenAI model solved the 80-year-old unit distance problem in combinatorial geometry. The math community describes that proof as readable and largely linking known results from disparate areas, not a brute-force search.
- Even so, AI is still nowhere near solving major open problems in math, according to Scientific American's reporting.

**The dominant architecture is generator plus verifier, often multi-agent.**
- AlphaEvolve pairs LLMs with program search and automated evaluation, drawing on the co-scientist pattern where agents act as hypothesis generator, critic and reviewer.
- This works best where an objective scoring function exists (algorithms, optimization, proofs, simulations) and worst on vague, open-ended problems.

## 2. Who is working on it

| Player | Focus |
|---|---|
| **Google / DeepMind** | AlphaEvolve, Co-Scientist, Aletheia (math). Packaged as "Gemini for Science" at I/O on May 20, 2026. Early access is via Google Cloud account teams. |
| **OpenAI** | GPT-5.x Pro / Thinking line, leading FrontierMath; unit distance result; FrontierScience benchmark |
| **Anthropic** | Claude Opus/Fable line; strong on coding, agentic and knowledge-work reasoning |
| **Others** | xAI (Grok), Meta (Muse Spark), and open-weight challengers such as DeepSeek and Moonshot's Kimi, which have narrowed the gap to commercial models sharply in early 2026 |
| **Specialists** | Axiom Math (formal proofs), ByteDance Seed-Prover (5 of 6 IMO 2025 problems) |

At the frontier, six labs sit within 79 Elo points of each other on Chatbot Arena, so the lead rotates by benchmark.

## 3. Business benefits and profit potential

**Where the value is clearest:**
- **Algorithm and systems optimization.** AlphaEvolve-style loops target GPU instruction optimization for AI training and inference, plus scheduling, logistics and chip design. Savings are directly measurable.
- **R&D acceleration.** Co-Scientist is aimed at target discovery and mechanistic hypotheses for complex diseases, which matters for pharma and materials, where each year saved is worth a great deal.
- **Engineering and debugging at scale.** Reasoning models handle multi-file debugging, audits and root-cause analysis that previously needed senior experts.
- **Complex multi-hop decisions** such as risk, policy and compliance, where reasoning plus retrieval (GraphRAG-style) is becoming standard.

**What the ROI data says:**
- Positive but uneven. One compilation cites a median 171% ROI over 12 months in an IBM survey, and a Deloitte finding that custom-built agents beat off-the-shelf ones by 2.3x. The same source notes only 23% of enterprises report significant ROI despite 51% running agents in production, and that agents on vague, open-ended tasks rarely show measurable returns.
- McKinsey's 2026 survey shows the gap: 80% report personal productivity gains, but the share seeing EBIT impact has stalled at 37%, and AI costs now constrain usage for one in five organizations.
- Gartner expects 40% of agentic projects to fail by 2027. The usual cause is organizational (pilots that never scale, weak governance), not model quality.

## 4. How to actually capture the profit

1. **Pick problems with a verifiable objective.** The best returns come where outputs can be scored automatically (cost, latency, accuracy, proof checked).
2. **Use reasoning tiers selectively.** Heavy "thinking" modes cost much more, so route only hard cases to them.
3. **Build custom, domain-bounded agents on proprietary data**, since that is where the ROI evidence is strongest.
4. **Invest in governance and evaluation first**, especially in regulated industries. The EU AI Act's full applicability date of Aug 2, 2026 makes audit trails and a system inventory table stakes.
5. **Keep humans on verification.** The Erdős experience shows AI can rediscover existing literature or solve a subtly different statement than intended.

**Bottom line:** the technology has crossed from "answering hard questions" to "contributing to unsolved ones," but the profit story is still concentrated in narrow, measurable, well-governed applications. Broad enterprise-wide returns remain unproven.

Sources:
- [Smartest AI in 2026 (fast.io)](https://fast.io/resources/smartest-ai-2026/)
- [Most Powerful AI in 2026 (fast.io)](https://fast.io/resources/most-powerful-ai-2026/)
- [FrontierMath leaderboard (DataLearner)](https://www.datalearner.com/en/benchmarks/frontier-math)
- [FrontierScience (arXiv)](https://arxiv.org/pdf/2601.21165.pdf)
- [LLM-Driven Formal Mathematics survey (arXiv)](https://arxiv.org/pdf/2607.07779)
- [A Case Study on the Erdős Problems (arXiv)](https://arxiv.org/html/2601.22401)
- [Scientific American via Harvard](https://people.math.harvard.edu/~williams/scientificamerican2.pdf)
- [CMS Notes editorial, June 2026](https://notes.math.ca/en/?p=21309)
- [Everything-list thread on Google's Erdős results](https://groups.google.com/g/everything-list/c/oC4iWZ89u8Y/m/wvDD7h47AAAJ)
- [Feedbagel summary of the unit distance result](https://feedbagel.com/post/a-famous-math-problem-stumped-humans-for-80-years-ai-just-cracked-it-2)
- [Inside DeepMind's AlphaEvolve and co-scientist](https://inferencebysequoia.substack.com/p/inside-deepminds-alphaevolve-and)
- [Google Cloud: Co-Scientist and AlphaEvolve docs](https://docs.cloud.google.com/gemini/enterprise/docs/co-scientist-and-alphaevolve)
- [Gemini for Science announcement summary](https://vpsranking.com/news/ai/ai-2026-05-20-google-gemini-for-science/)
- [Enterprise AI Agents: The ROI Reality in 2026](https://www.callmissed.com/hi/blog/enterprise-ai-agents-roi-reality-2026)
- [McKinsey State of AI 2026 summary](https://zeli.app/story/49433759)
- [Superintelligent Enterprises 2026 (gend.co)](https://www.gend.co/blog/superintelligent-enterprises-2026)
- [AI 2026: 10 Uncomfortable Truths (innobu)](https://www.innobu.com/en/articles/ai-2026-10-uncomfortable-truths-transformation-phase.html)
