# MediSentinel_AI
Agentic AI-powered medicine verification and safety assistant using OCR, computer vision, QR/barcode scanning, drug databases, and evidence-based reasoning.
# 💊 MediSentinel AI

### An Agentic Medicine Verification & Safety Assistant

MediSentinel AI is an AI-powered mobile application designed to help users identify medicines, check expiry dates, verify available batch information, and understand medicine-related safety information.

By combining **Agentic AI, Computer Vision, OCR, QR/Barcode Scanning, and structured drug-information sources**, MediSentinel AI aims to provide evidence-based medicine assessments through an intelligent, multi-agent workflow.

> **Important:** A photograph alone cannot establish that a medicine is chemically genuine. MediSentinel AI aims to assess available evidence, identify uncertainty, and recommend further verification when necessary.

---

## 🎯 Problem Statement

Medicine packaging can contain difficult-to-read information, and users may struggle to understand expiry dates, medicine uses, side effects, precautions, and potential safety alerts.

MediSentinel AI aims to bring these capabilities together in one application that can analyze medicine packaging, retrieve relevant drug information, and guide users through a structured verification process.

## 🚀 Key Features

### 📷 1. Medicine Image Scanning
- Capture medicine images using a mobile camera.
- Upload existing medicine photographs.
- Scan the front, back, and sides of medicine packaging.

### 🖼️ 2. Image Preprocessing
- Image cropping and deskewing.
- Noise removal and contrast enhancement.
- Text enhancement for improved OCR performance.

**Tools:** Python, OpenCV, Pillow.

### 🔤 3. OCR-Based Information Extraction
Extract relevant information from medicine packaging:

- Medicine name and composition.
- Strength and dosage information.
- Batch number.
- Manufacturing date.
- Expiry date.
- Manufacturer details.

**Tools:** EasyOCR, Tesseract OCR, OpenCV.

### 📱 4. QR and Barcode Scanning
- Detect and decode supported QR codes and barcodes.
- Extract available identifiers or package information.
- Use OCR when machine-readable codes are unavailable or unreadable.

**Tools:** ZXing, pyzbar, OpenCV.

### 💊 5. Medicine Identification
- Identify medicine names using extracted text.
- Normalize OCR errors and spelling variations.
- Match brand names with generic medicine information when supported by available data.

**Potential sources:** RxNorm, OpenFDA, and suitable structured medicine databases.

### 📅 6. Expiry Detection and Alerts
- Extract manufacturing and expiry dates.
- Classify medicines as valid, nearing expiry, or expired.
- Save scanned medicines in a personal medicine cabinet.
- Notify users before saved medicines reach their expiry dates.

### 🔎 7. Batch Verification
Check available medicine, manufacturer, batch, and regulatory information against accessible verification sources.

Possible outcomes:
- Batch information matched.
- Batch information not found.
- Potential quality or recall alert.
- Insufficient information for verification.

**Potential sources:** CDSCO publications, manufacturer verification services where available, and application-maintained alert records.

### 👁️ 8. Packaging Anomaly Detection
Analyze packaging characteristics for potential visual anomalies, including:

- Printing and typography.
- Spacing and layout.
- Color consistency.
- Other visible packaging characteristics.

**Potential tools:** OpenCV, PyTorch, ResNet, EfficientNet.

This feature requires suitable training and evaluation data. Visual anomalies do not independently prove that a medicine is counterfeit.

### 🤖 9. Agentic AI Workflow
MediSentinel AI is designed to use specialized agents coordinated by an orchestrator.

- **Orchestrator Agent:** Coordinates tasks and decides what to do next.
- **Vision Agent:** Evaluates image quality and visible packaging characteristics.
- **OCR Agent:** Extracts and validates readable text.
- **QR/Barcode Agent:** Decodes supported machine-readable codes.
- **Identification Agent:** Matches extracted information to medicine records.
- **Verification Agent:** Checks available batch and regulatory information.
- **Safety Agent:** Retrieves and organizes medicine safety information.
- **Evidence Checker:** Evaluates whether the collected evidence supports the proposed result.

**Tools:** Python, LangGraph, FastAPI, and an API-based LLM.

### 🔄 10. Intelligent Re-planning
When information is missing or unreliable, the system can request additional information rather than guessing.

Example:

1. The user uploads a blurry medicine image.
2. The system identifies the medicine but cannot read its batch number.
3. The orchestrator determines that batch verification cannot proceed.
4. The app requests a clearer image of the back of the package.
5. The system processes the new image and resumes verification.

This demonstrates the agentic cycle:

**Observe → Reason → Act → Verify → Re-plan**

### 📚 11. Medicine Information
Present structured, source-backed information about:

- Common uses.
- Common and serious side effects.
- Precautions and contraindications.
- Important warnings.
- Special-population considerations where supported.
- Potential drug interactions.

Medical facts should come from appropriate drug-information sources. The LLM should primarily explain retrieved information rather than invent medical advice.

### 🔄 12. Drug Interaction Checker
Check available interaction information for medicines selected or saved by the user.

Potential interactions should be presented with appropriate warnings and recommendations to consult a doctor or pharmacist.

### 🗃️ 13. Personal Medicine Cabinet
Allow users to save scanned medicines and manage:

- Medicine names and strengths.
- Expiry dates.
- Scan history.
- Verification summaries.
- Upcoming expiry alerts.

### 🚨 14. Medicine Alerts and Reporting
- Notify users about approaching expiry dates.
- Flag matches to available regulatory or quality alerts.
- Allow users to report suspicious medicine packaging.
- Maintain a record of submitted reports.

Reports should be treated as unverified until appropriately reviewed.

### 📊 15. Confidence-Based Assessment
Instead of simply declaring a medicine genuine or fake, provide separate assessments for identification, expiry extraction, batch verification, packaging analysis, and drug-information retrieval.

The final report should distinguish verified information, possible anomalies, unavailable evidence, and unresolved uncertainty.

---

## 🏗️ System Architecture

```text
                    MOBILE APPLICATION
                           |
                           v
                     FASTAPI BACKEND
                           |
                           v
                  ORCHESTRATOR AGENT
                           |
              +------------+------------+
              |            |            |
              v            v            v
          VISION AGENT  OCR AGENT    QR AGENT
              |            |            |
              +------------+------------+
                           |
                           v
                 IDENTIFICATION AGENT
                           |
                           v
                  VERIFICATION AGENT
                           |
              +------------+------------+
              |            |            |
              v            v            v
          EXPIRY CHECK  BATCH CHECK  PACKAGE ANALYSIS
              |            |            |
              +------------+------------+
                           |
                           v
                     SAFETY AGENT
                           |
                           v
                    EVIDENCE CHECKER
                           |
                           v
                      FINAL REPORT
```

## 🛠️ Technology Stack

| Component | Technologies |
|---|---|
| Mobile application | React Native, Expo |
| UI styling | NativeWind or equivalent |
| Backend | Python, FastAPI, Pydantic |
| Agent orchestration | LangGraph |
| Language model | API-based LLM |
| Computer vision | OpenCV, PyTorch |
| OCR | EasyOCR, Tesseract |
| QR/barcode | ZXing, pyzbar |
| Database | PostgreSQL, Supabase |
| Drug information | RxNorm, OpenFDA |
| Regulatory information | CDSCO sources where available |
| Deployment | Vercel for web components; suitable backend hosting for APIs |

The final technology choices may evolve during implementation.

## 📂 Planned Project Structure

```text
MediSentinel_AI/
├── mobile/
├── backend/
├── agents/
├── vision/
├── ocr/
├── database/
├── tests/
├── docs/
├── .gitignore
└── README.md
```

## 🗺️ Development Roadmap

### Phase 1 — Core MVP
- [ ] Create the mobile application.
- [ ] Implement camera capture and image upload.
- [ ] Build the FastAPI backend.
- [ ] Implement image preprocessing and OCR.
- [ ] Extract medicine names and expiry dates.
- [ ] Implement medicine identification.

### Phase 2 — Agentic Workflow
- [ ] Implement the orchestrator using LangGraph.
- [ ] Integrate OCR and QR/barcode processing.
- [ ] Build identification and verification agents.
- [ ] Implement the Safety Agent and Evidence Checker.
- [ ] Add missing-information handling and re-planning.

### Phase 3 — Medicine Safety
- [ ] Integrate suitable drug-information APIs.
- [ ] Display uses, side effects, and precautions.
- [ ] Implement expiry tracking and notifications.
- [ ] Add available batch and regulatory alert checks.
- [ ] Implement drug interaction checking.

### Phase 4 — Advanced Features
- [ ] Personal medicine cabinet.
- [ ] Scan history.
- [ ] Suspicious medicine reporting.
- [ ] Packaging anomaly analysis.
- [ ] Model evaluation and confidence calibration.
- [ ] Explore offline capabilities.

## 🧪 Testing and Evaluation

The project will be evaluated using a dedicated test dataset and component-specific metrics.

- OCR field-extraction accuracy.
- Medicine identification accuracy.
- Expiry-date extraction accuracy.
- QR/barcode decoding success rate.
- Batch verification performance.
- Drug-information retrieval correctness.
- Agent decision accuracy.
- False-positive and false-negative rates.

Performance claims will be reported only after testing. Verification accuracy will be evaluated separately from the ability to establish chemical authenticity.

## 🔐 Privacy and Medical Safety

- Protect user accounts and stored medicine records.
- Avoid storing uploaded images unnecessarily.
- Secure API credentials and sensitive configuration.
- Use reliable, traceable sources for medical information.
- Clearly communicate uncertainty and unavailable evidence.

MediSentinel AI is intended for educational and informational purposes. It does not replace a doctor, pharmacist, laboratory test, or official regulatory verification process.

## 🌟 Vision

To build an intelligent medicine safety assistant that combines agentic reasoning, computer vision, structured drug information, and evidence-based verification to help users make better-informed decisions about the medicines they encounter.

## 📌 Project Status

**Status:** Under Development

**Project:** MediSentinel AI

**Category:** Agentic AI · Healthcare Technology · Computer Vision · Mobile Application

---

*Built to explore how agentic AI can support medicine identification, verification, and safety through evidence-based reasoning.*
