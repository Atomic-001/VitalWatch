# VitalWatch

**Real-Time Patient Vital-Sign Monitoring and Alerting Dashboard**
PRT661 – Data Science Practice | Theme 1: Real-Time Analytics and Streaming Data

VitalWatch simulates continuous patient vital-sign streams (heart rate, SpO2, blood
pressure, respiratory rate), ingests them in real time, flags clinically abnormal
readings, stores both raw and processed data, and displays everything on a live,
auto-refreshing dashboard with automated alerting.

## Team

| Name | Student ID | Role |
|---|---|---|
| Sayed Rakibul Hasan Shanto | S394549 | Project Manager / Data & Ingestion Engineer |
| Shahidur Rahman Shimul | S395447 | Stream Processing & Storage Engineer |
| Rakib Uddin Asim | S[ID] | Visualisation, Alerting & QA/Documentation Lead |

## Architecture

```
Vitals Simulator -> Kafka (ingestion) -> Spark Structured Streaming (rules)
      -> InfluxDB (time-series) + PostgreSQL (metadata)
      -> Dash/Plotly Dashboard (live view) + Alert Service (email/SMS)
```

See `docs/architecture.png` and `docs/workflow.png` for the full diagrams, and
`docs/PRT661_Assessment1_Proposal.docx` for the complete written proposal.

## Repository Structure

```
vitalwatch/
├── README.md
├── docs/
│   ├── PRT661_Assessment1_Proposal.docx
│   ├── architecture.png
│   └── workflow.png
├── simulator/
│   └── vitals_simulator.py        # generates simulated patient vitals events
├── streaming/
│   └── (Spark Structured Streaming jobs — added in Phase 3)
├── storage/
│   └── (DB schema / migration scripts — added in Phase 3)
├── dashboard/
│   └── (Dash/Plotly app — added in Phase 4)
├── alerting/
│   └── (alert service — added in Phase 4)
└── tests/
    └── (unit/integration tests — added in Phase 5)
```

## Alert Thresholds (initial)

| Vital | Normal Range | Alert Trigger |
|---|---|---|
| Heart rate | 60–100 bpm | < 40 or > 120 bpm |
| SpO2 | 95–100% | < 92% |
| Respiratory rate | 12–20 /min | < 8 or > 28 /min |
| Systolic BP | 90–120 mmHg | < 80 or > 180 mmHg |

Thresholds are provisional and will be tuned during testing (see risk register in
the proposal).

## Getting Started

```bash
# clone the repo
git clone <repo-url> && cd vitalwatch

# create a virtual environment
python3 -m venv .venv && source .venv/bin/activate

# install simulator dependencies
pip install -r simulator/requirements.txt

# run the simulator (prints JSON events to stdout by default)
python simulator/vitals_simulator.py --patients 3 --interval 1
```

Once Kafka is available (Phase 2), the simulator will publish directly to a
`vitals` topic instead of stdout — see comments in `vitals_simulator.py`.

## Workflow

| Phase | Weeks | Focus |
|---|---|---|
| 1 | 1–2 | Planning & environment setup |
| 2 | 3–5 | Ingestion pipeline & stream simulator |
| 3 | 6–8 | Stream processing & storage |
| 4 | 9–10 | Dashboard & alerting |
| 5 | 11–12 | Integration testing, documentation, demo |

## License

Academic project for PRT661 – Data Science Practice. Not for clinical use.VitalWatch simulates continuous patient vital-sign streams (heart rate, SpO2, blood pressure, respiratory rate), ingests them in real time, flags clinically abnormal readings, stores both raw and processed data, and displays everything on a live, auto-refreshing dashboard with automated alerting.
