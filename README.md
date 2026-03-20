# GUARDIAN NETWORK
## AI-Powered Parametric Insurance for India's Gig Workers

**DEVTrails 2026 – Phase 1 Submission**  
**Team: Tinkerers**

---

## Quick Overview

- **Problem:** Income loss for gig workers due to disruptions
- **Solution:** AI-powered parametric insurance with auto payouts
- **Key Innovation:** Multi-layer fraud detection + trust scoring
- **Differentiator:** Detects coordinated fraud rings (not just individuals)
- **Wow Feature:** Weather Shadow Map

---

## Team Members

**By Team Tinkerers:**
- Sindhu J
- Sri Aashritha K
- Varshitha G
- Snehitha B

---

## 1. Executive Summary

Guardian Network is an AI-powered parametric insurance platform for gig delivery workers in India. It protects against income loss caused by external disruptions such as extreme weather, AQI spikes, cyclones, and curfews.

The system requires **zero manual claims** — disruptions are detected automatically and payouts are triggered instantly via UPI.

### Key Highlights

| Aspect | Details |
|--------|---------|
| **Target Users** | Delivery partners (Zomato, Swiggy, Zepto, Blinkit, ONDC) |
| **Coverage Model** | Parametric triggers based on real-time external data |
| **Pricing** | Weekly opt-in (₹15–₹60 based on zone risk & activity) |
| **Payout Speed** | < 90 seconds after trigger confirmation |
| **Fraud Defense** | Behavioural trust scoring over a rolling usage history |
| **Platform** | Android-first mobile app (with PWA fallback) |
| **AI Usage** | Dynamic pricing, fraud detection, real-time risk alerts |

---

## 2. The Problem & Persona-Based Scenarios

### 2.1 Who We Are Building For

India has over 12 million registered gig delivery workers. The vast majority earn ₹400–₹800 per day with zero income protection. A single rain event or an AQI spike can wipe out an entire week's earnings. Existing insurance products require paperwork, have long claim cycles, and are designed for salaried employees—not daily-wage riders on two-wheelers.

### 2.2 Persona Scenarios

#### Persona A - Ravi, Hyderabad (Flood Zone Rider)

**Guardian Network workflow for Ravi:**

1. IMD rainfall API logs 62mm in Ravi's pincode polygon - exceeds the ₹200 threshold of 50mm.
2. Ravi's trust score is 820 (built over 9 weeks of verified active riding). Auto-approve triggered.
3. System cross-checks: his cell tower history confirms he was in the zone; accelerometer shows he stopped moving, consistent with road flooding; device and behavioral signals confirm inactivity.
4. UPI payout of ₹200 hits his PhonePe wallet at 2:09 PM. He never opened the app.
5. He receives a push notification: *'Rain disruption detected in your area. ₹200 credited. Stay safe.'*

#### Persona B - Meera, Bengaluru (AQI Disruption)

**Guardian Network workflow for Meera:**

1. CPCB AQI data feed registers AQI 423 at the nearest monitoring station mapped to Meera's zone.
2. Meera is in her 3rd week. Trust score is 540 - above the 500 threshold after 15–20 verified claims.
3. Payout of ₹300 processed automatically. No verification challenge needed given trust score > 500.
4. She also receives a real-time safety alert with a route map showing lower-AQI corridors - sourced from our NDMA/CPCB data tie-up.

#### Persona C - Kumar, Mumbai (Cyclone Alert)

**Guardian Network workflow for Kumar:**

1. IMD cyclone alert API fires for the zone polygon.
2. System does not wait for Kumar to stop moving - the alert itself is the trigger. ₹1,000 payout initiates.
3. Kumar receives an advance safety alert 12 hours before the trigger payout: *'Cyclone warning for your area. Avoid Zone B routes. Your insurance will activate automatically if the alert persists.'*
4. Real-time incident map (integrated with NDMA/rescue teams) pushed to all workers in the zone.

---

## 3. Weekly Premium Model

### 3.1 Design Philosophy

Monthly premiums fail gig workers because income is irregular. A worker who earns nothing in a bad week cannot afford a monthly deduction. The weekly opt-in model matches the financial rhythm of gig work: workers earn week-by-week and protect week-by-week.

Each Monday, workers choose to activate their cover for the coming week. They can skip any week with zero penalty.

### 3.2 Premium Calculation Formula

**Premium = Base Rate × Zone Risk Multiplier × Trust Discount**

Where:
- **Base Rate** = ₹20/week
- **Zone Risk Multiplier** = 1.0 (low-risk) to 2.5 (very high-risk)
- **Trust Discount** = 0.7 (low trust) to 1.0 (no discount for new users)

#### Examples:

- **Ravi** (Himayatnagar, Hyderabad - high flood risk zone, 8 weeks active): ₹20 × 2.4 × 0.80 = **₹38/week**
- **Meera** (Koramangala, Bengaluru - moderate AQI risk, 3 weeks active): ₹20 × 1.8 × 0.92 = **₹33/week**
- **New worker** in a low-risk zone: ₹20 × 1.0 × 1.0 = **₹20/week**

### 3.3 Zone-Based Risk Differentiation

Premium is tightly coupled to locality, not just city. The platform divides every city into micro-zones (approximately 2–4 km radius polygons, aligned to PIN code clusters). Each zone carries an independent risk score derived from:

- Historical rainfall frequency and intensity (IMD 24-month data)
- Historical AQI exceedance days (CPCB data)
- Government-declared disaster zone classifications (NDMA registry)
- Historical claim frequency from our own platform data (grows over time)
- Flood plain and elevation data (open government GIS data)

A worker's zone is determined by their **primary working area** - the geographic centroid of their last 4 weeks of order activity - not their home address. This ensures pricing reflects actual exposure, not registered address (which is often in a different area for migrant workers).

---

## 4. Parametric Trigger System

### 4.1 How It Works

Parametric insurance pays out when a pre-agreed objective parameter crosses a threshold - no human assessment required. Our system monitors live government and meteorological data feeds and automatically initiates payouts when conditions are met in a worker's active zone.

### 4.2 Trigger Table

| Trigger Event | Data Source | Threshold | Payout |
|---------------|-------------|-----------|--------|
| Rainfall | IMD API | >50mm / 4-hour window | ₹200 |
| AQI Spike | CPCB Feed | AQI > 400 | ₹300 |
| Cyclone Alert | IMD Alert | Active alert zone | ₹1,000 |
| Curfew Notice | State notification | Zone polygon locked | ₹250 |
| Air Raid Siren | Siren API (select metros) | Activation | ₹400 |

### 4.3 Data Sources

- **IMD (India Meteorological Dept.):** Rainfall, cyclones, weather forecasts
- **CPCB (Central Pollution Control Board):** Real-time AQI feeds
- **NDMA (National Disaster Management Authority):** Disaster zone classifications
- **Government APIs:** Curfew notices, traffic incidents
- **Cell Tower Data:** Location confirmation (with user consent)

---

## 5. Platform Choice - Mobile App (Android-First)

### 5.1 Decision and Rationale

We chose a native Android app as the primary platform, with a Progressive Web App (PWA) fallback for devices that cannot install the app. The rationale is straightforward and grounded in the realities of Indian gig workers:

**Why Android:**
- 96% of gig delivery workers use Android devices
- Native performance ensures payouts process in < 3 seconds
- Background services (location tracking, offline fraud checks) are reliable
- Native sensors (accelerometer, GPS) are critical for fraud detection

**Why PWA Fallback:**
- The PWA fallback exists for workers on very old devices (Android 5 and below) or those who cannot install apps due to storage constraints
- The PWA offers manual claim submission with photo proof - less automated, but accessible

---

## 6. AI/ML Integration Plan

### 6.1 Overview

AI/ML is embedded at three distinct points in the product workflow:
1. **Premium calculation** before the week begins
2. **Fraud detection** at claim time
3. **Real-time risk communication** throughout the week

Each layer uses models that are practical to train and deploy.

### 6.2 Module 1: Dynamic Premium Pricing

We use a **Gradient Boosted Regressor (XGBoost)** to calculate a personalized weekly premium for each worker before the Monday opt-in window. The model runs server-side as a scheduled batch process.

It considers multiple factors:
- Historical disruption frequency in the worker's zone over the past 24 months
- Seasonal risk (e.g., increased rainfall during monsoon)
- The worker's engagement history and active weeks
- Their primary working zone derived from recent activity
- Short-term weather forecasts for the upcoming week

The model outputs a single premium value in rupees, which is communicated to the worker at the start of each week.

### 6.3 Module 2: Fraud Detection - Three-Layer Architecture

#### Layer A: Isolation Forest (per-worker anomaly detection)

This layer builds a behavioral baseline for each worker using a rolling history. It runs both on-device and server-side.

It detects inconsistencies such as:
- Sudden changes in working location
- Unrealistic inactivity during claimed disruptions
- Mismatches between GPS and network signals
- Unusually precise claim timings

These signals help identify users whose behavior deviates from their normal patterns.

#### Layer B: Graph Neural Network (network-level fraud ring detection)

We model workers as nodes in a graph, where connections represent shared working zones, overlapping time windows, or network-level similarities.

During a claim event, we analyze the group of active claimants and compare it with normal working patterns. Genuine workers typically form loosely connected, geographically consistent groups. In contrast, fraud rings appear as tightly connected clusters with abnormal similarity and no organic linkage to real workers in that zone.

We use embedding and clustering techniques to identify such dense clusters. If a group shows significantly higher internal similarity than expected, it is flagged as a coordinated fraud attempt.

#### Layer C: Time-Series Anomaly Detection (synchronized spike detection)

Real disruptions cause gradual claim patterns over time, as workers stop working at different moments. Fraud attacks, however, often produce sudden spikes, where many claims are triggered within a short window.

We monitor claim volume trends and detect abnormal spikes that deviate significantly from expected patterns. When such spikes occur, payouts are temporarily paused and routed for review, preventing large-scale fund drain.

### 6.4 Trust Score System

Every worker has a dynamic trust score (0–1000) that evolves over time. This score gates the verification requirement at claim time.

**Trust score increases with:**
- Each verified legitimate claim
- Consistent weekly opt-in
- Behavioral consistency with established patterns
- Positive peer attestation from other high-trust workers

**Trust score decreases with:**
- Flagged anomalies
- Failed verification challenges
- Cluster association with detected fraud rings

### 6.5 Model Evolution Over Time

The system learns from every outcome:

- **Confirmed legitimate claim** → behavioural pattern strengthened as positive example in Isolation Forest
- **Confirmed fraud** → cluster traits added as negative examples; model retrained weekly
- **Fraud ring detected** → ring's spoofing pattern logged and added to adversarial test set
- **Premium model recalibrated** → monthly as actual claim frequency data accumulates by zone

This creates compounding adversarial resilience: attackers who fail teach the system exactly how they operate.

---

## 7. Real-Time Safety Alert System

### 7.1 The Feature

Guardian Network is not just insurance - it is a real-time safety intelligence layer for delivery workers. In partnership with NDMA, state disaster response teams, and municipal authorities, the app pushes geo-targeted alerts to workers in affected zones before and during disruptions.

**Alert Types:**
- **Advance warnings:** Cyclone alerts 12–24 hours ahead, flood zone activations, curfew notices
- **Route intelligence:** Real-time map overlay showing safe vs disrupted corridors, sourced from government rescue team data
- **Incident markers:** Live crowdsourced pins from verified workers (flooded road, waterlogging)
- **Emergency contacts:** Nearest government-empanelled clinic, NDMA helpline, zone-specific rescue team number

### 7.2 Weather Shadow Map - The Wow Factor Feature

Before enrolling, any delivery worker can open the app and see a city-level 'income shadow map' - a heat map overlay showing which zones have experienced the most trigger events in the past 90 days, with aggregated (anonymized) payout data per zone.

**This does two things:**

1. **Proves the product is real** before the worker spends a single rupee - they can see that real money was paid to workers in their area
2. **Acts as a professional intelligence tool** - workers can identify which zones to avoid during high-risk periods, and which zones offer the best risk-adjusted earnings

This map is the product's primary organic growth driver. Workers show it to each other. Distribution becomes peer-to-peer.

---

## 8. UX Design - Built for Low-Income, Low-Literacy Users

### 8.1 Core UX Principles

- **Zero default action:** Workers do nothing to receive payouts. The app works in the background.
- **Visual-first:** The app uses icons and colour over text wherever possible. Hindi language default with regional language options.
- **2G-tolerant:** All core functions (claim processing, trust score update, alert display) work on 2G. Heavy content (map) lazy-loads.
- **Low storage:** App target < 15MB installed. No video features in core flow.
- **Battery-conscious:** Background services use Android WorkManager with adaptive scheduling - no battery drain on low-charge devices.

### 8.2 Graceful Verification (Never Harsh Blocking)

The system never uses the word 'fraud', never accuses workers, and never hard-blocks a payment. All verification is framed as 'routine processing':

| Trust Level | Action |
|-------------|--------|
| **Trust 400–499** | 'We're confirming your location - tap to take a quick 3-second video.' (Scene classifier runs in background.) |
| **Trust < 400 or cluster flag** | 'Your payment is being processed. It will arrive within 24 hours.' (Human review queue, escrowed funds.) |
| **Peer attestation** | 'Two riders near you can confirm the disruption - we've sent them a quick ping.' (No action required from the claimant.) |

### 8.3 The Trust Passport

Each worker sees their trust score as a **0–5 star rating** in the app home screen. The stars grow visibly over weeks. Higher trust = faster payouts + higher coverage limits + lower premiums.

Workers with 5-star trust scores can refer others and receive a **₹50 credit** when the referred worker completes their first 4 weeks. This turns the fraud-prevention mechanism into a growth engine - the workers most invested in the system's legitimacy are the ones most motivated to bring in genuine workers.

---

## 9. Tech Stack

| Layer | Technology |
|-------|------------|
| **Frontend** | Kotlin (native Android), Flutter (optional cross-platform), PWA (TypeScript + Next.js) |
| **Backend** | Node.js + Express, Python (ML models), PostgreSQL (transactional), MongoDB (logging) |
| **ML/AI** | XGBoost (pricing), PyTorch (GNN for fraud rings), Scikit-learn (Isolation Forest) |
| **APIs & Integration** | IMD REST API, CPCB MQTT feeds, Twilio (SMS), Google Maps API, PhonePe/Google Pay SDK |
| **Infrastructure** | AWS (scalable), Kubernetes (orchestration), Redis (caching) |
| **Security** | OAuth 2.0, JWT, SSL/TLS, E2E encryption for sensitive data |

---

## 10. Why Guardian Network Stands Out

### 10.1 What Makes This Different

1. **Fraud Detection at Coordinated Ring Level**
   - Most insurance systems detect individual fraud. We detect organized fraud rings using Graph Neural Networks—a first in gig insurance.

2. **Trust Passport as Growth Mechanism**
   - High-trust workers refer genuine workers → organic scaling without marketing spend.

3. **Hyper-Local Premium Pricing**
   - Premiums are pinned to actual working zones, not home address or city. Migrant workers pay fair rates.

4. **Weather Shadow Map**
   - Workers make data-driven decisions about where to work. Income volatility decreases, worker satisfaction increases.

5. **Zero Paperwork, < 90 Seconds**
   - From trigger to payout in < 90 seconds via UPI. No forms. No pushback.

6. **NDMA Partnership**
   - Safety alerts are powered by real government disaster response data. Workers trust the information because it's official.

7. **Weekly Premium Matching Income Cycles**
   - Workers earn week-by-week. They protect week-by-week. No forced monthly deductions.

8. **2G-Compatible, < 15MB App**
   - Works on ₹3000 devices with spotty connectivity. Not every delivery worker has a ₹30k phone.

---


**Last Updated:** March 2026  
**Status:** DEVTrails 2026 Phase 1 Submission
