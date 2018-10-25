# azure-databricks-labs
This lab gives the hands-on experience with the Databricks python job submission through CLI.

# pre-requisites
Please follow the complete instructions from **db-labs-01-dbcli** labs

# Upload your python script to DBFS

1. Dowload the **pi.py** file to your local file system 
2. Copy the file to DBFS
    `code` dbfs cp <YOUR_LOCAL_PatH>/pi.py dbfs:/docs/pi.py `code`
3. This is the Apache open source program to calculate PI Value, reveiw the code snippet 

*Note: Our intent here is to learn how to submit the jobs via the Azure Databricks CLI rather thand learning how to calculate the pi value*

# Configure and Create the job through Databricks CLI

1. Download the **azuredatabricks-py-config.json** to your local file system 
2. Review the configurations in this json file

# Execute the python job and monitor the results from Databricks CLI

1. Run the below command to create the job in Azure Databricks workspace
    `code` databricks jobs create --json-file <YOUR_LOCAL_PATH>\azuredatabricks-py-config.json `code`
2. You should get the response as below

```
{
  "job_id": X
}
```
3. The above response indicates that the job is created successfully in your Databricks workspace
4. You can login to your databricks workspace and click on jobs, this will display a new job with the above displayed ID
5. Run the job from CLI
    `code` databricks jobs run-now --job-id <JOB_ID> `code`
6. You will get response as below
```
{
  "run_id": X,
  "number_in_job": Y
} 
```
7. In your databricks workspace you will now see the new cluster under the **Job Clusters** section
8. Once the cluster is job is successfully completed you can click on Spark UI/**Logs** link and you will find the value of pi as **Pi is roughly 3.137528**

# Submit your python job through Databricks REST APIs

## Pre-Requisites
You need to have CURL installed in your machine

1. Run the below command to create the job from jobs API

`code` curl -H "Authorization: Bearer <ACCESS_TOKEN>" --data @<YOUR_LOCAL_PATH>\azuredatabricks-py-config.json <DATABRICKS_URL> `code`

*NOTE: You can find the ACCESS TOKEN creation steps in the labs **db-labs-01-dbcli***
*NOTE: You can find the <DATABRICKS_URL> from your Azure Portal, once you click on the databricks resource under overview section you can copy the databricks **URL***

2. Once the job is submitted successfully, you will find below output
```
{"job_id":X}
```

3. From your Databricks workspace click on the **jobs**, you will see the new job got created with the above ID
4. Click on the job ID link and click **run** link
5. You can now select **clusters** link and monitor the progress of the job and once completed you can review the ouput by clicking on the **logs** link 

