#Task2

To create an Azure Bill of Materials we require data integration needs, we need to consider several Azure services that will help us ingest, process, and store the data from the sources:

1. Azure Data Factory (ADF): For orchestrating data movement and transformation.
2. Azure SQL Database : For storing structured data from Oracle and Salesforce.
3. Azure Blob Storage: For storing semi-structured files.
4. Azure Data Lake Storage (ADLS): For scalable data storage.
5. Azure Logic Apps or Azure Functions: For handling FTP transfers and other automation.
6. Azure Integration Runtime: For connecting to on-premise Oracle databases.
7. Azure Virtual Network: To securely connect your on-premise Oracle database to Azure services.


 1. Azure Data Factory (ADF)
- Description: Orchestrates and automates data movement and data transformation.
- Assumptions: 20 tables from Oracle, 120 tables from Salesforce, 20 semi-structured files.
- Estimated Cost: 
  - Data Pipeline runs: $1 per 1000 runs
  - Data Movement: $0.25 per DIU-hour
  - Estimated Monthly Cost: $150 (based on usage patterns and data volume)

 2. Azure SQL Database / Azure Synapse Analytics
- Description: Storing and querying structured data.
- Assumptions: Approx. 80 GB of incremental data per month.
- Estimated Cost: 
  - Azure SQL Database (P4): $1,706.40/month
  - Synapse Analytics (DW1000c): $4,704/month (more scalable)
  - Choose based on performance requirements.
  - Estimated Monthly Cost: $2,000 - $5,000

 3. Azure Blob Storage / Azure Data Lake Storage (ADLS)
- Description: Storing semi-structured files.
- Assumptions: 5 GB of data per month, 20 files.
- Estimated Cost: 
  - Blob Storage: $0.02 per GB for hot storage, $0.01 per GB for cool storage
  - Estimated Monthly Cost: $5 - $10

 4. Azure Logic Apps / Azure Functions
- Description: For FTP automation and other serverless workflows.
- Assumptions: Automated FTP transfers, small volume functions.
- Estimated Cost: 
  - Logic Apps: $0.000025 per action
  - Azure Functions: $0.20 per million executions
  - Estimated Monthly Cost: $10 - $50

 5. Azure Integration Runtime
- Description: For connecting to on-premise Oracle databases.
- Assumptions: Continuous connection for data extraction.
- Estimated Cost: 
  - Self-hosted Integration Runtime: No additional cost but requires VM.
  - VM (D4s_v3): $0.192/hour
  - Estimated Monthly Cost: $140 (for continuous operation)

 6. Azure Virtual Network (VNet)
- Description: For secure connection to on-premise Oracle databases.
- Assumptions: Basic VNet setup.
- Estimated Cost: 
  - VNet: $0.02 per hour
  - Estimated Monthly Cost: $15

# Total Estimated Monthly Cost
- Low Estimate: $2,320
- High Estimate: $5,365


# Summary Table

          Service                             Description                    Estimated Cost (Monthly) 
--------------------------------------------------------------------------------------------------
 Azure Data Factory                  Data orchestration and automation               $150                     
 Azure SQL Database/Synapse         Structured data storage and querying         $2,000 - $5,000          
 Azure Blob Storage                   Semi-structured data storage                 $5 - $10                 
 Azure Logic Apps                     FTP automation and workflows                $10 - $50                
 Azure Integration Runtime            On-premise Oracle connection                    $140                     
 Azure Virtual Network (VNet)            Secure connection setup                       $15                      
 Total Estimated Monthly Cost                                                    $2,320 - $5,365
