# CDC
CDC pipeline-Replication on going in AWS using glue, lambda, RDS

In this project i have developed a complete end to end CDC pipeline where we do the following. 

1. We will going to read the files from mysql database.
2. To load the data inside a S3 bucket  we will create DMS source point and end points, After this using DMS task using IAM role(s3 full access) and using the job we will load all the files inside a S3 bucket in AWS: This is a temporary bucket. 
3. After loading the data inside s3, we will create the lambda function and glue job to update the data in case of any delete, insert or update operations inside mysql. 
4. If any of the above mentioned activites are done the glue and the lambda fuctions will automatically update the data and load inside a final S3 bucket. 

Note: The temporary S3 will trigger the lambda function and the lambda function will call the glue job and the glue job wil if a fresh data has been uploaded in temporary s3 and when it is there it will pick that file and do the update in the original dataset and will push it into the destination aka the final S3 bucket. 


