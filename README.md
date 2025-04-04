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

## 🚀 Getting Started

1. **Install required libraries in R:**

```r
install.packages(c("shiny", "shinydashboard", "plotly", "leaflet", "dplyr"))

# Load necessary packages
library(shiny)
library(shinydashboard)
library(plotly)
library(leaflet)
library(dplyr)

# Sample data
departments <- data.frame(
  Department = c("DOE", "VA", "EPA", "DHS", "HUD"),
  Layoffs = c(22000, 18000, 12000, 9000, 7000)
)

map_data <- data.frame(
  Region = c("Washington, D.C.", "San Antonio, TX", "Denver, CO", "Atlanta, GA", "San Diego, CA"),
  Lat = c(38.89511, 29.42412, 39.7392, 33.749, 32.7157),
  Lon = c(-77.03637, -98.49363, -104.9903, -84.388, -117.1611),
  Layoffs = c(25000, 12000, 9000, 8000, 7000)
)

private_sector <- data.frame(
  Sector = c("Healthcare", "Cybersecurity", "Logistics", "Education", "Tech Support"),
  Demand = c(35000, 30000, 28000, 26000, 25000)
)

ui <- dashboardPage(
  dashboardHeader(title = "Federal Workforce Fallout"),
  dashboardSidebar(
    sidebarMenu(
      menuItem("Overview", tabName = "overview", icon = icon("dashboard")),
      menuItem("Layoffs by Department", tabName = "departments", icon = icon("building")),
      menuItem("Geographic Impact Map", tabName = "map", icon = icon("globe")),
      menuItem("Private Sector Demand", tabName = "private", icon = icon("industry")),
      menuItem("Layoff Scenarios", tabName = "scenarios", icon = icon("sliders-h"))
    )
  ),
  dashboardBody(
    tabItems(
      tabItem(tabName = "overview",
              fluidRow(
                valueBox(75000, "Total Layoffs", icon = icon("users"), color = "red"),
                valueBox("6.5%", "Potential Unemployment Spike", icon = icon("chart-line"), color = "orange"),
                valueBox("Healthcare & Tech", "Top Absorbing Sectors", icon = icon("hospital"), color = "blue")
              ),
              fluidRow(
                box(title = "Overview Summary", status = "primary", solidHeader = TRUE, width = 12,
                    "This dashboard explores the projected impact of mass federal layoffs due to DOGE policy shifts. It simulates ripple effects across departments, geographic areas, and private sector industries.")
              )
      ),
      tabItem(tabName = "departments",
              fluidRow(
                box(title = "Layoffs by Department", width = 12, status = "warning", solidHeader = TRUE,
                    plotlyOutput("layoffsPlot"))
              )
      ),
      tabItem(tabName = "map",
              fluidRow(
                box(title = "Regions Most Affected", width = 12, status = "success", solidHeader = TRUE,
                    leafletOutput("layoffMap", height = 500))
              )
      ),
      tabItem(tabName = "private",
              fluidRow(
                box(title = "Projected Private Sector Demand", width = 12, status = "info", solidHeader = TRUE,
                    plotlyOutput("privatePlot"))
              )
      ),
      tabItem(tabName = "scenarios",
              fluidRow(
                box(title = "Simulate Layoffs", width = 12, status = "danger", solidHeader = TRUE,
                    sliderInput("layoffSlider", "Number of Layoffs:", min = 0, max = 150000, value = 75000, step = 5000),
                    textOutput("unemploymentText"))
              )
      )
    )
  )
)

server <- function(input, output) {
  output$layoffsPlot <- renderPlotly({
    plot_ly(departments, x = ~Department, y = ~Layoffs, type = 'bar', text = ~Layoffs,
            marker = list(color = 'rgb(255,99,71)')) %>%
      layout(title = "Estimated Layoffs by Department",
             xaxis = list(title = "Department"),
             yaxis = list(title = "Number of Layoffs"))
  })
  
  output$layoffMap <- renderLeaflet({
    leaflet(map_data) %>%
      addTiles() %>%
      addCircleMarkers(
        ~Lon, ~Lat,
        label = ~paste0(Region, ": ", Layoffs, " layoffs"),
        radius = ~Layoffs / 5000,
        color = "red", fillOpacity = 0.7
      ) %>%
      addLegend("bottomright", colors = "red", labels = "Layoffs", title = "Regional Impact")
  })
  
  output$privatePlot <- renderPlotly({
    plot_ly(private_sector, x = ~Sector, y = ~Demand, type = 'bar', text = ~Demand,
            marker = list(color = 'rgb(100,149,237)')) %>%
      layout(title = "Private Sector Demand Surge",
             xaxis = list(title = "Sector"),
             yaxis = list(title = "Projected New Openings"))
  })
  
  output$unemploymentText <- renderText({
    base_rate <- 5.0
    layoffs <- input$layoffSlider
    added_rate <- layoffs * 0.00002
    total_rate <- base_rate + added_rate
    paste("Projected national unemployment rate with", layoffs, "layoffs: ", round(total_rate, 2), "%")
  })
}

shinyApp(ui, server)

## 💡 Why This Matters

> 🧠 **Federal employees often accept lower pay in exchange for long-term security and benefits.**
>
> 💼 Their sudden transition into the private workforce alters **salary expectations, skill demands**, and **industry readiness**.

This project explores whether **non-federal employees may also need to adopt new mindsets** around job security, adaptability, and compensation as a result.

This app is more than numbers — it’s about **resilience in workforce ecosystems**.

---

