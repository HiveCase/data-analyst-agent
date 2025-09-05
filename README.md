# 📊 Data Analyst Agent

An API-powered **Data Analyst Agent** that leverages LLMs to source, prepare, analyze, and visualize data.
It can handle unstructured and structured inputs, perform queries, generate plots, and return results in the requested format — all through a single API endpoint.

---

## 🚀 Features

* Accepts **questions + optional data files** via `POST` requests.
* Supports **text, images, and datasets** (CSV, JSON, Parquet, etc.).
* Performs:

  * Web scraping
  * Data preprocessing & transformation
  * SQL-like queries
  * Statistical analysis
  * Visualization (plots encoded as Base64 images)
* Returns results within **3 minutes**, formatted as requested (JSON, plots, arrays, etc.).

---

## 📡 API Usage

### Endpoint

```
POST https://app.example.com/api/
```

### Example Request

```bash
curl "https://app.example.com/api/" \
  -F "questions.txt=@question.txt" \
  -F "image.png=@image.png" \
  -F "data.csv=@data.csv"
```

* `questions.txt` → **Always required** (contains the analysis questions).
* Other files (CSV, images, PDFs, JSON, Parquet, etc.) → **Optional**.

---

## 📝 Example Questions

### 1. Film Dataset (Scraping + Analysis)

**Input (questions.txt):**

```
Scrape the list of highest grossing films from Wikipedia:
https://en.wikipedia.org/wiki/List_of_highest-grossing_films

1. How many $2 bn movies were released before 2000?
2. Which is the earliest film that grossed over $1.5 bn?
3. What's the correlation between Rank and Peak?
4. Draw a scatterplot of Rank and Peak with a dotted red regression line.
```

**Output (JSON):**

```json
[1, "Titanic", 0.485782, "data:image/png;base64,iVBORw0KG..."]
```

---

### 2. Indian High Court Judgments Dataset

Dataset hosted on [ecourts](https://judgments.ecourts.gov.in/).

**Input (questions.txt):**

```
1. Which high court disposed the most cases from 2019–2022?
2. What's the regression slope of date_of_registration vs. decision_date by year in court=33_10?
3. Plot the year vs. delay (# of days) as a scatterplot with regression line. Encode as base64 < 100 KB.
```

**Output (JSON):**

```json
{
  "Which high court disposed the most cases from 2019 - 2022?": "Delhi High Court",
  "What's the regression slope ...": -0.27,
  "Plot the year and delay ...": "data:image/webp;base64,iVBORw0KG..."
}
```

---

## 📊 Supported Data Sources

* 🌐 Web (scraping & APIs)
* 📂 Local / Uploaded files (`.csv`, `.json`, `.parquet`, `.pdf`)
* 🗄️ Databases (via SQL/ DuckDB/ Pandas queries)
* 🖼️ Images (vision-based extraction)

---


## 🛠️ Local Development

### Prerequisites

* Python 3.10+
* Virtual environment
* OpenAI API key (or other LLM provider)
* Dependencies from `requirements.txt`

### Setup

```bash
git clone https://github.com/HiveCase/data-analyst-agent.git
cd data-analyst-agent
pip install -r requirements.txt
```

### Run API

```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

API available at:

```
http://localhost:8000/api/
```

---

## 📦 Deployment

You can deploy to:

* **Vercel**
* **Render**
* **Fly.io**
* **AWS Lambda / API Gateway**
* **Docker + Cloud Provider**

Example (Docker):

```bash
docker build -t data-analyst-agent .
docker run -p 8000:8000 data-analyst-agent
```

---

## 📚 Tech Stack

* **FastAPI** – API framework
* **LangChain / LLMs** – reasoning & natural language understanding
* **Pandas / DuckDB** – data analysis
* **Matplotlib / Seaborn** – visualization
* **Playwright / Requests** – web scraping
* **PyPDF / Tika** – document parsing

---

## 🤝 Contributing

Contributions are welcome!
Please open an issue or submit a pull request.

---

## 📄 License

MIT License © 2025 [HiveCase](https://github.com/HiveCase)
