# Lambda-trim-SFDC
#Setup Steps
1. Download Lambda-trim-SFDC
2. Select `trim.js & node_modules` folder and create a zip file
3. In AWS, create a lambda function and upload this zip in `Function code` section, Change the HandlerInfo name to 
```trim.handler``` 
4. In the designer section, add trigger S3 bucket to your AWS lambda function. 
5. In the environment variable section, Create a key "Client_Identifier" and fill sandbox client identifier. 
6. Setup done.
7. Now when ever you upload a file to bucket, based on the file name, it will get the SFDC Planogram record refernce and creates the attachment.

In this version, full flow implemented.
1. When ever PDF uploaded to S3, trigger calls our lambda event.
2. Our lambda logic passes Client_Identifier and calls “apiGWandFunctionalToken_Lambda” to get a session token.
3. Then logic gets the name of the pdf and query the Planogram details from SFDC for column number. 
4. Logic calculates total number of pages and identify start and end page number which needs to be converted.
5. Then logic converting pdf into images with the page start number and end number.
6. Once the images converted, It trimmed(Removed white background) by our logic and saved to S3.
7. We already identified the planogram, so logic continued and starts pushing the images to SFDC attachment to that planogram record.
8. After successful attachment, local s3 file were deleted.
9. If any error occurred, then the error message recorded in the s3 bucket as “folderName + 'result’”  JSON file.
10. Failed uploads processed in next lambda run. 

