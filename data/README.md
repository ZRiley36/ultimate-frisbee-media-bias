# Data

All data scraped from public sources between November and December 2023 for a Cal Poly Data 301 final project. Stored as flat CSVs for reproducibility.

| File | Source | Description |
|---|---|---|
| `articles.csv` | [Ultiworld](https://ultiworld.com/division/usau-college-d-i-mens) | 163 men's D-I articles (cleaned from 169 scraped). Columns: title, author, date, text. |
| `team_rankings.csv` | [USA Ultimate](https://play.usaultimate.org/) | Top 20 D-I men's teams. Columns: rank, name, power rating, region, conference. |
| `rosters.csv` | USA Ultimate | Player rosters for each ranked team. Columns: team, player name. |
| `team_mentions.csv` | Derived | Per-team mention count per article, computed using the moniker dictionary in `03_data_analysis.ipynb`. |

## Re-scraping

If you want to regenerate `articles.csv`: notebook `01_web_scraping.ipynb` handles login + scrape against your Ultiworld account. Takes ~30 minutes. Rate-limited by Selenium driver waits, not API limits.
