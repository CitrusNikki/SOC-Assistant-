# SOC-Assistant-
An AI-assisted SOC triage system built on top of Wazuh. It ingests security alerts, filters them by severity, runs them through an AI model for first-pass analysis, and turns the results into structured incident reports — cutting down the manual triage work analysts would otherwise have to do by hand.

## Repository Layout

| Path | Contents |
|---|---|
| `backend/` | Core application |
| `backend/src/soc/` | SOC processing logic |
| `backend/src/soc/ai/` | AI analysis |
| `backend/src/soc/report/` | Incident report generation |
| `backend/src/soc/notify/` | Notifications |
| `dashboard/` | Streamlit dashboard |
| `tests/` | Test suite |
| `docs/` | Project documentation |
| `reports/` | Generated reports |
| `main.py` | Application entry point |

## Architecture

Alerts flow from Wazuh through the pipeline, get analyzed, and fan out to three destinations:

```
Wazuh
  │
  ▼
Alert Reader
  │
  ▼
Alert Model
  │
  ▼
Severity Filter
  │
  ▼
AI Analysis
  │
  ▼
Response Validation
  │
  ├──────────────┬──────────────┐
  ▼              ▼              ▼
Report       Dashboard     Notification
```

## Requirements

- Git
- Python 3.11+
- Virtualization software (for the Wazuh lab)
- A running Wazuh lab environment
- An AI API provider (OpenAI, Anthropic, etc.)

## Setup

**1. Clone the repository**

```bash
git clone <repository-url>
cd ai-soc-assistant
```

**2. Create a virtual environment**

Windows:
```bash
python -m venv .venv
.venv\Scripts\activate
```

Linux / macOS:
```bash
python3 -m venv .venv
source .venv/bin/activate
```

**3. Install dependencies**

```bash
pip install -r requirements.txt
```

**4. Configure environment variables**

Copy `.env.example` to `.env` and fill in the required values.

## Configuration

The following environment variables need to be set:

- `AI_API_KEY` — API key for your AI provider
- `AI_BASE_URL` — Base URL for the AI API
- `AI_MODEL` — Model to use for analysis
- `WAZUH_ALERTS_PATH` — Path to the Wazuh alerts file
- `DASHBOARD_MIN_LEVEL` — Minimum severity level shown on the dashboard

Notification settings are optional and configured separately.

## Wazuh Integration

The system reads alerts directly from Wazuh's alert log:

```
/var/ossec/logs/alerts/alerts.json
```

## Usage

*(add run instructions here)*

## Testing

```bash
pytest
```

### Results

### Screenshots

### Detection Tuning


## Development
The codebase is organized so each stage of the pipeline can be developed and tested independently:

```
Wazuh Lab
    ↓
Alert Reader
    ↓
Alert Model
    ↓
Severity Processing
    ↓
AI Analysis
    ↓
Reports
    ↓
Notifications
    ↓
Dashboard
```


## License

MIT License — see [LICENSE](LICENSE) for details.