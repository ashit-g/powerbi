# Power BI Fraud Analytics Dashboard 📊

An interactive Power BI report for exploring credit-card transactions and identifying fraudulent activity. The project contains the report definition, semantic model, reusable DAX queries, calculated measures, and supporting report resources in Power BI Project (`.pbip`) format.

![Fraud analytics dashboard preview](https://github.com/user-attachments/assets/271ff2c5-a738-4593-81d7-64ccd754a980)

## Overview

This dashboard analyzes transaction-level fraud data and helps users investigate risk by:

- Tracking total transactions, fraud cases, fraud-related losses, and merchants involved
- Analyzing activity by transaction date and time, including the derived transaction hour
- Exploring fraud by merchant, category, age group, location, and other customer attributes
- Filtering and comparing transactions using a configurable amount threshold
- Highlighting higher-risk transactions using amount, fraud-label, and nighttime activity signals

> **Note:** This repository contains the Power BI project files and model definitions. The source `fraudTrain.csv` file is not included in the repository.

## Project contents

```text
.
├── ccfd.pbip                         # Power BI Project entry point
├── ccfd.Report/                      # Report definition and visuals
│   ├── definition/
│   └── StaticResources/
├── ccfd.SemanticModel/               # Semantic model and DAX/M queries
│   ├── definition/
│   └── DAXQueries/
└── .gitignore
```

### Main model components

- **`fraudTrain`** — imported transaction table containing transaction, merchant, customer, geography, amount, timestamp, and fraud-label fields.
- **`Amount`** — What-if parameter ranging from 0 to 29,000 in increments of 1,000, used as a configurable risk threshold.
- **`Option`** — field parameter for switching analysis between age group, merchant, and category.
- **Date relationships** — transaction timestamp and date of birth are connected to Power BI local date tables.
- **Report resources** — includes the report theme and dashboard background image.

## Key measures and calculations

The semantic model includes measures such as:

- `Total transactions`
- `Fraud Case Count`
- `FraudCount`
- `Amount lost to frauds`
- `Merchants Involved`
- `Population Involved`
- `Risk Count`
- `Current Age`
- `Threshold Amount`

The model also derives:

- **Hour** from `trans_date_trans_time`
- **Age Group** using the following bands: Under 25, 25–35, 36–50, 51–65, and Over 65
- **Risk Score** using transaction amount, the fraud label, and nighttime activity between 22:00 and 05:00

## Requirements

- [Power BI Desktop](https://powerbi.microsoft.com/desktop/)
- Access to a compatible `fraudTrain.csv` dataset
- Permission to access the local folder or data source where the CSV is stored

## Getting started

1. Clone this repository:

   ```bash
   git clone https://github.com/ashit-g/powerbi.git
   cd powerbi
   ```

2. Open `ccfd.pbip` in Power BI Desktop.

3. When prompted, update the `fraudTrain` Power Query source to point to your local copy of `fraudTrain.csv`.

   The current model contains a local file reference, so the original path will not work on another machine without being changed.

4. Refresh the model.

5. Review the report page and use the available filters, field selector, and amount threshold to explore the data.

## Data fields

The model is designed around fields including:

- **Transaction:** `trans_date_trans_time`, `trans_num`, `amt`, `is_fraud`, `unix_time`
- **Card and merchant:** `cc_num`, `merchant`, `category`
- **Customer:** `first`, `last`, `gender`, `dob`, `job`
- **Location:** `street`, `city`, `state`, `zip`, `lat`, `long`, `city_pop`
- **Merchant location:** `merch_lat`, `merch_long`

Avoid publishing or sharing real payment-card numbers or personally identifiable information when using this project with non-public data.

## Working with the project

Power BI Project source files are stored as text-based report and semantic-model definitions. This makes it possible to review changes to:

- Report pages and visual configurations
- Power Query source steps
- DAX measures and calculated columns
- Relationships and model metadata
- Themes and static resources

After making changes in Power BI Desktop, save the project and review the resulting file changes before committing them. Local Power BI cache and settings files are excluded through `.gitignore`.

## Limitations

- The source dataset is not included in this repository.
- The current Power Query definition references a machine-specific local Windows path and must be updated before refresh on another computer.
- The repository does not currently include a published Power BI Service workspace link or deployment configuration.
- No open-source license is currently declared; add a license if you intend to permit reuse.

## Contributing

1. Create a feature branch.
2. Make and test your changes in Power BI Desktop.
3. Confirm that the report refreshes successfully with a valid data source.
4. Review generated project-file changes for secrets, local paths, and sensitive data.
5. Open a pull request describing the model or report changes.

## License

No license has been specified for this repository. Unless a license is added, all rights remain with the repository owner.

## Repository

[ashit-g/powerbi](https://github.com/ashit-g/powerbi)
