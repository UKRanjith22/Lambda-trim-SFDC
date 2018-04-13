# Lambda-trim-SFDC
1. Download Lambda-trim-SFDC
2. Select `trim.js & node_modules` folder and create a zip file
3. In AWS, create a lambda function and upload this zip in `Function code` section, Change the HandlerInfo name to 
```trim.handler``` 
4. In the designer section, add trigger S3 bucket to your AWS lambda function. 
5. In the environment variable section, Create a key "Client_Identifier" and fill sandbox clientidentifier. 
6. Setup done.
7. Now when ever you upload a file to bucket, based on the file name, it will get the SFDC Planogram record refernce and creates the attachment.


