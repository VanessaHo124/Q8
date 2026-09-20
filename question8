from futures_data_downloader import FuturesDataDownloader
import pandas as pd
import matplotlib.pyplot as plt

# Initialize downloader
downloader = FuturesDataDownloader()

# Download continuous futures data
cl = downloader.download_contract_data(
    "CL=F",
    start_date="2020-01-01",
    end_date="2026-01-01",
    fallback_to_continuous=False
)

rb = downloader.download_contract_data(
    "RB=F",
    start_date="2020-01-01",
    end_date="2026-01-01",
    fallback_to_continuous=False
)

ho = downloader.download_contract_data(
    "HO=F",
    start_date="2020-01-01",
    end_date="2026-01-01",
    fallback_to_continuous=False
)

# Keep only Date and Close
cl = cl[["Date", "Close"]].rename(columns={"Close": "CL"})
rb = rb[["Date", "Close"]].rename(columns={"Close": "RB"})
ho = ho[["Date", "Close"]].rename(columns={"Close": "HO"})

# Merge the three series by date
df = cl.merge(rb, on="Date").merge(ho, on="Date")

# Calculate crack spread
df["Crack_Spread"] = 3 * df["CL"] - 2 * df["RB"] - df["HO"]

# Plot
plt.figure(figsize=(12, 5))
plt.plot(df["Date"], df["Crack_Spread"])

plt.xlabel("Date")
plt.ylabel("Crack Spread")
plt.title("3-2-1 Crack Spread")

plt.show()
