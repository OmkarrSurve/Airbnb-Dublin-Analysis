# 🏡 Airbnb Dublin — Market Analysis

> Identifying demand-supply gaps to help the city manager boost host quality and quantity in Dublin.

---

## 📌 Project Overview

This project is a full exploratory data analysis (EDA) of Airbnb's Dublin market. The goal is to understand **what guests are searching for** and **which inquiries hosts tend to accept** — and more importantly, where the gaps between the two lie.

The findings are intended to help a newly appointed Airbnb city manager in Dublin make data-driven decisions about host recruitment, onboarding, and platform strategy.

---

## 🎯 Business Questions

- What are guests searching for in Dublin? (room type, duration, timing, origin)
- Which inquiries do hosts accept — and which do they reject?
- Where are the biggest gaps between guest demand and host supply?
- What can the city manager do to increase the number and quality of bookings?

---

## 📂 Dataset

The dataset contains two files sourced from Kaggle's Airbnb Dublin dataset:

### `searches.tsv`
One row per search set made by a user for Dublin listings.

| Column | Description |
|--------|-------------|
| `ds` | Date of the search |
| `id_user` | Alphanumeric user ID |
| `ds_checkin` | Check-in date of the search |
| `ds_checkout` | Check-out date of the search |
| `n_searches` | Number of searches in the search set |
| `n_nights` | Number of nights searched for |
| `n_guests_min` | Minimum number of guests selected |
| `n_guests_max` | Maximum number of guests selected |
| `origin_country` | Country the search was made from |
| `filter_price_min` | Lower bound of price filter (if used) |
| `filter_price_max` | Upper bound of price filter (if used) |
| `filter_room_types` | Room types filtered by (if used) |
| `filter_neighborhoods` | Neighbourhoods filtered by (if used) |

### `contacts.tsv`
One row per guest inquiry made for a Dublin listing.

| Column | Description |
|--------|-------------|
| `id_guest` | Alphanumeric guest user ID |
| `id_host` | Alphanumeric host user ID |
| `id_listing` | Listing identifier |
| `ts_contact_at` | Timestamp of the inquiry |
| `ts_reply_at` | Timestamp of host reply (if replied) |
| `ts_accepted_at` | Timestamp of acceptance (if accepted) |
| `ts_booking_at` | Timestamp of booking (if booked) |
| `ds_checkin` | Check-in date of the inquiry |
| `ds_checkout` | Check-out date of the inquiry |
| `n_guests` | Number of guests in the inquiry |
| `n_messages` | Total messages exchanged around the inquiry |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3.12 | Core language |
| Pandas | Data loading, cleaning, transformation |
| NumPy | Numerical operations |
| Matplotlib | Chart rendering |
| Seaborn | Heatmap and styled visualizations |
| Kaggle Notebooks | Development environment |

---

## 📊 Analysis Performed

### 1. Data Preparation
- Parsed all date and timestamp columns into `datetime64` format
- Derived new columns: `checkin_dow`, `checkin_month`, `lead_time`, `n_nights`
- Created boolean funnel flags: `replied`, `accepted`, `booked`
- Cleaned `filter_room_types` column — split combined values, standardised casing, exploded multi-value rows
- Binned stay duration into 9 buckets for comparison across datasets

### 2. Guest–Host Conversion Funnel
- Measured drop-off at each stage: Inquiry → Reply → Accepted → Booked
- Found that **acceptance rate (46%)** is the primary bottleneck — not reply rate (92%)
- Only **27.8%** of all inquiries result in a confirmed booking

### 3. Check-in Day of Week
- Compared the distribution of search check-in days vs accepted check-in days
- Annotated demand–supply gap (Δ) per day of week

### 4. Trip Duration Analysis
- Compared stay length distribution between searches and accepted contacts
- Identified **single-night stays** as consistently underserved

### 5. Room Type Demand
- Cleaned and exploded multi-value room type filter column
- Visualised top room types guests filter for
- **Entire home/apt** dominates demand at ~39%

### 6. Acceptance Rate by Group Size
- Calculated acceptance rate per guest count
- Larger groups (5+) face lower acceptance rates — supply of large listings is limited

### 7. Monthly Seasonality
- Plotted monthly demand vs accepted supply
- Overlaid acceptance rate as a line chart on a twin axis
- **October** shows a major demand spike — driven by the Dublin Marathon and events calendar

### 8. Origin Countries & Lead Time
- **Ireland, US, and GB** are the top 3 source markets
- Median search lead time is **26 days** before check-in
- Significant last-minute demand exists (within 7 days)

### 9. Host Response Behaviour
- Compared response time distributions for accepted vs not-accepted inquiries
- Response speed alone does not determine acceptance outcome
- Median messages per inquiry: **4**

### 10. Demand–Supply Gap Heatmap
- Built a month × stay-duration matrix
- Normalised both demand and supply shares then subtracted to find the gap
- **June with 6–7 night stays** shows the clearest underserved demand pocket

---

## 💡 Key Findings

| # | Finding | Implication |
|---|---------|-------------|
| 1 | 46% acceptance rate is the main funnel bottleneck | Focus on host quality, not just quantity |
| 2 | Single-night stays are underserved | Encourage hosts to lower minimum night settings |
| 3 | October demand spikes significantly | Recruit event-ready hosts ahead of peak season |
| 4 | Summer 6–7 night stays are underserved | Target medium-stay hosts for summer |
| 5 | Entire home/apt is the most demanded room type | Prioritise whole-property host acquisition |
| 6 | Large groups (5+) face lower acceptance | Recruit multi-bedroom property hosts |
| 7 | Ireland, US, GB are top source markets | Focus marketing and partnerships accordingly |

---

## 📁 Repository Structure

```
airbnb-dublin-analysis/
│
├── data/
│   ├── searches.tsv          # Guest search data
│   └── contacts.tsv          # Guest inquiry and host response data
│
├── analysis.py               # Full analysis and chart generation script
├── README.md                 # Project documentation
```

---

## 🚀 How to Run

### On Kaggle (Recommended)
1. Go to [kaggle.com](https://kaggle.com) and create a new notebook
2. Upload `searches.tsv` and `contacts.tsv` via **Add Data → Upload**
3. Copy the contents of `analysis.py` into notebook cells
4. Run all cells top to bottom

### Locally
```bash
# Clone the repo
git clone https://github.com/yourusername/airbnb-dublin-analysis.git
cd airbnb-dublin-analysis

# Install dependencies
pip install pandas numpy matplotlib seaborn

# Run the analysis
python analysis.py
```

---

## 📈 Sample Outputs

| Chart | Insight |
|-------|---------|
| Conversion Funnel | 92% reply rate but only 46% acceptance |
| Day of Week | Fairly even demand across weekdays |
| Trip Duration | 2–3 night stays dominate; 1-night underserved |
| Room Type | Entire home/apt is ~39% of filtered demand |
| Monthly | October peaks due to events; supply doesn't follow |
| Countries | Ireland #1, US #2, GB #3 source markets |
| Response Time | Fast response doesn't guarantee acceptance |
| Heatmap | June 6–7 night stays are the clearest gap |

---


## 📄 License

This project is open source and available under the [MIT License](LICENSE).
