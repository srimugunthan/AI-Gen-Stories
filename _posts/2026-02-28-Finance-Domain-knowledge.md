# Finance domain knowledge

## Core Knowledge Areas to Master

**1. Financial Products & Markets**
Understand the mechanics of equities, fixed income, derivatives, structured products, FX, and commodities. You don't need to be a trader, but you need to reason about the data these products generate and the risks they carry.

**2. Risk Management**
This is central to banking DS work — credit risk (PD, LGD, EAD models), market risk (VaR, stress testing), operational risk, and liquidity risk. Understand Basel III/IV regulatory frameworks, CCAR/DFAST stress testing, and how models feed into capital adequacy.

**3. Regulatory & Compliance Landscape**
SR 11-7 (model risk management), Fair Lending (ECOA, HMDA), BSA/AML regulations, and KYC. Understanding *why* regulators care about explainability and fairness directly shapes how you build models.

**4. Financial Statements & Accounting**
Reading balance sheets, income statements, cash flow statements. Understanding GAAP basics, loan loss provisioning (CECL), and how financial health is assessed.

**5. Credit & Lending**
Underwriting processes, credit scoring (FICO, internal scorecards), loan lifecycle, delinquency/default patterns, collections strategies. This is bread-and-butter for banking DS.

**6. Fraud & Financial Crime**
Transaction monitoring, suspicious activity detection, network analysis for money laundering, identity fraud patterns. You're already exploring this with your GNN fraud detection work.

**7. Payments & Treasury**
Wire transfers, ACH, real-time payments, correspondent banking, cash management — increasingly important as banks digitize.

**8. Macroeconomics & Econometrics**
Interest rate dynamics, yield curves, inflation, monetary policy, business cycles. These are the exogenous variables that drive most financial models.

---

## Recommended Resources

**Books**
- *Options, Futures, and Other Derivatives* — John Hull (the gold standard for derivatives)
- *Financial Risk Management* — Steve Allen (very practitioner-oriented)
- *Credit Risk Modeling* — David Lando
- *The Concepts and Practice of Mathematical Finance* — Mark Joshi
- *Advances in Financial Machine Learning* — Marcos López de Prado (bridges ML and finance beautifully)
- *Machine Learning for Asset Managers* — López de Prado
- *Bank Management and Financial Services* — Peter Rose
- *An Introduction to the Mathematics of Financial Derivatives* — Ali Hirsa & Salih Neftci

**Certifications & Structured Learning**
- **FRM (Financial Risk Manager)** — highly relevant for banking DS; the curriculum alone is an excellent structured syllabus even if you don't sit the exam
- **CFA Level 1** — gives broad financial literacy; Level 1 alone covers a lot of ground
- **Coursera/edX**: Yale's *Financial Markets* (Robert Shiller), NYU's risk management courses
- **GARP** (Global Association of Risk Professionals) — free webinars and whitepapers

**Regulatory Reading**
- OCC Comptroller's Handbook (free, covers every banking activity)
- Federal Reserve SR Letters (especially SR 11-7)
- Basel Committee publications (bis.org)
- CFPB guidance documents

**Staying Current**
- *Risk.net* — industry-standard for quant finance and risk
- *Journal of Financial Economics*, *Journal of Banking & Finance*
- BIS Working Papers and Fed research papers
- Matt Levine's *Money Stuff* newsletter (Bloomberg) — makes finance intuitive and entertaining
- *The Banker*, *American Banker*

**Applied / DS-Specific**
- Kaggle financial datasets and competitions
- QuantLib (open-source quantitative finance library)
- Papers from KDD, ICAIF (ACM Conference on AI in Finance)

## Practical Advice

The fastest way to build domain knowledge isn't just reading — it's **sitting with business stakeholders**. Spend time with risk officers, credit analysts, compliance teams, and product managers. Ask them what keeps them up at night. The mental models you build from those conversations are far more valuable than textbook knowledge alone, and they'll serve you well in Principal-level discussions where you're expected to frame problems, not just solve them.

Would you like me to create a structured reading plan or deep-dive into any of these areas?

## Blockchain and crypto
Fair point! I didn't include it because in traditional banking (especially at Wells Fargo, which has historically been conservative on crypto), blockchain/crypto hasn't been a core DS focus area. But you're right that it's increasingly relevant — here's why and what to cover:

## Why It Matters for Finance DS

Crypto and blockchain are intersecting with banking in several ways now: digital asset custody, stablecoin payments, CBDC (Central Bank Digital Currency) exploration, DeFi risk assessment, and critically — **crypto-related fraud/AML detection**, which directly connects to your fraud detection work.

## Key Knowledge Areas

**Blockchain Fundamentals** — consensus mechanisms (PoW, PoS), smart contracts, tokenization, distributed ledger architecture. You need to understand the data structures to reason about on-chain analytics.

**Cryptocurrency Markets** — Bitcoin, Ethereum, stablecoins (USDT, USDC), how exchanges work, order book dynamics, market microstructure differences from traditional finance.

**DeFi (Decentralized Finance)** — lending protocols (Aave, Compound), DEXs (Uniswap), yield farming, liquidity pools. These are creating new financial primitives that traditional finance is watching closely.

**Regulatory Landscape** — SEC vs CFTC jurisdiction debates, MiCA (EU), RBI's stance on crypto in India, AML/KYC requirements for crypto (Travel Rule), and how banks are expected to handle digital asset exposure under Basel crypto-asset standards.

**On-Chain Analytics & DS Applications** — wallet clustering, transaction graph analysis (this ties directly into your GNN work), whale tracking, anomaly detection on blockchain data, Chainalysis-style forensics.

**Tokenization of Real-World Assets** — this is where traditional banking and blockchain converge most. Tokenized bonds, real estate, trade finance — JPMorgan's Onyx, Goldman's GS DAP are real examples.

## Resources

**Books**
- *Mastering Bitcoin* — Andreas Antonopoulos (technical deep-dive)
- *Mastering Ethereum* — Antonopoulos & Wood
- *The Bitcoin Standard* — Saifedean Ammous (economic philosophy)
- *DeFi and the Future of Finance* — Campbell Harvey et al.

**Courses**
- Princeton's *Bitcoin and Cryptocurrency Technologies* (Coursera, free)
- Berkeley's *Blockchain Fundamentals* (edX)
- Chainanalysis Academy (free — great for forensics/AML angle)

**For the DS/ML Angle**
- Elliptic dataset on Kaggle (Bitcoin transaction fraud — labeled graph dataset, perfect for your GNN experiments)
- Dune Analytics — SQL-based on-chain analytics platform
- Google BigQuery public blockchain datasets (Bitcoin, Ethereum)
- Papers from IEEE and ACM on blockchain anomaly detection

**Staying Current**
- *The Block*, *CoinDesk* for industry news
- Messari research reports
- BIS and IMF working papers on CBDC and stablecoins
- Vitalik Buterin's blog (surprisingly accessible for deep technical thinking)

## The Banking-Specific Angle

What matters most for your role is understanding how crypto **creates risk and opportunity for banks** — not becoming a crypto trader. Focus on: how does a bank evaluate crypto custody risk? How do you detect layering through crypto on/off ramps? What does tokenized settlement mean for payments infrastructure? These are the questions that'll come up at Principal-level strategy discussions.

The Elliptic Kaggle dataset in particular would be a great applied project — it's a graph-based fraud detection problem that directly leverages your GNN expertise.

Want me to put together a consolidated reading plan covering both traditional finance and crypto/blockchain?


## 
This comprehensive curriculum is designed specifically for a **Data Scientist in the Finance Domain** in 2026. It balances core technical skills with the specific "Quant" knowledge required to navigate high-stakes financial environments.

---

## **Phase 1: The Quantitative Foundation (Months 1–2)**

Before coding, you must understand the mathematical "laws" of the market.

* **Financial Mathematics:** Time value of money ($TVM$), compounding, and discounting.
* **Probability & Statistics:** Normal vs. "Fat-tailed" distributions (common in market crashes), Hypothesis testing (p-values in trading signals).
* **Financial Econometrics:** Time-series analysis ($ARIMA$, $GARCH$ for volatility), Cointegration, and Unit Root tests.
* **Calculus & Linear Algebra:** Optimization techniques for portfolio management and understanding the "Greeks" in options.

---

## **Phase 2: The Technical Powerhouse (Months 3–4)**

The 2026 tech stack moves beyond basic Python into high-performance computing.

* **Python for Finance:** Mastery of `Pandas`, `NumPy`, and `SciPy`.
* **High-Speed Data:** Learning `Polars` or `PySpark` for handling "Tick Data" (millisecond-level market movements).
* **SQL for Finance:** Window functions for calculating rolling averages and running totals in transaction databases.
* **Cloud & MLOps:** Using **AWS SageMaker** or **Databricks** to deploy models that must run with zero downtime.

---

## **Phase 3: Deep Finance Domain Knowledge (Months 5–7)**

This is where you differentiate yourself from a generalist Data Scientist.

* **Financial Instruments:** Detailed mechanics of Equities, Fixed Income (Bonds), FX, and Derivatives (Options/Futures).
* **Risk Management:** Calculating **Value at Risk (VaR)**, **Expected Shortfall (ES)**, and conducting Stress Tests.
* **Portfolio Theory:** Mean-Variance Optimization and the **Black-Litterman Model**.
* **Regulatory Knowledge:** Understanding **GDPR**, **BASEL IV**, and **SEC** reporting requirements for AI models.

---

## **Phase 4: Advanced AI & Alt-Data (Months 8–10)**

Applying the latest 2026 AI trends to financial forecasting.

* **Alternative Data NLP:** Using LLMs (like GPT-4o or specialized Finance-LLMs) to perform sentiment analysis on earning calls and central bank speeches.
* **Reinforcement Learning:** Training "Agents" for automated execution and algorithmic trading.
* **Graph Neural Networks (GNNs):** Using graph data to detect complex **Anti-Money Laundering (AML)** patterns and fraud networks.

---

## **Phase 5: Capstone & Portfolio (Months 11–12)**

Build three distinct projects to prove your domain expertise:

1. **Credit Scoring Model:** Build an end-to-end pipeline to predict loan defaults using an imbalanced dataset.
2. **Trading Strategy Backtester:** Develop a momentum-based strategy, including transaction costs and slippage.
3. **Market Risk Dashboard:** A real-time PowerBI/Streamlit app showing a portfolio's VaR across different market scenarios.

---

### **Top Recommended Resources**

* **Books:** *Options, Futures, and Other Derivatives* by John C. Hull; *Advances in Financial Machine Learning* by Marcos López de Prado.
* **Platforms:** **QuantConnect** (for backtesting), **Kaggle** (Financial datasets), and **CFA Institute** (Level 1 curriculum).
