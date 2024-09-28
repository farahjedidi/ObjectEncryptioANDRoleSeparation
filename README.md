# Demo - SSE Object Encryption and Role Separation

In this demo, I showcase how to create an S3 bucket and upload images using different server-side encryption (SSE) methods, including SSE-S3, SSE-KMS with an AWS-managed key, and SSE-KMS with a customer-generated key. Additionally, I apply role-based access restrictions through an IAM policy and set default bucket encryption.

## Steps

### 1. Create an S3 Bucket
- I navigated to the S3 service.
- Created a bucket named `catpics-farah`.
- Clicked **Create Bucket**.
- ![Screenshot](https://imgur.com/8u7A8ZR.png)

### 2. Create a Key in KMS
- I navigated to AWS Key Management Service (KMS).
- Clicked **Create Key**.
- Used the default settings and set the alias to `catpics`.
- Skipped Key Administrative Positions and Key Usage Permissions.
- Finished the key creation process.
- ![Screenshot](https://imgur.com/EMriIYI.png)

### 3. Upload Image with SSE-S3 Encryption
- I navigated back to the `catpics-farah` S3 bucket.
- Uploaded the image `sse-s3-dweez.jpg`.
- Expanded the **Properties** section and specified the server-side encryption:
  - Selected **Override bucket settings**.
  - Chose **SSE-S3** as the encryption key type.
  - ![Screenshot](https://imgur.com/cthDXIs.png)
  - Clicked **Upload**.
  - The image can be opened
  - ![Screenshot](https://imgur.com/ApSdbb2.png)
    
### Extra step : Upload Image with SSE-KMS Using AWS Managed Key
- I uploaded the image `see-kms-ginny.jpg`.
- Expanded the **Properties** section and specified the server-side encryption:
  - Selected **Override bucket settings**.
  - Chose **SSE-KMS** as the encryption key type.
  - Selected the AWS managed key (`aws/s3`).
  - Clicked **Upload**.
  
### 4. Upload Image with SSE-KMS Using Customer-Generated Key
- I uploaded the same image `see-kms-ginny.jpg` (which will override the first one)
- Expanded the **Properties** section and specified the server-side encryption:
  - Selected **Override bucket settings**.
  - Chose **SSE-KMS** as the encryption key type.
  - Selected the key with alias `catpics` (not the AWS managed key (`aws/s3`)).
  - ![Screenshot](https://imgur.com/3GdRYS5.png)
  - Clicked **Upload**.
  - The image can be opened
  - ![Screenshot](https://imgur.com/qcTmgPB.png)


### 5. Apply IAM Deny Policy to Prevent KMS Usage
- I navigated to the **IAM Dashboard**.
- Went to **Users > iamadmin > Permissions**.
- Clicked **Add Policy** > **Inline Policy**.
- In the JSON tab, I deleted the template and pasted the provided JSON policy found in the "denyKMS" file.
- Reviewed and named the policy `denyKMS`.
- Clicked **Create policy**.
- ![Screenshot](https://imgur.com/sYqVhzh.png)
- Verified that I could access the SSE-S3 encrypted image but not the SSE-KMS encrypted image.
- ![Screenshot](https://imgur.com/bTFSCaM.png)
- ![Screenshot](https://imgur.com/uuH7Mbz.png)
- Removed the `denyKMS` policy (now I can open the SSE-KMS encrypted image)


### 6. Set Default Bucket Encryption
- I went to the **catpics** bucket in S3.
- Under the **Properties** tab, clicked **Edit** next to **Default Encryption**.
- Selected **SSE-KMS** as the encryption type.
- Chose the key with alias `catpics` created in Step 2.
- ![Screenshot](https://imgur.com/oauGcmk.png)

### 7. Upload Image with Default Encryption
- I uploaded the image `default-merlin.jpg` without changing any encryption settings.
- Under the **Properties** tab, I verified that the server-side encryption was set to the default configuration from Step 6.
- ![Screenshot](https://imgur.com/timjBB1.png)

## Conclusion
In this demo, I demonstrated how to configure different encryption methods in S3, apply role-based access restrictions through IAM policies, and set default encryption for an S3 bucket. By the end of this demo, I had a deeper understanding of AWS S3 object encryption and role separation.
