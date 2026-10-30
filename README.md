🏠 Global Airbnb Performance Dashboard

An interactive Power BI dashboard that analyzes Airbnb's growth, market share, pricing, guest ratings, review behavior and host trust across 10 major global cities.

## 📌 Business Problem

Airbnb operates in cities with very different levels of demand, pricing, regulation and guest satisfaction. Stakeholders need one view that answers:

- **Where should Airbnb focus its growth, regulation or marketing efforts?**
- **Where is Airbnb doing well, and where is it failing customers?**

## 🎯 Questions the Dashboard Answers

| Area | Key Questions |
|---|---|
| **Big Picture** | How big is Airbnb across major cities? How has it grown over time and where did it peak? Are listings concentrated or evenly spread? |
| **Market Share by City** | Which cities dominate listings? Are a few cities driving most of the supply? What is the cumulative contribution of Paris, NYC and Sydney? |
| **Property Type & Pricing** | Which property types are most listed? Are hotel rooms more expensive than Airbnb stays? Does pricing explain higher adoption in cities like Paris? |
| **Ratings & Satisfaction** | Which cities deliver the best guest experience? Are low ratings driven by cleanliness, value or communication? |
| **Reviews & Trust** | Do reviews come from new or repeat guests? Which months are busiest per city? How many hosts are verified? |

## 📊 Dashboard Overview

The report has 3 pages:

1. **Overview**: headline KPIs and the Airbnb lifecycle from 2008 to 2021
2. **Market, Pricing & Ratings**: city market share (Pareto), average price by room type, and a ratings heatmap
3. **Reviews & Trust**: review frequency, seasonality and host verification

### Headline KPIs
| Metric | Value |
|---|---|
| Listings | 2,79,712 |
| Cities | 10 |
| Hosts | 1,82,024 |
| Property Types | 144 |
| Reviews | 5,373K |

## 🔍 Key Insights

- **Growth story:** New listings peaked in **2015**, slowed in 2016–2017 due to stricter local regulations, resumed in 2018 and were halted by COVID-19 in 2019.
- **Concentration:** **Paris, New York and Sydney** make up almost half of all listings (48.4% cumulative) and about **48% of total reviews**. Paris has the most listings and reviews.
- **Pricing:** Average price is highest for **Hotel rooms ($800)**, then Entire place ($673), Shared room ($580) and Private room ($462). Higher hotel prices may help explain Airbnb's pull in cities like Paris.
- **Ratings:** **Mexico City** scores highest across most rating categories. **Hong Kong** is weakest on cleanliness and value (8.99), and Istanbul is low on cleanliness (9.05).
- **Review behavior:** **86%** of reviewers wrote only one review and 98.6% wrote three or fewer, so volume comes mostly from new guests. One reviewer with 283 reviews is an outlier worth validating.
- **Trust:** **66.9%** of hosts are verified with a profile picture. Only 0.3% are unverified with no picture, so anonymous profiles are minimal.

## 🛠️ Project Steps

### 1. Data Loading & Understanding
- Imported the Airbnb dataset into Power BI Desktop (`[dataset source / link]`).
- Worked with a **Listings** table (city, district, neighbourhood, room type, bedrooms, accommodates, latitude/longitude, minimum and maximum nights, instant bookable, host details) and a **Reviews** table (review ID, reviewer ID, listing ID, date).

### 2. Data Cleaning & Transformation (Power Query)
- Checked data types, null values and duplicates (`[add what you actually fixed]`).
- Created date helper fields: **Review Month**, **Month Number** and **Month Short** (Jan, Feb, ...), sorted by month number so the seasonality chart shows months in calendar order.

### 3. Data Modelling
- Connected the Listings and Reviews tables through `listing_id` (`[confirm your relationship setup]`).
- Set correct data types, summarization and sort-by-column settings.

### 4. DAX Measures & Calculated Columns
Built a measure layer for KPIs, ratings, host verification, Pareto and review analysis. Full list in the section below.

### 5. Visualization & Storytelling
- Designed three pages in a consistent Airbnb-style theme (red, grey and green).
- Added a short insight text beside each visual so every chart ends with a business takeaway.
- Added buttons and bookmarks, including the "Select the detail level" switch between Overall and Detailed ratings.
- Used conditional formatting on the ratings table to make strong and weak cities stand out.

### 6. Review & Validation
- Cross-checked measure totals against the source data.
- Flagged outliers such as the 283-review reviewer.

## 📐 DAX Measures Created

### Listings & Host KPIs
| Measure | Purpose |
|---|---|
| `Total Listing` | Total number of listings |
| `Hosts Total` | Distinct number of hosts |
| `Superhost Listings` | Listings owned by Superhosts |
| `Non Superhost Listing` | Listings owned by non-Superhosts |
| `Entire Place`, `Hotel Room`, `Shared Room` | Listings by room type for the lifecycle chart |
| `Avg Price` | Average price, used for the room-type price comparison |

### Market Share & Pareto Analysis
| Measure | Purpose |
|---|---|
| `City Rank` | Ranks cities by listings |
| `Cumulative Listings` | Running total of listings across ranked cities |
| `Cumulative %` | Running share of total listings, for the Pareto line |

### Ratings
| Measure | Purpose |
|---|---|
| `Avg Rating` | Overall average rating |
| `Accuracy`, `Cleanliness`, `Communication`, `Location`, `Values` | Average score per rating category for the city heatmap |

### Host Trust & Verification
| Measure | Purpose |
|---|---|
| `Verified`, `Verified %` | Verified hosts and their share |
| `Verified_Noprofile`, `Verified_Noprofile %` | Verified hosts with no profile picture |
| `Notverified_profile` | Unverified hosts with a profile picture |
| `Notverified_Noprofile`, `Notverified_Noprofile %` | Unverified hosts with no profile picture |

These drive the four circles in the Trust shield.

### Reviews & Seasonality
| Measure | Purpose |
|---|---|
| `Total Reviews` | Total review count |
| `Reviewers`, `Total Reviewers` | Distinct number of reviewers |
| `% of Monthly Reviews` | Each city's share of reviews per month, for the ribbon chart |
| `% of Total Reviewers` | Share of reviewers in each review-count bucket |
| `Cumulative Reviewers` | Running total of reviewers |
| `Cummulative % reviewers` | Running share, for the Review Frequency Pareto line |

### Calculated Columns / Helper Fields
| Field | Purpose |
|---|---|
| `Month Number` | Numeric month (1–12) for sorting |
| `Review Month` | Month extracted from the review date |
| `Month Short` | Short month name (Jan, Feb, ...) for chart axes |
| `Reviews per Reviewer` | Number of reviews each reviewer wrote |
| `Show in Review Frequency` | Limits the review frequency chart to the buckets shown |

### Techniques Used
- Pareto analysis with cumulative percentages
- Ribbon chart for seasonal ranking
- Conditional formatting heatmap
- Sort-by-column for month order
- Bookmarks and buttons for a detail-level toggle
- Insight text boxes for data storytelling

## 🧰 Tools Used

- Power BI Desktop
- DAX
- Power Query
- Excel / CSV (`[data format]`)

## 📁 Repository Structure

```
├── Airbnb_Dashboard.pbix
├── screenshots/
│   ├── 1_overview.png
│   ├── 2_market_pricing_ratings.png
│   └── 3_reviews_trust.png
├── data/            (optional)
└── README.md
```

## 🖼️ Dashboard Screenshots

1) Overview
   
   <img width="1416" height="738" alt="image" src="https://github.com/user-attachments/assets/0453f9bf-0d57-4828-aaaf-0488f8683b32" />
   
3) Market, Pricing and Ratings
   
   <img width="1116" height="756" alt="image" src="https://github.com/user-attachments/assets/414a9bab-a80c-4902-be6d-7fb59c8457ff" />
   
5) Reviews and Trust
   
   <img width="1266" height="747" alt="image" src="https://github.com/user-attachments/assets/8342bcf0-22d9-4b41-bae4-d2b2f71b0e46" />

## 💡 Recommendations

- Focus growth and marketing on the top cities, but diversify to reduce dependence on Paris, New York and Sydney.
- Work with hosts in Hong Kong and Istanbul to improve cleanliness and value ratings.
- Encourage repeat bookings, since most reviews come from first-time guests.
- Keep investing in host verification to protect trust.

## 👤 Author

**Dhanush Raju**
[LinkedIn](https://linkedin.com/in/dhanushrajuu) | [GitHub](https://github.com/dhanush-20045)
