# slprices: Grocery Price Collection & Comparison

Collect, clean, and compare product prices from **Kroger** (via API) and **Superlo Foods** (via web scraping).  
Get your results as an easy-to-read Excel spreadsheet, ready to share or analyze.

---

## 🚦 Quick Start (Non-Technical Users)

### What You’ll Need:
- A Windows, Mac, or Linux computer
- [Anaconda](https://www.anaconda.com/products/distribution) installed (see below)
- The project folder (`slprices/`) unzipped and ready

---

### 1. Install Anaconda (one time only)

- Go to https://www.anaconda.com/products/distribution
- Download the Anaconda installer for your operating system and run it.
- Follow the prompts to complete the installation.

---

### 2. Set Up the Project Environment

- Open **Anaconda Prompt** (Windows) or your terminal (Mac/Linux).
- Use `cd` to navigate to the project folder, for example:
    cd C:\Users\YourName\Downloads\slprices

- Run the following command to create your Python environment:
    `conda env create -f environment.yml`

- Activate the new environment:
    `conda activate slprices`


---

### 3. Edit Your Product List

- Open `input/items_to_price_check.xlsx` in Excel.
- Add or update the items, UPCs, and URLs you want to price check.
- Save and close the file when finished.

---

### 4. Run the Entire Workflow

- **Windows:**  
Double-click `run_all.bat` in the project folder.
- **Mac/Linux:**  
In your terminal, run:
    `./run_all.sh`
(If you see a permissions error, first run `chmod +x run_all.sh`)

---

### 5. View Your Results

- Your completed price sheet will be found at:
    `output/items_to_price_check_updated.xlsx`

- Open this file in Excel.

---

### If You Get Stuck:

- Double-check that you edited and saved the correct input file.
- Make sure you activated your Anaconda environment:  
`conda activate slprices`
- For technical issues, contact your project admin.

---

## 🛠️ Technical/Advanced User Guide

### Overview

This project orchestrates:
- Kroger product price pulling via API (`kroger_api_scraper.py`)
- Superlo Foods price scraping via Scrapy spider (`superlo.py`)
- Data cleaning and merging (`clean_excel.py`, `merge_prices.py`)
- Test mode support for safer, faster runs (`slprices/config.py`)

---

### Setup & Dependencies

#### Anaconda Environment (Recommended)

- All Python packages and dependencies are managed for you.
- Install Anaconda: https://www.anaconda.com/products/distribution
- Create the environment:
    `conda env create -f environment.yml`
- Activate it:
    `conda activate slprices`
#### Manual pip install (if needed):
    pip install -r requirements.txt

---

### Workflow Steps

1. **Edit** `input/items_to_price_check.xlsx` with your products.

2. **Clean the Excel file:** 
    `python -m slprices.scripts.clean_excel`
Creates `input/items_to_price_check_cleaned.xlsx`.

3. **Pull Kroger prices:**  
    `python kroger_api_scraper.py`
Creates `output/kroger_products.csv`.

4. **Scrape Superlo prices:**  
    `scrapy crawl superlo -O output/superlo_products.csv`
(The `-O` argument is required!)

5. **Merge everything into a final report:**  
python -m slprices.scripts.merge_prices
Output: `output/items_to_price_check_updated.xlsx`

---

### All-in-One Automation

- **Windows:**  
Run `run_all.bat` by double-clicking it.
- **Mac/Linux:**  
Run `./run_all.sh` in your terminal (make it executable with `chmod +x run_all.sh` if needed).

---

### Switching Between Test and Production Modes

- In `slprices/config.py`, set:
```python
TEST_MODE = True   # Use test files for safe/quick runs
TEST_MODE = False  # Use all items for real results
```
All scripts will use the appropriate input files automatically.


---

### Typical Folder Structure

slprices/
  input/
    items_to_price_check.xlsx
    items_to_price_check_cleaned.xlsx
    kroger_upcs.txt / kroger_upcs_test.txt
    superlo_urls.txt / superlo_test.txt
  output/
    kroger_products.csv
    superlo_products.csv
    items_to_price_check_updated.xlsx
  logs/
    ...
  scripts/
    clean_excel.py
    merge_prices.py
  kroger_api_scraper.py
  superlo.py
  run_all.bat
  run_all.sh
  slprices/
    config.py
    paths.py
    ...
  environment.yml

---

### Support
For technical help, bug reports, or feature requests, contact your project admin or developer.
