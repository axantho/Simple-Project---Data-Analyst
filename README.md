# Simple-Project---Data-Analyst
FMCG Industries - Jakarta - Indonesia
SIMPLE PROJECT

===================================
**Project Description: Raw Material Ordering Estimation with Ordering Form Report Generation**
===================================

The Raw Material Ordering Estimation project is designed to optimize the ordering and management of raw materials in a food and beverage operation. The system integrates sales forecasting, buffer stock calculations, yield adjustments, and real-time stock tracking to ensure that raw materials are ordered in the right quantities. In addition to these features, the system includes the capability to generate detailed ordering form reports, streamlining communication with suppliers and ensuring a smooth procurement process.

Key Components:
**Sales Forecasting**: 
The system uses historical sales data to predict future raw material requirements. By analyzing past consumption patterns and accounting for seasonal trends, it generates accurate estimates for ingredient needs in upcoming periods.

**Buffer Stock Calculation**: 
Buffer stock is factored into the order estimation to ensure the business has enough stock to handle unexpected spikes in demand or variations in supply. This safety stock helps prevent stockouts during periods of high demand.

**Yield and Conversion Rates**: 
The system accounts for ingredient yield and conversion rates, such as weight loss during processing (e.g., trimming, cooking losses). This ensures that the correct amount of raw materials is ordered to achieve the required number of servings while minimizing waste.

**Order Adjustment for Special Circumstances**: 
The system provides flexibility to manually adjust the estimates for special situations, such as promotional events, catering orders, or seasonal surges in demand. This customization ensures that the business can accommodate varying needs beyond the standard ordering logic.

**Supplier Coordination**: 
The system generates detailed ordering form reports that can be sent directly to suppliers. These reports include:

 **Ingredient Name and Code**: 
  Clear identification of each item to be ordered.

  **Required Quantity**: 
  The exact amount of each ingredient based on the estimation calculations, including any buffer stock.

  **Unit of Measure (UOM)**: 
  The standard unit of measurement for each ingredient (e.g., kg, liters, pieces).

**Automated Report Generation**: 
Once the raw material quantities have been estimated and adjusted, the system automatically generates an ordering form report in a user-friendly format (e.g., PDF). Ts  provides a comprehensive overview of the raw materials to be ordered, ready for review or direct submission to suppliers.

By incorporating the ordering form report generation, this system not only enhances internal inventory management but also streamlines the procurement process, ensuring that orders are placed accurately and on time. This reduces administrative workload, minimizes errors, and improves communication with suppliers, making the overall raw material ordering process more efficient.

**Benefits**:
Reduced Waste: Accurate ordering and buffer stock calculation minimize waste by ensuring ingredients are ordered in optimal quantities.
Improved Efficiency: The automated report generation reduces manual effort in preparing order forms and eliminates human errors.
Faster Procurement: With detailed and automated order reports, procurement teams can quickly send orders to suppliers, ensuring timely deliveries and stock availability.

By leveraging these features, the Raw Material Ordering Estimation system enhances operational efficiency, cost control, and supplier management, leading to smoother business operations and improved profitability.



===================================
**Project Description: Promotion Manifest**
===================================

The Promotion Manifest is a comprehensive tool designed to track and analyze promotional campaigns over a specific period, providing detailed insights into sales performance and the effectiveness of the promotion. This report is intended for the marketing team to assess the market response to ongoing promotions and determine their impact on overall sales.

**Key Features of the Promotion Manifest**:

**Promo Item Sales Tracking**: The manifest includes a detailed record of the sales for each promotional item, monitored on a weekly basis throughout the promotion period. This allows for a clear understanding of how the promotional items are performing over time.

**Sales Performance Graph (Weekly Sales)**: A graphical representation of the weekly sales data for each promotional item is provided. This helps to visualize trends, identify peak sales periods, and evaluate how sales fluctuate during the promotion.

**Promo Sales to Total Check Ratio**: A graph depicting the percentage of total promotional sales relative to the total check amount is included. This metric helps to assess how much of the total sales value is driven by the promotion, offering insights into the promotion's success in terms of overall customer spending.

**Promo Sales to Total Nett Sales Ratio**: Another key graph shows the percentage of total promotional sales relative to total nett sales. This metric indicates the contribution of the promotional sales to the overall sales performance, helping to determine the direct impact of the promotion on overall revenue.

**Market Response and Effectiveness Evaluation**: The Promotion Manifest serves as a valuable tool for the marketing team to gauge market interest and engagement with the promotion. By analyzing the sales trends, as well as the ratios of promotional sales to total sales, the marketing team can determine the effectiveness of the promotion in driving sales and customer engagement.

The Promotion Manifest allows marketing teams to assess the success of their campaigns, optimize future promotions, and make data-driven decisions to maximize sales performance. By continuously tracking key metrics and visualizing the impact of promotional activities, the team can fine-tune strategies to achieve better market penetration and sales outcomes.

===================================
**IU Non-Food Project**
===================================

The IU Non-Food Project is designed to provide a comparative analysis of non-food item usage in outlets, comparing the quantities and costs of items used in the last month (H-1) versus two months ago (H-2). 

The project will focus on the following key data points for each outlet:

**Item Name**: The name of the non-food item used.
**Item Code**: A unique identifier for the item.
**Category Name**: The specific category to which the item belongs (e.g., cleaning supplies, packaging, etc.).
**UOM (Unit of Measure)**: The measurement unit used for the item (e.g., pieces, liters, etc.).
**Unit Price**: The cost per unit of the item.
**Quantity Used (Qty)**: The total amount of the item consumed by the outlet for the respective month (H-1 and H-2).
**Difference (Selisih)**: The difference in quantity used between H-1 and H-2.
**Price Difference (Selisih Harga)**: The price difference for the item between the two months.

The purpose of this project is to provide the Finance Department with a clear view of the usage trends for non-food items across different outlets. It will highlight any significant increases or decreases in the quantity of non-food items used, as well as any changes in unit prices. This will allow Finance to identify any irrational increases in usage or pricing, serving as a basis for accountability and further investigation by the respective outlets.

In essence, this analysis helps finance teams understand the reason behind fluctuations in non-food item consumption, enabling them to take appropriate actions, such as asking outlets to justify unexpected increases or decreases in their usage. The project ensures better financial oversight and helps improve inventory and procurement management.


===================================
Project: Deviasi Form - All Outlet
===================================

Description:

The Deviasi Form project is designed to streamline the process of monitoring and analyzing deviations in raw material usage and inventory management across all outlets in the organization. The main objective of this project is to create a standardized form that can be used at each outlet to record and analyze discrepancies between the expected (theoretical) stock usage and the actual stock used, ensuring that raw materials are used efficiently and any variances are detected and addressed promptly.

Key features of the Deviasi Form include:

**Data Input and Tracking**:
The form will capture key information related to each outlet, such as menu code, menu name, gramasi (portion size), total sales per portion, total sales x gramasi (total weight sold), yield, and yield value.
Store Request Out (SR Out), Stock Awal (starting stock), Purchases, Store Request In (SR In), Stock Akhir Fisik (actual stock remaining), and Stock Akhir Teoritis (theoretical stock remaining) will also be recorded.

**Deviation Calculation**:
The deviation value will be calculated by comparing the actual stock usage with the theoretical stock usage. The formula for calculating deviation involves comparing the total sales x gramasi against the stock usage as expected based on yield and theoretical values.
A percentage deviation will be computed, showing the variance between the expected and actual stock usage.

**Upper and Lower Limits**:
The system will incorporate upper and lower deviation limits, typically set as 5% of the theoretical stock used, to determine acceptable variance thresholds.
If the actual stock usage exceeds the upper limit, it indicates waste; if it falls below the lower limit, it signals an opportunity for better efficiency.
Deviations falling within the acceptable range are tolerated, while those outside the range trigger corrective actions.

**Outlet-Level Reporting**:
The form will generate reports at the outlet level, allowing each location to track its deviation data and make necessary adjustments to optimize raw material usage.
The data will be collected periodically, helping to identify trends, track performance, and pinpoint areas for improvement at the outlet level.

**Centralized Monitoring**:
All outlet data will be consolidated into a central database or system, allowing for comprehensive monitoring of stock usage across all locations. This will enable the organization to make informed decisions, improve inventory control, reduce waste, and optimize purchasing strategies.


The Deviasi Form project aims to enhance the accuracy and efficiency of inventory management, reduce waste, and improve overall operational performance. By ensuring that raw materials are used within optimal limits, the system will contribute to cost savings and improve the profitability of the organization across all outlets.




