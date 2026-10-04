# Complete Application Workplan
## Direct Farmer-to-Buyer Market Access Platform (ML-Enabled MVP)

---

## 1. Executive Summary

This document is a complete, industry-aligned development workplan for building the Direct Farmer-to-Buyer Market Access Platform as a fully functional, ML-enhanced application - evolving it from a basic hackathon prototype into a technically credible, demonstrable system. It covers prior art, related research, architecture, technology selection, machine learning design, database and API design, a phased development timeline, team structure, testing, security, and deployment - structured the way a real product team would plan a short product cycle.

The platform's core purpose remains unchanged: reduce the price information gap between farmers and buyers in Sri Lanka's agricultural supply chain. What changes here is depth - this version includes a genuine ML component (fair-price prediction) rather than a purely CRUD-based prototype, is grounded in documented research on this exact problem, and follows software engineering practices suitable for academic and industry evaluation.

---

## 2. Problem Statement (Refined)

Sri Lankan farmers frequently sell produce through multiple layers of intermediaries, receiving a reduced share of the final retail price due to a lack of real-time market price visibility and limited direct access to buyers. This platform addresses that gap by combining:

1. A **direct listing and discovery system** connecting farmers and buyers.
2. A **data-driven fair-price suggestion feature**, so farmers have an objective reference point when setting an asking price, rather than relying solely on what a single buyer tells them.

**Target Users:** Small-to-medium scale farmers, local retailers, small buyers (shops, guest houses, bulk purchasers).

---

## 3. Related Existing Projects & Prior Art

This problem space is well-trodden - both by real deployed products and by student-level projects. Reviewing these matters for two reasons: it lets the team position their work honestly in presentation ("this problem is validated, here is our specific contribution"), and it prevents the team from unknowingly rebuilding something that already exists without a clear point of differentiation.

### 3.1 Deployed, Real-World Products (Sri Lanka)

- **[Govipola](https://www.themorning.lk/articles/22416)** - Sri Lanka's first dedicated agriculture marketplace app. Connects farmers directly to buyers, shows real-time price/order-book data, supports multiple languages, and reportedly reached roughly 10,000 active farmers within six months of launch. This is the closest real-world equivalent to the platform described in this workplan and is worth studying as a functional benchmark. Additional coverage: [Sunday Times](https://www.sundaytimes.lk/190922/business-times/govipola-mobile-app-creates-dynamic-digital-marketplace-for-farmers-369435.html)
- **[Agrimarket.lk](https://agrimarket.lk/)** - An active Sri Lankan farmers' marketplace platform (available in Sinhala/Tamil/English) with region-based produce listings.
- **TradeNet ("Govi Gnana")** - An earlier LIRNEasia-led ICT initiative connecting Sri Lankan farmers to Dambulla wholesale market price data via mobile phones; documented in the research listed in Section 4.

### 3.2 Comparable Student / Academic-Level Projects

Useful for calibrating scope and complexity - these show what a beginner-to-intermediate team can realistically build in an academic timeframe:

- **[FarmCartlk](https://github.com/Ruzan-Mohamed/FarmCartlk)** - Sri Lanka-focused farmer marketplace project.
- **[FarmConnect](https://github.com/lakshikaariyathilaka/FarmConnect)** - "Digital marketplace prototype connecting farmers and shops in Sri Lanka" - very close in framing to this workplan's MVP scope.
- **[AgriDirect](https://github.com/reezmahanan/AgriDirect)** - Farmer-direct marketplace project.
- **[KisanDirect](https://github.com/SaiVatsal/45-agriculture-farmer-app)** - "Farmer-Buyer Marketplace," a full-stack academic project (India-focused, architecturally comparable).
- **[Accreage Mart](https://accreage-mart-fe.vercel.app/)** - An AI-powered agricultural B2B marketplace demo; a useful reference for how an ML/AI layer can be framed on top of a similar core platform.

**Recommendation for the team:** Reference Govipola briefly in the presentation as proof the problem is real and commercially validated, while being explicit that this project's differentiator is the ML-based fair-price suggestion feature (Section 9), since the core marketplace mechanic is already a well-established pattern.

---

## 4. Related Research & Literature

The following academic and industry sources ground both the problem statement and the ML approach. Citing 2–3 of these in the project report or presentation strengthens academic credibility by showing the work is built on documented research rather than assumption.

### 4.1 Problem Grounding - Market Information Asymmetry & Middlemen

- de Silva, H. (LIRNEasia) - [*Agricultural Market Development through Information and Communication Technology (ICT): A Developing Country Experience*](https://www.researchgate.net/publication/23941248_Harsha_de_Silva_Director_E-development_Labs_private_Limited_and_Senior_Economist_LIRNEasia_-_Agricultural_Market_Development_through_Information_and_Communication_Technology_ICT_A_Developing_Country_E) - Documents LIRNEasia's TradeNet initiative in Sri Lanka; direct prior evidence that ICT-based price information sharing measurably helps farmers.
- [*TradeNet: The Mobile Trade Platform*](https://silo.tips/download/tradenet-the-mobile-trade-platform-for) - Project documentation of the Sri Lankan mobile trade platform referenced above.
- [*Towards Using ICT to Enhance Flow of Information to Aid Farmer Sustainability in Sri Lanka*](https://www.researchgate.net/publication/235424315_Towards_using_ICT_to_Enhance_Flow_of_Information_to_aid_Farmer_Sustainability_in_Sri_Lanka) - Sri Lanka-specific study on information flow gaps affecting farmers.
- [*Market Efficiency on Vegetable Commodities in Developing Countries: Case Study from Dambulla Wholesale Market, Sri Lanka*](https://www.researchgate.net/publication/275983845_Market_Efficiency_on_Vegetable_Commodities_in_Developing_Country_Case_Study_from_Dambulla_Wholesale_Market_in_Sri_Lanka) - Directly relevant to the core problem statement; a strong citation for why the price-gap problem is real and measurable in the Sri Lankan context specifically.
- Mitra, S. et al. (International Growth Centre) - [*Asymmetric Information and Middleman Margins: An Experiment*](https://www.theigc.org/sites/default/files/2015/02/Mitra-Et-Al-2012-Working-Paper.pdf) - Economics working paper giving the formal theoretical basis for why middleman margins arise from information asymmetry; useful for the report's problem-justification section.
- [*Ranking the Factors Influencing e-Trading Usage in Agricultural Marketing*](https://www.academia.edu/50861400/Ranking_the_Factors_Influencing_e_Trading_Usage_in_Agricultural_Marketing) - Relevant for justifying design/adoption decisions (e.g., why simplicity and local-language support matter for farmer adoption).

### 4.2 ML Approach - Crop Price Prediction

- [*Predicting Agricultural Commodities Prices with Machine Learning: A Review of Current Research*](https://arxiv.org/abs/2310.18646) (arXiv, 2023) - A recent survey of ML approaches to crop price prediction; a strong single citation to justify the overall ML strategy.
- [*A Methodology for Crop Price Prediction Using Machine Learning*](https://ieeexplore.ieee.org/document/10031852/) (IEEE) - Methodology reference supporting the regression-based approach recommended in Section 9.
- [*Agricultural Commodity Price Prediction Model: A Machine Learning Framework*](https://dl.acm.org/doi/abs/10.1007/s00521-023-08528-7) (Neural Computing and Applications) - Supports the baseline-to-improved-model reasoning used in Section 9.3.
- [*An Innovative Deep Learning Based Approach for Accurate Agricultural Crop Price Prediction*](https://arxiv.org/abs/2304.09761) (arXiv) - Useful as a "future work" citation if the team wants to note a deep-learning upgrade path beyond this MVP's scope.

**Recommendation for the team:** Cite the Dambulla market study and the de Silva/TradeNet paper on the problem-statement slide - they are Sri Lanka-specific and immediately credible to local judges - and cite the arXiv ML review paper when justifying the regression-based model choice in the technical section.

---

## 5. Solution Overview

| Layer | Capability |
|---|---|
| Core Platform | Listing creation, browsing/filtering, buyer-farmer connect |
| ML Layer | Fair-price suggestion engine based on historical price trends |
| ML Layer (Stretch) | Farmer-buyer relevance matching (content-based recommendation) |
| Admin Layer | Listing moderation, basic reporting |

---

## 6. System Architecture

```
                        ┌───────────────────────┐
                        │      Web Frontend       │
                        │   (React + Tailwind)    │
                        └───────────┬─────────────┘
                                    │ REST/HTTPS
                        ┌───────────▼─────────────┐
                        │     Backend API          │
                        │  (Node.js/Express)       │
                        │  - Auth (future phase)   │
                        │  - Listings CRUD         │
                        │  - Connect requests      │
                        └───────┬──────────┬───────┘
                                │          │
                 ┌──────────────▼──┐   ┌───▼─────────────────┐
                 │   Relational DB  │   │   ML Microservice     │
                 │   (PostgreSQL)   │   │   (Python/FastAPI)    │
                 │  Users, Listings,│   │  Price prediction,    │
                 │  PriceHistory    │   │  matching logic       │
                 └──────────────────┘   └────────────────────────┘
```

**Why this shape:** Separating the ML component into its own microservice (rather than embedding it in the main backend) is standard industry practice - it lets the Python-based ML stack evolve independently of the Node.js application stack, and keeps the core CRUD application simple to maintain and demo.

---

## 7. Recommended Technology Stack (with Justification)

| Component | Recommendation | Justification |
|---|---|---|
| Frontend | React + Tailwind CSS | Fast to build, component-driven, widely used in industry, team likely has partial exposure |
| Backend API | Node.js + Express | Lightweight, fast to prototype, large ecosystem, easy JSON handling |
| Database | PostgreSQL | Strong relational integrity for structured listing/price data; free-tier hosting available (Supabase, Neon) |
| ML Microservice | Python + FastAPI | FastAPI is lightweight, async-friendly, and standard for serving ML models via REST |
| ML Libraries | scikit-learn, pandas | Simple, explainable models are more defensible in a presentation than a black-box deep learning model for this data size |
| Version Control | Git + GitHub | Industry standard; enables commit-history-based collaboration evaluation |
| CI/CD | GitHub Actions | Free, integrates directly with GitHub, runs lint/test on every push |
| Containerization | Docker (backend + ML service) | Ensures consistent environment between development and demo/deployment |
| Hosting (Frontend) | Vercel or Netlify | Free tier, zero-config React deployment |
| Hosting (Backend/ML) | Render or Railway | Free tier, supports Docker deployments |

---

## 8. Core Features & Scope

### 8.1 Must-Have (Core MVP)
- Farmer produce listing (crop, quantity, location, asking price, contact)
- Buyer browse/search/filter by crop type and district
- "Express Interest" action revealing farmer contact details
- Admin view to moderate/remove inappropriate listings

### 8.2 ML-Enabled Features
- **Fair-Price Suggestion Engine:** When a farmer enters a crop type and district, the system suggests a price range based on historical price trend data for that crop.
- **Farmer-Buyer Relevance Matching (Stretch Goal):** Rank listings shown to a buyer using a simple content-based similarity score (crop type match, location proximity, recency).

### 8.3 Explicitly Deferred (Future Phase, Not This Cycle)
- Online payments/escrow
- Delivery/logistics coordination
- Full user authentication and verified farmer profiles
- Multi-language UI (Sinhala/Tamil) - noted as a required future phase given the target users
- Live external market price feed integration

---

## 9. Machine Learning Component Design

### 9.1 Problem Framing
The fair-price suggestion is framed as a **regression problem**: given crop type, district, and month, predict an expected price range (LKR/kg) based on historical patterns.

### 9.2 Data Requirements and Sourcing
- **Primary option:** Publicly available historical price data from Sri Lanka's Department of Agriculture / HARTI (Hector Kobbekaduwa Agrarian Research and Training Institute) market price bulletins, where accessible.
- **Fallback for hackathon timeline:** A structured synthetic dataset generated to reflect realistic seasonal price variation per crop, clearly labelled as synthetic/illustrative in the presentation. This is an acceptable and common approach when real data acquisition is time-constrained - the key evaluation point is that the modeling *approach* is sound, not that the dataset is production-grade.
- **Minimum viable dataset:** At least 5–8 common crops × 12 months of price observations to allow a meaningful trend model.

### 9.3 Model Selection and Justification
| Approach | Use Case | Why |
|---|---|---|
| Linear Regression | Baseline price trend | Fast, interpretable, easy to explain to judges |
| Random Forest Regressor | Improved accuracy over baseline | Handles non-linear seasonal patterns better, still explainable via feature importance |
| Simple moving average / basic time-series smoothing | Fallback if data is very limited | Extremely simple, still demonstrates data-driven reasoning |

**Recommendation:** Start with Linear Regression as the working baseline (fast to implement, easy to defend in Q&A), and upgrade to Random Forest if time permits, showing a before/after accuracy comparison as an evaluation artifact.

### 9.4 Evaluation Approach
- Train/test split (e.g., 80/20) on the historical price dataset.
- Report Mean Absolute Error (MAE) as the primary metric - easy to explain as "average price prediction error in LKR."
- Include a simple actual-vs-predicted chart as a presentation artifact.

### 9.5 Integration
- ML microservice exposes a single endpoint: `POST /predict-price` accepting `{ crop, district, month }`, returning `{ suggested_min, suggested_max, confidence_note }`.
- Backend calls this endpoint when a farmer is creating a listing and displays the suggestion as a non-mandatory guide (farmer can still set their own price).

---

## 10. Database Design (Entity Overview)

| Table | Key Fields |
|---|---|
| `users` | id, name, role (farmer/buyer/admin), contact_number, district |
| `listings` | id, farmer_id, crop_type, quantity, unit, asking_price, district, status (open/resolved), created_at |
| `price_history` | id, crop_type, district, month, avg_price (used to train/serve the ML model) |
| `connect_requests` | id, listing_id, buyer_id, status, created_at |

---

## 11. API Design (Core Endpoints)

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/api/listings` | Create a new produce listing |
| GET | `/api/listings?crop=&district=` | Browse/filter listings |
| PATCH | `/api/listings/:id/status` | Mark listing as resolved (admin) |
| POST | `/api/listings/:id/connect` | Buyer expresses interest |
| POST | `/api/ml/predict-price` | Get ML fair-price suggestion (proxied to ML microservice) |

---

## 12. Development Workplan (Phased Timeline)

Recommended as a **4–6 week cycle**, structured in sprints so it can also be compressed into a shorter hackathon-style sprint if needed.

| Phase | Duration | Deliverables |
|---|---|---|
| **Phase 0 - Planning & Design** | Week 1 | Finalized scope, wireframes, DB schema, API contract, dataset sourced/prepared |
| **Phase 1 - Core Platform Build** | Weeks 2–3 | Listing creation, browse/filter, connect-request flow, admin moderation view |
| **Phase 2 - ML Integration** | Week 4 | Price prediction model trained, ML microservice built, integrated into listing form |
| **Phase 3 - Testing & Hardening** | Week 5 | Unit + integration tests, bug fixes, basic security review, UI polish |
| **Phase 4 - Deployment & Demo Prep** | Week 6 | Dockerized deployment, hosted live demo, presentation deck, rehearsed walkthrough |

**Compressed hackathon variant (if the real event is 24–48 hours):** Compress Phases 0–2 into Day 1, and Phases 3–4 into Day 2, dropping the Random Forest upgrade and relevance-matching stretch goal to protect the core deliverable.

---

## 13. Team Roles & Responsibilities

| Role | Responsibility |
|---|---|
| Team Lead / Backend Dev | API design, database, backend-ML integration |
| Frontend Dev | React UI, listing form, browse/filter view |
| ML/Data Lead | Dataset preparation, model training, ML microservice |
| UI/UX & QA | Wireframes, usability checks, test case execution |
| Presenter/Documentation Lead | Pitch deck, demo script, README, presentation delivery |

*In a small beginner team, roles can be merged (e.g., one person covers both ML and backend), but each responsibility above should have a clearly named owner.*

---

## 14. Testing & QA Strategy

- **Unit tests:** Core backend logic (listing validation, filter logic) using Jest or Mocha.
- **Integration tests:** API endpoint tests confirming listing → browse → connect flow works end-to-end.
- **ML model validation:** Train/test split evaluation as described in Section 9.4, documented with actual metric values.
- **Manual UAT (User Acceptance Testing):** At least one non-technical person (e.g., a fellow student unfamiliar with the build) walks through the app and the team records friction points.

---

## 15. Security & Best-Practice Considerations

- Input validation and sanitization on all form submissions (prevent injection/XSS).
- Environment variables (`.env`, excluded from Git) for database credentials and API keys - never hard-coded.
- HTTPS enforced on all deployed endpoints.
- Basic rate limiting on public endpoints (e.g., `express-rate-limit`) to prevent listing spam.
- Even though full authentication is deferred, contact information should only be revealed after an explicit "Express Interest" action, not shown openly, as a basic privacy safeguard.

---

## 16. Deployment Strategy

- Backend and ML microservice containerized separately with Docker; `docker-compose` for local development parity.
- GitHub Actions pipeline: run lint + tests on every push to `main`; deploy on successful merge.
- Frontend deployed via Vercel/Netlify (auto-deploy from `main` branch).
- Backend/ML deployed via Render or Railway free tier, using the same Docker images tested locally.

---

## 17. Updated Evaluation Rubric

| Criterion | Weight | What Is Being Assessed |
|---|---|---|
| Problem Understanding & Real-World Grounding | 10% | Can the team explain the price-gap problem, cite supporting research (Section 4), and justify the ML approach's relevance? |
| Core Platform Implementation | 25% | Does the listing → browse → connect flow work end-to-end? |
| ML Component Implementation | 20% | Is the price prediction model trained, evaluated, and genuinely integrated (not hardcoded)? |
| Code Quality & Architecture | 15% | Is the codebase modular, documented, and reasonably version-controlled? |
| Testing & Robustness | 10% | Evidence of tests, error handling, and honest acknowledgement of known limitations |
| Presentation & Communication | 15% | Clear explanation of both the real-world problem and technical decisions, including trade-offs |
| Team Collaboration | 5% | Evidence of task division (commit history, role clarity) |

---

## 18. Risk Assessment & Mitigation

| Risk | Likelihood | Mitigation |
|---|---|---|
| Real price data unavailable/hard to source in time | Medium | Use a clearly labelled synthetic dataset as fallback (Section 9.2) |
| ML integration takes longer than planned | Medium | Keep Linear Regression as the guaranteed baseline; treat Random Forest and matching as stretch goals only |
| Team underestimates core platform effort | High (common in beginner teams) | Enforce Phase 1 completion before any ML work begins - a working core app with a weak ML feature beats a broken app with a strong one |
| Presentation focuses only on tech, not real-world impact | Medium | Require the presentation script to open with the farmer's real economic problem (citing Section 4 research) before touching architecture |
| Judges perceive the idea as unoriginal (Govipola already exists) | Medium | Proactively acknowledge prior art (Section 3) and lead with the ML differentiator as the project's specific contribution |

---

## 19. Success Metrics (for Demo/Evaluation Day)

- Core flow (list → browse → connect) completes without errors in a live demo.
- ML price suggestion returns a plausible, explainable result for at least 3 different crop/district combinations.
- Team can state the model's MAE and explain what it means in plain language.
- Team can name at least two specific, honest limitations of the current build.
- Team can name at least one existing product (Section 3) and one research source (Section 4) and articulate this project's point of differentiation.

---

## 20. Suggested Repository Structure

```
farmer-market-platform/
├── frontend/              # React app
├── backend/               # Node.js/Express API
├── ml-service/            # Python/FastAPI ML microservice
│   ├── data/               # Historical or synthetic price dataset
│   ├── train_model.py
│   └── app.py
├── docker-compose.yml
├── .github/workflows/      # CI pipeline
└── README.md               # Setup, architecture overview, demo instructions
```

---

*This workplan is intentionally structured so it can scale down into a compressed hackathon sprint (Section 12) or scale up into a full multi-week capstone-style build, depending on the actual event format and time available.*
