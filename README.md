# 📉 Federal Workforce Fallout: Visualizing the Impact of DOGE Layoffs

> **A Shiny App Case Study on How Massive Federal Layoffs Could Reshape the U.S. Labor Market**  
> *By [Maurice McDonald] — Data Analyst, Policy Enthusiast, and Veteran Advocate*

# 💼 Federal Workforce Fallout: A Shiny App Case Study

This case study explores the **economic shockwaves** caused by the Department of Government Efficiency (DOGE)'s decision to lay off tens of thousands of federal employees. This interactive Shiny app lets users explore the **impact by department, region, and industry**, and simulates how the private sector might respond to absorb the displaced workforce.

---

## 📌 Table of Contents
- [🔍 Project Summary](#project-summary)
- [📊 App Features](#app-features)
- [💡 Why This Matters](#why-this-matters)
- [🚀 Getting Started](#getting-started)
- [💻 Full Shiny App Code](#full-shiny-app-code)
- [📌 Conclusion](#conclusion)

---

## 🔍 Project Summary

In response to DOGE’s sweeping cost-cutting initiatives, more than **75,000 federal employees** are facing layoffs. These roles, typically lower-salaried but benefit-rich, span from departments like **Veterans Affairs (VA)** to **Housing and Urban Development (HUD)**.

This case study addresses:

- Which **federal departments** are most affected?
- Which **U.S. cities** bear the brunt?
- How might the **private sector** respond?
- What if this expands to **100K+ layoffs**?

The interactive dashboard provides **data-driven answers** to these questions — visually and intuitively.

---

## 📊 App Features

### ✅ **Overview Dashboard**
- Instant snapshot of total layoffs, unemployment projections, and impacted sectors.

### 🏢 **Layoffs by Department**
- Interactive bar chart showing estimated cuts by agency (DOE, VA, EPA, etc.).

### 🌍 **Geographic Impact Map**
- Clickable Leaflet map of affected cities like D.C., Denver, Atlanta, San Diego.

### 🏭 **Private Sector Demand**
- Predictive bar chart estimating increased demand in Healthcare, Cybersecurity, and Tech.

### 📈 **Scenario Simulator**
- Use a slider to simulate how unemployment scales with rising layoffs.

---

## 💡 Why This Matters

> 🧠 **Federal employees often accept lower pay in exchange for long-term security and benefits.**
>
> 💼 Their sudden transition into the private workforce alters **salary expectations, skill demands**, and **industry readiness**.

This project explores whether **non-federal employees may also need to adopt new mindsets** around job security, adaptability, and compensation as a result.

This app is more than numbers — it’s about **resilience in workforce ecosystems**.

---

## 🚀 Getting Started

1. **Install required libraries in R:**

```r
install.packages(c("shiny", "shinydashboard", "plotly", "leaflet", "dplyr"))
