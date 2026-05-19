# Consumption Monitor

A Power BI report for tracking SaaS consumption, budget utilization, and spend trends across enterprise business units.

---

## Report Pages

### 1. Consumption Monitor (Main Dashboard)

The primary page contains 18 visuals organized into four zones:

| Visual | Type | Description |
|--------|------|-------------|
| Last Refresh | Card | Timestamp of the latest data refresh |
| Active BUs | Card | Count of distinct Business Units |
| Service | Card | Current SaaS service being viewed |
| Instance | Card | Instance identifier |
| Application Filter | Slicer | Filter by application name |
| Date Filter | Slicer | Filter by Year / Month |
| Cumulative Spend | Line Chart | YTD Consumption over time with forecast band |
| Usage Trend | Line Chart | Quantity usage over time with forecast band |
| Usage vs Budget | Pie Chart (ZoomCharts) | Visual comparison of actual usage against budget |
| Service Type | Pivot Table | Usage quantity broken down by service |
| BU Budget Breakdown | Pivot Table | Per-BU: budget, utilization %, burn rate, consumption ratio |
| BU Usage by Month | Pivot Table | Per-BU and instance, usage quantity by year and month |

### 2. Page 1 (Detail / Drill-Through)

Secondary page used for BU-level budget drill-through with additional slicers and pivot breakdowns.

---

## Data Model

### Tables & Columns

#### `usages`
| Column | Description |
|--------|-------------|
| `usage_date` | Date of usage record |
| `quantity` | Raw usage quantity |
| `service` | SaaS service name |

#### `budgets`
| Column | Description |
|--------|-------------|
| `bu_id` | Business Unit identifier |
| `bu_name` | Business Unit display name |
| `budget` | Allocated budget amount |
| `budget_current` | Current period budget |
| `validity_start_date` | Budget period start date |

#### `applications`
| Column | Description |
|--------|-------------|
| `name` | Application / SaaS tool name |

#### `instance`
| Column | Description |
|--------|-------------|
| `instance_id` | Unique instance identifier |
| `instance_name` | Instance display name |

#### `LastRefresh`
| Column | Description |
|--------|-------------|
| `LastRefresh` | Timestamp of the most recent data refresh |

---

### Measures

#### Consumption Measures (in `usages`)

| Measure | Description |
|---------|-------------|
| `YTD Consumption` | Year-to-date cumulative usage |
| `forecastValue` | Forecasted future usage |
| `confidenceHighBound` | Upper confidence bound for the forecast |
| `confidenceLowBound` | Lower confidence bound for the forecast |

#### Budget Measures (in `budgets`)

| Measure | Description |
|---------|-------------|
| `Utilization` | Absolute spend consumed against budget |
| `% Utilization by Budget Year Column` | Utilization as a percentage of the annual budget |
| `%Budget` | Budget consumed percentage |
| `Consumption Ratio` | Ratio of actual consumption to budget |
| `Burn Rate` | Rate at which budget is being consumed |

---

## Custom Visuals

| Visual | Source |
|--------|--------|
| ZoomCharts Pie Chart (Paid) | [ZoomCharts](https://zoomcharts.com) — interactive drill-down pie for Usage vs Budget |
| Radar Chart | AppSource built-in radar chart |

---

## Data Source

This report connects to a **Power BI Service cloud dataset** (live connection — no local data embedded).

| Property | Value |
|----------|-------|
| Dataset ID | `<your-dataset-id>` |
| Report ID | `<your-report-id>` |
| Workspace ID | `<your-workspace-id>` |
| Created From | Power BI Cloud (Release 2025.08) |

> **Note:** To refresh data locally in Power BI Desktop, you must have access to the upstream cloud dataset and appropriate credentials. Replace the placeholder IDs above with your own workspace values after forking.

---

## Prerequisites

- [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (August 2025 release or later recommended)
- Access to the cloud workspace/dataset listed above
- ZoomCharts Pie Chart visual (installed automatically from AppSource on first open)

---

## Getting Started

```bash
# Clone the repo
git clone https://github.com/<your-username>/consumption-monitor.git
cd consumption-monitor
```

1. Open `Consumption Monitor.pbix` in Power BI Desktop
2. When prompted, sign in with your organizational account that has access to the dataset
3. Click **Refresh** to load the latest data
4. Use the **Application** and **Date** slicers to filter to your area of interest

---

## Publishing to Power BI Service

```
Home → Publish → Select workspace → Confirm
```

After publishing, pin visuals to a dashboard or set up a scheduled refresh via the Power BI Service settings.

---

## Repository Structure

```
consumption-monitor/
├── Consumption Monitor.pbix   # Power BI report file
├── README.md                  # This file
└── .gitignore
```

---

## License

MIT License — see [LICENSE](LICENSE) for details.
