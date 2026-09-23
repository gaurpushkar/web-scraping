# Web Scraping – State Agricultural Beneficiary Lists

Selenium notebooks that walk the cascading dropdowns on two Indian state government portals and collect beneficiary lists at the Gram Panchayat level.

| Notebook | Portal | Hierarchy | Output |
|---|---|---|---|
| `bihar_farmech_scraper.ipynb` | [Bihar FarMech](https://farmech.bih.nic.in/FMNEW/BenefGPListFrom1920.aspx) | Year → District → Block → GP | `data/bihar/<year>.xlsx` |
| `odisha_kalia_scraper.ipynb` | [Odisha KALIA](https://kaliaportal.odisha.gov.in/Beneficiarylist.aspx) | District → Block → GP | PDF downloads + `data/odisha/<district>-<block>.csv` index |

## Setup

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

You need Google Chrome installed. Selenium (4.6+) downloads a matching ChromeDriver automatically. To use your own driver, set `CHROMEDRIVER_PATH`:

```bash
export CHROMEDRIVER_PATH=/path/to/chromedriver          # macOS/Linux
set CHROMEDRIVER_PATH=C:\path\to\chromedriver.exe       # Windows
```

## Usage

```bash
jupyter notebook
```

Open a notebook and run the cells top to bottom. The output goes to `data/` next to the notebook. Git ignores that folder.

**Bihar – resuming a run:** the `l_d`, `l_b` and `l_gp` variables set the District, Block and GP codes to skip up to. Set them to `"0"` to scrape everything. The year range is set in the loop near the end (`range(2022, 2023)`).

**Odisha:** a run on this portal can stop with `StaleElementReferenceException`. The page reloads after each dropdown change, so the saved element references go stale. Re-run from the last block that finished.

## Notes

- Browsers run headless. Remove the `--headless=new` line to watch the browser.
- Use these notebooks responsibly. Follow each portal's terms of use and throttle requests where you can.

## Author

**Pushkar Gaur** – gaur.pushkar8@gmail.com
