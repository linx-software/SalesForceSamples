# Linx connect to Salesforce
The following samples will help you to get started with using Salesforce and Linx for data migration, integration and process automation.  Please note that the Linx samples are built using Linx version 5.20.2.0 and Salesforce version v50.0.  

## Automate lead management with Excel
This template integrates Excel data with Salesforce to ensure that while users continue capturing leads using their preferred tool.  This template serves as a foundation for creating Leads in Salesforce as Leads are updated and created in Excel Sheet. 

## Automate lead management with GoogleSheets
Business today demands up-to-the-minute data. Latency requirements are shrinking at the same time.  Sales use different tools to capture various information easily and quickly.
This template integrates GoogleSheet data with Salesforce to ensure that users continue capturing leads using their preferred tool.  This template serves as a foundation for creating Leads in Salesforce as Leads are updated and created in GoogleSheet.  This integration saves time by copying and pasting data from Googlesheet into Salesforce.

## Salesforce and Database Synchronization
Migrating data to and from Salesforce can be challenging due to data inconsistencies, invalid mapping, or improper formatting.
This template synchronizes products data between Salesforce and a database system like SQL Server. Download CreateProductTable.sql and run the script. This template makes it fast to configure the fields to be synchronized, how they map, and criteria on when to trigger the synchronization.  This template imports products from the existing database into Salesforce and updates the product table in SQL Server with the salesforce ID.

## Automated account management with Bulk Data Process
The movement of large quantities of data is necessary during daily data sync.
This template upload account records that are stored in CSV format to Salesforce.  Download Bulk API Sample Contact Data.csv.  It uses the Bulk Api from salesForce.  It also verifies the job status and writes the result to a log file. 
 
### The template processes data in the following order;
1.	Create a new job that specifies the object and action.
2.	Send data to the server.
3.	Once all data has been submitted, close the job. Once closed, no more batches can be sent as part of the job.
4.	Check status. 
5.	Save the result sets with the original data set in a file, to determine which records failed and succeeded.
# The following functions/processes are used as helpers.  
1.	Authenticating Salesforce using OAuth 2.0
     - Parameters - Consumer Key, Consumer Secret, Base URI
     - Result - Access Token
2.	SoQL Query 
     - Parameters - query, access_url, token
     - Result – RESTEndpoint.ResponseBody as String
3.	Data - Create, Delete, Update, Query All, Query by ID 
     - Parameter - sObject Name
     - Result - RESTEndpoint.ResponseBody as string
4.	Bulk data process 
    #### Covers step for creating a job, adding data to job, get status, verifying its status and closing the job
     - AddDataToJob 
          - Parameters – action, body, instance_url, token, object
          - Result – Linx type -  batchJobInfo 
     - CloseJob
          - Parameters – instance_url, token, query, JobId
          - Result – RESTEndpoint.Status.code
     - CreateJob
          - Parameters – action, body, instance_url, token, object
          - Result – RESTEndpoint.ResponseBody
     - GetJobStatus
          - Parameters -  instance_url, token, JobId
          - Result – RESTEndpoint.ResponseBody
     - VerifyJobStatus
          - Parameters -  instance_url, token, JobId
          - Result – RESTEndpoint.ResponseBody

5.	Authenticating GoogleSheets using OAuth 2.0
     - Parameters - Consumer Key, Consumer Secret, Base URI
     - Result - Authentication Code
### Common Utilities Helper
6.   GoogleSheets
     - GetToken - Reads token saved in file generated in Authenticating GoogleSheets using OAuth 2.0    
7.   Salesforce
     - GetAccessTokenAndInstanceURL - Reads Access Token and Instance url from file generated in Authenticating Salesforce using OAuth 2.0
### Additional resources to configure settings 
- [Salesforce-Linx integration guide](https://community.linx.software/community/t/integrating-with-salesforce/494)
- [Salesforce API authentication documentation](https://help.salesforce.com/articleView?id=sf.remoteaccess_oauth_web_server_flow.htm&type=5)
     
# How to use the helper functions to generate Access token
### To Generate Access Token and Exchange Code in Salesforce: 
 - Click on RUN in AuthorizationOAuthTemplate and start
 - In Browser - Navigate to base_uri/oauth/authorize
     - instance url saved in c:\temp\instance_url
     - access token saved in c:\temp\access_token
- The above notepad paths can be changed if needed inside the function.
### To Generate Access Token in Google: 
- Click on RUN in GoogleSheetOAuthTemplate and start
 - In Browser - Navigate to base_uri/oauth/authorize
     - instance url saved in c:\temp\google\instance_url
     - access token saved in c:\temp\google\access_token
- The above notepad paths can be changed if needed inside the function.

## Other Information
#### Bulk API
 - CreateBulkJobTemplate  - State : open
 - CloseJob - State : UploadComplete
 - VerifyJobStatus - Get the state of the job in batch at a particular time after UploadComplete
 - GetJobStatus - Once a job has been completed and is in the JobComplete state (or Failed state), you can get details of which job data records were successfully processed

## Utilities samples
### GetGoogleSheetByID
- Parameter - Google SpreadSheet ID
- Result - Google Spreadsheet

### DeleteExistingLeadRecords_In_Salesforce
Serves to delete all Leads in Salesforce.  This is useful to avoid duplicating data when running sample tests. 

### Get_All_Leads 
To generate sample file and data, or simply download Lead.xlsx for use in Automate lead management with Excel.

### Get_MetaData_Object_Template
A sample to retrieve metadata for an object




     
