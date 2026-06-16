# CTI Phishing Analysis Platform
### Built by Hunain | Pre-Sales Intern @ CyberKnight

A full-stack Cyber Threat Intelligence platform for automated phishing email analysis, built for the CyberKnight C-suite evaluation.

---

## What it does

Upload a `.eml` file and get back a complete threat intelligence report in seconds:

- **AI-powered analysis** — deep phishing indicator detection, urgency language, spoofing, suspicious headers
- **MITRE ATT&CK mapping** — automatic technique attribution (T1566 and related)
- **Risk scoring** — 0-100 score with weighted breakdown across 5 factors
- **PhishTank enrichment** — cross-reference extracted URLs against 64,000+ verified phishing URLs
- **Threat actor profiling** — origin, sophistication, motivation, attribution notes
- **OpenCTI integration** — push extracted IOCs (URLs, domains, IPs, emails) as observables
- **PDF report generation** — professional C-suite ready report with all findings
- **Product recommendations** — 3 defense-in-depth CyberKnight vendor recommendations based on attack pattern
- **Batch analysis** — analyze up to 3 emails simultaneously

---

## Stack

| Layer | Technology |
|-------|-----------|
| Backend | Python, Flask |
| AI Analysis | Anthropic Claude API (claude-sonnet-4-6) |
| Threat Intel | PhishTank offline feed |
| TIP Integration | OpenCTI 6.2 via GraphQL |
| PDF Generation | fpdf2 |
| Infrastructure | Docker Compose (OpenCTI, Elasticsearch, Redis, MinIO, RabbitMQ) |

---

## Setup

### Prerequisites
- Python 3.10+
- Docker Desktop
- Anthropic API key (console.anthropic.com)

### Installation

```bash
git clone https://github.com/hunainraza1/phishing-analyzer
cd phishing-analyzer
pip install -r requirements.txt
```

### Environment variables

Create a `.env` file in the project root:

```env
ANTHROPIC_API_KEY=sk-ant-...
OPENCTI_URL=http://localhost:8080
OPENCTI_TOKEN=your-uuid-token
FLASK_SECRET_KEY=your-secret-key
```

### Start OpenCTI

```bash
docker-compose up -d
```

Wait for all 5 containers to be healthy (roughly 2-3 minutes on first boot).

### Start the platform

```bash
python run.py
```

Visit `http://localhost:5000`

---

## Project structure

```
phishing-analyzer/
├── app/
│   ├── modules/
│   │   ├── parser.py       # .eml parsing and artifact extraction
│   │   ├── phishtank.py    # PhishTank offline feed enrichment
│   │   ├── analyzer.py     # Claude API — analysis, MITRE, scoring
│   │   ├── opencti.py      # IOC push to OpenCTI via GraphQL
│   │   └── reporter.py     # PDF report generation
│   ├── templates/
│   │   └── index.html      # Frontend UI
│   ├── static/             # Assets
│   ├── __init__.py         # Flask factory
│   └── routes.py           # API endpoints
├── reports/                # Generated PDF reports
├── docker-compose.yml      # OpenCTI stack
├── requirements.txt
├── run.py
└── .env
```

---

## API endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Main UI |
| POST | `/analyze` | Analyze `.eml` file |
| POST | `/report` | Generate PDF report |

---

## Analysis output

Each analysis returns:

- Verdict: `PHISHING` / `SUSPICIOUS` / `CLEAN`
- Confidence score (0-100%)
- Executive summary (C-suite ready)
- Phishing indicators with severity ratings
- MITRE ATT&CK technique mapping
- Risk score breakdown (5 weighted factors)
- Extracted IOCs (URLs, domains, IPs, email addresses)
- Threat actor profile and attribution
- 3 vendor product recommendations
- PhishTank enrichment results
- OpenCTI push confirmation

---

## Demo

Built and presented to CyberKnight C-suite (CEO, CISO, COO, CTO) as part of internship evaluation.

**Test corpus:**
- Brazilian Bradesco/Livelo phishing email — verdict: PHISHING, risk score: 93/100
- Clean legitimate email — verdict: CLEAN

---

## Author

**Hunain** — Cybersecurity student at University of Wollongong Dubai  
Pre-Sales Intern @ CyberKnight, Dubai  
[GitHub](https://github.com/hunainraza1) | [LinkedIn](https://linkedin.com/in/hunainraza)
