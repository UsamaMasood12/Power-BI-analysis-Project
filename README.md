# Power BI Jewelry Store Analytics Dashboard

[![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-yellow)](https://powerbi.microsoft.com/)
[![DAX](https://img.shields.io/badge/DAX-Formulas-orange)](https://docs.microsoft.com/en-us/dax/)
[![Business Intelligence](https://img.shields.io/badge/Business-Intelligence-blue)](https://powerbi.microsoft.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> **MSc Data Science Project** | Teesside University  
> A comprehensive Power BI dashboard for jewelry retail analytics featuring sales performance, inventory management, and customer insights

## 🎯 Project Overview

This project delivers an **interactive business intelligence solution** for a jewelry retail store using Microsoft Power BI. The dashboard provides real-time insights into sales performance, inventory management, customer behavior, and profitability metrics to support data-driven decision-making.

### Key Features
- 📊 **Interactive Dashboard** with drill-down capabilities
- 💰 **Sales Performance Analytics** across multiple dimensions
- 📦 **Inventory Management** tracking and optimization
- 👥 **Customer Segmentation** and behavior analysis
- 📈 **Trend Analysis** with time intelligence
- 🎯 **KPI Tracking** with visual indicators
- 🔄 **Real-time Updates** with data refresh capabilities

---

## 📊 Dashboard Components

### 1. Executive Summary Dashboard
**Purpose:** High-level overview for management decision-making

**Key Metrics:**
- **Total Revenue:** Overall sales performance
- **Total Profit:** Net profitability
- **Profit Margin %:** Profitability ratio
- **Total Orders:** Transaction volume
- **Average Order Value (AOV):** Revenue per transaction
- **Customer Count:** Unique customers

**Visualizations:**
- KPI cards with trend indicators
- Revenue and profit trends (line charts)
- Monthly/quarterly performance comparisons
- Year-over-year growth metrics

### 2. Sales Analytics
**Purpose:** Detailed sales performance analysis

**Key Analyses:**
- **Sales by Category:** Product category performance
- **Sales by Product:** Individual item analysis
- **Sales by Time Period:** Temporal trends (daily, monthly, yearly)
- **Sales by Location:** Geographic performance (if applicable)
- **Sales by Salesperson:** Team performance metrics

**Visualizations:**
- Bar charts for category comparisons
- Pie charts for revenue distribution
- Time series line charts
- Heatmaps for seasonal patterns
- Top/bottom performers tables

### 3. Inventory Management
**Purpose:** Stock optimization and inventory control

**Key Metrics:**
- **Current Stock Levels:** Real-time inventory
- **Stock Value:** Total inventory worth
- **Turnover Rate:** Inventory efficiency
- **Low Stock Alerts:** Reorder notifications
- **Dead Stock:** Slow-moving items
- **Stock-to-Sales Ratio:** Inventory optimization

**Visualizations:**
- Inventory level gauges
- Stock aging analysis
- Reorder point indicators
- Category-wise stock distribution
- Inventory trends over time

### 4. Customer Analytics
**Purpose:** Customer behavior and segmentation insights

**Key Analyses:**
- **Customer Segmentation:** RFM (Recency, Frequency, Monetary) analysis
- **Customer Lifetime Value (CLV):** Long-term customer worth
- **Purchase Patterns:** Buying behavior trends
- **Customer Retention:** Loyalty metrics
- **New vs Returning Customers:** Acquisition vs retention

**Visualizations:**
- Customer distribution charts
- Purchase frequency histograms
- CLV segmentation matrix
- Customer journey maps
- Cohort analysis

### 5. Product Performance
**Purpose:** Product-level insights and optimization

**Key Metrics:**
- **Best Sellers:** Top revenue products
- **Slow Movers:** Underperforming items
- **Product Margins:** Profitability by product
- **Cross-sell Analysis:** Product associations
- **Product Mix:** Category distribution

**Visualizations:**
- Product performance matrix
- Margin vs volume scatter plots
- Product lifecycle analysis
- Category contribution pie charts

---

## 🛠️ Technical Implementation

### Data Sources
```
Data Format: CSV / Excel / SQL Database
Tables:
├── Sales Transactions
├── Products Master
├── Customers Master
├── Inventory Records
├── Categories/Subcategories
└── Date Dimension
```

### Data Model
```
Star Schema Design:
┌─────────────┐
│ Fact: Sales │ (Center)
└─────────────┘
      ↓
Connected to Dimensions:
├── Dim_Products (1:Many)
├── Dim_Customers (1:Many)
├── Dim_Date (1:Many)
├── Dim_Categories (1:Many)
└── Dim_Inventory (1:Many)
```

### DAX Measures Created

#### Revenue Metrics
```dax
Total Revenue = 
SUM(Sales[Sales Amount])

Revenue YTD = 
TOTALYTD([Total Revenue], Date[Date])

Revenue vs Last Year = 
VAR CurrentYearRevenue = [Total Revenue]
VAR LastYearRevenue = 
    CALCULATE(
        [Total Revenue],
        SAMEPERIODLASTYEAR(Date[Date])
    )
RETURN
    CurrentYearRevenue - LastYearRevenue

Revenue Growth % = 
DIVIDE([Revenue vs Last Year], [Total Revenue LY], 0)
```

#### Profitability Metrics
```dax
Total Profit = 
SUMX(
    Sales,
    Sales[Sales Amount] - Sales[Cost]
)

Profit Margin % = 
DIVIDE([Total Profit], [Total Revenue], 0)

Average Profit per Order = 
DIVIDE([Total Profit], [Total Orders], 0)
```

#### Customer Metrics
```dax
Total Customers = 
DISTINCTCOUNT(Sales[Customer ID])

Average Order Value = 
DIVIDE([Total Revenue], [Total Orders], 0)

Customer Retention Rate = 
VAR ReturningCustomers = 
    CALCULATE(
        [Total Customers],
        FILTER(
            Sales,
            Sales[Purchase Count] > 1
        )
    )
RETURN
    DIVIDE(ReturningCustomers, [Total Customers], 0)
```

#### Inventory Metrics
```dax
Current Stock Value = 
SUMX(
    Inventory,
    Inventory[Quantity] * Inventory[Unit Cost]
)

Stock Turnover Ratio = 
DIVIDE(
    [Total Revenue],
    [Average Stock Value],
    0
)

Days of Inventory = 
DIVIDE(
    365,
    [Stock Turnover Ratio],
    0
)
```

#### Time Intelligence
```dax
Sales MTD = 
TOTALMTD([Total Revenue], Date[Date])

Sales QTD = 
TOTALQTD([Total Revenue], Date[Date])

Sales LY = 
CALCULATE(
    [Total Revenue],
    SAMEPERIODLASTYEAR(Date[Date])
)
```

---

## 📈 Key Visualizations

### 1. KPI Cards
- **Purpose:** Quick metric overview
- **Features:** Sparklines, trend indicators, conditional formatting
- **Metrics:** Revenue, Profit, Orders, Customers, AOV

### 2. Line Charts
- **Purpose:** Trend analysis over time
- **Features:** Multiple series, forecasting, drill-down
- **Usage:** Revenue trends, profit trends, customer growth

### 3. Bar/Column Charts
- **Purpose:** Category comparisons
- **Features:** Sorting, filtering, drill-through
- **Usage:** Sales by category, top products, regional performance

### 4. Pie/Donut Charts
- **Purpose:** Composition analysis
- **Features:** Percentage labels, drill-down
- **Usage:** Revenue distribution, category mix, customer segments

### 5. Matrix/Tables
- **Purpose:** Detailed data display
- **Features:** Conditional formatting, hierarchies, subtotals
- **Usage:** Product performance, customer lists, sales details

### 6. Slicers
- **Purpose:** Interactive filtering
- **Types:** 
  - Date range picker
  - Category dropdown
  - Product selector
  - Location filter
  - Salesperson filter

### 7. Maps (if geographic data available)
- **Purpose:** Location-based analysis
- **Features:** Bubble sizes, heat maps, drill-down
- **Usage:** Sales by region, store performance

---

## 🎨 Design Principles

### Color Scheme
```
Primary Colors:
- Revenue/Positive: #0078D4 (Blue)
- Profit: #107C10 (Green)
- Alerts/Negative: #D83B01 (Red)
- Neutral: #737373 (Gray)

Background: White/Light Gray for professional appearance
Accents: Gold/Jewelry-themed colors for branding
```

### Layout
- **Consistent header:** Logo, title, refresh timestamp
- **Logical grouping:** Related visuals clustered together
- **White space:** Adequate spacing for readability
- **Responsive design:** Adapts to different screen sizes
- **Navigation:** Buttons/bookmarks for easy switching

### User Experience
- **Intuitive interactions:** Click, hover, drill-down
- **Clear labels:** Self-explanatory titles and axes
- **Tooltips:** Additional context on hover
- **Filters:** Easy-to-use slicers and filters
- **Performance:** Fast load times and smooth interactions

---

## 📊 Key Insights & Findings

### Sales Performance
- **Peak Seasons:** Identified highest revenue periods (holidays, special occasions)
- **Best-Selling Categories:** Gold jewelry accounts for X% of revenue
- **Revenue Trends:** Year-over-year growth patterns
- **Pricing Analysis:** Optimal price points for maximum profitability

### Inventory Optimization
- **Stock Efficiency:** Turnover rates by category
- **Slow-Moving Items:** Identified for clearance/promotion
- **Reorder Points:** Optimized inventory levels
- **Stock Costs:** Reduced carrying costs by X%

### Customer Behavior
- **Customer Segments:** High-value vs occasional buyers
- **Purchase Patterns:** Seasonal buying behaviors
- **Retention Metrics:** Customer loyalty indicators
- **Cross-sell Opportunities:** Product associations discovered

### Profitability
- **Margin Analysis:** High-margin vs high-volume products
- **Cost Optimization:** Areas for cost reduction identified
- **Pricing Strategy:** Data-driven pricing recommendations

---

## 🚀 Getting Started

### Prerequisites
- **Microsoft Power BI Desktop** (Latest version)
- **Data Source Access** (CSV files or database connection)
- **Refresh Credentials** (if connecting to live data)

### Installation & Setup

#### Step 1: Download Power BI
```
1. Go to https://powerbi.microsoft.com/desktop/
2. Download Power BI Desktop
3. Install and launch application
```

#### Step 2: Open the Dashboard
```
1. Clone this repository:
   git clone https://github.com/UsamaMasood12/Power-BI-analysis-Project.git

2. Open the .pbix file in Power BI Desktop

3. If prompted, update data source connections
```

#### Step 3: Refresh Data
```
1. Click "Refresh" in the Home ribbon
2. Update credentials if necessary
3. Wait for data to load
```

#### Step 4: Explore the Dashboard
```
1. Use slicers to filter data
2. Click on visuals to cross-filter
3. Drill down for detailed insights
4. Export visuals if needed
```

---

## 📁 Project Structure

```
Power-BI-Jewelry-Analytics/
│
├── Jewelry_Store_Dashboard.pbix   # Main Power BI file
├── Jewelry_project_report.pdf     # Project documentation
├── README.md                       # This file
│
├── data/
│   ├── sales_data.csv             # Sales transactions
│   ├── products.csv               # Product master data
│   ├── customers.csv              # Customer information
│   └── inventory.csv              # Stock data
│
├── screenshots/
│   ├── executive_dashboard.png    # Dashboard preview
│   ├── sales_analytics.png        # Sales page
│   ├── inventory_view.png         # Inventory page
│   └── customer_insights.png      # Customer page
│
├── documentation/
│   ├── data_dictionary.md         # Data field descriptions
│   ├── dax_formulas.txt           # DAX measures documentation
│   └── user_guide.pdf             # End-user manual
│
└── templates/
    └── dashboard_template.pbit    # Power BI template
```

---

## 🎓 Academic Context

**Institution:** Teesside University  
**Program:** MSc Data Science  
**Course:** Business Intelligence / Data Visualization  
**Student:** Usama Masood

### Learning Outcomes Demonstrated

**Power BI Skills:**
- Dashboard design and development
- Data modeling (star schema)
- DAX formula creation
- Time intelligence functions
- Interactive visualizations
- Performance optimization

**Business Intelligence:**
- Requirements gathering
- KPI identification
- Metric calculation
- Insight generation
- Stakeholder communication

**Data Analytics:**
- Retail analytics
- Customer segmentation
- Inventory optimization
- Profitability analysis
- Trend forecasting

---

## 📚 Features Implemented

### Advanced Power BI Features

**1. Time Intelligence**
```dax
- Year-to-Date (YTD) calculations
- Month-to-Date (MTD) metrics
- Quarter-over-Quarter comparisons
- Year-over-Year growth rates
- Rolling averages (moving averages)
```

**2. Dynamic Filtering**
- Cross-filtering between visuals
- Synchronized slicers
- Drill-through pages
- Report-level and page-level filters
- Dynamic titles based on selections

**3. Custom Measures**
- Complex DAX calculations
- Conditional formatting rules
- What-if parameters
- Calculated columns
- Measure groups

**4. Data Refresh**
- Scheduled refresh setup
- Incremental refresh configuration
- Query folding optimization
- Data source management

**5. Performance Optimization**
- Optimized data model
- Reduced cardinality
- Aggregations
- DirectQuery vs Import considerations

---

## 🔍 Business Value

### For Store Owners
- **Revenue Optimization:** Identify best-selling products and peak seasons
- **Inventory Control:** Reduce stock-outs and overstock situations
- **Cost Reduction:** Identify slow-moving inventory for clearance
- **Customer Insights:** Understand customer preferences and behavior

### For Store Managers
- **Daily Operations:** Monitor real-time sales and stock levels
- **Staff Performance:** Track salesperson metrics
- **Customer Service:** Identify loyal customers for rewards
- **Planning:** Data-driven decisions for purchasing and promotions

### For Marketing Teams
- **Campaign Effectiveness:** Measure promotion success
- **Customer Segmentation:** Target high-value customers
- **Product Positioning:** Optimize product mix
- **Seasonal Planning:** Plan inventory for peak seasons

---

## 🔮 Future Enhancements

### Planned Features

1. **Predictive Analytics**
   - Sales forecasting using AI
   - Demand prediction for inventory
   - Customer churn prediction
   - Price optimization modeling

2. **Mobile Dashboard**
   - Power BI Mobile app optimization
   - Simplified mobile views
   - Push notifications for alerts
   - Touch-friendly interactions

3. **Advanced Analytics**
   - Market basket analysis
   - Customer lifetime value prediction
   - Sentiment analysis (if review data available)
   - Cohort analysis

4. **Integration**
   - Real-time POS system integration
   - E-commerce platform connection
   - Email marketing system integration
   - CRM system synchronization

5. **AI Features**
   - Power BI AI visuals (Key Influencers, Decomposition Tree)
   - Q&A natural language queries
   - Smart narratives
   - Anomaly detection

---

## 🤝 Contributing

Contributions and suggestions are welcome! Here's how:

### How to Contribute
- 🐛 Report issues or bugs
- 💡 Suggest new visualizations or metrics
- 📝 Improve documentation
- 🔧 Optimize DAX formulas
- 🎨 Enhance dashboard design

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Usama Masood**
- 📧 Email: usamamasood531@gmail.com
- 💼 LinkedIn: [linkedin.com/in/usama-masood-b4a35014b](https://www.linkedin.com/in/usama-masood-b4a35014b)
- 🐙 GitHub: [@UsamaMasood12](https://github.com/UsamaMasood12)

---

## 🙏 Acknowledgments

- **Teesside University** for academic guidance and resources
- **Microsoft Power BI Community** for excellent documentation
- **DAX Patterns** for formula templates and best practices
- **Jewelry Store** for providing real-world business context
- **Power BI User Group** for design inspiration

---

## 📞 Support & Contact

For questions about:
- **Dashboard Functionality:** Review user guide in documentation
- **Data Sources:** Contact via email
- **Custom Implementations:** Available for consultation
- **Training:** Can provide Power BI training sessions

---

## 📊 Project Stats

![Power BI](https://img.shields.io/badge/Power%20BI-100%25-yellow)
![DAX Measures](https://img.shields.io/badge/DAX%20Measures-50%2B-orange)
![Visualizations](https://img.shields.io/badge/Visualizations-25%2B-blue)
![Pages](https://img.shields.io/badge/Dashboard%20Pages-5-green)

---

## 🌟 Key Takeaways

This Power BI project demonstrates:
- ✅ Professional dashboard design principles
- ✅ Advanced DAX formula implementation
- ✅ Business intelligence best practices
- ✅ Real-world retail analytics application
- ✅ Data storytelling and visualization skills
- ✅ Technical proficiency in Microsoft Power BI

---

**⭐ If you find this Power BI dashboard useful, please star the repository!**

---

*Transforming Jewelry Retail Data into Actionable Business Intelligence*
