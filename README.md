![Downtown Winnipeg - Portage Place construction, January 2026](visuals/header.png)

# Downtown Winnipeg Transition Analysis

**Troy Dela Rosa** | Independent academic project, Python Essentials With Data Analysis (COMP-2040), RRC Polytech | April 2026, revised November 2026

![Python](https://img.shields.io/badge/python-3670A0?style=flat-square&logo=python&logoColor=ffdd54)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat-square&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=flat-square&logo=Matplotlib&logoColor=black)

> **Revised November 2026.** The first version of this project claimed more than its data could support. This README separates what the sources show from what I estimated or assumed. See [What changed](#what-changed-in-this-revision).

## Question

Is downtown Winnipeg in decline, or is it partway through a shift from office and retail toward housing and mixed use?

**Short answer:** the public sources show a large building program next to high office vacancy. They cannot show whether street-level business is recovering, because no public dataset I found measures it.

## What the sources show

These figures come from published sources listed in the [source registry](data/downtown_wpg_sources_2026.csv).

| Measure | Figure | Source and limits |
|---|---|---|
| Office vacancy | 8.7% (2016) to 18.6% (2025) | CBRE reports. 6 of 10 years are published figures; 2017, 2018, 2020 and 2021 are interpolated. |
| Vacancy vs. Canada, 2025 | Winnipeg 18.6%, national 18.0% | CBRE Q4 2025 |
| Named capital projects since 2008 | About $2.36B across 12 projects | Press releases and news reports. $189M of this is my estimate for three projects with no published cost. |
| ...already completed | About $1.21B | For example True North Square and the Canadian Museum for Human Rights |
| ...under construction or planned | About $1.15B | Mostly Portage Place ($650M) and the former Bay building ($310M) |
| Housing units, named projects | 1,381 to 1,539 | 7 projects in [`housing_pipeline_2026.csv`](data/housing_pipeline_2026.csv) |
| ...already built | 584 to 592 | 225 Carlton and 300 Main |
| ...under construction or planned | 797 to 947 | Completion windows run to 2028 |

### Office vacancy more than doubled, and the rise has slowed

![Office vacancy rates: Winnipeg vs. the national average, 2016-2025](visuals/fig_vacancy.png)

Vacancy went from 8.7% in 2016 to 18.3% in 2023, then rose only 0.3 points over the next two years.

### The projects cluster along Portage Avenue

![Map of construction and development projects across downtown Winnipeg](visuals/fig_spatial.png)

Most of the large projects sit along Portage Avenue between the former Bay building and True North Square. Much of the work is conversion of existing buildings, not new towers. The map uses 32 hand-compiled project and event records with coordinates.

### Most of the new housing is not finished yet

![Residential pipeline by project and status](visuals/fig_residential.png)

About 590 units are built. The larger share, 797 to 947 units, depends on projects finishing between now and 2028. That timing is the main open question for downtown.

## What the sources cannot show

**Street-level business activity.** I could not find a public count of open shops, restaurants or offices downtown over time.

- The City of Winnipeg business licence data does not cover it. The City licenses only a short list of activities (rooming houses, used goods dealers and similar), so a shop or restaurant never appears in that file. I found this later in my [Winnipeg Business Licence Data Governance](https://github.com/rynetroy/winnipeg-licence-governance) project.
- The first version of this project filled the gap with a **synthetic series** for 2010 to 2024 ([`Winnipeg_Synthetic_License_Model_2010_2024.xlsx`](data/Winnipeg_Synthetic_License_Model_2010_2024.xlsx)). Those numbers were written to match a storyline, not collected. The earlier claims that retail is "down about 63% from 2013" and that "restaurants are recovering" came from that file, and I have withdrawn them.

The file and its chart (`visuals/fig_business_activity.png`) stay in the repo for transparency. They are not evidence.

## Scenario sketch (my judgment, not a measurement)

To compare "what if projects finish on time" against "what if they stall", I built a 0 to 100 index called the Downtown Health Score. It is a thinking tool. Most of its inputs are numbers I chose.

| Component | Weight | Score | How it was set |
|---|---:|---:|---|
| Residential demand | 25% | 92 | Partly calculated from housing units; the scaling and a population input of 65 are my choices |
| Investment pipeline | 25% | 78 | My judgment |
| Business stability | 25% | 42 | My judgment, informed by the withdrawn synthetic series |
| Spatial anchoring | 15% | 72 | My judgment |
| Vacancy and distress | 10% penalty | 8 of 10 | My judgment |

| Scenario | Score |
|---|---:|
| Projects delivered on time | ~72 |
| Today | 63 |
| 2+ year delay | ~44 |
| Pipeline stalls | ~34 |

What this is good for: showing that the outlook swings mostly on whether the housing and mixed-use projects get finished. With equal weights the baseline is 55.2, in the same band.

What it is not: a measurement, a forecast, or an official city metric. Different judgment scores would give different numbers.

## What I would take from this

- The housing still to come (797 to 947 units) is the thing to watch. Tracking completions and occupancy would say more than any index.
- Office vacancy near 18% looks like the new normal, close to the national rate, not a temporary dip.
- Anyone who wants to measure street-level recovery needs a better source than licence data, such as a storefront survey or business improvement zone counts.

## What changed in this revision

| First version (April 2026) | Now |
|---|---|
| "Retail down ~63% from 2013" | Withdrawn. Based on a synthetic series. |
| "Restaurants are recovering, retail is not" | Withdrawn. Same reason. |
| "$2B+ redevelopment pipeline" | About $2.36B in named projects since 2008, of which about $1.21B is already complete |
| "1,635 to 1,793 new apartments confirmed or proposed" | 1,381 to 1,539 in named projects. The earlier figure counted two projects twice. |
| Health score presented as a finding | Presented as a scenario sketch built on my own judgment scores |

The notebook text and some chart labels still carry the April wording. Where they disagree with this README, this README is correct.

## Data

| File | What it is | Type |
|---|---|---|
| `downtown_wpg_sources_2026.csv` | 53 sources with links and the figures taken from each | Compiled by hand |
| `winnipeg_downtown_projects_2026.csv` | 32 projects and events with dates and coordinates | Compiled by hand from sources |
| `housing_pipeline_2026.csv` | 7 named housing projects with unit ranges and status | Compiled by hand from sources |
| `downtown_wpg_gantt_sourced_2026.csv` | Project timeline records | Compiled by hand from sources |
| `Business_Licenses_20260404.csv` | City of Winnipeg open data export, April 4, 2026 | Real, but does not cover retail or restaurants |
| `Winnipeg_Synthetic_License_Model_2010_2024.xlsx` | Invented business activity series | Synthetic, not used for findings |

## How it was built

- **Notebook:** [`notebooks/downtown_winnipeg_transition_analysis.ipynb`](notebooks/downtown_winnipeg_transition_analysis.ipynb) covers loading, cleaning, eight charts and the scenario index. A shorter version is in [`notebooks/stakeholder_report.ipynb`](notebooks/stakeholder_report.ipynb).
- **Helper module:** [`src/helpers.py`](src/helpers.py) holds the cleaning and plotting functions.
- **Tools:** Python 3.11+, pandas, matplotlib, seaborn, scikit-learn.
- **Course requirement:** Section 8 fits a decision tree to the 7 housing projects to show a scikit-learn workflow. With 3 test rows its accuracy (0.33) means nothing, and no conclusion uses it.

**To run:** open the main notebook and run all cells.

*Personal academic project on public sources. Not affiliated with or endorsed by the City of Winnipeg.*
