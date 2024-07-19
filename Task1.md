# week-7
#Task 1

import os
import glob
from datetime import datetime

# Define the data lake container and folder paths
data_lake_container = 'mydatalakecontainer'
cust_mstr_folder = 'CUST_MSTR'
master_child_folder = 'master_child'
h_ecom_order_folder = 'H_ECOM_ORDER'

# Define the table names
cust_mstr_table = 'CUST_MSTR'
master_child_table = 'master_child'
h_ecom_order_table = 'H_ECOM_Orders'

# Get the list of files in the data lake container
files = glob.glob(f'abfss://{data_lake_container}/*.csv')

# Loop through each file and process accordingly
for file in files:
    filename = os.path.basename(file)
    
    # Process CUST_MSTR files
    if filename.startswith('CUST_MSTR_'):
        date_str = filename.split('_')[2].split('.')[0]
        date_obj = datetime.strptime(date_str, '%Y%m%d')
        date_col = date_obj.strftime('%Y-%m-%d')
        
        # Load data into CUST_MSTR table with additional date column
        df = pd.read_csv(file)
        df['Date'] = date_col
        load_data_into_table(df, cust_mstr_table)
        
    # Process master_child_export files
    elif filename.startswith('master_child_export-'):
        date_str = filename.split('-')[1].split('.')[0]
        date_obj = datetime.strptime(date_str, '%Y%m%d')
        date_col = date_obj.strftime('%Y-%m-%d')
        date_key_col = date_str
        
        # Load data into master_child table with additional date and date key columns
        df = pd.read_csv(file)
        df['Date'] = date_col
        df['DateKey'] = date_key_col
        load_data_into_table(df, master_child_table)
        
    # Process H_ECOM_ORDER files
    elif filename.startswith('H_ECOM_ORDER'):
        # Load data into H_ECOM_Orders table as is
        df = pd.read_csv(file)
        load_data_into_table(df, h_ecom_order_table)

def load_data_into_table(df, table_name):
    # Truncate the table
    truncate_table(table_name)
    
    # Load data into the table
    df.to_sql(table_name, con=engine, if_exists='append', index=False)

def truncate_table(table_name):
    # Truncate the table
    engine.execute(f'TRUNCATE TABLE {table_name}')
