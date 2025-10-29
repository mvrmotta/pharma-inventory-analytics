# Project Charter  
**Title**: Inventory Optimization and Stockout Reduction for Pharmaceutical Operations

## 1. Business Problem
Pharmaceutical businesses rely on the availability of critical consumables and medications. Frequent **stockouts** lead to delays in patient care and operational inefficiencies, while **excess stock and expired products** generate financial losses and waste. Purchasing decisions are often made with limited visibility and low predictability.

## 2. Project Objective
Develop a data-driven system to **monitor, forecast, and optimize inventory levels**, enabling better decision-making for procurement, reducing stockouts, and minimizing financial waste from overstock and product expiration.

## 3. Scope
 In Scope:  
- Pharmaceutical consumables and medications  
- 1–2 operational locations  
- 12 months of historical simulated data  
- ETL pipelines and relational database  
- Inventory KPIs and dashboards  
- Basic demand forecasting and reorder policies  

 Out of Scope (initial version):  
- Complex traceability of controlled substances  
- Financial contract negotiation with suppliers  
- Multi-warehouse logistics automation  

## 4. Stakeholders
- Operations Manager  
- Procurement Team  
- Pharmacists / Healthcare Staff  
- End Customers / Patients

## 5. Deliverables
- **Relational database** (PostgreSQL) with historical records  
- **Python ETL** processes for automated data loading  
- **Power BI Dashboard** with key operational indicators  
- **Demand forecasting model** for high-impact items  
- **Reorder policies and scenario simulation** for decision support  
- **Executive business report**, focused on financial impact  

## 6. Expected Benefits
- ↓ Stockouts → better service quality and operational continuity  
- ↓ Inventory waste → reduced financial losses  
- ↑ Predictability → improved purchasing strategies  
- ↑ Visibility → decisions guided by data, not guesswork  

## 7. Success Metrics (KPIs)
- Stockout Rate  
- Inventory Turnover  
- Days of Inventory on Hand (DOH)  
- Fill Rate  
- Value of Expiring Inventory  
- Forecast Accuracy (MAPE)

---

## Project Roadmap

| Phase | Focus | Outputs |
|------|------|---------|
| Phase 1 | Foundation | Charter, data model, initial schema |
| Phase 2 | Data Integration | Python ETL + simulated datasets |
| Phase 3 | Insights | Power BI dashboard + KPIs |
| Phase 4 | Decision Support | Forecasting + reorder policy simulation |
| Phase 5 | Business Impact | Report with financial/value results |

---

## Notes  
All data used will be **simulated** to protect sensitive healthcare information.  
The project will be fully documented and versioned to ensure reproducibility.

