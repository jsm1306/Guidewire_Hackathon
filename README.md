# Guidewire_Hackathon
GUARDIAN NETWORK
AI-Powered Parametric Insurance for India's Gig Workers
 

DEVTrails 2026 – Phase 1 Submission
Team: Tinkerers




 Quick Overview

Problem: Income loss for gig workers due to disruptions
Solution: AI-powered parametric insurance with auto payouts
Key Innovation: Multi-layer fraud detection + trust scoring
Differentiator: Detects coordinated fraud rings (not just individuals)
Wow Feature: Weather Shadow Map









By Team Tinkerers:
Sindhu J
Sri Aashritha K
Varshitha G
Snehitha B 
1. Executive Summary

Guardian Network is an AI-powered parametric insurance platform for gig delivery workers in India. It protects against income loss caused by external disruptions such as extreme weather, AQI spikes, cyclones, and curfews.

The system requires zero manual claims — disruptions are detected automatically and payouts are triggered instantly via UPI.

Key Highlights
	Target Users: Delivery partners (Zomato, Swiggy, Zepto, Blinkit, ONDC)
	Coverage Model: Parametric triggers based on real-time external data
	Pricing: Weekly opt-in (₹15–₹60 based on zone risk & activity)
	Payout Speed: < 90 seconds after trigger confirmation
	Fraud Defense: Behavioural trust scoring over a rolling usage history
	Platform: Android-first mobile app (with PWA fallback)
	AI Usage: Dynamic pricing, fraud detection, real-time risk alerts
2. The Problem & Persona-Based Scenarios
2.1  Who We Are Building For
India has over 12 million registered gig delivery workers. The vast majority earn ₹400–₹800 per day with zero income protection. A single rain event, an AQI spike can wipe out an entire week's earnings. Existing insurance products require paperwork, have long claim cycles, and are designed for salaried employees - not daily-wage riders on two-wheelers.

2.2  Persona Scenarios
Persona A - Ravi, Hyderabad (Flood Zone Rider)
Scenario	July monsoon. Ravi's delivery zone - Himayatnagar - receives 62mm of rainfall in 3 hours. Roads flood. Orders dry up. He earns ₹0 between 2 PM and 7 PM.

Guardian Network workflow for Ravi:
•	IMD rainfall API logs 62mm in Ravi's pincode polygon - exceeds the ₹200 threshold of 50mm.
•	Ravi's trust score is 820 (built over 9 weeks of verified active riding). Auto-approve triggered.
•	System cross-checks: his cell tower history confirms he was in the zone; accelerometer shows he stopped moving, consistent with road flooding, device and behavioral signals confirm inactivity.
•	UPI payout of ₹200 hits his PhonePe wallet at 2:09 PM. He never opened the app.
•	He receives a push notification: 'Rain disruption detected in your area. ₹200 credited. Stay safe.'

Persona B - Meera, Bengaluru (AQI Disruption)
Scenario	October Diwali week. AQI in Meera's zone - Koramangala - crosses 420 for 4 consecutive hours. She has mild asthma and stops riding at noon.

Guardian Network workflow for Meera:
•	CPCB AQI data feed registers AQI 423 at the nearest monitoring station mapped to Meera's zone.
•	Meera is in her 3rd week. Trust score is 540 - above the 500 threshold after 15–20 verified claims.
•	Payout of ₹300 processed automatically. No verification challenge needed given trust score > 500.
•	She also receives a real-time safety alert with a route map showing lower-AQI corridors - sourced from our NDMA/CPCB data tie-up.

Persona C - Kumar, Mumbai (Cyclone Alert)
Scenario	IMD issues a Cyclone Alert for the Mumbai coastal zone. Kumar's zone - Worli - is within the warned area. He stays home.

Guardian Network workflow for Kumar:
•	IMD cyclone alert API fires for the zone polygon.
•	System does not wait for Kumar to stop moving - the alert itself is the trigger. ₹1,000 payout initiates.
•	Kumar receives an advance safety alert 12 hours before the trigger payout: 'Cyclone warning for your area. Avoid Zone B routes. Your insurance will activate automatically if the alert persists.'
•	Real-time incident map (integrated with NDMA/rescue teams) pushed to all workers in the zone.

3. Weekly Premium Model
3.1  Design Philosophy
Monthly premiums fail gig workers because income is irregular. A worker who earns nothing in a bad week cannot afford a monthly deduction. The weekly opt-in model matches the financial rhythm of gig work: workers earn week-by-week and protect week-by-week. Each Monday, workers choose to activate their cover for the coming week. They can skip any week with zero penalty.

3.2  Premium Calculation Formula
Formula	Weekly Premium = Base Rate × Zone Risk Multiplier × Engagement Discount

Factor	Range	How It's Determined
Base Rate	₹20 / week	Actuarial minimum for the product to be solvent
Zone Risk Multiplier	1.0× – 3.0×	Historical disruption frequency in the worker's home zone (last 24 months of weather, AQI, curfew data)
Engagement Discount	0.75× – 1.0×	Workers active for 4+ weeks get up to 25% discount. Incentivises retention.
Resulting Range	₹15 – ₹60 / week	Low-risk zone, engaged worker → ₹15. High-risk zone, new worker → ₹60.


Examples:
•	Ravi (Himayatnagar, Hyderabad - high flood risk zone, 8 weeks active): ₹20 × 2.4 × 0.80 = ₹38/week
•	Meera (Koramangala, Bengaluru - moderate AQI risk, 3 weeks active): ₹20 × 1.8 × 0.92 = ₹33/week
•	New worker in a low-risk zone: ₹20 × 1.0 × 1.0 = ₹20/week

3.3  Zone-Based Risk Differentiation
Premium is tightly coupled to locality, not just city. The platform divides every city into micro-zones (approximately 2–4 km radius polygons, aligned to PIN code clusters). Each zone carries an independent risk score derived from:
•	Historical rainfall frequency and intensity (IMD 24-month data)
•	Historical AQI exceedance days (CPCB data)
•	Government-declared disaster zone classifications (NDMA registry)
•	Historical claim frequency from our own platform data (grows over time)
•	Flood plain and elevation data (open government GIS data)
A worker's zone is determined by their primary working area - the geographic centroid of their last 4 weeks of order activity - not their home address. This ensures pricing reflects actual exposure, not registered address (which is often in a different area for migrant workers).

4. Parametric Trigger System
4.1  How It Works
Parametric insurance pays out when a pre-agreed objective parameter crosses a threshold - no human assessment required. Our system monitors live government and meteorological data feeds and automatically initiates payouts when conditions are met in a worker's active zone.

Key Principle	The trigger is the claim. Workers never file anything. The system monitors, detects, and pays.

4.2  Trigger Table
Trigger Event	Threshold	Payout
Heavy Rainfall	Rainfall > 50mm in 3 hours (zone polygon)	₹200
Extreme AQI	AQI > 400 for 2+ consecutive hours	₹300
Cyclone Alert	IMD Cyclone/Severe Cyclone Warning for zone	₹1,000
Civil Curfew / Section 144	Official government order for zone	₹500
Flood Alert (govt declared)	NDMA / State govt flood warning for zone	₹400
Heatwave Alert	IMD heatwave alert + temperature > 45°C in zone	₹150
Multiple triggers in 24h	Two or more triggers fire in same day	Sum, capped at ₹1,500/day

4.3  Data Sources
Data Feed	Provider
Rainfall / Weather	India Meteorological Department (IMD) API
Air Quality Index	Central Pollution Control Board (CPCB) API
Cyclone / Disaster Alerts	NDMA (National Disaster Management Authority)
Curfew / Section 144	State Police / District Administration (web scraping + manual verification)
Flood Zone Mapping	NRSC GIS open data


5. Platform Choice - Mobile App (Android-First)
5.1  Decision and Rationale
We chose a native Android app as the primary platform, with a Progressive Web App (PWA) fallback for devices that cannot install the app. The rationale is straightforward and grounded in the realities of Indian gig workers:

Factor	Why Mobile (not Web)
Sensor access	Accelerometer, gyroscope, cell tower ID, and ambient signals are only accessible via native mobile APIs - impossible on web
Background operation	Claims must trigger even when the app is closed. Native background services handle this; PWAs cannot reliably.
Offline resilience	Workers operate in low-connectivity zones. The app caches behavioral data locally and syncs when online.
UPI integration	Deep-link UPI payment flows work natively on Android via Intent system.
Device diversity	99%+ of target users use Android. iOS is irrelevant for this demographic.
Push notifications	Real-time safety alerts require reliable push delivery - FCM on Android is far more reliable than web push.

The PWA fallback exists for workers on very old devices (Android 5 and below) or those who cannot install apps due to storage constraints. The PWA offers manual claim submission with photo proof - less automated, but accessible.

 
6. AI/ML Integration Plan
6.1  Overview
AI/ML is embedded at three distinct points in the product workflow: premium calculation before the week begins, fraud detection at claim time, and real-time risk communication throughout the week. Each layer uses models that are practical to train and deploy.

6.2  Module 1: Dynamic Premium Pricing

We use a Gradient Boosted Regressor (XGBoost) to calculate a personalized weekly premium for each worker before the Monday opt-in window. The model runs server-side as a scheduled batch process.
It considers multiple factors: historical disruption frequency in the worker’s zone over the past 24 months, seasonal risk (for example, increased rainfall during monsoon), the worker’s engagement history and active weeks, their primary working zone derived from recent activity, and short-term weather forecasts for the upcoming week.
The model outputs a single premium value in rupees, which is communicated to the worker at the start of each week.

6.3  Module 2: Fraud Detection - Three-Layer Architecture
Layer A: Isolation Forest (per-worker anomaly detection)

This layer builds a behavioral baseline for each worker using a rolling history. It runs both on-device and server-side.
It detects inconsistencies such as sudden changes in working location, unrealistic inactivity during claimed disruptions, mismatches between GPS and network signals, and unusually precise claim timings. These signals help identify users whose behavior deviates from their normal patterns.

Layer B: Graph Neural Network (network-level fraud ring detection)

We model workers as nodes in a graph, where connections represent shared working zones, overlapping time windows, or network-level similarities.
During a claim event, we analyze the group of active claimants and compare it with normal working patterns. Genuine workers typically form loosely connected, geographically consistent groups. In contrast, fraud rings appear as tightly connected clusters with abnormal similarity and no organic linkage to real workers in that zone.
We use embedding and clustering techniques to identify such dense clusters. If a group shows significantly higher internal similarity than expected, it is flagged as a coordinated fraud attempt.

Layer C: Time-Series Anomaly Detection (synchronized spike detection)

Real disruptions cause gradual claim patterns over time, as workers stop working at different moments. Fraud attacks, however, often produce sudden spikes, where many claims are triggered within a short window.
We monitor claim volume trends and detect abnormal spikes that deviate significantly from expected patterns. When such spikes occur, payouts are temporarily paused and routed for review, preventing large-scale fund drain.

6.4  Trust Score System
Every worker has a dynamic trust score (0–1000) that evolves over time. This score gates the verification requirement at claim time.

Trust Score Band	System Behavior
0–399	All claims held in escrow. Human review within 24 hours. Worker notified of 'processing delay' - no fraud language.
400–499	Micro-challenge: 3-second video of surroundings. Scene classifier checks weather consistency.
500–749	No verification needed for first 15–20 claims. Peer attestation option offered.
750–1000	Full auto-approve. Payout in under 90 seconds. No friction whatsoever.

Trust score increases with: each verified legitimate claim, consistent weekly opt-in, behavioral consistency with established patterns, and positive peer attestation from other high-trust workers. Trust score decreases with: flagged anomalies, failed verification challenges, and cluster association with detected fraud rings.

Key rule	After 15–20 verified legitimate claims with trust score > 500, the worker enters the auto-approve tier permanently unless a new anomaly is detected. Trust is earned, not assumed - but once earned, it is honoured.

6.5  Model Evolution Over Time
The system learns from every outcome:
•	Confirmed legitimate claim → behavioural pattern strengthened as positive example in Isolation Forest
•	Confirmed fraud → cluster traits added as negative examples; model retrained weekly
•	Fraud ring detected → ring's spoofing pattern logged and added to adversarial test set
•	Premium model recalibrated monthly as actual claim frequency data accumulates by zone
This creates compounding adversarial resilience: attackers who fail teach the system exactly how they operate.

7. Real-Time Safety Alert System
7.1  The Feature
Guardian Network is not just insurance - it is a real-time safety intelligence layer for delivery workers. In partnership with NDMA, state disaster response teams, and municipal authorities, the app pushes geo-targeted alerts to workers in affected zones before and during disruptions.

•	Advance warnings: cyclone alerts 12–24 hours ahead, flood zone activations, curfew notices
•	Route intelligence: real-time map overlay showing safe vs disrupted corridors, sourced from government rescue team data
•	Incident markers: live crowdsourced pins from verified workers (flooded road, waterlogging)
•	Emergency contacts: nearest government-empanelled clinic, NDMA helpline, zone-specific rescue team number

Partnership Strategy	We integrate with NDMA's ICRN (Incident Communication and Response Network) API and State Police data feeds. This positions Guardian Network as a government-aligned safety infrastructure.

7.2  Weather Shadow Map - The Wow Factor Feature
Before enrolling, any delivery worker can open the app and see a city-level 'income shadow map' - a heat map overlay showing which zones have experienced the most trigger events in the past 90 days, with aggregated (anonymized) payout data per zone.
This does two things:
•	Proves the product is real before the worker spends a single rupee - they can see that real money was paid to workers in their area
•	Acts as a professional intelligence tool - workers can identify which zones to avoid during high-risk periods, and which zones offer the best risk-adjusted earnings
This map is the product's primary organic growth driver. Workers show it to each other. Distribution becomes peer-to-peer.

8. UX Design - Built for Low-Income, Low-Literacy Users
8.1  Core UX Principles
•	Zero default action: workers do nothing to receive payouts. The app works in the background.
•	Visual-first: the app uses icons and colour over text wherever possible. Hindi language default with regional language options.
•	2G-tolerant: all core functions (claim processing, trust score update, alert display) work on 2G. Heavy content (map) lazy-loads.
•	Low storage: app target < 15MB installed. No video features in core flow.
•	Battery-conscious: background services use Android WorkManager with adaptive scheduling - no battery drain on low-charge devices.

8.2  Graceful Verification (Never Harsh Blocking)
The system never uses the word 'fraud', never accuses workers, and never hard-blocks a payment. All verification is framed as 'routine processing':
•	Trust 400–499: 'We're confirming your location - tap to take a quick 3-second video.' (Scene classifier runs in background.)
•	Trust < 400 or cluster flag: 'Your payment is being processed. It will arrive within 24 hours.' (Human review queue, escrowed funds.)
•	Peer attestation: 'Two riders near you can confirm the disruption - we've sent them a quick ping.' (No action required from the claimant.)

8.3  The Trust Passport
Each worker sees their trust score as a 0–5 star rating in the app home screen. The stars grow visibly over weeks. Higher trust = faster payouts + higher coverage limits + lower premiums.
Workers with 5-star trust scores can refer others and receive a ₹50 credit when the referred worker completes their first 4 weeks. This turns the fraud-prevention mechanism into a growth engine - the workers most invested in the system's legitimacy are the ones most motivated to bring in genuine workers.

 
9. Tech Stack 
Layer	Technology	Rationale
Mobile App	React Native (Android-first)	Single codebase, native sensor access, large Indian developer pool
Backend API	FastAPI (Python)	Fast to build, async support, native ML library integration
ML Models	scikit-learn, PyTorch Geometric, statsmodels	Isolation Forest (sklearn), GNN (PyG), ARIMA (statsmodels)
Database	PostgreSQL + TimescaleDB	Relational for worker data; Timescale for time-series behavioral logs
Graph Engine	Neo4j (free tier) or NetworkX	Worker social graph for GNN fraud detection
Real-time Alerts	Firebase Cloud Messaging (FCM)	Reliable push on Android, free tier sufficient
Weather / AQI	IMD API + CPCB API + OpenWeatherMap fallback	Primary: government sources. Fallback: commercial for gaps.
Payments	Razorpay UPI Payout API	Instant UPI disbursement, supports bulk payouts
Hosting	AWS (EC2 + RDS) or Render.com	Render for speed; AWS for production
Map / GIS	MapLibre GL (open source)	No per-tile cost; works with NRSC GIS data
PWA Fallback	Next.js	Shares API layer with mobile app


10. Why Guardian Network Stands Out
10.1  What Makes This Different
Dimension	Our Differentiation
Fraud architecture	Behavioural identity as the primary trust primitive - not GPS verification. Trust is earned over 6 weeks, not asserted at claim time.
Fraud ring defense	Graph-based detection of coordinated attacks
Zone-level pricing	Premiums based on micro-zone risk polygons, not city-level averages. Hyderabad flood-zone ≠ Hyderabad hilltop.
Real-time safety	NDMA/government data tie-up for advance warnings and evacuation routes - positions us as public safety infrastructure.
Trust Passport	Fraud prevention becomes a worker benefit and a growth mechanism. High-trust workers earn better terms and refer others.
Weather Shadow Map	Proves the product before enrolment. Zero-cost, zero-marketing distribution engine.
Graph thinking	Using GNN + DBSCAN on claimant social graphs is genuinely novel for parametric insurance. It is architecturally hard to replicate quickly.

The test of a great system	The adversarial constraint (fraud rings) made the product better for genuine workers, not just safer. Faster payouts, smarter pricing, a safety intelligence layer, and a trust economy that rewards honest participation - all derived from designing against the hardest attack first.

11. Appendix - Key Assumptions & Constraints
Assumption / Constraint	Mitigation
IMD API availability and latency	OpenWeatherMap commercial fallback; 5-minute polling interval acceptable for parametric triggers
Workers may share devices	Device fingerprint combined with SIM identity; multi-identity detection flags for manual review
Low-connectivity zones	On-device Isolation Forest runs offline; claim queued locally and submitted when connected
Workers may have < 6 weeks history	New worker defaults to mid-trust (400) with manual review option; trust builds quickly with legitimate usage
Razorpay UPI payout limits	Payouts > ₹5,000/day per worker require KYC - enforced at enrollment. Daily cap: ₹1,500 per policy.
Platform API access (Zomato/Swiggy)	Consent-based OAuth. Fallback: order activity inferred from movement + timing if API not granted.
Regulatory (IRDAI)	Parametric insurance in India requires IRDAI sandbox participation. We position as a technology layer partnered with a licensed insurer.

