# FraudGenuineApp
🔍 Fraudetect: Google Play Fraudulent App Detection System
Detect fraudulent, genuine, or suspicious Android apps using Gemini 1.5 Flash (v2.5), rule-based heuristics, and structured JSON outputs.

📌 🎯 Objective
Design an automated system that flags fraudulent or harmful apps by analyzing:

Metadata

Permissions

Reviews

Developer patterns

using Gemini 1.5 Flash for semantic interpretation.

🧱 💡 Architecture Overview
mermaid
Copy
Edit
flowchart TD
    A[📲 Google Play Scraper/API] --> B[🧾 App Data JSON]
    B --> C[🧠 Gemini 1.5 Flash (v2.5)]
    C --> D[🧰 Rule-based Validator]
    D --> E[📦 Structured Output: {type, reason}]
    E --> F[📊 Evaluation w/ Labeled Dataset]
🧩 Core Components
1️⃣ Data Collection
Use google-play-scraper or a custom crawler to extract:

App title, description, installs, developer info

Permissions list (dangerous, normal)

Review body & star rating

bash
Copy
Edit
python fetch_app_data.py --app_id com.example.fakevpn
2️⃣ LLM Integration: Gemini 1.5 Flash (v2.5)
Gemini is used for semantic pattern recognition in:

Descriptions (misleading marketing)

Review authenticity (bots, repetition)

Permission misuse (e.g., SMS or location without purpose)

🔐 Gemini Configuration (Python SDK):

python
Copy
Edit
import google.generativeai as genai
genai.configure(api_key=GEMINI_API_KEY)

model = genai.GenerativeModel("models/gemini-1.5-flash")
response = model.generate_content(app_json_input)
3️⃣ Structured Output Format
All Gemini outputs are parsed using Pydantic to ensure clean structure:

json
Copy
Edit
{
  "type": "fraud" | "genuine" | "suspected",
  "reason": "Concise explanation (max 300 characters)"
}
✅ Example:

json
Copy
Edit
{
  "type": "fraud",
  "reason": "Requests SMS & call log access without justification, and fake reviews detected."
}
4️⃣ Fraud Detection Framework
A hybrid of:

✅ Rule-Based Flags:

Suspicious keywords in title/description

Dangerous permissions (SMS, Contacts, etc.)

Dev email anomalies, excessive updates

🤖 LLM Inference via Gemini:

Language-based deception patterns

Review spam detection

Developer trust scoring

5️⃣ Testing & Validation
Run Gemini-based detector over labeled dataset.

Compare against known fraud/genuine classifications.

📊 Metrics Computed:

Accuracy

Precision / Recall (especially for "fraud")

Confusion Matrix

Execution time per app (Gemini inference benchmark)
