# **FIFA 21 Messy, Raw Dataset for Cleaning/Exploring**

## Acknowledgements

The data for this project is from [click 🆓](https://www.kaggle.com/datasets/yagunnersya/fifa-21-messy-raw-dataset-for-cleaning-exploring/data). All thanks to [Rachit Toshniwal](https://www.kaggle.com/yagunnersya) who scrapped this data from [sofifa](www.sofifa.com)

## Inspiration
### **🔹 Data Cleaning & Wrangling Tasks for FIFA 21 Dataset**
Based on the dataset structure, the following **data cleaning and wrangling** tasks can be performed:

#### **1️⃣ Handling Missing Data**
- **Column `Loan Date End` has many missing values** → Fill with `"Not on Loan"` or drop the column.
- **Column `Hits` has missing values** → Fill missing values with `"0"` or the median.

#### **2️⃣ Removing Unnecessary Columns**
- Columns like **`photoUrl`**, **`playerUrl`**, and **`\n\n\n\n` artifacts in `Club`** may not be useful for numerical analysis.
- Remove redundant columns like **LongName** (similar to **Name**).
- Rename all columns and replace spaces with underscores to encourage usability and to avoid syntax error due to naming convention.

#### **3️⃣ Fixing Data Types**
- **Convert `Value`, `Wage`, `Release Clause` from string to numeric** (e.g., `€110.5M` → `110500000`).
- **Convert `Height` and `Weight` into numerical values**:
  - `"5'7"` → Convert to **cm** (e.g., `170 cm`)
  - `"176lbs"` → Convert to **kg** (e.g., `80 kg`).
- **Columns `W/F`, `SM`, `IR` contain special characters (`★`)** → Convert them to integers.

#### **4️⃣ Standardizing Text Formatting**
- Strip **extra spaces and newlines** from categorical columns (`Club`, `Nationality`, etc.).
- Convert **all string-based categories to lowercase** for consistency (`Preferred Foot`, `Best Position`).

#### **5️⃣ Handling Outliers**
- **Check extreme values in numerical features** (`PAC`, `SHO`, `PAS`, etc.).
- Detect outliers using **Interquartile Range (IQR)** and **Z-score**.

#### **6️⃣ Feature Engineering**
- **Extract contract length** from `Contract` (e.g., `"2025"` → `Years remaining`).
- **Create a new feature `Market Value per OVA`**:
  ```python
  df["Market Value per OVA"] = df["Value"] / df["↓OVA"]
  ```
- **Group Players by Age Categories**:
  ```python
  df["Age Group"] = pd.cut(df["Age"], bins=[15, 20, 25, 30, 35, 40], labels=["Teen", "Young", "Prime", "Veteran", "Old"])
  ```
---

## 📌 Table of Abbreviated Features

Here’s a breakdown of abbreviations in the dataset:

| **Abbreviation** | **Full Meaning** |
|-----------------|-----------------|
| **OVA** | Overall Rating |
| **POT** | Potential Rating |
| **BOV** | Best Overall Rating |
| **W/F** | Weak Foot (1-5 Stars) |
| **SM** | Skill Moves (1-5 Stars) |
| **A/W** | Attacking Work Rate (Low, Medium, High) |
| **D/W** | Defensive Work Rate (Low, Medium, High) |
| **IR** | International Reputation (1-5 Stars) |
| **PAC** | Pace (Acceleration + Sprint Speed) |
| **SHO** | Shooting (Finishing, Long Shots, etc.) |
| **PAS** | Passing (Short & Long Passing, Vision) |
| **DRI** | Dribbling (Ball Control, Agility, Balance) |
| **DEF** | Defense (Marking, Tackling) |
| **PHY** | Physicality (Strength, Stamina, Jumping) |
