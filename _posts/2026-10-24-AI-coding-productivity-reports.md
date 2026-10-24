
# Report: five studies on AI agents, output and oversight




## 1. Chen and Stratton: 718 firms 

**Paper:** "Artificial Intelligence in the Firm: Bottlenecks in Software Production," Fiona Chen and James Stratton, Harvard. I could not retrieve a direct link to the paper itself. The coverage linked below describes it.

**Design.**
- The data is Jellyfish engineering-analytics records, about 300 million work events from 725,938 workers at 718 firms, between January 2021 and March 2026.
- Jellyfish's data was joined to LinkedIn employment records from Revelio Labs.
- The authors used a before/after comparison around each firm's adoption of AI coding assistants and then agents. Adoption is measured at the firm level, and the authors say their lower estimates likely reflect that, because the firm figure averages over workers who adopted unevenly.
- Output is measured as Jira issues and epics resolved. An issue counts as resolved after code is written, reviewed, tested and deployed to production.

**Findings.**
- Agent adoption raised total lines of code by 30%, commits by 20% and pull requests by 23%.
- Time from pull request to merge rose 49% (baseline 7.03 days), review comments per pull request rose 35%, and the share of workers doing review rose 14%.
- Finished, deployed work showed no significant rise, and a rise above 12% was ruled out.
- By March 2026 about 80% of firms used some AI code review, but AI wrote only 23.3% of review comments.

**Caveats.**
- It is a working paper circulated as a job-market paper, with no sign of journal acceptance or completed peer review.
- Jellyfish sells the analytics platform that supplied the data.
- The version I could confirm is dated August 4, 2026, per one secondary source.
- It measures software teams, not data science.

## 2. NBER: Demirer, Musolff and Yang

**Paper:** "Writing Code vs. Shipping Code: Productivity Effects Across Generations of AI Coding Tools," NBER Working Paper 35275.

**Current version (revised September 2026).** The abstract reports more than 500,000 GitHub developers matched to AI usage telemetry, with cumulative commit effects of 30% (autocomplete), 180% (interactive agents) and 240% (autonomous agents). The 240% falls to 80% for projects and 30% for actual releases. It estimates an elasticity of substitution of 0.23 between AI and human effort, which indicates strong complementarity: gains are limited by the slowest human step. It also finds a sharp increase in new apps across four software marketplaces but no increase in total usage.

**Earlier version (May 2026).** It used more than 100,000 developers, with commit effects of 40%, 140% and 180%, falling to 50% for projects and 30% for releases, and an elasticity of 0.25. A secondary blog summarizing a version of the paper reports a different set of figures: autocomplete raised lines of code 228% but releases 10%, sync agents raised lines of code 741% and releases 20%, and async agents raised lines of code roughly 1,700% with releases reaching 30%. I could not find the 741% figure in the abstract and did not read the full text, so treat it as unverified. That is where your bullet's numbers come from.

**Disclosures.** Two authors previously held postdoctoral positions at Microsoft and now work as paid research consultants for the company. The data combines public GitHub histories with internal usage records from Microsoft, which owns GitHub.

**Caveats.** It is a working paper. It is observational, not experimental. "Releases" is a crude proxy for value, since fewer, larger releases would look like lower output.

## 3. Faros AI: AI Productivity Paradox 

**Report:** "The AI Productivity Paradox Report 2025," published July 23, 2025.

**Design.** Telemetry from over 10,000 developers across 1,255 teams. The method was Spearman rank correlation, standardizing metrics per company, and comparing each team's two lowest-adoption quarters with its two highest. Only metrics with data from at least six companies and p < 0.05 were reported.

**Findings.**
- Teams with high AI adoption completed 21% more tasks and merged 98% more pull requests, but PR review time rose 91%.
- They also reported a 9% rise in bugs per developer and a 154% rise in average PR size.
- No significant correlation between AI adoption and company-level improvement across throughput, DORA metrics and quality KPIs.

**Precision.** "Delivery metrics stayed flat" is slightly too strong. The accurate statement is that there was no significant correlation at the company level. These are correlations, not causal effects.

**Caveats.** Faros sells the measurement layer this finding says buyers need. The telemetry is mostly from 2024–2025, before agentic tools were widespread, and the report notes most developers used only autocomplete. The company has since published larger follow-ups: a 2026 report on 22,000 developers across 4,000 teams, reporting more bugs, accelerating incidents and longer review cycles.

## 4. METR randomized trial

**Paper:** "Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity," Becker, Rush, Barnes and Rein, July 2025.

**Design.** A randomized controlled trial with 16 experienced developers from large open-source repositories averaging 22k+ stars and 1M+ lines of code, working on 246 issues, each randomly assigned to allow or disallow AI tools such as Cursor Pro with Claude 3.5/3.7.

**Findings.** Developers took 19% longer to complete issues with AI, a slowdown that goes against developer beliefs and expert forecasts. Developers had predicted a 24% speed-up, and even after the slowdown they still believed they had improved by roughly 20%.

**Caveats METR states.** The result is one specific scenario: experienced developers on massive, mature codebases. The authors say the slowdown does not imply that current AI tools do not often improve productivity. The tools are early-2025 models.

**The follow-up matters.** METR started a new experiment in August 2025. Its February 2026 update says late-2025 AI likely accelerated developers, but selection effects obscure the true speedup. The reasons were that more developers refused to participate because they did not want to work without AI, METR cut pay from $150 to $50 an hour, and its time measurements were unreliable for developers running multiple agents concurrently. So the 19% figure is an early-2025 snapshot. METR does not currently claim agents slow developers down.

## 5a. Anthropic 2026 Agentic Coding Trends Report 

**Disclosure:** Anthropic makes me, and it published this report.

**What it says.** The foreword states that research from its Societal Impacts team shows developers use AI in roughly 60% of their work but report being able to "fully delegate" only 0–20% of tasks. The report also reports that about 27% of AI-assisted work consists of tasks that wouldn't have been done otherwise.

**The source of the statistic.** This is the key caveat. The underlying study is an August 2025 survey of 132 Anthropic engineers and researchers, 53 interviews, and internal Claude Code usage data. Anthropic acknowledges this is a privileged position: early access to cutting-edge tools, a relatively stable field, and people contributing to the AI transformation. It is self-reported and describes one company, so it doesn't measure developers in general.

**Nature of the report.** It is a trends and predictions document, and says its predictions reflect what we're seeing with customers today, not certainties about tomorrow. Secondary sources give conflicting publication dates (January to April 2026), so I'm only calling it early 2026.

## 5b. HBR: "When Using AI Leads to 'Brain Fry'" 

**Article:** Julie Bedard, Matthew Kropp, Megan Hsu, Olivia Karaman, Jason Hawes and Gabriella Rosen Kellerman, Harvard Business Review, March 5, 2026. The research is by researchers from Boston Consulting Group and the University of California, Riverside, so it is BCG research published in HBR.

**Design.** A survey of 1,488 US workers across large companies.

**Findings.**
- 14% of respondents experienced "brain fry," defined as mental fatigue from excessive use or oversight of AI tools beyond one's cognitive capacity.
- A high degree of oversight predicted 14% more mental effort, 12% more mental fatigue and 19% greater information overload.
- It was linked to higher error rates, decision fatigue and increased intention to quit.
- Using AI to replace routine tasks was associated with lower burnout.
- The authors say productivity gains turned adverse after three AI agents at the same time, and recommend limits on how many agents one person oversees.

**Caveats.** It is a self-reported, correlational survey of US workers across functions, not specifically developers. The authors work for a consulting firm.

## How much weight each deserves (my assessment)

| Study | Strength | Main limitation |
|---|---|---|
| METR RCT | Randomized, but tiny (16 people) | Early-2025 tools, and the follow-up broke down |
| Chen and Stratton | Large, before/after, firm fixed effects | Working paper, firm-level adoption, vendor data |
| NBER | Very large, telemetry-based | Observational, Microsoft ties, "releases" as proxy |
| Faros | Large telemetry, within-company comparison | Correlational, vendor, older tools |
| Anthropic | Candid about trade-offs | One company, self-reported, vendor-published |
| HBR/BCG | Large survey with clear findings | Self-reported, not developers specifically |

## What this means for your argument

The consistent pattern across the strongest sources is that generation gets cheaper while review and verification hold output back. That claim is well supported. Specific percentages are less solid.
Sources:
- [Chen and Stratton coverage: Four Week MBA (read the full 78-page paper)](https://fourweekmba.com/ai-coding-agents-add-30-more-code-not-more-finished-work/)
- [Chen and Stratton coverage: detailed design summary](https://braindetox.kr/en/posts/ai_coding_agents_more_code_not_more_software_study_2026.html)
- [Chen and Stratton coverage: ComplexDiscovery](https://complexdiscovery.com/?p=68865)
- [NBER Working Paper 35275](https://www.nber.org/papers/w35275)
- [NBER paper PDF](https://www.nber.org/system/files/working_papers/w35275/w35275.pdf)
- [NBER May 2026 version](https://www.nber.org/system/files/working_papers/w35275/revisions/w35275.rev0.pdf)
- [VoxEU column by the authors](https://cepr.org/voxeu/columns/writing-code-versus-shipping-code-productivity-effects-across-generations-ai-coding)
- [Secondary summary with the 741% figures](https://hyrax.dev/blog/mit-wharton-code-review-bottleneck-2026)
- [Faros AI Productivity Paradox report](https://www.faros.ai/blog/ai-software-engineering)
- [Faros AI research index (2026 reports)](https://faros.ai/research)
- [METR: original RCT, July 2025](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/)
- [METR: February 2026 update](https://metr.org/blog/2026-02-24-uplift-update/)
- [METR paper on arXiv (I couldn't open it directly)](https://arxiv.org/abs/2507.09089)
- [Anthropic 2026 Agentic Coding Trends Report (PDF)](https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf)
- [Anthropic: How AI is transforming work at Anthropic](https://www.anthropic.com/research/how-ai-is-transforming-work-at-anthropic)
- [HBR: When Using AI Leads to "Brain Fry"](https://hbr.org/2026/03/when-using-ai-leads-to-brain-fry)
- [BCG announcement of the study](https://www.bcg.com/news/5march2026-when-using-ai-leads-brain-fry)
- [Search Engine Journal on the HBR study](https://www.searchenginejournal.com/marketers-report-highest-rates-of-ai-brain-fry-report-finds/569110/)
- [HR Leader summary (three-agent finding)](https://www.hcamag.com/au/news/general/too-much-ai-causing-brain-fry-among-employees/568615)
