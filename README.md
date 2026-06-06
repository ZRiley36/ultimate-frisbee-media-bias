# Ultimate Frisbee Media Bias

A regression + classification study of whether Cal Poly's men's ultimate frisbee team (Slocore) was underreported in 2023 D-I coverage on Ultiworld. Co-authored with Calahan Lackovic for Data 301 at Cal Poly.

**Spoiler:** they weren't. Cal Poly had **63 more mentions than their rank predicted**.

## Stack

Python · Selenium · pandas · scikit-learn · TF-IDF · K-Nearest Neighbors · Jupyter

## What we did

**1. Built a Selenium scraper for Ultiworld.** Site requires auth, so the scraper handles the login flow before pulling each article. ~30 minutes runtime for 169 articles.

**2. Collected 169 D-I men's articles + USAU rankings + full rosters** for the top 20 teams. Manually cleaned to 163 relevant articles. Built a moniker dictionary for every plausible team mention — acronyms, school names, player names — to disambiguate counts. (UNC-Wilmington kept matching as "UNC" until we hard-coded it out.)

**3. Regressed total team mentions on rank and on power rating.** Residuals above the line are the bias signal: teams over-mentioned relative to their on-field strength.

**4. Trained a TF-IDF + K-Nearest-Neighbors classifier** to predict article author from text alone. Hyper-parameter tuning across k = 1..20.

## Findings

- **Cal Poly was over-mentioned by ~63 articles** relative to what their rank predicted. The "we're being ignored" Slocore narrative was wrong.
- **One author drives most of it.** Jake Thorne (Cal Poly alum, Slocore alum) accounted for 154 of the Cal Poly mentions. A single writer dominated the team's coverage.
- **UNC dominated overall.** They were ranked #1 for most of the season, so other teams' articles repeatedly used them as a comparison benchmark, inflating their mention count beyond what their rank alone would explain.
- **The author classifier didn't work.** Best K-NN model hit ~40% accuracy, and that's misleading — it just predicted Keith Raynor (38% of all articles) for 142 of 169 cases. K-NN over TF-IDF wasn't expressive enough; the task wanted learned representations, not nearest-neighbor lookup.

## Limitations

- One season, one outlet (Ultiworld). No generalization claim beyond 2023 D-I men's coverage.
- Single-outlet selection bias — Ultiworld readers are the most engaged subset of fans.
- Mention counts aren't sentiment. An over-mentioned team isn't necessarily positively covered.

## Notebooks

- `notebooks/01_web_scraping.ipynb` — Selenium login flow + article scrape
- `notebooks/02_webscraping_rosters.ipynb` — USAU rankings + rosters
- `notebooks/03_data_analysis.ipynb` — regression + mention counts
- `notebooks/04_tfidf_cosine_distances.ipynb` — TF-IDF + K-NN author prediction

## Data

- `data/articles.csv` — 163 cleaned articles
- `data/team_rankings.csv` — top 20 D-I men's teams: rank, power rating, region
- `data/rosters.csv` — full rosters for each ranked team
- `data/team_mentions.csv` — mention counts per team per article

## Docs

- `docs/proposal.md` — original research proposal (Oct 2023)
- `docs/executive_summary.md` — methodology + findings write-up

## Run it

```bash
git clone https://github.com/ZRiley36/ultimate-frisbee-media-bias.git
cd ultimate-frisbee-media-bias
pip install -r requirements.txt
jupyter notebook
```

The data CSVs are already in `data/`, so analysis notebooks run without re-scraping. To re-scrape, you'll need a personal Ultiworld login.
