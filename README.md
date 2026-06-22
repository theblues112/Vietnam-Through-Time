# Vietnam History Dashboard

An interactive data visualization project that captures the history of Vietnam through structured datasets, timelines, maps, historical figures, and major events.

The goal of this project is to transform Vietnamese history into an explorable dashboard where users can study different periods, dynasties, people, locations, and historical themes in one place.

---

## Project Objective

This project aims to answer questions such as:

- What are the major periods in Vietnamese history?
- Which events shaped Vietnam’s political, cultural, and territorial development?
- Where did important historical events happen?
- Who were the key historical figures in each period?
- How did Vietnam change from ancient states to modern Vietnam?
- Which events are well-documented, approximate, disputed, or legendary?

The project combines historical research, data cleaning, data modeling, and interactive visualization.

---

## Dataset Overview

The project is built from multiple CSV datasets.

| Dataset | Description |
|---|---|
| `events_completed.csv` | Main event dataset containing historical events, dates, categories, locations, people, descriptions, and importance scores |
| `periods.csv` | Historical periods and dynasties of Vietnam |
| `people_with_life_years.csv` | Important historical figures with roles, related periods, and birth/death years where available |
| `locations.csv` | Historical and modern locations connected to events |
| `sources_completed.csv` | Source information used for verification and documentation |
| `events_completed_data_dictionary.csv` | Explanation of columns in the events dataset |

---

## Main Event Dataset Columns

The main dataset is `events_completed.csv`.

Important columns include:

| Column | Description |
|---|---|
| `event_id` | Unique ID for each historical event |
| `event_name` | Name of the event |
| `year_start` | Start year of the event |
| `year_end` | End year of the event, if applicable |
| `year_label` | Human-readable year label, especially useful for BCE dates |
| `period_id` | ID linking the event to `periods.csv` |
| `period_name` | Historical period or dynasty |
| `broad_era` | Larger era group, such as Ancient Vietnam or Colonial Vietnam |
| `category` | Event type, such as Politics, Military, Culture, Economy, or Territory |
| `location_ids` | IDs linking the event to `locations.csv` |
| `location_names` | Names of related locations |
| `person_ids` | IDs linking the event to `people_with_life_years.csv` |
| `person_names` | Related historical figures |
| `description_short` | Short description for dashboard display |
| `description_long` | Longer explanation of the event |
| `importance_score` | Project-based score from 1 to 5 |
| `source_id` | ID linking the event to `sources_completed.csv` |
| `verification_status` | Whether the event has been checked or still needs review |
| `date_status` | Whether the date is historical, approximate, disputed, or legendary |

---

## Importance Score

The `importance_score` column is a project-based rating from 1 to 5.

| Score | Meaning |
|---:|---|
| 1 | Minor event or brief mention |
| 2 | Secondary historical event |
| 3 | Important within one period |
| 4 | Very important national or regional event |
| 5 | Major turning point in Vietnamese history |

This score is not an official historical rating. It is used to help filter and rank events in the dashboard.

---

## Date Status

The `date_status` column helps show how certain the date is.

| Status | Meaning |
|---|---|
| `historical` | Generally accepted historical date |
| `approximate` | Estimated date or broad time range |
| `disputed` | Date is debated by sources |
| `legendary_or_traditional` | Traditional or legendary date, especially for ancient history |
| `needs_verification` | Date should be checked again |

This is important because ancient Vietnamese history contains legendary and traditional material that should not be treated the same as modern documented events.

---

## Missing Data Rule

For numeric columns, missing data is left blank.

Examples:

- Unknown `birth_year` is left blank
- Unknown `death_year` is left blank
- Unknown `latitude` or `longitude` is left blank

Do not write text such as `"null"` or `"unknown"` inside numeric columns. Status columns are used to explain missing values.

Example:

```csv
person_name,birth_year,death_year,life_dates_status
Kinh Duong Vuong,,,legendary_or_unknown
Ngo Quyen,898,944,verified
To Lam,1957,,living
```

---

## Project Folder Structure

Recommended project structure:

```text
vietnam-history-dashboard/
│
├── data/
│   ├── raw/
│   │   ├── periods.csv
│   │   ├── people_with_life_years.csv
│   │   ├── locations.csv
│   │   ├── events_completed.csv
│   │   ├── sources_completed.csv
│   │   └── events_completed_data_dictionary.csv
│   │
│   ├── processed/
│   │   ├── events_clean.csv
│   │   ├── periods_clean.csv
│   │   ├── people_clean.csv
│   │   ├── locations_clean.csv
│   │   └── sources_clean.csv
│
├── notebooks/
│   ├── 01_data_validation.ipynb
│   ├── 02_data_cleaning.ipynb
│   └── 03_exploratory_analysis.ipynb
│
├── dashboard/
│   └── app.py
│
├── README.md
└── requirements.txt
```

---

## Data Validation Plan

Before building the dashboard, the datasets should be validated.

Validation checks include:

- Check that all IDs are unique
- Check that all `period_id` values in events exist in `periods.csv`
- Check that all `person_ids` in events exist in `people_with_life_years.csv`
- Check that all `location_ids` in events exist in `locations.csv`
- Check that all `source_id` values exist in `sources_completed.csv`
- Check that BCE years are stored as negative numbers
- Check that categories are consistent
- Check missing values in important columns
- Check duplicated events
- Check rows marked as `needs_verification`

---

## Dashboard Plan

The first dashboard version will be built with Streamlit.

Suggested dashboard pages:

### 1. Overview Page

Main summary of the dataset.

Possible visuals:

- Total number of events
- Total periods
- Total people
- Total locations
- Events by broad era
- Events by category
- Most important events

### 2. Historical Timeline

Interactive timeline of Vietnamese history.

Filters:

- Broad era
- Period
- Category
- Importance score
- Date status
- Verification status

### 3. Historical Map

Map of event locations.

Features:

- Plot historical locations using latitude and longitude
- Filter by period and category
- Click a location to view related events
- Mark approximate locations clearly

### 4. People and Events

Explore historical figures.

Features:

- Important figures by period
- People ranked by importance score
- Events connected to each person
- Life years where available

### 5. Sources and Verification

Show transparency of the dataset.

Features:

- Events by source
- Events needing verification
- Disputed or approximate dates
- Legendary/traditional ancient entries

---

## Tech Stack

Recommended tools:

| Tool | Purpose |
|---|---|
| Python | Main programming language |
| Pandas | Data cleaning and validation |
| Streamlit | Dashboard application |
| Plotly | Interactive charts |
| PyDeck or Folium | Interactive maps |
| Jupyter Notebook | Data validation and exploration |
| GitHub | Version control and portfolio hosting |

---

## Installation

Clone the repository:

```bash
git clone https://github.com/your-username/vietnam-history-dashboard.git
cd vietnam-history-dashboard
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate the environment:

Windows:

```bash
.venv\Scripts\activate
```

macOS/Linux:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Run the Dashboard

After preparing the cleaned data files, run:

```bash
streamlit run dashboard/app.py
```

---

## Suggested `requirements.txt`

```text
pandas
streamlit
plotly
pydeck
openpyxl
```

---

## Current Project Status

Current status:

- [x] Created period dataset
- [x] Created people dataset
- [x] Added life years for people where available
- [x] Created location dataset
- [x] Created event dataset
- [x] Added supplemental Vietnamese narrative events
- [ ] Validate dataset links and missing values
- [ ] Clean and export processed datasets
- [ ] Build dashboard MVP
- [ ] Add timeline visualization
- [ ] Add interactive map
- [ ] Deploy dashboard
- [ ] Write project report

---

## Limitations

This project uses historical sources that may contain uncertainty, especially for ancient Vietnamese history.

Important limitations:

- Some early dates are legendary or traditional
- Some ancient political entities are debated
- Some locations are approximate
- Some people have uncertain birth or death years
- Some events still need source verification
- Importance scores are project-based and subjective

These limitations are handled using columns such as:

- `date_status`
- `verification_status`
- `coordinate_status`
- `life_dates_status`
- `notes`

---

## Future Improvements

Possible improvements:

- Add more verified academic sources
- Add Vietnamese and English descriptions
- Add historical map layers by period
- Add dynasty family trees
- Add network graph between people and events
- Add topic modeling for event descriptions
- Add search function for people, places, and events
- Deploy the dashboard on Streamlit Community Cloud

---

## Portfolio Value

This project demonstrates:

- Data collection
- Data cleaning
- Relational dataset design
- Historical data modeling
- Data validation
- Interactive dashboard development
- Data storytelling
- Research-based visualization

It can be used as a strong data science portfolio project because it combines technical skills with a meaningful historical topic.