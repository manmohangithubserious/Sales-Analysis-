import zipfile
import os

# Define the file path
zip_file_path = "/mnt/data/1717583705_sales_datasets (5).zip"
extract_folder = "/mnt/data/extracted_sales_data"

# Extract the ZIP file
with zipfile.ZipFile(zip_file_path, 'r') as zip_ref:
    zip_ref.extractall(extract_folder)

# List the extracted files
extracted_files = os.listdir(extract_folder)
extracted_files
import pandas as pd

# Define the CSV file path
csv_file_path = os.path.join(extract_folder, "AusApparalSales4thQrt2020.csv")

# Load the CSV file into a DataFrame
df = pd.read_csv(csv_file_path)

# Display basic information and the first few rows
df.info(), df.head()

# The dataset contains 7,560 sales records with the following columns:

Date: The transaction date.
Time: The time of the transaction (e.g., Morning, Afternoon, Evening).
State: The Australian state where the sale occurred.
Group: Customer group (Kids, Men, Women, Seniors).
Unit: Number of units sold.
Sales: Total revenue from the sale.

# Now, I'll analyze the total sales by state to identify the highest-revenue states and suggest strategies for lower-performing states.

# Aggregate total sales by state
state_sales = df.groupby("State")["Sales"].sum().reset_index()

# Sort by sales in descending order
state_sales = state_sales.sort_values(by="Sales", ascending=False)

# Display the top states by revenue
state_sales

# Here are the total sales by state for the fourth quarter of 2020:

VIC (Victoria) - $105,565,000 (Highest revenue)
NSW (New South Wales) - $74,970,000
SA (South Australia) - $58,857,500
QLD (Queensland) - $33,417,500
TAS (Tasmania) - $22,760,000
NT (Northern Territory) - $22,580,000
WA (Western Australia) - $22,152,500 (Lowest revenue)
Key Insights:
Victoria (VIC) and New South Wales (NSW) are the top-performing states, contributing the highest revenue.
Western Australia (WA), Northern Territory (NT), and Tasmania (TAS) are among the lowest-performing states.
Now, I'll analyze sales by customer group in these lower-revenue states to identify potential areas for improvement. ​

# Filter data for lower-performing states (WA, NT, TAS)
low_revenue_states = ["WA", "NT", "TAS"]
low_state_sales = df[df["State"].isin(low_revenue_states)]

# Aggregate sales by state and customer group
low_state_group_sales = low_state_sales.groupby(["State", "Group"])["Sales"].sum().reset_index()

# Sort for better readability
low_state_group_sales = low_state_group_sales.sort_values(by=["State", "Sales"], ascending=[True, False])

# Display the results
low_state_group_sales

# Filter data for lower-performing states (WA, NT, TAS)
low_revenue_states = ["WA", "NT", "TAS"]
low_state_sales = df[df["State"].isin(low_revenue_states)]

# Aggregate sales by state and customer group
low_state_group_sales = low_state_sales.groupby(["State", "Group"])["Sales"].sum().reset_index()

# Sort for better readability
low_state_group_sales = low_state_group_sales.sort_values(by=["State", "Sales"], ascending=[True, False])

# Display the results
low_state_group_sales

#It looks like there might be an issue with filtering the lower-revenue states. Let me verify the state names in the dataset to ensure accuracy before proceeding with further analysis
It looks like there might be an issue with filtering the lower-revenue states. Let me verify the state names in the dataset to ensure accuracy before proceeding with further analysis
It looks like there might be an issue with filtering the lower-revenue states. Let me verify the state names in the dataset to ensure accuracy before proceeding with further analysis
# Sales Breakdown by Customer Group in Lower-Revenue States:
Northern Territory (NT)
Men: $5,762,500 (Highest)
Kids: $5,700,000
Women: $5,652,500
Seniors: $5,465,000 (Lowest)
Tasmania (TAS)
Kids: $5,775,000 (Highest)
Men: $5,757,500
Seniors: $5,650,000
Women: $5,577,500 (Lowest)
Western Australia (WA)
Men: $5,752,500 (Highest)
Kids: $5,625,000
Seniors: $5,512,500
Women: $5,262,500 (Lowest)
Insights & Recommendations
Target Women’s Segment for Growth:

In WA, TAS, and NT, the Women’s category generates the lowest sales.
Strategy: Run promotional campaigns, introduce new product lines, and optimize inventory for this category.
Expand Kids’ Apparel Marketing in NT & WA:

Kids' sales in NT & WA are slightly lower than other groups.
Strategy: Partner with schools, offer back-to-school discounts, and create bundled offers.
Boost Senior Segment Sales in NT & WA:

Seniors' sales are the lowest in NT & WA.
Strategy: Introduce senior citizen discounts and tailor marketing efforts toward comfort-based apparel.

import matplotlib.pyplot as plt
import seaborn as sns

# Set style
sns.set_style("whitegrid")

# Create a bar plot for sales by customer group in lower-revenue states
plt.figure(figsize=(12, 6))
sns.barplot(data=low_state_group_sales, x="State", y="Sales", hue="Group", palette="coolwarm")

# Labels and title
plt.title("Sales by Customer Group in Low-Revenue States", fontsize=14)
plt.xlabel("State", fontsize=12)
plt.ylabel("Total Sales ($)", fontsize=12)
plt.legend(title="Customer Group")

# Show plot
plt.show()

# Re-import necessary libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Define the new file path
csv_file_path = "/mnt/data/AusApparalSales4thQrt2020.csv"

# Load the CSV file into a DataFrame
df = pd.read_csv(csv_file_path)

# Strip spaces from state names (if any)
df["State"] = df["State"].str.strip()

# Define lower-revenue states
low_revenue_states = ["WA", "NT", "TAS"]

# Filter data for lower-revenue states
low_state_sales = df[df["State"].isin(low_revenue_states)]

# Aggregate sales by state and customer group
low_state_group_sales = low_state_sales.groupby(["State", "Group"])["Sales"].sum().reset_index()

# Sort for better readability
low_state_group_sales = low_state_group_sales.sort_values(by=["State", "Sales"], ascending=[True, False])

# Set style
sns.set_style("whitegrid")

# Create a bar plot for sales by customer group in lower-revenue states
plt.figure(figsize=(12, 6))
sns.barplot(data=low_state_group_sales, x="State", y="Sales", hue="Group", palette="coolwarm")

# Labels and title
plt.title("Sales by Customer Group in Low-Revenue States", fontsize=14)
plt.xlabel("State", fontsize=12)
plt.ylabel("Total Sales ($)", fontsize=12)
plt.legend(title="Customer Group")

# Show plot
plt.show()

# Re-import necessary libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Define the new file path
csv_file_path = "/mnt/data/AusApparalSales4thQrt2020.csv"

# Load the CSV file into a DataFrame
df = pd.read_csv(csv_file_path)

# Strip spaces from state names (if any)
df["State"] = df["State"].str.strip()

# Define lower-revenue states
low_revenue_states = ["WA", "NT", "TAS"]

# Filter data for lower-revenue states
low_state_sales = df[df["State"].isin(low_revenue_states)]

# Aggregate sales by state and customer group
low_state_group_sales = low_state_sales.groupby(["State", "Group"])["Sales"].sum().reset_index()

# Sort for better readability
low_state_group_sales = low_state_group_sales.sort_values(by=["State", "Sales"], ascending=[True, False])

# Set style
sns.set_style("whitegrid")

# Create a bar plot for sales by customer group in lower-revenue states
plt.figure(figsize=(12, 6))
sns.barplot(data=low_state_group_sales, x="State", y="Sales", hue="Group", palette="coolwarm")

# Labels and title
plt.title("Sales by Customer Group in Low-Revenue States", fontsize=14)
plt.xlabel("State", fontsize=12)
plt.ylabel("Total Sales ($)", fontsize=12)
plt.legend(title="Customer Group")

# Show plot
plt.show()

Key Takeaways from the Visualization:
Men’s and Kids' segments generate the highest sales in NT and TAS.
Women’s segment has the lowest sales across all three states.
WA has the lowest overall sales, with Women’s and Seniors' categories lagging behind.
Strategic Recommendations:
✅ Boost Women’s Apparel Sales: Run targeted marketing campaigns, introduce loyalty discounts, and expand fashion choices.
✅ Senior Citizen Promotions: Offer special discounts, promote comfort-focused apparel, and explore partnership deals with community centers.
✅ Expand Kids’ Apparel in WA: Promote schoolwear bundles, seasonal discounts, and influencer-driven campaigns.



