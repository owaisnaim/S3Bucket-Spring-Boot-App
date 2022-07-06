# Amazon S3 Bucket Using Spring Boot

AWS Account

•	Create AWS Free Tier Account.

•	Create a new Amazon S3 Bucket.
An Amazon S3 bucket is a public cloud storage resource available in Amazon Web Services' (AWS) Simple Storage Service (S3), an object storage offering. Amazon S3 buckets, which are similar to file folders, store objects, which consist of data and its descriptive metadata.

•	Create a new access key and secret key to access that S3 Bucket.


Spring Boot Application
•	Create a new Spring Boot Application with Lombok, Spring Web and AWS Core Dependency.

•	In Application.yml define all the values like access-key, secret-key, region for S3 Bucket.

•	Create a Config Class Bean (StorageConfig) for configuring S3 bucket in Spring Boot.

•	Create a Service Class (StorageService) and define four methods :
1.	uploadFile (takes Multipartfile as input and converts it to File), 
2.	downloadFile and 
3.	deleteFile.
4.	convertMultiPartFileToFile


•	Create a Controller Class (StorageController) and make the end points for all the three operations and returns the response entity as follows:
1.	@PostMapping("/upload")
2.	@GetMapping("/download/{fileName}")
3.	@DeleteMapping("/delete/{fileName}")

 

 
