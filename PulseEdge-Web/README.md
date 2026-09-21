# PulseEdge AI — Offline Multimodal Risk & Referral Assistant

> **Hackathon Prototype | Offline-First Healthcare Workflow | Android + PWA**

PulseEdge AI is an offline-first prototype designed to help frontline health workers **capture patient observations, structure basic clinical information, validate vital signs, and prepare a clear referral handoff** when connectivity is limited or unavailable.

**Core workflow: Capture → Structure → Validate → Refer**

> **Safety:** This is a hackathon prototype, not a medical device, diagnostic system, or substitute for a qualified healthcare professional.

---

## 1. Problem

Frontline healthcare workflows can become difficult when:

- Internet connectivity is unreliable.
- Patient observations are captured as unstructured notes or speech.
- Vital signs are recorded separately from observations.
- Referral information has to be manually reconstructed.
- A receiving clinician needs a concise, structured handoff.

PulseEdge AI demonstrates an offline-first workflow that turns field observations and vital signs into an **explainable referral workflow**.

---

## 2. Proposed Solution

PulseEdge AI lets a user:

1. Capture a patient observation.
2. Enter or capture vital signs.
3. Use predefined demo data.
4. Structure the collected information.
5. Validate it against transparent safety rules.
6. Generate an explainable risk level.
7. Prepare a referral/handoff report.
8. Continue the core workflow without internet connectivity.

```text
┌─────────────┐
│   CAPTURE   │
│ Observation │
│ Voice/Text  │
│ Camera      │
│ Vitals      │
└──────┬──────┘
       ↓
┌─────────────┐
│  STRUCTURE  │
│ Organize    │
│ Case data   │
└──────┬──────┘
       ↓
┌─────────────┐
│  VALIDATE   │
│ Vital rules │
│ Explainable │
│ escalation  │
└──────┬──────┘
       ↓
┌─────────────┐
│    REFER    │
│ Result      │
│ Handoff     │
│ Report      │
└─────────────┘
```

---

## 3. Key Features

### Offline-first operation

The core prototype can operate without a cloud server for:

- Case storage
- Demo scenarios
- Vital-sign evaluation
- Risk-rule evaluation
- Assessment stages
- Referral report generation
- Core navigation

The Android prototype bundles the application locally so the core demonstration can run without active internet.

### Multimodal capture

The interface supports:

- Text observations
- Voice input where supported
- Camera access
- Image upload
- Vital-sign entry

If a device does not support a capability, manual input remains available.

### Explainable risk evaluation

PulseEdge does **not make a medical diagnosis**.

The prototype uses deterministic rules:

```text
If systolic >= 160 OR diastolic >= 110
        → URGENT

Else if systolic >= 140 OR diastolic >= 90
        → REVIEW

Else
        → ROUTINE
```

The output includes the rule that caused escalation.

### Referral handoff

The referral workflow prepares a structured handoff containing:

- Case ID
- Scenario
- Observation
- Vital signs
- Risk level
- Rule/threshold used
- Available case information
- Referral information

---

## 4. Demonstration Scenario

The included maternal demonstration uses:

```text
Observation:
"Patient ki severe headache undi, vision blurred ga undi."

Blood Pressure:
165 / 110 mmHg

Pulse:
92 bpm

Temperature:
37.1 °C

SpO₂:
98%
```

Configured prototype result:

```text
Risk Level: URGENT
```

Reason:

```text
Systolic >= 160
OR
Diastolic >= 110
```

This is a **prototype escalation demonstration**, not a clinical diagnosis.

---

## 5. Architecture

### Current prototype

```text
                 ┌──────────────────────────┐
                 │       User / Worker      │
                 └────────────┬─────────────┘
                              │
                              ▼
                 ┌──────────────────────────┐
                 │   Mobile-first UI        │
                 │   React + TypeScript     │
                 └────────────┬─────────────┘
                              │
              ┌───────────────┼────────────────┐
              ▼               ▼                ▼
       Observation        Camera/Input       Vitals
              │               │                │
              └───────────────┼────────────────┘
                              ▼
                 ┌──────────────────────────┐
                 │   Local Case Storage     │
                 │      localStorage        │
                 └────────────┬─────────────┘
                              ▼
                 ┌──────────────────────────┐
                 │ Deterministic Risk Rules │
                 └────────────┬─────────────┘
                              ▼
                 ┌──────────────────────────┐
                 │ Assessment / Result      │
                 └────────────┬─────────────┘
                              ▼
                 ┌──────────────────────────┐
                 │ Referral / Handoff       │
                 └──────────────────────────┘
```

---

## 6. Technology Stack

### Frontend

- React
- TypeScript
- Vite
- Tailwind CSS
- shadcn/ui
- TanStack Router

### Offline / PWA

- Web App Manifest
- Service Worker
- Local storage
- Cached static assets
- PWA installation support

### Android

- Android Studio
- Android application wrapper
- Bundled web application assets
- Local execution of the core workflow

### Device capabilities

Where supported:

- Camera
- Microphone / speech recognition
- Local storage
- Print/save functionality

---

## 7. Offline Design

| Capability | Offline |
|---|---|
| Open application | ✅ |
| Demo case | ✅ |
| Manual observation | ✅ |
| Vital entry | ✅ |
| Risk-rule evaluation | ✅ |
| Assessment workflow | ✅ |
| Result screen | ✅ |
| Referral report | ✅ |
| Local case storage | ✅ |
| Static application assets | ✅ |
| Camera capture | Device-dependent |
| Speech recognition | Device/browser-dependent |

Speech recognition may depend on the Android/browser speech engine and should therefore not be treated as guaranteed offline. Manual text entry remains available.

---

## 8. Android APK

Open the Android project in Android Studio.

Build using:

```text
Build
→ Build Bundle(s) / APK(s)
→ Build APK(s)
```

The debug APK is normally generated at:

```text
app/build/outputs/apk/debug/app-debug.apk
```

For demonstration, install the APK on an Android device and disable Wi-Fi/mobile data to verify the offline workflow.

---

## 9. Web / PWA Prototype

**Live prototype:**

https://pulseedge-ai.lovable.app

The web version is also installable as a PWA and uses local browser storage for prototype case persistence.

---

## 10. Application Screens

### Home
Introduces PulseEdge and the case workflow.

### Capture
Collects observations, language, vitals, camera/image input, and voice input where supported. Includes demo data.

### Structure
Organizes captured information into a structured case.

### Validate
Runs the deterministic escalation rules and explains the resulting risk level.

### Result
Displays the risk level, supporting rule, vitals, and structured observations.

### Referral Report
Creates a clinician-facing handoff summary.

### Architecture
Explains the current implementation and intended production architecture.

### Settings
Provides prototype/application configuration and status information.

---

## 11. Production Architecture — Future Direction

The prototype separates the working demonstration from the proposed production architecture.

A future production implementation could use:

```text
Android / Kotlin
        │
        ▼
Jetpack Compose
        │
        ├── Local OCR
        ├── Local Vision
        ├── Local Speech
        │
        ▼
On-device ML Runtime
        │
        ├── Quantized Llama-family model
        ├── ExecuTorch / QNN
        │
        ▼
Local encrypted storage
        │
        └── SQLCipher
```

**Important:** the production architecture above is a target design. The current browser prototype does not claim that a Llama-family clinical AI model is running locally.

---

## 12. Safety and Responsible Use

PulseEdge AI is a **hackathon prototype**.

It is:

- Not a medical device.
- Not a replacement for a qualified healthcare professional.
- Not intended to diagnose disease.
- Not intended to prescribe treatment.
- Not clinically validated.
- Not a substitute for emergency medical services.

The risk levels are generated using explicit demonstration rules and should not be interpreted as clinical decision-making.

A real deployment would require clinical validation, regulatory review, security controls, privacy protections, model validation, human oversight, and appropriate healthcare integration.

---

## 13. Privacy Approach

The prototype prioritizes local handling of demonstration data.

The core workflow does not require sending the entered case to a remote AI service.

A production deployment would additionally require:

- Encryption at rest
- Secure authentication
- Role-based access
- Audit logs
- Consent management
- Secure synchronization
- Data retention policies
- Applicable healthcare/privacy compliance

---

## 14. Hackathon Demo Flow

### Step 1 — Launch
Open the PulseEdge AI Android APK.

### Step 2 — Start a case
Open the case workflow.

### Step 3 — Use demo values
Load the predefined maternal scenario.

### Step 4 — Show capture
Demonstrate the observation and vital signs.

### Step 5 — Structure
Move the case into the structured assessment stage.

### Step 6 — Validate
Show:

```text
165 / 110
      ↓
Systolic ≥ 160 OR Diastolic ≥ 110
      ↓
URGENT
```

### Step 7 — Refer
Open the referral report and show the structured handoff.

### Step 8 — Prove offline operation
Turn off Wi-Fi and mobile data, reopen the APK, and repeat the core workflow.

---

## 15. Project Structure

```text
PulseEdge/
│
├── app/
│   └── Android application
│
├── src/
│   ├── components/
│   ├── routes/
│   │   ├── case/
│   │   ├── architecture/
│   │   └── settings/
│   ├── lib/
│   │   └── pulseedge.ts
│   └── styles.css
│
├── public/
│   ├── icons/
│   └── manifest.webmanifest
│
├── package.json
├── vite.config.ts
└── README.md
```

---

## 16. Core Risk Logic

The central prototype logic is intentionally simple and auditable:

```typescript
if (systolic >= 160 || diastolic >= 110) {
  return "URGENT";
}

if (systolic >= 140 || diastolic >= 90) {
  return "REVIEW";
}

return "ROUTINE";
```

This lets an evaluator understand exactly why the demonstration case produces its result.

---

## 17. Why Offline-First?

Connectivity should not become a prerequisite for every step of a frontline workflow.

The prototype treats connectivity as an enhancement rather than a requirement for the core demonstration:

```text
                    INTERNET
                       │
              ┌────────┴────────┐
              │                 │
          Available          Unavailable
              │                 │
              ▼                 ▼
       Optional future      Core workflow
       synchronization      continues locally
```

This design is intended for environments where network availability can vary.

---

## 18. Current Prototype vs Production

| Capability | Current Prototype | Production Target |
|---|---|---|
| Offline core workflow | ✅ | ✅ |
| Local case storage | ✅ | Encrypted storage |
| Deterministic risk rules | ✅ | Clinically validated rules |
| Camera input | Device-dependent | Native camera pipeline |
| Voice input | Browser/device-dependent | On-device speech model |
| OCR | Architecture concept | On-device OCR |
| Vision AI | Architecture concept | Validated on-device model |
| Llama-family model | Not running in browser | Quantized on-device model |
| Cloud sync | Not required | Secure optional sync |
| Clinical validation | ❌ | Required |
| Medical-device approval | ❌ | Required where applicable |

---

## 19. Evaluation Highlights

### 1. Offline resilience
The core workflow can continue without internet connectivity.

### 2. Multimodal input
Text, voice, camera and vitals can contribute to a single case.

### 3. Explainable escalation
The system exposes the rule behind the risk level rather than hiding it behind an unexplained score.

### 4. Actionable handoff
The workflow ends with a structured referral report instead of stopping at data collection.

---

## 20. Repository Purpose

This repository contains the hackathon prototype and supporting Android/PWA implementation.

The objective is to demonstrate:

> **Offline multimodal patient information capture, transparent risk escalation, and structured referral handoff.**

It is intentionally designed as a prototype that can be demonstrated, inspected, and extended toward a production-grade healthcare workflow.

---

## License

Provided for hackathon/prototype evaluation and development purposes.

---

## PulseEdge AI

**Offline Multimodal Risk & Referral Assistant**

```text
CAPTURE → STRUCTURE → VALIDATE → REFER
```

**Prototype status:** Hackathon Demo / Proof of Concept

**Important:** Not a medical device. Not clinically validated. Not a substitute for professional medical care.
