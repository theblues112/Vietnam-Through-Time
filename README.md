# Vietnam History Dashboard

An interactive data visualization project that captures the history of Vietnam through structured datasets, timelines, maps, historical figures, and major events.

The goal of this project is to transform Vietnamese history into an interactive scrollytelling dashboard that guides users era by era, connecting major events, smaller related events, people, and locations into one visual historical journey.

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

## Project Experience

The dashboard is designed around two modes.

### Story Mode

Story Mode is the main guided experience. Each scroll section represents one major era in Vietnamese history:

- Ancient Vietnam
- Bắc thuộc and resistance
- Independent dynastic Vietnam
- Division and Nam tiến
- Nguyễn dynasty and French colonization
- Revolution and war
- Vietnam War
- Đổi Mới and modern Vietnam

Each era can show an era title, time range, short historical summary, major events, smaller connected events, key people, key locations, a map, and historical certainty/status. Events are arranged as connected sequences so users can follow how one turning point leads to another.

### Explore Mode

Explore Mode is the full dashboard for all events. Users can filter and search the complete dataset by period, broad era, category, importance score, people, locations, and timeline range.

---

## Dataset Overview

The project is built from multiple CSV datasets.

| Dataset | Description |
|---|---|
| `data/raw/events.csv` | Main event dataset containing historical events, dates, categories, locations, people, descriptions, and importance scores |
| `data/raw/people.csv` | Important historical figures with roles, related periods, and birth/death years where available |
| `data/raw/periods.csv` | Historical periods and dynasties of Vietnam |
| `data/raw/locations.csv` | Historical and modern locations connected to events |
| `data/processed/story_eras.csv` | Story Mode eras used as the main scrollytelling sections |
| `data/processed/story_events.csv` | Selected ordered events for each Story Mode era |

---

## Main Event Dataset Columns

The main dataset is `data/raw/events.csv`.

Important columns include:

| Column | Description |
|---|---|
| `event_id` | Unique ID for each historical event |
| `event_name` | Name of the event |
| `year_start` | Start year of the event |
| `year_end` | End year of the event, if applicable |
| `year_label` | Human-readable year label, especially useful for BCE dates |
| `period_id` | ID linking the event to `data/raw/periods.csv` |
| `period_name` | Historical period or dynasty |
| `broad_era` | Larger era group, such as Ancient Vietnam or Colonial Vietnam |
| `category` | Event type, such as Politics, Military, Culture, Economy, or Territory |
| `location_ids` | IDs linking the event to `data/raw/locations.csv` |
| `location_names` | Names of related locations |
| `person_ids` | IDs linking the event to `data/raw/people.csv` |
| `person_names` | Related historical figures |
| `description_short` | Short description for dashboard display |
| `description_long` | Longer explanation of the event |
| `importance_score` | Project-based score from 1 to 5 |

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

Current project structure:

```text
Vietnam-Through-Time/
|
|-- data/
|   |-- raw/
|   |   |-- events.csv
|   |   |-- periods.csv
|   |   |-- people.csv
|   |   `-- locations.csv
|   `-- processed/
|       |-- events_clean.csv
|       |-- periods_clean.csv
|       |-- people_clean.csv
|       |-- locations_clean.csv
|       |-- story_eras.csv
|       `-- story_events.csv
|
|-- notebooks/
|   |-- 01_data_validation.ipynb
|   |-- 02_data_cleaning.ipynb
|   `-- 03_exploratory_analysis.ipynb
|
|-- dashboard/
|   `-- app.py
|
|-- README.md
`-- requirements.txt
```

---

## Data Validation Plan

Before building the dashboard, the datasets should be validated.

Validation checks include:

- Check that all IDs are unique
- Check that all `period_id` values in events exist in `data/raw/periods.csv`
- Check that all `person_ids` in events exist in `data/raw/people.csv`
- Check that all `location_ids` in events exist in `data/raw/locations.csv`
- Check that BCE years are stored as negative numbers
- Check that categories are consistent
- Check missing values in important columns
- Check duplicated events

---

## Dashboard Plan

The dashboard will be built around two complementary modes.

### 1. Story Mode

Story Mode is a scrollytelling journey through the major eras of Vietnamese history. It uses `story_eras.csv` to define each scroll section and `story_events.csv` to define the connected sequence of major and supporting events inside each era.

Each era section should include:

- Era title and time range
- Short historical summary
- Connected event sequence with arrows
- Major events and smaller related events
- Key people
- Key locations
- Map view
- Historical certainty/status note

### 2. Explore Mode

Explore Mode is a full interactive dashboard for all events in the dataset.

Suggested views:

- Overview metrics for events, periods, people, and locations
- Interactive timeline with filters
- Map of historical locations
- People and event relationships
- Category and importance score summaries

Explore filters:

- Broad era
- Period
- Category
- Importance score
- Year range
- Person
- Location

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

