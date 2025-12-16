# Z-Downloader

Download and analyze payslips from Zucchetti HR portal.

## Installation

```bash
pip install -r requirements.txt
```

## Tools Overview

This repository contains three tools for managing Zucchetti payslips:

1. **main.py** - Download payslips from the Zucchetti portal
2. **extractor.py** - Extract net salary data to Excel
3. **payslip_analysis.ipynb** - Interactive Jupyter notebook for comprehensive analysis

---

## main.py - Payslip Downloader

Download payslip PDFs from Zucchetti HR portal.

### Usage

```bash
python main.py -u USERNAME -o ORGANIZATION [-p PASSWORD] [-d OUTPUT_DIR] [-H HOST]
```

### Options

> [!CAUTION]
> It's strongly suggested to not use the -p option, as it will leak your password to your CLI history file.
> Use the script without the -p flag to have an interactive prompt for the password.
> Always read and verify the script to understand that your credentials and data are not leaked.

| Flag | Description |
|------|-------------|
| `-u, --username` | Zucchetti username (required) |
| `-o, --org` | Organization slug from URL (required) |
| `-p, --password` | Password (prompts securely if omitted) |
| `-d, --output-dir` | Download directory (default: current) |
| `-H, --host` | Base URL of the portal (default: `https://saas.zucchetti.it`) |

### Example

```bash
# Download to ~/Documents/payslips using default portal
python main.py -u john.doe -o HRPORTAL -d ~/Documents/payslips

# Use a different Zucchetti portal
python main.py -u john.doe -o MYCOMPANY -H https://saas.zucchetti.it -d ./payslips
```

---

## extractor.py - Simple Net Salary Extractor

Extract net salary amounts from downloaded payslip PDFs and save to an Excel file.

### Usage

```bash
python extractor.py [-i INPUT_DIR] [-o OUTPUT_DIR]
```

### Options

| Flag | Description |
|------|-------------|
| `-i, --input-dir` | Directory containing payslip PDFs (default: current) |
| `-o, --output-dir` | Output directory for Excel file (default: current) |

### Example

```bash
# Extract from ~/payslips and save to ~/reports
python extractor.py -i ~/Documents/payslips -o ~/Documents/reports
```

### Output

Creates `output.xls` with columns:
- **DATA** - Payslip date (MM-YYYY)
- **NETTO DEL MESE** - Net salary amount

---

## payslip_analysis.ipynb - Interactive Analysis Notebook

Comprehensive Jupyter notebook for analyzing payslip data with visualizations.

### Features

- **Data Extraction**: Parses all payslip PDFs extracting:
  - Net salary (Netto del mese)
  - Gross salary (Totale competenze)
  - Deductions (Totale trattenute)
  - TFR contributions
  - Vacation hours (Ferie)
  - Leave hours (Permessi P.A.R.)
  - Bonus Aziendale (one-time bonuses)
  - Rimborso Spese (expense reimbursements)

- **Income Categorization**:
  - Regular monthly salary
  - Tredicesima (13th month salary)
  - Bonus Aziendale
  - Expense reimbursements

- **Visualizations**:
  - Net salary trend over time
  - Year-over-year comparison
  - Deduction breakdown (pie chart)
  - Vacation/leave hours balance
  - TFR accumulation
  - Gross vs Net vs Deductions

- **Exports**:
  - CSV file with all extracted data
  - PDF report with charts and summary

### Configuration

Edit the configuration section in the first cell:

```python
# ========== CONFIGURATION ==========
INPUT_DIR = "."    # Directory containing payslip PDFs
OUTPUT_DIR = "."   # Directory for generated reports and CSV
# ===================================
```

### Example

```python
# Analyze payslips from a specific folder
INPUT_DIR = "/Users/john/Documents/payslips"
OUTPUT_DIR = "/Users/john/Documents/reports"
```

### Running the Notebook

1. Open in VS Code or Jupyter:
   ```bash
   jupyter notebook payslip_analysis.ipynb
   ```

2. Set `INPUT_DIR` and `OUTPUT_DIR` in the first cell

3. Run all cells (Shift+Enter or "Run All")

### Generated Files

- `payslip_data.csv` - Complete extracted data
- `payslip_report.pdf` - Multi-page PDF with:
  - Executive summary
  - Salary trends
  - Year-over-year comparisons
  - Vacation/leave tracking
  - TFR accumulation
  - Gross/Net/Deduction breakdown

