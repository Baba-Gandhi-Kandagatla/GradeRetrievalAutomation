# OU Grade Retrieval Automation

OU Grade Retrieval Automation collects a batch of Osmania University exam results into one Excel workbook. College staff supply the exam page and hall-ticket numbers. The application retrieves the individual results in parallel and organizes the grades by student and subject.

Developed by Baba Gandhi Kandagatla during his first year of engineering, the project received a college letter of appreciation. The author reports use by multiple OU-affiliated colleges.

## From hall-ticket list to workbook

1. Open the Flask form and enter the OU results page for the exam.
2. Enter an inclusive range of 12-digit hall-ticket numbers or upload a CSV or Excel file. For a file, include a header row and put the numbers in the first column.
3. The app divides the list among worker threads. Each worker requests individual result pages and extracts rows from their HTML tables with Beautiful Soup.
4. Download `results.xlsx`. It lists the roll number, subject code, subject name, grade points, grade secured and SGPA. The app adds a “not found” entry for hall tickets it recognizes as missing.

## Local setup

Use Python 3.9 in a virtual environment for compatibility with the pinned NumPy and pandas versions. From the repository root, run the following commands and open `http://127.0.0.1:5000`.

```sh
python -m pip install -r requirements.txt
python app.py
```

The Flask implementation is in `app.py`, with the collection form in `templates/index.html`. The repository also includes a desktop implementation in `trinetra.py`, which requires PyQt5 separately.

The parser expects the OU result URL pattern and table layout encoded in `app.py`. Changes to the university site can affect extraction. Use authorized hall-ticket lists and check a sample of exported grades against the source before relying on a batch result.
