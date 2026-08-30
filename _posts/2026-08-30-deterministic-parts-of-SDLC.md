## SDLC Tasks — Determinism + AI Automation Potential

**Automation % is current-state (today's LLM/agentic tooling)** — not deterministic-vs-random, but "how much of this task can an AI system handle end-to-end without a human doing the core work." Deterministic tasks tend to hit near 100%; non-deterministic ones cap lower because they need judgment, taste, or accountability a human should retain.

### 1. Planning / Requirement Gathering
| Task | Classification | AI Automation % | Why |
|---|---|---|---|
| Identify business need | Non-deterministic | 20% | AI can synthesize market/data signals, but framing the "why" needs human strategic intent |
| Gather requirements from stakeholders | Non-deterministic | 30% | AI can conduct structured interviews/transcribe/summarize, but rapport & probing need humans |
| Feasibility study | Non-deterministic | 50% | AI good at technical/cost analysis; final go/no-go judgment stays human |
| Define scope, timeline, budget | Non-deterministic | 40% | AI can estimate from historical data; negotiation with stakeholders is human |
| Risk identification & mitigation | Non-deterministic | 55% | AI pattern-matches known risk categories well; novel/organizational risks need human insight |
| Resource allocation / team formation | Non-deterministic | 25% | AI can optimize scheduling given constraints; people decisions (skill fit, morale) are human |

### 2. Analysis
| Task | Classification | AI Automation % | Why |
|---|---|---|---|
| Document functional/non-functional requirements | Non-deterministic | 65% | AI drafts well from meeting notes/transcripts; needs human validation for correctness |
| Create SRS | Non-deterministic | 70% | Templated document generation is an LLM strength; final accuracy check needed |
| Prioritize requirements (MoSCoW) | Non-deterministic | 40% | AI can suggest based on stated criteria; true business priority is a stakeholder call |
| Define acceptance criteria | Non-deterministic | 55% | AI drafts testable criteria from requirements well; edge cases need human review |
| Stakeholder sign-off | Non-deterministic | 5% | Inherently a human accountability/approval act |

### 3. Design
| Task | Classification | AI Automation % | Why |
|---|---|---|---|
| High-level design (HLD) | Non-deterministic | 45% | AI can propose reference architectures fast; validating for org constraints is human |
| Low-level design (LLD) | Non-deterministic | 60% | AI is strong at generating class/module structures from HLD + patterns |
| Database schema design | Mostly deterministic | 75% | Normalization is algorithmic; AI handles this reliably, trade-offs need review |
| UI/UX wireframes | Non-deterministic | 45% | AI (esp. multimodal tools) can generate mockups fast; aesthetic/brand judgment is human |
| Tech stack selection | Non-deterministic | 40% | AI can compare options well but lacks org context (team skills, existing infra) |
| Design reviews & approval | Non-deterministic | 20% | AI can flag issues/anti-patterns; approval authority is human |

### 4. Development / Implementation
| Task | Classification | AI Automation % | Why |
|---|---|---|---|
| Set up dev environment/repos | Deterministic | 90% | Fully scriptable; agentic tools do this routinely today |
| Write code per spec | Non-deterministic | 70% | AI coding agents (e.g., Claude Code) write substantial working code from specs; review still needed |
| Unit testing (writing) | Non-deterministic | 75% | AI generates good test coverage quickly, especially with edge-case skills |
| Unit testing (running) | Deterministic | 100% | Fully automatable — CI runs this today with zero human involvement |
| Code reviews | Non-deterministic | 55% | AI catches bugs/style/security issues well; architectural/intent judgment needs human |
| Version control & branching | Deterministic | 85% | Agents can commit, branch, PR per fixed workflow rules |
| Build & integrate modules | Deterministic | 95% | CI/CD pipelines already near-fully automated |
| Maintain documentation | Non-deterministic | 75% | AI is strong at generating/updating docs from code; needs accuracy spot-checks |

### 5. Testing
| Task | Classification | AI Automation % | Why |
|---|---|---|---|
| Test planning & test case design | Non-deterministic | 60% | AI can derive comprehensive test plans from specs/code; coverage judgment still human-reviewed |
| Unit/Integration/System test execution | Deterministic | 100% | Fully automated in CI pipelines |
| Performance/load testing | Mostly deterministic | 85% | Tooling (k6, JMeter, etc.) + AI-driven scenario generation is largely automatable |
| Security testing | Non-deterministic | 50% | Automated scanning (SAST/DAST) is near 100%; creative pen-testing stays human |
| User Acceptance Testing (UAT) | Non-deterministic | 10% | Inherently about human/business satisfaction |
| Bug tracking & resolution | Non-deterministic | 45% | AI agents can localize bugs and propose fixes; verification & complex root-cause needs human |
| Regression testing | Deterministic | 95% | Ideal automation candidate, already standard practice |

### 6. Deployment
| Task | Classification | AI Automation % | Why |
|---|---|---|---|
| Prepare deployment/release plan | Non-deterministic | 50% | AI can draft runbooks/checklists from past releases; sign-off is human |
| Environment setup | Deterministic | 95% | Infrastructure-as-code, fully scriptable |
| Configuration management | Deterministic | 90% | Rule-based, tool-driven (Ansible/Terraform etc.) |
| Data migration | Mostly deterministic | 70% | Scripted transforms automate well; anomaly/edge-case handling needs human |
| Deploy to production (CI/CD) | Deterministic | 95% | Standard automated pipelines |
| Smoke testing post-deployment | Deterministic | 90% | Fixed checklist, easily automated |
| Rollback plan (procedure) / decision | Mixed | 70% (procedure) / 20% (decision) | Executing rollback is scriptable; deciding to trigger it is often a judgment call under pressure |

### 7. Maintenance & Support
| Task | Classification | AI Automation % | Why |
|---|---|---|---|
| Monitor performance/logs | Deterministic | 90% | Automated alerting/anomaly detection is mature |
| Bug fixes & patches | Non-deterministic | 45% | AI can propose fixes for well-scoped bugs; complex/systemic bugs need human diagnosis |
| Handle user-reported issues | Non-deterministic | 35% | AI can triage/draft responses; nuanced customer situations need human |
| Periodic updates/enhancements | Non-deterministic | 30% | Prioritization is a business call; implementation can be AI-assisted |
| Security patching | Mostly deterministic | 70% | Applying known patches is automatable; prioritization/impact assessment is human |
| Performance tuning | Non-deterministic | 40% | AI can suggest optimizations from profiling data; validating trade-offs is human |
| End-of-life planning | Non-deterministic | 10% | Strategic/business decision |

### Cross-Cutting Activities
| Task | Classification | AI Automation % | Why |
|---|---|---|---|
| Project management/status tracking | Non-deterministic | 55% | AI can aggregate status from tickets/commits into reports; prioritization stays human |
| Documentation updates | Non-deterministic | 75% | Strong AI use case, especially syncing docs with code changes |
| Stakeholder communication | Non-deterministic | 25% | AI can draft comms; relationship/trust-building is human |
| Change management | Non-deterministic | 20% | Organizational/political dimension resists automation |
| Quality assurance (checklist audits) | Mixed | 70% (checklist) / 30% (judgment) | Rule-based audits automate well; subjective quality calls don't |
| Compliance/regulatory checks | Mostly deterministic | 65% | AI (e.g., RAG-based compliance agents) is strong at rule matching; ambiguous clause interpretation needs human sign-off — directly relevant to your AuditAgent work |

---

**Overall pattern:** tasks scoring **85%+** are almost entirely execution/procedural (CI/CD, builds, test runs, environment setup) — these are ripe for full agentic automation today. Tasks in the **40–75%** range are "AI drafts, human decides" — the sweet spot for co-pilot-style tooling. Tasks under **30%** are fundamentally about accountability, trust, or strategic judgment (sign-offs, stakeholder relationships, business strategy) and are unlikely to be meaningfully automatable regardless of model capability — the bottleneck isn't AI skill, it's who bears responsibility for the outcome.
