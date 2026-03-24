# Pipeline Setup & Usage Guide

## Prerequisites
- Python 3.10+
- A MongoDB Atlas account with a cluster set up
- Access to the project repository

---

## 1. Clone the Repository
```bash
git clone <repository-url>
cd <project-folder>
```

---

## 2. Create a Virtual Environment
```bash
# Create
python -m venv venv

# Activate (Mac/Linux)
source venv/bin/activate

# Activate (Windows)
venv\Scripts\activate
```

---

## 3. Install Dependencies
```bash
pip install -r requirements.txt
```

---

## 4. Create the `.env` File
Create a file named `.env` in the project root folder with the following:

```
MONGO_URI=mongodb+srv://<user>:<password>@<cluster>.mongodb.net/?retryWrites=true&w=majority
```

Replace `<user>`, `<password>`, and `<cluster>` with your MongoDB Atlas credentials.

---

## 5. Tag the Parameters Cell in the Notebook
Open `notebook.ipynb` in Jupyter:

```bash
jupyter lab
```

Then:
1. Click on the parameters cell at the top of the notebook (the one with `MONTH_LABEL`, `DATA_PATH`, `RESULTS_PATH`)
2. Go to **View → Cell Toolbar → Tags**
3. Type `parameters` in the tag box and click **Add Tag**
4. Save the notebook

This only needs to be done once.

---

## 6. Run the Pipeline

### Process the previous month automatically:
```bash
python run_pipeline.py
```

### Process a specific month:
```bash
python run_pipeline.py "April 2024"
```

---

## 7. Check the Output
- Executed notebooks are saved to the `outputs/` folder with the month in the filename e.g. `outputs/notebook_April_2024.ipynb`
- Results are stored in MongoDB Atlas under the `lagos_air_quality` database in two collections:
  - `processed_months` — metrics and centroids per month
  - `daily_observations` — all daily rows with cluster assignments

---

## Notes
- Make sure your virtual environment is active (`(venv)` shows in your terminal) before running
- Add `.env` to your `.gitignore` so secrets are never committed to git
- The pipeline automatically cleans up all temporary files after each run