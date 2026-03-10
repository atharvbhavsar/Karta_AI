# ⚡ KARTA AI

**India's First RBI-Compliant AI Credit Intelligence Platform**

KARTA AI is a powerful, automated credit appraisal engine built for the Indian mid-market lending sector. It ingests complex, messy financial documents, detects fraud, evaluates risk, and automatically writes the full Credit Appraisal Memo (CAM) natively. It takes subjective, unorganized MSME data and turns it into concrete, explainable lending decisions.

---

## 🚀 What We Have Built

1. **Intelligent Document Parsing**: Created an engine that accepts scanned, handwritten, and mixed-language (Hindi/English) PDFs like Balance Sheets, Bank Statements, and GST Filings. It bypasses simple text scraping and uses layout-aware extraction to structure the data.
2. **Real-time Early Warning System (EWS)**: Built a dynamic dashboard with live WebSocket telemetry that monitors active portfolios for volatility using simulated real-time drift algorithms. It flags upcoming defaults before they happen based on sentiment, bank flow, and GST mismatch.
3. **Advanced Risk Assessment UI**: Designed an interface that presents XGBoost Default Risk, Fraud Multipliers, Data Quality, and News Sentiment scores natively within a highly intuitive, corporate-grade React dashboard.
4. **SHAP Value Explanations**: Visualized the actual drivers behind a rejection or approval utilizing Waterfall SHAP diagrams. It shows exactly *why* a model made a decision (e.g., negative impact from high short-term debt).
5. **Generative CAM Synthesis**: Integrated Large Language Models (LLMs) to instantly generate a comprehensive, multi-page Credit Appraisal Memo synthesizing all financial records and background findings.
6. **Robust Hackathon Demo Flow**: Designed a built-in stress-test flow that takes "messy" distressed company data and successfully proves an AI-driven "REJECT" decision based on EMI bounces and plunging revenue.

---

## 🛠️ Detailed Technology Stack

### Frontend Hub (Client-Side)
- **Vite & React.js**: Ultra-fast hot-module reloading and optimized production build setups.
- **TypeScript**: Strict type-checking mapped perfectly to the Python backend models to prevent data parsing errors.
- **Vanilla CSS / Lucide React Icons**: We avoided heavy styling frameworks (like Tailwind) and built custom CSS from scratch to ensure pixel-perfect, tailored aesthetic matching modern fintech applications.
- **React Router DOM**: Client-side routing for navigating between Analysis, EWS, and History pages without reloading.
- **Recharts**: For dynamic, SVG-based graphing of risk factors and financial data.

### Backend Engine (Server-Side)
- **FastAPI (Python)**: The core orchestration framework. chosen for its extreme speed and native async support handling heavy I/O tasks like concurrent OCR and LLM calling.
- **WebSockets**: Implemented custom socket handlers pointing to `/ws/ews` for live telemetry data streaming to the frontend.
- **SQLite Database**: A lightweight, robust local database mapped with `sqlite3` to store document states, features, and analysis histories securely without external dependencies.
- **PyMuPDF (fitz) & FPDF**: For high-speed rendering of PDFs into analyzable image bytes and generative reporting. 
- **pdfplumber**: Used for layout-aware table extraction when reading bank statements.

### AI, NLP, and Machine Learning Architecture
- **Cohere Command V2 Model**: Used for synthesizing the final Credit Appraisal Memo by analyzing a JSON dictionary of risk signals and writing a human-readable banking report.
- **XGBoost (Decision Emulation)**: Emulated machine learning decision trees for calculating the ultimate Probability of Default (PD) and corresponding interest rate.
- **FinBERT Pipeline**: Financial sentiment analysis against live news streams to flag macro-economic risks for a specific borrower.
- **Tesseract OCR / Boto3 Textract**: Utilized for extracting raw text from messy, noisy, and rotated scanned financial images.

---

## 🔑 External API Integrations

To run this platform successfully, KARTA AI requires specific API keys to connect to various data enrichment and intelligence platforms. You must create a `.env` file in the root directory (`/KARTA/.env`) and add the following keys. 

*Here is exactly what we used and why:*

```env
# 1. COHERE API 
# Purpose: Powers the Generative CAM engine. Synthesizes thousands of data points into a fluent banking report.
COHERE_API_KEY="your-cohere-api-key"

# 2. NEWS API
# Purpose: Feeds live macro-economic and company-specific news into our FinBERT NLP pipeline for sentiment scoring.
NEWS_API_KEY="your-news-api-key"

# 3. MCA21 API (Ministry of Corporate Affairs)
# Purpose: Cross-checks director DINs, company registration status (CIN), and flags shell corporations automatically.
MCA_API_KEY="your-mca-api-key"

# 4. SENDGRID API
# Purpose: Hooks into the Early Warning System (EWS) to dispatch instant SMS/Email alerts to bank managers when a risk threshold breaches.
SENDGRID_API_KEY="your-sendgrid-api-key"

# 5. AWS CREDENTIALS (Optional for OCR scaling)
# Purpose: Bridges Tesseract OCR with AWS Textract for extreme low-resolution document recovery.
AWS_ACCESS_KEY_ID="your-aws-access-key"
AWS_SECRET_ACCESS_KEY="your-aws-secret-key"
AWS_REGION="ap-south-1"

# 6. SYSTEM CONFIG
ENVIRONMENT="development"
FRONTEND_URL="http://localhost:5173"
```

---

## 🏁 How to Run the Project Locally

You will need two separate terminal windows or standard command prompts to run both platforms simultaneously.

### 1. Start the Backend API Engine (Terminal 1)
```bash
# Navigate to the project root
cd /path/to/KARTA

# Create and activate a virtual environment (Windows)
python -m venv venv
.\venv\Scripts\activate

# Install the required Python packages
pip install -r requirements.txt

# Start the FastAPI server on port 8000
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```
*The backend API will be live and accepting uploads at: `http://localhost:8000`*

### 2. Start the Frontend Web Application (Terminal 2)
```bash
# Navigate to the frontend source folder
cd /path/to/KARTA/src

# Install Node dependencies
npm install

# Start the Vite development system
npm run dev
```
*The React UI will launch instantly and be available at: `http://localhost:5173`*

---

*Built with passion, late nights, and heavy AI engineering to bridge the gap between deep-tech and realistic Indian banking operations.*
