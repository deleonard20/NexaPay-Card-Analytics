# data/raw

Place the two source CSVs here to run the notebook locally:

- `card.csv` — card-level table (see `../../02_data_discovery/data_dictionary.md`)
- `user.csv` — cardholder-level table

These files are **not tracked** in git (see `.gitignore`) because the dataset is synthetic and generated for portfolio demonstration. In the notebook they are loaded from Google Drive via `gdown`; to run offline, download them into this folder and adjust the read paths to `data/raw/card.csv` and `data/raw/user.csv`.
