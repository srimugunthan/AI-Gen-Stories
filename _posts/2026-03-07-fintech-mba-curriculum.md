
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

-----
-----
-----
----
.

---

## Ten AI Problem Domains in Financial Services

| # | Domain | Core ML/AI Problems |
|---|--------|---------------------|
| 1 | **Risk & Compliance** | Credit risk modeling (PD/LGD/EAD), market risk (VaR, stress testing), regulatory compliance automation (KYC/AML), Basel III/IV, CCAR/DFAST |
| 2 | **Fraud & Financial Crime** | Transaction fraud, identity fraud, money laundering network detection, insider trading surveillance, synthetic identity |
| 3 | **Trading & Markets Intelligence** | Algorithmic trading, portfolio optimization, market microstructure, sentiment signals, derivatives pricing, RL-based execution |
| 4 | **Lending & Credit Decisioning** | Underwriting automation, credit scoring, loan pricing, collections optimization, fair lending compliance |
| 5 | **Document Intelligence** | Processing 10-Ks, contracts, earnings calls, regulatory filings; RAG and agentic systems for extraction and summarization |
| 6 | **Customer Intelligence** | Churn prediction, next-best-action, CLV, product recommendation, conversational AI for banking |
| 7 | **Financial Planning & Advisory** | Robo-advisory, goal-based planning, tax-loss harvesting, retirement modeling, LLM-powered interfaces |
| 8 | **Operations & Process Automation** | Reconciliation, payment routing, claims processing, back-office automation — prime territory for LangGraph-style orchestration |
| 9 | **Capital Markets & Research** | Equity research automation, ESG scoring, alternative data, due diligence automation, multimodal analysis |
| 10 | **Payments & Treasury** | Cash flow forecasting, liquidity management, FX optimization, real-time payment fraud, cross-border intelligence |

---

---

## 12-Month Study Plan at a Glance

| Month(s) | Phase | Deliverable / Project |
|----------|-------|-----------------------|
| 1–2 | Phase 1: Financial Mathematics & Econometrics | GARCH volatility analysis on multi-asset portfolio; yield curve construction in Python |
| 2–3 | Phase 2: Financial Products & Markets | Implied volatility surface from CBOE options data using QuantLib; derivatives pricing notebook |
| 4–5 | Phase 3: Risk Management & Regulatory | Full PD model with WoE, XGBoost challenger, SHAP, SR 11-7 style model documentation |
| 5–8 | Phase 4: Adversarial Intelligence | Adversarial ML pipeline on IEEE-CIS: XGBoost + GNN + AGCE noise-robust training + streaming simulation |
| 8–10 | Phase 5: Blockchain & On-Chain Intelligence | GNN illicit transaction classifier on Elliptic dataset; AML typology report |
| 10–12 | Phase 6: Credit, Accounting & Document Intelligence | 10-K Insight Assistant: RAG pipeline over bank filings with RAGAS evaluation |

---

## Phase 1: Financial Mathematics & Econometrics (Months 1–2)

*Build the quantitative foundations before writing a single model.*

Before applying ML to finance, you need to understand the mathematical "laws" of markets: time value of money, fat-tailed distributions, stochastic processes, and time-series dynamics. These underpin every model in risk, pricing, and macro forecasting.

| Module / Topic | Platform & Course | Key Outcomes |
|----------------|-------------------|--------------|
| Time Value of Money, Discounting, Compounding | Coursera — Financial Engineering and Risk Management (Columbia) | DCF, NPV, IRR; bond pricing mechanics |
| Probability & Fat-Tailed Distributions | Coursera — Financial Markets (Yale / Robert Shiller) | Normal vs heavy-tailed distributions; VaR intuition |
| Financial Econometrics: ARIMA, GARCH | Coursera — Econometrics (Erasmus) + DataCamp Time Series track | ARIMA, GARCH volatility modeling, ADF unit root tests |
| Stochastic Processes & Ito Calculus | edX — Introduction to Mathematical Finance (MIT OCW 18.S096) | Brownian motion, Geometric Brownian Motion, Ito's lemma |
| Yield Curves & Interest Rate Dynamics | GARP FRM Part I (free study materials at garp.org) | Term structure, yield curve construction, duration & convexity |
| Cointegration & Pairs Trading Math | Udemy — Algorithmic Trading & Quantitative Analysis | Engle-Granger test, spread modeling, mean-reversion |

### Books for This Phase
- *Options, Futures, and Other Derivatives* — John C. Hull (Chapters 1–10)
- *The Concepts and Practice of Mathematical Finance* — Mark Joshi
- *An Introduction to the Mathematics of Financial Derivatives* — Hirsa & Neftci

### Applied Exercise
Download 5-year daily price data for SPY, GLD, TLT, and USD/INR from Yahoo Finance. Fit GARCH(1,1) to each series. Plot realized vs conditional volatility. Apply ADF tests and document which series are stationary. This single exercise validates ARIMA, GARCH, yield intuition, and time-series reasoning.

---

## Phase 2: Financial Products & Markets (Months 2–3)

*Understand the instruments before modeling them — equities, fixed income, derivatives, FX, structured products.*

A Data Scientist working in banking must be able to reason about the data generated by every financial instrument. This phase covers the mechanics of markets deeply enough for Principal-level conversations with traders, risk officers, and product managers.

| Module / Topic | Platform & Course | Key Outcomes |
|----------------|-------------------|--------------|
| Equities & Equity Markets | Coursera — Financial Markets (Yale / Shiller, free audit) | Market microstructure, order books, corporate actions, dividends |
| Fixed Income: Bonds, Duration, Credit Spreads | Coursera — Bond Valuation (Rice via Coursera) | Pricing, yield, duration, convexity, credit spreads, Z-spread |
| Derivatives: Options & Futures | Coursera — Financial Engineering (Columbia) OR Hull Chapters 9–19 | Black-Scholes, Greeks, put-call parity, futures pricing |
| FX Markets & Cross-Currency | Udemy — Forex Trading Fundamentals | Spot vs forward FX, carry trade, currency risk for banks |
| Structured Products & Securitization | GARP FRM Study Materials (free on garp.org) | MBS, ABS, CDO mechanics; tranching; prepayment risk |
| Commodity Markets | CME Group Education (free — cmegroup.com/education) | Futures specs, basis, contango/backwardation |
| Portfolio Theory & Factor Models | Coursera — Investment Management (Geneva / EDHEC) | CAPM, Fama-French factors, mean-variance optimization |

### Books for This Phase
- *Options, Futures, and Other Derivatives* — Hull (complete text)
- *Advances in Financial Machine Learning* — López de Prado (Chapters 1–5)

### Applied Exercise
Using QuantLib (open-source Python), price a European call option on a stock using Black-Scholes. Then build an implied volatility surface from real options data (CBOE has free data). Plot the volatility smile. This exercise is commonly discussed in Principal-level interviews on model risk.

---

## Phase 3: Risk Management & Regulatory Landscape (Months 4–5)

*The domain where ML meets regulation — credit risk, market risk, operational risk, and Basel.*

Risk management is the primary entry point for Data Science in banking. Understanding how risk metrics feed into regulatory capital requirements (Basel III/IV), stress testing (CCAR/DFAST), and model governance (SR 11-7) is non-negotiable for Principal-level work.

| Module / Topic | Platform & Course | Key Outcomes |
|----------------|-------------------|--------------|
| Credit Risk: PD, LGD, EAD Models | Udemy — Credit Risk Modeling in Python (365 Data Science) | Logistic regression for PD, LGD estimation, EAD, IFRS 9 staging |
| Market Risk: VaR, Expected Shortfall | Coursera — Financial Engineering & Risk Mgmt (Columbia) | Historical simulation VaR, parametric VaR, ES, backtesting |
| Stress Testing: CCAR, DFAST | Federal Reserve public CCAR documents + GARP FRM Part II | Scenario design, loss estimation, capital buffer calculations |
| Basel III/IV Capital Framework | BIS.org — Basel III summary documents (free) | Tier 1/2 capital, RWA, leverage ratio, liquidity coverage ratio |
| SR 11-7 Model Risk Management | OCC Comptroller's Handbook + Fed SR Letter 11-7 (free PDFs) | Model validation, challenger models, conceptual soundness |
| Operational & Liquidity Risk | GARP FRM Part I & II study materials | Op risk capital (AMA), NSFR, LCR, stress liquidity scenarios |
| Fair Lending: ECOA, HMDA, CFPB | CFPB Supervisory Guidance + HMDA Data Explorer (ffiec.cfpb.gov) | Disparate impact, adverse action, fair lending model testing |
| BSA/AML & KYC Compliance | ACAMS free eLearning (acams.org) + FinCEN guidance (fincen.gov) | SAR filing, CDD/EDD, beneficial ownership, transaction monitoring |

### Key Regulatory Documents to Read (All Free)
- Federal Reserve **SR Letter 11-7**: Supervisory Guidance on Model Risk Management
- Basel Committee **BCBS 239**: Risk Data Aggregation and Risk Reporting
- OCC **Comptroller's Handbook** — Credit Risk section
- CFPB **Supervisory Highlights** — Fair Lending editions
- BIS Paper: **Machine Learning in Credit Risk — Implications for Banks**

### Applied Exercise
Build a PD model on the Home Credit Default Risk (Kaggle) dataset: (1) logistic regression baseline with WoE binning, (2) XGBoost challenger, (3) SHAP explanations for each prediction, (4) document as if writing for model validation under SR 11-7. This is a full credit risk model governance workflow.

---

## Phase 4: Adversarial Intelligence — Fraud, AML & Cyber (Months 5–8)

*The domain moat: fraud, financial crime networks, identity attacks, and cyber threats to financial infrastructure.*

Adversarial Intelligence is the highest-leverage domain for a Data Scientist in banking — technically deep, strategically broad, and increasingly in demand. This phase covers all six sub-problems across four sub-tracks.

### 4A. Transaction Fraud Detection

| Module / Topic | Platform & Course | Key Outcomes |
|----------------|-------------------|--------------|
| Fraud Detection Fundamentals | Udemy — Credit Card Fraud Detection with ML (Jose Portilla) | Class imbalance, SMOTE, XGBoost/LightGBM, threshold calibration |
| Real-Time Streaming ML | Coursera — Serverless ML on AWS (DeepLearning.AI) | Kafka + Flink feature stores, <50ms inference patterns |
| Noise-Robust Learning for Fraud | Papers: AGCE loss + arXiv 2106.11325 | Label noise in fraud, bi-tempered loss, transition matrices |
| Calibration & Decisioning | Scikit-learn docs + Niculescu-Mizil & Caruana 2005 | Platt scaling, isotonic regression, tiered risk decisioning |

### 4B. AML & Financial Crime Networks

| Module / Topic | Platform & Course | Key Outcomes |
|----------------|-------------------|--------------|
| Graph ML for AML | Coursera — Graph Neural Networks (DeepLearning.AI, free audit) | GraphSAGE, GAT for transaction network analysis |
| AML Typologies & Regulations | ACAMS free eLearning modules (acams.org) | Layering, structuring, smurfing, correspondent banking risk |
| Alert Triage & SAR Optimization | IEEE papers on SAR false positive reduction | Active learning for alert prioritization, NLP over SARs |
| Temporal Knowledge Graphs | PyTorch Geometric tutorials + Papers with Code | Evolving criminal network representation, dynamic GNNs |

### 4C. Identity & Synthetic Identity Fraud

| Module / Topic | Platform & Course | Key Outcomes |
|----------------|-------------------|--------------|
| Behavioral Biometrics | Udemy — Anomaly Detection in Python (365 Data Science) | Keystroke dynamics, session behavior modeling, isolation forest |
| Document Verification ML | Papers: MIDV-2020 dataset + OpenCV tutorials | OCR, tamper detection on ID documents, liveness detection |
| Synthetic Identity Detection | FRB Working Paper 2019-066 (free, federalreserve.gov) | Identity element reuse, application velocity, graph clustering of synthetics |

### 4D. Cyber Threat Detection for Financial Systems

| Module / Topic | Platform & Course | Key Outcomes |
|----------------|-------------------|--------------|
| Sequence Anomaly Detection | Coursera — Sequences, Time Series & Prediction (TF Specialization) | LSTM/Transformer anomaly detection on user behavior logs |
| Network Traffic Analysis | Udemy — Network Analysis in Python (NetworkX track) | Autoencoder on NetFlow, isolation forest for intrusion detection |
| LLM-Powered SOC Triage | Anthropic Cookbook + LangChain docs (free) | Alert summarization, incident narrative generation, LangGraph orchestration |
| SecOps AI Landscape | MITRE ATT&CK for financial services (attack.mitre.org, free) | Threat framework, TTPs for financial institutions, detection engineering |

### Books & Papers for Phase 4
- *Advances in Financial Machine Learning* — López de Prado (Chapters 17–20)
- *Machine Learning for Asset Managers* — López de Prado
- arXiv: GNN-based Fraud Detection Survey (2023) — search "fraud detection GNN survey"
- FATF: Virtual Assets Red Flag Indicators (free, fatf-gafi.org)

### Phase 4 Capstone Project
Build an end-to-end Adversarial Intelligence pipeline on the **IEEE-CIS Fraud Detection dataset**: (1) Baseline XGBoost with class imbalance handling, (2) GNN layer for account/device/IP relationships using PyTorch Geometric, (3) SHAP-based explainability panel, (4) noise-robust training with AGCE loss, (5) streaming simulation with latency benchmarks. This is a Principal-level portfolio piece.

---

## Phase 5: Blockchain, Crypto & On-Chain Intelligence (Months 8–10)

*The emerging frontier: blockchain forensics, DeFi risk, tokenization, and on-chain AML.*

Blockchain intersects with banking primarily through crypto-related AML, tokenized assets, CBDC infrastructure, and DeFi risk assessment. The AI problems — wallet clustering, graph analytics on transaction DAGs, anomaly detection on-chain — are methodologically close to existing GNN expertise.

| Module / Topic | Platform & Course | Key Outcomes |
|----------------|-------------------|--------------|
| Blockchain Fundamentals | Coursera — Bitcoin and Cryptocurrency Technologies (Princeton, free) | Consensus (PoW/PoS), Merkle trees, UTXO vs account model, smart contracts |
| Ethereum & Smart Contracts | Udemy — Ethereum and Solidity: The Complete Developer's Guide | EVM, Solidity basics, DeFi protocol mechanics (Uniswap, Aave) |
| On-Chain Analytics & Wallet Clustering | Chainalysis Academy (free — academy.chainalysis.com) | Heuristic clustering, change address detection, OSINT on wallets |
| DeFi Risk & Protocol Analysis | *DeFi and the Future of Finance* — Campbell Harvey (book + free lectures) | Liquidity pools, impermanent loss, smart contract exploit patterns |
| Crypto AML & Regulatory Landscape | FATF Guidance on Virtual Assets (free) + FinCEN Travel Rule docs | Travel Rule, KYT (Know Your Transaction), sanctions on-chain |
| Tokenization of Real-World Assets | BIS Working Papers on tokenization (free, bis.org) | Tokenized bonds, repo on blockchain, JPMorgan Onyx case study |
| CBDC Architecture & Implications | IMF Working Paper WP/22/12 — CBDC (free, imf.org) | Retail vs wholesale CBDC, privacy tradeoffs, monetary policy implications |
| ML on Blockchain Data | Kaggle — Elliptic Bitcoin Dataset (labeled graph fraud) | GNN on UTXO graph, illicit transaction classification, chain analysis |

### Books for This Phase
- *Mastering Bitcoin* — Andreas Antonopoulos (Chapters 1–8 for data/forensics angle)
- *Mastering Ethereum* — Antonopoulos & Wood (Chapter 14: DEX and DeFi)
- *DeFi and the Future of Finance* — Campbell Harvey et al.

### Data Sources & Tools
- **Kaggle Elliptic Dataset** — Bitcoin transaction graph with illicit/licit labels (ideal GNN project)
- **Google BigQuery Public Datasets** — `bitcoin_blockchain`, `crypto_ethereum` (free tier)
- **Dune Analytics** — SQL-based on-chain analytics, free tier available
- **Etherscan API** — transaction data, token transfers, contract events (free tier)
- **Glassnode / Nansen** — institutional-grade on-chain metrics (paid, but research reports free)

### Phase 5 Project
Train a GNN on the Elliptic Bitcoin dataset to classify illicit transactions. Extend with temporal features (transaction timing, cluster velocity). Write a short report framing it as a regulatory submission: what patterns indicate mixing behavior? How would this integrate into a bank's crypto-exposure monitoring workflow?

---

## Phase 6: Document Intelligence, Credit & Macro (Months 10–12)

*Completing the picture: lending, financial statements, LLM-powered document extraction, and macro modeling.*

### 6A. Credit & Lending Deep Dive

| Module / Topic | Platform & Course | Key Outcomes |
|----------------|-------------------|--------------|
| Credit Scoring & FICO Architecture | Udemy — Credit Risk Modeling in Python (365 Data Science) | Scorecard construction, WoE/IV, population stability index |
| Loan Lifecycle & Collections | CFPB Consumer Credit Panel data + FDIC academic datasets | Delinquency roll rates, vintage analysis, collections model design |
| CECL Loan Loss Provisioning | FASB ASC 326 summary + Fed papers on CECL transition | Current Expected Credit Loss, lifetime PD curves, macro conditioning |
| Alternative Data for Thin-File Credit | Lending Club data (Kaggle) + academic papers | Cash flow underwriting, rent/utility data, buy-now-pay-later scoring |

### 6B. Financial Statements & Accounting

| Module / Topic | Platform & Course | Key Outcomes |
|----------------|-------------------|--------------|
| Reading Balance Sheets & Income Statements | Coursera — Financial Accounting Fundamentals (UVA, free audit) | Assets/liabilities/equity structure, P&L drivers, ROAE, NIM |
| Cash Flow Analysis | Coursera — Business Analytics (Wharton, free audit) | OCF vs FCF, cash conversion cycle, liquidity ratios |
| GAAP vs IFRS Essentials | CFA Level 1 Study Materials (free portions on CFA Institute site) | Fair value accounting, loan loss provisioning, IFRS 9 vs GAAP |
| Bank Financial Analysis | *Bank Management and Financial Services* — Peter Rose (text) | Analyzing bank earnings, NIM compression, deposit funding costs |

### 6C. Document Intelligence & LLM Systems for Finance

| Module / Topic | Platform & Course | Key Outcomes |
|----------------|-------------------|--------------|
| 10-K & Earnings Call Processing | SEC EDGAR Full-Text Search API (free) + LangChain docs | Extraction pipelines, entity recognition in filings, RAG over 10-Ks |
| Contract Intelligence & Clause Extraction | Hugging Face FinBERT + CUAD dataset (free) | NER on legal text, obligation extraction, risk clause detection |
| Financial RAG Systems | LangChain / LlamaIndex tutorials (free on their docs sites) | Chunking strategies for financial documents, hybrid retrieval, RAGAS evaluation |
| Agentic Finance Workflows | LangGraph documentation + LangSmith tracing | Multi-agent orchestration for document analysis, tool-use for financial data |

### 6D. Macroeconomics & Macro Factor Models

| Module / Topic | Platform & Course | Key Outcomes |
|----------------|-------------------|--------------|
| Monetary Policy & Interest Rate Dynamics | Coursera — Economics of Money and Banking (Columbia / Perry Mehrling) | Fed funds rate, transmission mechanism, yield curve inversions |
| Business Cycles & Recession Indicators | FRED API tutorials (Federal Reserve Bank of St. Louis, free) | Leading indicators, credit spreads as predictors, Sahm Rule |
| Macro Conditioning of Financial Models | BIS Working Papers (free) + academic papers | Macro-conditional PD models, GDP stress scenarios, climate risk factors |
| Alternative Data & Nowcasting | *Advances in Financial ML* — López de Prado (Chapter 3) | Satellite data, Google Trends, credit card data as real-time macro signals |

### Phase 6 Project
Build the **10-K Insight Assistant**: ingest 10 annual reports from US banks, extract risk factor disclosures using FinBERT + RAG, build a structured comparison table of risk exposures, and score each bank's credit risk narrative for sentiment and severity. Evaluate with RAGAS (FactualCorrectness, SummarizationScore). This directly connects to your existing RAGAS evaluation pipeline work.

---

## Full Course Directory

### Coursera

| Course | Institution | Relevance |
|--------|-------------|-----------|
| Financial Markets | Yale (Robert Shiller) | Phases 1 & 2 — markets intuition, valuation, risk |
| Financial Engineering & Risk Management | Columbia | Phases 1, 2, 3 — derivatives, risk metrics, VaR |
| Bond Valuation & Analysis | Rice | Phase 2 — fixed income pricing |
| Investment Management with Python | EDHEC / Geneva | Phase 2 — portfolio theory, factor models |
| Graph Neural Networks Specialization | DeepLearning.AI | Phase 4 — GNNs for fraud/AML |
| Bitcoin & Cryptocurrency Technologies | Princeton | Phase 5 — blockchain fundamentals |
| Economics of Money and Banking | Columbia (Perry Mehrling) | Phase 6 — monetary policy, macro |
| Sequences, Time Series, Prediction | DeepLearning.AI (TF Specialization) | Phase 4 — sequence models, anomaly detection |
| Econometrics (Methods & Applications) | Erasmus | Phase 1 — ARIMA, GARCH, hypothesis testing |
| Financial Accounting Fundamentals | UVA Darden | Phase 6 — balance sheets, income statements |
| Business Analytics Specialization | Wharton | Phase 6 — cash flow, financial analysis |
| Serverless ML on AWS / MLOps | DeepLearning.AI / AWS | Phase 4 — real-time inference, feature stores |

### edX

| Course | Institution | Relevance |
|--------|-------------|-----------|
| Mathematical Finance (18.S096) | MIT OCW | Phase 1 — stochastic calculus, Ito lemma |
| Blockchain for Business | Linux Foundation | Phase 5 — enterprise blockchain, Hyperledger |
| Data Analysis: Statistical Modeling | MIT | Phase 1 — econometrics, regression for finance |

### Udemy

| Course | Relevance |
|--------|-----------|
| Credit Risk Modeling in Python (365 Data Science) | Phases 3 & 6 — end-to-end PD model, WoE, scorecard |
| Algorithmic Trading & Quantitative Analysis | Phases 1 & 2 — backtesting, strategy, pairs trading |
| Ethereum and Solidity: Complete Developer's Guide | Phase 5 — EVM, smart contracts, DeFi mechanics |
| Anomaly Detection in Python (365 Data Science) | Phase 4C — isolation forest, autoencoders, LOF |
| Python for Finance: Algorithmic Trading (Lazy Programmer) | Phases 2 & 3 — pricing, portfolio optimization |
| Network Analysis in Python / NetworkX | Phase 4 — graph analytics for cyber/fraud |

### Free / Open Access Resources

| Resource | Platform / URL | Relevance |
|----------|----------------|-----------|
| GARP FRM Study Materials | garp.org (free sections) | Phase 3 — comprehensive risk management syllabus |
| Chainalysis Academy | academy.chainalysis.com | Phase 5 — on-chain forensics, AML blockchain |
| Fed SR Letter 11-7 | federalreserve.gov | Phase 3 — model risk management bible |
| MITRE ATT&CK for Finance | attack.mitre.org | Phase 4D — cyber threat framework for banks |
| FATF Virtual Asset Guidance | fatf-gafi.org | Phases 4 & 5 — AML for crypto |
| BIS Working Papers | bis.org/research | All phases — Basel, CBDC, crypto risk, AI in finance |
| CFPB Supervisory Guidance | cfpb.gov | Phase 3 — fair lending, ECOA, HMDA |
| MIT OCW Finance Courses | ocw.mit.edu | Phases 1–3 — derivatives, corporate finance, investments |
| OCC Comptroller's Handbook | occ.gov | Phase 3 — banking activities, credit risk |
| Princeton Bitcoin Crypto Course | coursera.org (free audit) | Phase 5 — blockchain architecture |
| FRED API + St. Louis Fed Research | fred.stlouisfed.org | Phase 6 — macro data, economic indicators |
| SEC EDGAR Full-Text API | efts.sec.gov | Phase 6 — 10-K extraction, filing analysis |

---

## Recommended Books

| Book | Focus Area & Why It Matters |
|------|-----------------------------|
| *Options, Futures, and Other Derivatives* — John Hull | The gold standard. Covers every instrument. Essential for Phases 2 & 3. |
| *Advances in Financial Machine Learning* — López de Prado | Bridges ML and finance. Must-read for Principal-level interviews. |
| *Machine Learning for Asset Managers* — López de Prado | Portfolio ML, feature engineering from price data, overfitting in finance. |
| *Credit Risk Modeling* — David Lando | Structural and reduced-form credit models; academic depth on PD/LGD. |
| *Financial Risk Management* — Steve Allen | Practitioner-oriented. Covers risk systems as they exist in real banks. |
| *Bank Management and Financial Services* — Peter Rose | Banking industry structure, funding, NIM, capital management. |
| *Mastering Bitcoin* — Andreas Antonopoulos | Technical blockchain internals; essential for on-chain analytics work. |
| *DeFi and the Future of Finance* — Campbell Harvey | DeFi primitives, protocol risk, institutional implications. |
| *The Mathematics of Financial Derivatives* — Hirsa & Neftci | Mathematical foundations: SDEs, PDEs, numerical methods. |
| *Concepts & Practice of Mathematical Finance* — Mark Joshi | Practical quant math; recommended before diving into Hull derivatives. |

---

## Certifications & Professional Development

Certifications are not required, but the study curricula are independently valuable. The FRM Part I & II syllabus alone is one of the best structured finance curricula available.

| Certification | Time Investment | Value for Finance DS |
|---------------|-----------------|----------------------|
| **FRM Part I (GARP)** | 200–300 hrs; exam optional | Best structured risk curriculum available. Covers VaR, credit risk, Basel, liquidity — exactly what banking DS teams use. |
| **CFA Level 1 (CFA Institute)** | 300 hrs; exam optional | Broad financial literacy: equities, fixed income, derivatives, ethics. Level 1 alone is a strong foundation. |
| **ACAMS CAMS (AML)** | 100–150 hrs; exam optional | AML/KYC/BSA expertise. Directly relevant to fraud & financial crime work. Recognized by compliance teams. |
| **AWS Certified ML Specialty** | 100 hrs | Validates cloud MLOps skills; useful if deploying fraud/risk models on AWS infrastructure. |
| **Chainalysis Reactor Certification** | 40–60 hrs (free) | On-chain analytics and blockchain forensics. Highly specific to crypto AML work. |

---

## Key Datasets for Applied Projects

| Dataset | Domain | Use Case |
|---------|--------|----------|
| IEEE-CIS Fraud Detection (Kaggle) | Transaction Fraud | Tabular + GNN fraud detection; class imbalance, feature engineering |
| Home Credit Default Risk (Kaggle) | Credit Risk | PD modeling, CECL pipeline, alternative data credit scoring |
| Elliptic Bitcoin Dataset (Kaggle) | Blockchain Forensics | GNN on Bitcoin transaction graph; illicit/licit labels; ideal for AML |
| HMDA Loan Application Data (FFIEC) | Fair Lending | Disparate impact analysis, fair lending model testing, CFPB compliance |
| SEC EDGAR Full-Text Filings (API) | Document Intelligence | 10-K extraction, risk factor NLP, RAG over financial filings |
| FRED Economic Data (St. Louis Fed) | Macro / Credit Risk | Macro-conditional models, recession indicators, yield curve data |
| Google BigQuery: crypto_bitcoin | On-Chain Analytics | Full Bitcoin UTXO history; wallet clustering, chain tracing |
| Bank of England / ECB Market Data | Market Risk | Government bond yields, FX rates, volatility indices |
| QuantLib Sample Data + CBOE Options | Derivatives Pricing | Options chain data for implied volatility surface construction |
| Lending Club Historical Data (Kaggle) | Credit & Collections | Vintage analysis, delinquency roll rates, LGD estimation |

---

## Staying Current: Reading & Following the Field

A Principal Data Scientist is expected to know what's happening at the frontier — in research, regulation, and industry.

### Industry Publications
- **Risk.net** — industry standard for quant finance and risk modeling
- **American Banker / The Banker** — banking strategy, regulation, fintech
- **BIS Quarterly Review** — macro and financial system analysis
- **Matt Levine's Money Stuff (Bloomberg)** — makes finance intuitive; read daily
- **GARP Risk Intelligence** — weekly risk management updates

### Academic Journals
- Journal of Financial Economics
- Journal of Banking & Finance
- Review of Financial Studies
- BIS Working Papers (bis.org)
- Federal Reserve Finance & Economics Discussion Series (FEDS)

### AI/ML in Finance Conferences
- **ICAIF** — ACM International Conference on AI in Finance (key venue for finance ML papers)
- **KDD** Financial Technology track
- **NeurIPS** — Workshop on Machine Learning for Finance
- **arXiv:** q-fin and cs.LG sections for preprints

### Newsletters & Communities
- Finimize — daily financial news digest
- The Block / CoinDesk — crypto and DeFi news
- Messari Research — institutional crypto analysis
- Vitalik Buterin's blog (vitalik.eth.limo) — Ethereum ecosystem depth

### Regulatory Sources to Monitor
- Federal Reserve Press Releases — federalreserve.gov/newsevents
- OCC News Releases — occ.gov/news-issuances
- CFPB Supervisory Highlights — cfpb.gov/data-research/research-reports
- FinCEN Advisories — fincen.gov/resources/advisories
- FATF Mutual Evaluation Reports and Guidance Notes

> **The Fastest Path to Domain Knowledge**
>
> Reading is necessary but insufficient. The highest ROI activity is sitting with business stakeholders — risk officers, credit analysts, compliance leads, fraud investigators. Ask them what keeps them up at night. The mental models you build from those conversations are far more valuable than any textbook, and they'll serve you in Principal-level discussions where you're expected to frame problems, not just solve them.

---

*Version 1.0 | March 2026*

-----
# Can you surive 10 years with this knowledge?
Honest answer: **partially, but not fully — and the gap matters.**

Mastering this curriculum gets you deep domain fluency and a strong technical foundation. That's genuinely rare and valuable. But "surviving 10 years with AI" is a different question from "knowing a lot about finance and ML." Here's the real breakdown.

---

**What this curriculum protects well**

The regulatory and judgment-heavy work is highly durable. SR 11-7 model validation, fair lending compliance, AML typology reasoning, stress testing design — these require contextual judgment, accountability, and regulatory relationships that AI cannot own. A regulator doesn't accept "the model said so." Someone has to sign off, explain, and defend. That role stays human for the foreseeable future.

Deep adversarial intelligence is also durable because the threat model is adversarial *and* evolving. Fraudsters adapt to whatever detection system exists. That requires human reasoning about attacker behavior, not just pattern matching on historical data.

---

**Where this curriculum is insufficient for 10 years**

The curriculum is a strong *2026 snapshot*, but finance AI is moving fast in three directions this doesn't fully cover:

**Agentic systems are replacing pipelines.** The curriculum touches LangGraph and RAG, but the deeper shift is that entire workflows — document review, alert investigation, credit memo writing, reconciliation — are becoming agent orchestration problems. In 5 years, a lot of what junior and mid-level DS do today (feature engineering, model tuning, report generation) will be agent-automated. The 10-year survivor isn't the person who *builds* those pipelines — it's the person who *designs the system architecture and owns the outcomes*.

**The model-building commodity problem is real.** XGBoost, logistic regression, even GNNs — the execution of standard model types is getting automated. AutoML, foundation model fine-tuning, and AI-assisted code generation are compressing the value of "I can build a credit risk model" toward zero. What doesn't compress: knowing *which* model is appropriate given regulatory constraints, *why* a model is failing in production, and *how* to explain it to a non-technical risk committee.

**Domain knowledge alone isn't the moat — problem framing is.** This curriculum gives you the knowledge to understand financial problems. But the 10-year moat is being the person who *defines* what problem is worth solving, *scopes* it correctly given business and regulatory context, and *translates* between business intent and technical execution. That's a skill this curriculum doesn't explicitly train — it comes from years of stakeholder exposure and deliberate practice.

---

**What you'd need to add for genuine 10-year durability**

Three things sit outside this curriculum that matter as much as the content inside it:

The first is **AI system design literacy** — not just using LLMs and agents, but understanding when agentic architectures break, how to evaluate them, how to build guardrails, and how to govern them under regulatory scrutiny. Your Shield-Fin and RedTeamLoop work points in exactly this direction. That instinct needs to become a core competency, not a side project.

The second is **organizational leverage**. A Principal who survives isn't just technically deep — they make other people and teams more effective. That means mentoring, writing internal frameworks others adopt, influencing model governance standards, and being the person risk committees call before making decisions. This curriculum builds the knowledge substrate for that, but the leverage itself has to be deliberately cultivated.

The third is **continuous horizon scanning**. The curriculum is a 12-month investment, but the field will look meaningfully different in 2028. The durable habit is staying close to what's emerging — not just reading papers, but asking "what does this mean for how my organization will work in 3 years?" and positioning yourself ahead of that shift. The people who got disrupted by AI weren't ignorant — they were excellent at the *previous* paradigm and didn't notice the ground moving.

---

**The honest bottom line**

If you master this curriculum *and* develop strong problem-framing instincts *and* build organizational leverage *and* stay ahead of the agentic shift — then yes, 10 years is very survivable, probably at increasing seniority. The domain knowledge here is deep enough that AI will augment you rather than replace you, because the judgment layer in financial services has regulatory teeth.

If you master this curriculum but stay primarily in execution mode — building models, running pipelines, delivering analyses — the 10-year picture is shakier. Not because the knowledge is wrong, but because AI compresses execution value faster than domain value.

The curriculum is necessary. It's not sufficient. The difference is what you do with the knowledge once you have it.
