## **HealthCare provider Power BI – DAX Measures**


🧮 **Total Aggregations**


Total Billing Amount = 
    [Total Medication Amount] +
    [Total Insurance coverage] +
    [Total Room Charges]

Total Insurance coverage = 
    SUM(visits[Insurance Coverage])

Total Medication Amount = 
    SUM(visits[Medication Cost])

Total Treatment Cost = 
    SUM(visits[Treatment Cost])

Total Room Charges = 
    SUMX(
        visits,
        visits[Room Charges(daily rate)] * visits[Lenght of Stay]
    )

Total Patient = 
    DISTINCTCOUNT(visits[Patient ID])


---

💵 **Derived Financial Metrics**

Out of Pocket = 
    [Total Billing Amount] - [Total Insurance coverage]

Average Out of Pocket = 
    DIVIDE(
        [Out of Pocket],
        [Total Patient]
    )

Average Billing Amount per visit = 
    DIVIDE(
        [Total Billing Amount],
        [Total Patient]
    )

Average Treatment Cost = 
    -AVERAGE(visits[Treatment Cost])  -- Note: Negative sign used, confirm if intentional

Average Insurance Coverage = 
    AVERAGE(visits[Insurance Coverage])

Average Medication Cost = 
    AVERAGE(visits[Medication Cost])

Average Room Charges = 
    AVERAGEX(
        visits,
        visits[Room Charges(daily rate)] * visits[Lenght of Stay]
    )

---

🧍 Patient and Visit Statistics

Average Patient Score = 
    AVERAGE(visits[Patient Satisfaction Score])

Average Lenght of Stay = 
    AVERAGE(visits[Lenght of Stay])

---

📊 Percentage Metrics (Relative Contributions)

% Procedure = 
    DIVIDE(
        [Total Billing Amount],
        CALCULATE(
            [Total Billing Amount],
            ALL(procedures[Procedure])
        )
    )

% Department = 
    DIVIDE(
        [Total Billing Amount],
        CALCULATE(
            [Total Billing Amount],
            ALL(departments[Department])
        )
    )

---


📌 Slicer/Selection Helper Measures

Active Department = 
    SELECTEDVALUE(departments[Department])

---

🧪 Other Measures

Blank Measure = 0

---
