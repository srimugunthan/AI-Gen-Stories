
This curriculum is designed to be a 12-18 month self-study path, leveraging Coursera, Udemy, and freely available resources to build you into a Principal-level AI engineer in the financial services domain.

### Guiding Philosophy of this Curriculum

- **Phase-Driven:** It moves from foundational "must-haves" to the advanced, specialized "Adversarial Intelligence" domain you've identified.
- **Applied First:** Theory is immediately paired with application, coding, and real-world datasets.
- **Resource-Rich:** Every module maps to specific, often free or low-cost, courses and materials.
- **Principal-Focused:** The later phases are not just about building models, but about framing problems, understanding strategy, and communicating with stakeholders.

---

## Phase 1: The Unshakeable Financial Foundation (Months 1-3)

This phase builds the financial literacy required to have credible conversations with risk officers, traders, and compliance teams. You're not becoming a quant, you're becoming a data scientist who speaks their language.

**Goal:** Achieve fluency in financial statements, products, risks, and the language of the business.

| Module | Key Topics | Recommended Courses & Resources | Rationale |
| :--- | :--- | :--- | :--- |
| **1. Financial Accounting & Statements** | Balance Sheets, Income Statements, Cash Flow Statements. GAAP basics, Loan Loss Provisioning (CECL). | **Coursera:** [Introduction to Financial Accounting](https://www.coursera.org/learn/wharton-accounting) (Wharton) - up to Module 4. <br> **Read:** "Bank Management & Financial Services" by Peter Rose (Chapters on bank financial statements). | You can't model credit risk without understanding what a Non-Performing Loan (NPL) does to a balance sheet. |
| **2. Financial Products & Markets** | Equities, Fixed Income (bonds, yield curves), FX, Commodities. Mechanics, not trading. | **Coursera:** [Financial Markets](https://www.coursera.org/learn/financial-markets-global) (Yale - Robert Shiller). <br> **Udemy:** [The Complete Foundation of Stock Trading](https://www.udemy.com/course/stock-trading-foundations/) (Focus on market mechanics sections). <br> **Book:** "Options, Futures, and Other Derivatives" by John Hull (Chapters 1-5 for fundamentals). | This is the data your models will consume. Know what a derivative *is* before you try to predict its price. |
| **3. Core Risk Management** | Defining Credit, Market, Operational, and Liquidity Risk. Intro to Basel capital adequacy. | **FRM Curriculum (Part I):** Even if you don't take the exam, get the official GARP books or find summaries. Focus on "Foundations of Risk Management." <br> **BIS.org:** Read the summaries of Basel III/IV. | Risk is the lens through which banking views everything. This module is non-negotiable. |
| **4. Macroeconomics for Finance** | Interest rate dynamics, inflation, monetary policy, business cycles. Why these are the "exogenous shocks" to models. | **Coursera:** [Global Financial Crisis](https://campuspress.yale.edu/leverhulme/courses/global-financial-crisis-yale-coursera/) (Yale - can be found archived). <br> **Fed Listening:** Subscribe to and listen to 2-3 FOMC press conferences. Read the transcripts. | Every stress test scenario is built on macro variables. Understand what drives them. |
| **Milestone Project 1:** Pick a large bank (JPM, WFC, BAC). Download their 10-K filing. Can you identify their total assets, total loans, and provisions for credit losses? Can you explain in one paragraph the biggest risk they face? |

---

## Phase 2: The Modern Data Science Tech Stack for Finance (Months 4-6)

This phase upgrades your DS toolkit for the specific demands of financial data: speed, scale, and time-series rigor.

**Goal:** Move beyond standard Python libraries to handle tick data, backtest rigorously, and deploy in regulated environments.

| Module | Key Topics | Recommended Courses & Resources | Rationale |
| :--- | :--- | :--- | :--- |
| **1. Time Series Analysis & Econometrics** | ARIMA/SARIMA, GARCH (volatility modeling), Cointegration, Granger Causality. | **Coursera:** [Practical Time Series Analysis](https://www.coursera.org/learn/practical-time-series-analysis) (SUNY). <br> **Book:** "Intro to Time Series and Forecasting" by Brockwell & Davis (for reference). <br> **Python libs:** `statsmodels`, `pmdarima`. | Financial data is a time series. Standard CV (k-fold) will fail here. You need walk-forward validation. |
| **2. High-Performance Data Manipulation** | Moving beyond Pandas for large datasets. | **Udemy:** [Polars: The Future of DataFrames](https://www.udemy.com/course/polars-the-dataframe-library-for-data-science/). <br> **Databricks:** [Apache Spark for Data Engineers](https://www.databricks.com/learn/training/apache-spark) (free self-paced). <br> **Concept:** Tick data and backtesting at scale. | Bank transactions and market tick data are massive. Pandas will choke; Polars or PySpark won't. |
| **3. MLOps for Regulated Industries** | Model validation, reproducibility, explainability, and monitoring for drift. | **Coursera:** [MLOps Fundamentals](https://www.coursera.org/learn/mlops-fundamentals) (Google Cloud - focus on concepts). <br> **Read:** [SR 11-7 (Fed/OCC)](https://www.federalreserve.gov/supervisionreg/srletters/sr1107.htm) in full. This is the *bible* for model risk. | In banking, a good model is one you can explain to a regulator. MLOps here is about auditability. |
| **4. Graph Analytics Fundamentals** | Network analysis, centrality, community detection. Prerequisite for GNNs. | **Stanford:** [CS224W: Machine Learning with Graphs](http://web.stanford.edu/class/cs224w/) (lectures on YouTube are free). <br> **Python libs:** `NetworkX`, `PyTorch Geometric` (intro). | Fraud and money laundering are inherently graph problems. This is your foundation. |
| **Milestone Project 2:** Download a year of stock price data for 5 companies. Build a simple GARCH model to forecast volatility. Then, using `Polars`, calculate rolling 30-day correlations and Sharpe ratios. |

---

## Phase 3: Deep Dives into Core AI Problem Domains (Months 7-9)

Now you apply your skills to the specific buckets of problems in finance. We'll tackle two of the most critical ones as examples.

**Goal:** Master the unique challenges of lending/credit and fraud/financial crime.

| Module | Key Topics | Recommended Courses & Resources | Rationale |
| :--- | :--- | :--- | :--- |
| **1. Credit Risk & Lending** | PD/LGD/EAD models, credit scoring, underwriting automation, fair lending compliance (ECOA, HMDA). | **Coursera:** [Credit Risk Management](https://www.coursera.org/learn/credit-risk-management) (Hong Kong Institute). <br> **Read:** "Credit Risk Modeling" by David Lando. <br> **Dataset:** [Home Credit Default Risk](https://www.kaggle.com/competitions/home-credit-default-risk) on Kaggle. | The intersection of high-stakes prediction and strict explainability. Perfect for mastering SHAP and LIME. |
| **2. Fraud & Financial Crime (Adversarial Focus)** | Transaction fraud (real-time), AML network detection (GNNs), synthetic identity fraud. | **Udemy:** [AML and Financial Crime Detection](https://www.udemy.com/course/aml-and-financial-crime-detection-with-real-world-cases/) (focus on detection methods). <br> **Papers:** Read the papers accompanying the Elliptic dataset. <br> **Dataset:** [Elliptic Data Set (Bitcoin)](https://www.kaggle.com/datasets/ellipticco/elliptic-data-set) on Kaggle. | This directly maps to your "Adversarial Intelligence" domain. It's graph-based, noisy, and high-stakes. |
| **3. NLP for Finance** | Sentiment analysis on earnings calls, 10-K information extraction, news summarization. | **Coursera:** [Natural Language Processing with Attention Models](https://www.coursera.org/learn/attention-models-in-nlp) (DeepLearning.AI). <br> **FinBERT:** Explore the [ProsusAI/finBERT](https://huggingface.co/ProsusAI/finBERT) model on Hugging Face. <br> **Dataset:** FiQA (Financial Question Answering) task. | Alternative data is the new oil. Earnings call transcripts are a treasure trove of signal. |
| **Milestone Project 3:** Build a GNN-based AML screener using the Elliptic dataset to classify illicit transactions. Document your model's performance and, crucially, its explainability challenges. |

---

## Phase 4: Specialization: Adversarial Intelligence & Emerging Tech (Months 10-12)

This is your Principal-level differentiator. You'll synthesize everything into the domain you've strategically framed.

**Goal:** Become the go-to expert on the intersection of AI, finance, and adversarial actors.

| Module | Key Topics | Recommended Courses & Resources | Rationale |
| :--- | :--- | :--- | :--- |
| **1. Advanced Graph Neural Networks** | GraphSAGE, GAT (Graph Attention Networks), Temporal GNNs for evolving networks. | **Stanford CS224W:** Continue with the advanced lectures on GNNs and GATs. <br> **Papers:** Read key papers on GNNs for anomaly detection. | This is the technical moat for your domain. |
| **2. Blockchain & On-Chain Analytics** | Wallet clustering, DeFi protocol risk, tracing illicit flows across chains. | **Chainalysis Academy:** (Free, excellent for forensics). <br> **Coursera:** [Bitcoin and Cryptocurrency Technologies](https://www.coursera.org/learn/cryptocurrency) (Princeton). <br> **Tool:** [Dune Analytics](https://dune.com/) - learn to query on-chain data with SQL. | This is the new frontier for financial crime. Understand the data structure to build the models. |
| **3. Adversarial ML & AI Red Teaming** | Model poisoning, evasion attacks, defending against them. This is your RedTeamLoop concept. | **Read:** [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework). <br> **Papers:** Follow research on arXiv for "adversarial attacks on GNNs" and "jailbreaking LLMs." <br> **Project:** Design a red-teaming exercise for a financial LLM (e.g., trying to get it to give bad investment advice). | As AI becomes core to operations, defending the models themselves is critical. This is a green-field area. |
| **4. Agentic AI for Security & Ops** | LangGraph-based agents for alert triage, automated investigation, and incident response. | **DeepLearning.AI:** [AI Agents in LangGraph](https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/). <br> **Read:** LangGraph documentation and use cases. <br> **Concept:** Design an agent that takes a fraud alert, queries a knowledge base, summarizes transaction history, and drafts a SAR (Suspicious Activity Report). | This is the future of operations. An agent that augments a human analyst is a massive force multiplier. |
| **Milestone Project 4 (Capstone):** Build a multi-agent system for "Adversarial Intelligence." It should ingest a stream of transactions, use a GNN to flag a suspicious cluster, query a blockchain explorer for related wallet addresses, and generate a concise intelligence report for a fraud analyst. |

---

## Phase 5: Strategic Communication & The Principal Edge (Months 13+)

Technical depth is useless without influence. This phase is ongoing and focuses on how you present your work.

**Goal:** Frame problems, influence stakeholders, and build your professional brand.

| Module | Key Topics | Recommended Courses & Resources | Rationale |
| :--- | :--- | :--- | :--- |
| **1. Storytelling with Data for Executives** | Moving from "what the model does" to "what the business should do." | **Book:** "Storytelling with Data" by Cole Nussbaumer Knaflic. <br> **Practice:** Take a complex project (e.g., your GNN AML model) and explain it to a hypothetical non-technical CRO in 3 bullet points. | Principal-level conversations are about risk/reward trade-offs, not AUC scores. |
| **2. Regulatory Writing & Communication** | How to write model documentation (Model Development Documents) for regulators. | **Resource:** Find redacted model validation reports online. Study their structure: Purpose, Methodology, Data, Performance, Limitations, Conclusion. <br> **Read:** More SR 11-7. | This is the "language of compliance." A Principal DS is often the one defending the model in a regulatory meeting. |
| **3. Staying Current & Thought Leadership** | Building your network and knowledge. | **Newsletter:** Matt Levine's *Money Stuff* (Bloomberg). <br> **Conferences:** Follow proceedings from ICAIF (ACM International Conference on AI in Finance). <br> **Write:** Publish a blog post or LinkedIn article on a concept from your "Adversarial Intelligence" framework. | You need to be seen as someone who thinks about the future, not just today's ticket. |

This curriculum is a marathon, not a sprint. It’s designed to build a deep, durable, and strategically valuable expertise that will serve you well into a Principal-level career. Good luck
