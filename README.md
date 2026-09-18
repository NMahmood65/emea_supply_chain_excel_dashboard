# 📊 EMEA Supply Chain Control Tower (Advanced Excel)

### 🎮 Try the Interactive Dashboard
You can interact with the live Control Tower directly in your browser (no download required):
👉 [**View the Interactive Excel Dashboard Here**](https://1drv.ms/x/c/c497cb947e251d94/IQBYKsmp4FRdTr1axudcmHxKAcSNpC08p9YSZ4zIF_aGIUM?e=p0jD55)

*Alternatively, you can download the raw `.xlsx` file directly from this repository [here](./EMEA_Supply_Chain_Control_Tower.xlsx) to review the backend data modeling and formulas.*

### Project Overview
This project is an end-to-end data pipeline and interactive dashboard built entirely in native Microsoft Excel. It processes over 50,000 rows of messy logistics data to track 3PL carrier SLA performance, identify origin warehouse claim trends, and monitor a €5.6M financial leakage from overbilling. 

By avoiding external BI tools like Tableau or Power BI, this project demonstrates advanced, purely native Excel capabilities—including complex string parsing, dynamic data modeling, and seamless software-style UI design.

### 🛠️ Data Engineering & Cleaning
The raw dataset required significant cleaning before it could be modeled. All transformations were handled natively without Power Query to showcase advanced formula writing:
* **Duplicate Resolution:** Identified and removed approximately 4,000 duplicate shipment records, resulting in a clean dataset of 46,078 unique rows.
* **Complex Date Parsing:** The raw extract contained severely mixed regional date formats (EU `DD/MM/YYYY` vs. US `MM-DD-YYYY`). I engineered a nested parsing function to bypass Excel's regional text limitations and standardize the timeline:
  ```excel
  =IF(ISNUMBER(B2), B2, DATE(RIGHT(B2, 4), LEFT(B2, 2), MID(B2, 4, 2)))
  ```
* **Helper Columns:** Generated binary flags (1/0) for On-Time Delivery and Claims to enable rapid, lightweight PivotTable aggregation without complex DAX.

### ⚙️ Data Modeling & Interactivity
* **Dynamic Aggregation:** Built a robust reporting layer utilizing interconnected Pivot Tables that summarize millions of euros in freight spend and discrepancy data.
* **Report Connections:** Wired a custom `Carrier_3PL` Slicer to four independent PivotTables using Report Connections, allowing one-click, global dashboard filtering.
* **Date Grouping:** Aggregated daily transactional data into a clean 12-month fiscal view to track seasonal overbilling trends.

### 📈 Dashboard Interface & Visuals
The frontend was designed to mimic a standalone web application, utilizing strict formatting rules (hidden gridlines, white-out data matrices, stripped Slicer borders) for a clean UI.
* **Executive KPI Cards:** High-contrast banners tracking Total Shipments, Claim Rate, Financial Leakage, and On-Time Rate.
* **SLA Performance:** A targeted bar chart visualizing carrier reliability (e.g., highlighting sub-40% on-time rates for key partners).
* **Overbilling Trend Analysis:** An area chart tracking the monthly volume of invoice discrepancies across the fiscal year.
* **Warehouse Claims Distribution:** A stacked column chart breaking down failure types (Shortage, Lost Freight, Damaged in Transit) across five major origin facilities.

### 💡 Business Value
This Control Tower enables supply chain executives to:
1. **Recoup Lost Revenue:** Pinpoint the exact months and carriers driving a €5.6M overbilling leakage to initiate financial audits.
2. **Hold Carriers Accountable:** Use hard data to negotiate better rates or enforce SLA penalties based on severe on-time delivery failures.
3. **Optimize Warehouse Operations:** Identify which specific origin distribution centers are driving the highest rates of damaged and lost freight.

### 🔗 Related Projects: SQL & Tableau Version
This repository demonstrates how to build a robust data pipeline and dashboard using strictly **native Advanced Excel**. 

I have also tackled EMEA supply chain optimization using an enterprise tech stack. To see how I handled similar logistics data using **SQL for data engineering** and **Tableau for visualization**, check out my other repository here: 
👉 [EMEA Supply Chain Optimisation](https://github.com/NMahmood65/emea_supply_chain_optimisation/blob/main/README.md)
