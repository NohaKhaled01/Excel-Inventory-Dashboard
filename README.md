# Excel-Inventory-Dashboard
An Excel Store Inventory Dashboard Mini Project

Original store sales data was created by Claude AI
  Claude model: Opus 4.8, Max effort

### Dataset Columns:
  Transaction ID - Date - Time - Shift - Transaction Type [Restock/Sale/Return] - Branch ID - Branch Name - 
  City - Country - Employee ID - Employee Name - Product SKU - Category - Product Name - Color -
  Size - Quantity - Unit Cost - Unit Retail Price

### Project Goal:
Create an inventory sheet that can be used by business owners and employees easily.
  - Allow owner to see how the store is performing at a glance
  - Allow easy data entry, and automatic data updating
  - Limit human error through data validation [dropdown lists/rejected negative values]

## Design Points:

### Star Schema Model:
Star Center Table: Transactions
Star Corner Tables: Employees - Locations - Products

#### Center Table Details:
Transactions Columns: Transaction ID - Date - Time - Shift - Transaction Type - Branch ID - Employee ID - SKU - 
Quantity - Unit Cost - Unit Retail Price - Date(Year) - Date(Quarter) - Date(Month Index) - Date(Month)

#### Corner Tables Details:
Employees Columns: Shift - Branch ID - Employee ID - Employee Name
Locations Columns: Branch ID - Branch Name - City - Country
Products Columns: SKU - Category - Product Name - Color - Size

### Inventory Calculation:
Inventory calculated automatically from the transactions ledger [Units Received - Units Sold + Units Returned]
Units Received/Sold/Returned calculated using DAX formula, filtering on the transaction type

### Product Prices:
The original dataset contains different prices for the same products, based on the store branches.
The transaction ledger stores the selling price of products sold in each transaction, to be able to compute historical revenue if needed, especially in cases of price changes later on.

### Data Validation:
Dropdown lists used for columns:
  Branch ID - Employee ID - Product SKU
    Based on values already in the dataset [existing employee IDs/branch IDs/etc]
  Transaction Type
    Three fixed values; Restock/Sale/Return

Employees are assumed to be working at fixed branches at fixed shifts; branch ID and shifts get computed automatically using XLOOKUP from employee sheet when employee ID is input
Product unit costs and retail prices are computed automatically using XLOOKUP with a 'product SKU + Branch' key

### Ease of Use:
Employees/Sheet users log transactions into the main ledger, and the dashboard and inventory gets automatically updated
Columns input by users:
  Transaction Type - Employee ID - SKU - Quantity
Number of columns edited or logged into by users was kept to a minimal, to minimize human errors as much as possible
Charts in dashboard are slice-able by store branch, product category, and date
Inventory is slice-able by store branch, product category, product name, product color, and product size

### Project Structure
├── Store_Inventory_RawData.xlsx              ← Raw dataset created by Claude AI
├── Store_Inventory_Dashboard.xlsx            ← Excel Dashboard created from dataset
      Sheets inside dashboard file:
        ├── Inventory_Log [hidden]             ← Raw dataset
        ├── PriceList [hidden]                 ← Price list sheet for products, containing 'product SKU + Branch' key
                                                      -- Used later to compute product unit costs and retail prices in the ledger
        ├── Ledger                             ← Transactions Sheet
        ├── Employees                          ← Employees Sheet
        ├── Locations                          ← Store Branch Locations Sheet
        ├── Products                           ← Products Sheet
        ├── Pivot [hidden]                     ← Pivot tables sheet. Tables used for dashboard
        ├── Dashboard                          ← Dashboard Sheet
        ├── Inventory                          ← Inventory Sheet
        
        
        
        
        




  
