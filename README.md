# Resource Referral Assistant
### Clinical Co-pilot — Cowichan Valley, BC
*Built for the Saanich / Cowichan Valley Healthcare Hackathon*

---

## What This Is

A doctor-facing web application that helps clinicians quickly find and refer patients to community health resources in the Cowichan Valley and Duncan, BC area. The tool is designed around the real clinical workflow: review patient context before the appointment, add situational notes during the visit, search for relevant resources, and generate a referral note — all in one screen.

This is **not** a treatment recommendation tool, a medication advisor, or a clinical decision support system. It is a resource finder and referral note generator that keeps the physician as the final decision-maker at every step.

---

## How It Works

The app runs entirely in the browser as a single HTML file. On load, it fetches six CSV data files directly from this GitHub repository — no backend, no database, no server required.

**Workflow:**

1. **Select a patient** from the left panel — their demographics, diagnoses, active medications, recent encounters, latest vitals, and abnormal labs load automatically
2. **Add situational notes** — type or dictate anything the patient shared during the appointment that wasn't on their intake form
3. **Search for resources** using plain language — e.g. *"mental health support"*, *"autism assessment"*, *"speech therapy"*
4. The system builds an internal context query automatically combining patient age, gender, diagnoses, location, and doctor notes
5. **Review ranked results** — each resource card shows description, eligibility, how to access, phone number, and whether a referral is required
6. **Generate and download a referral note** — pre-filled with patient demographics and a generated reason for referral, fully editable before download

---

## Bias & Equity Transparency

Every search surfaces a **"What This Tool May Be Missing"** panel. This is intentional. The panel flags known gaps in coverage including missing Indigenous and First Nations-specific services, unverified referral requirements, absence of language-specific or culturally safe care options, and rural access limitations. The principle: the tool should be honest about what it does not know.

---

## Repository Structure

```
/
├── patients.csv                          Patient demographics (synthetic, 200 patients)
├── encounters.csv                        Clinical encounter history
├── medications.csv                       Medication records
├── lab_results.csv                       Lab results
├── vitals.csv                            Vital signs history
├── duncan_resources_from_hackathon.csv   Community resource directory (10 services)
└── resource_referral_assistant_v2.html   The application
```

---

## Data Files

All patient data is **synthetic** — generated for hackathon purposes and does not represent real individuals. The resource directory covers 10 services in the Duncan / Cowichan Valley area across categories including Mental Health, Pediatrics, Seniors, Youth, Chronic Disease, Respiratory, Pain, and Women's Health.

### CSV Column Reference

**patients.csv** — `id, name, age, sex, dob, blood, postal, language, insurance`

**encounters.csv** — `id, pid, date, type, facility, complaint, dx_code, dx, triage, disposition, hours, physician`

**medications.csv** — `id, pid, drug, dose, freq, route, prescriber, start, end, active`

**lab_results.csv** — `id, pid, eid, test, value, unit, low, high, flag, date`

**vitals.csv** — `id, pid, eid, hr, sbp, dbp, temp, rr, o2, pain, at`

**duncan_resources_from_hackathon.csv** — `resource_name, category, conditions, min_age, max_age, region, referral_required, self_referral, phone, description, referral_notes`

---

## Running the App

The app is a single HTML file with no dependencies to install.

**Requirements:**
- The GitHub repository must be **public** so the browser can fetch raw CSV files
- The branch must be named `main` (update the `BRANCH` variable in the HTML if different)

**To run:**
1. Open `resource_referral_assistant_v2.html` in any modern browser
2. The app fetches all data files on load and displays a loading screen while doing so
3. If any file fails to load, an error message identifies exactly which file and URL failed

**To update data files:**
Simply replace or edit the CSV files in this repository. The app always fetches the latest version on each page load — no code changes required.

---

## Configuration

At the top of the `<script>` section in the HTML file:

```javascript
var REPO   = 'neiljabez32/Clinical-Copilot-Public-Access';
var BRANCH = 'main';

var F_PATIENTS   = 'patients.csv';
var F_ENCOUNTERS = 'encounters.csv';
var F_MEDS       = 'medications.csv';
var F_LABS       = 'lab_results.csv';
var F_VITALS     = 'vitals.csv';
var F_RESOURCES  = 'duncan_resources_from_hackathon.csv';
```

Update `REPO`, `BRANCH`, or any filename here if the repository or file names change.

---

## Built With

- Vanilla HTML, CSS, JavaScript — no frameworks, no build tools
- Google Fonts: Lora, DM Sans, DM Mono
- Data fetched at runtime from GitHub raw content URLs
- CSV parsing handled client-side

---

## Hackathon Context

This project was developed for a healthcare innovation hackathon focused on reducing clinical complexity in Saanich and Cowichan Valley, BC. The problem framing: doctors spend significant time manually bridging patient intake data with community resource knowledge — this tool compresses that process into a single, transparent workflow that respects the physician's authority as the final decision-maker.

---

*For questions about this project, contact the repository owner.*
