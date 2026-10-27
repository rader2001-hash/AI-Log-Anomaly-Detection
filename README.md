# AI-Powered Log Anomaly Detection

A Python tool that automatically analyses Windows security logs using Google Gemini AI, classifying each event as a Threat, Suspicious, or Normal with plain English explanations and recommended actions for each.

Built as part of a SOC home lab portfolio to demonstrate how AI can be used to automate the first-pass triage of security alerts.

---

## What It Does

- Ingests Windows security event logs (simulating Splunk output)
- Sends each log to Google Gemini AI for analysis
- Classifies each event as THREAT, SUSPICIOUS, or NORMAL
- Provides confidence level, explanation, and recommended action for each
- Generates a professional HTML report with colour-coded results

---

## Project Files

| File | Description |
|---|---|
| `analyser.py` | Core script that sends logs to Gemini and returns classifications |
| `report.py` | Generates the HTML report from the analysis results |
| `analysis_results.json` | Raw JSON output from Gemini |
| `report.html` | Visual HTML report with colour-coded threat cards |

---

## Sample Output

Gemini correctly identified the following from the sample logs:

- 47 failed logon attempts against Tsmith from 192.168.111.129, classified as THREAT (brute force attack)
- Successful Administrator logon outside business hours, classified as SUSPICIOUS
- cmd.exe created under SYSTEM account, classified as THREAT (privilege escalation indicator)
- 52 failed logon attempts against Jsmith from 192.168.111.129, classified as THREAT (brute force attack)

The source IP 192.168.111.129 is the Kali Linux attacker machine from the AD Brute Force Detection lab. Gemini identified it as malicious purely from the log patterns.

---

## Key Splunk Queries Used (Lab 2 Reference)

```splunk
index=endpoint EventCode=4625
index=endpoint EventCode=4624
```

---

## Setup

1. Install dependencies:
```bash
pip install google-genai
```

2. Add your Gemini API key to `analyser.py`:
```python
client = genai.Client(api_key="API_KEY")
```

3. Run the analyser:
```bash
python analyser.py
```

4. Generate the HTML report:
```bash
python report.py
```

5. Open `report.html` in your browser.

---

## Screenshots

### Environment Setup
![Libraries Installed](screenshots/libraries%20installed%20success.png)
![Python Version](screenshots/python%20version.png)
![VS Code Setup](screenshots/vs%20code%20project%20setup.png)

### The Code
![Analyser Code](screenshots/analyser%20py%20code.png)
![Gemini Model Config](screenshots/gemini%20model%20config.png)
![Report Code](screenshots/report%20py%20code%20vs%20code.png)

### Running the Analyser
![Gemini Analysis Logs 1 and 2](screenshots/gemini%20analysis%20logs%201%20and%202.png)
![Gemini Analysis Logs 3 and 4](screenshots/gemini%20analysis%20logs%203%20and%204.png)

### Generating the Report
![Report Generated](screenshots/report%20generated%20terminal.png)

### HTML Report
![HTML Report Top](screenshots/html%20report%20top.png)
![HTML Report Bottom](screenshots/html%20report%20bottom.png)

---

## Tools Used

- Python 3.14
- Google Gemini AI (gemini-2.5-flash)
- VS Code
- Windows Event Log data (Event IDs 4624, 4625, 4688)

---

## Related Labs

- [Lab 1: SOC Automation with Wazuh, TheHive and Shuffle](https://github.com/rader2001-hash/SOC-Automation-Homelab)
- [Lab 2: Active Directory and Brute Force Detection with Splunk](https://github.com/rader2001-hash/AD-Brute-Force-Detection-Splunk)
