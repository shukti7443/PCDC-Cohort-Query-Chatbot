# 🩺 PCDC Cohort Query Chatbot

An AI-powered chatbot that lets researchers describe patient cohorts in natural language and automatically generates **GraphQL queries** for the Pediatric Cancer Data Commons (PCDC).

---

## 📌 Project Overview

Built as part of the GSoC / open-source initiative to enhance cohort discovery for the PCDC platform. Instead of manually navigating complex UI filters or writing raw GraphQL, researchers can simply describe their patient cohort in plain English and get a ready-to-use query.

### ✅ Features

- 🤖 **Agentic Chatbot** — Routes user intent to the right tool automatically
- 📖 **Tool 1: General Inquiry** — Answers general questions about PCDC and cohort discovery
- 📚 **Tool 2: Documentation Browser** — Searches and surfaces PCDC documentation
- ⚙️ **Tool 3: GraphQL Generator** — Converts natural language into valid PCDC GraphQL queries
- 🧪 **Query Evaluator** — Compares generated queries against saved filtersets
- 💾 **Query History** — Saves and loads past queries
- 📋 **Copy & Export** — One-click copy of generated GraphQL

---

## 🗂️ Project Structure

```
pcdc-chatbot/
├── public/
│   └── index.html
├── src/
│   ├── components/
│   │   ├── ChatWindow.js
│   │   ├── Message.js
│   │   ├── QueryDisplay.js
│   │   └── ToolBadge.js
│   ├── tools/
│   │   ├── agentRouter.js
│   │   ├── generalInquiry.js
│   │   ├── docsBrowser.js
│   │   └── graphqlGenerator.js
│   ├── utils/
│   │   ├── queryEvaluator.js
│   │   ├── queryHistory.js
│   │   └── pcdc-schema.js
│   ├── styles/
│   │   └── main.css
│   └── app.js
├── docs/
│   └── PCDC_DATA_MODEL.md
├── tests/
│   ├── graphqlGenerator.test.js
│   └── sampleFiltersets.json
├── .env.example
├── .gitignore
├── package.json
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js >= 18
- An Anthropic API key (https://console.anthropic.com/)

### Installation

```bash
git clone https://github.com/YOUR_USERNAME/pcdc-chatbot.git
cd pcdc-chatbot
npm install
```

### Configuration

```bash
cp .env.example .env
# Edit .env and add your API key
```

### Run Locally

```bash
npm start
# Opens at http://localhost:3000
```

### Run Tests

```bash
npm test
```

---

## 🧠 How the Agent Works

Every message is classified into one of three tools:

| Intent | Tool |
|---|---|
| General questions about PCDC | Tool 1: General Inquiry |
| "Show me docs for..." | Tool 2: Docs Browser |
| "Find patients with AML..." | Tool 3: GraphQL Generator |

### Example

**Input:** "Find all patients with AML diagnosis, age 2–10, who received chemotherapy"

**Output:**
```graphql
{
  subject(
    with_path_to: [
      { type: "diagnosis", diagnosis: "Acute Myeloid Leukemia" }
      { type: "diagnosis", age_at_diagnosis_min: 730, age_at_diagnosis_max: 3650 }
      { type: "treatment", treatment_type: "Chemotherapy" }
    ]
  ) {
    subject_id
    race
    ethnicity
    vital_status
    diagnosis { diagnosis age_at_diagnosis }
    treatment { treatment_type }
  }
}
```

---

## 🤝 Contributing

1. Fork the repo
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit: `git commit -m 'Add my feature'`
4. Push: `git push origin feature/my-feature`
5. Open a Pull Request

---

## 📄 License

MIT License
