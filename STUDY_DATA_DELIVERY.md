# Study Data Delivery
## Overview
Studies allow you, as the investigator, to collect data from other Sensor Logger users seamlessly. There are three ways data can be delivered back to the investigator.

1. **Sensor Logger Cloud**: Most seamless and with zero setup. Data is securely uploaded to our server for you to download later. Data is retained for up to 90 days. Only you as the Study investigator have access to the participants' recordings. This is the recommended way for most Sensor Logger users. 
2. **Bring Your Own Bucket**: Participants still benefit from one-tap upload, but data is uploaded directly to your S3-compatible storage bucket. No user data goes through our servers in this case. You only need to provide Sensor Logger with write-access to this bucket. You will have to keep track of and download uploaded recordings yourself. Use this only if you have specific data governance requirements. 
3. **Manual**: You provide participants with instructions on how to upload their data. The least seamless option of the three. 

Sensor Logger Cloud and Manual are available to all users, including in the free tier. Different tiers have different Sensor Logger Cloud storage limits, which you can see in the app. You can always upgrade as your Study and storage needs grow. Bring Your Own Bucket is only available if the investigator is subscribed to the Ultimate tier. In all cases, all Study participants can stay in the free tier. 

## Bring Your Own Bucket
Bring Your Own Bucket (BYOB) allows you to directly control where your Study data is stored by connecting your own cloud storage. Instead of uploading participant data to Sensor Logger Cloud, data is sent directly from the participant’s device into your S3-compatible storage bucket. This ensures that no recording data ever passes through or is retained on Sensor Logger servers.

### Requirements for Investigator
- On the latest version of Sensor Logger (1.46 or later).
- An active Ultimate tier subscription.
- An existing S3-compatible bucket (e.g., Amazon S3, Backblaze B2, Cloudflare R2), which supports presigned urls.
- A set of credentials with write-only permissions for the bucket (to ensure participants can only upload data).

### Requirements for Participants
- On the latest version of Sensor Logger (1.46 or later).

### Setup Steps
1. In the Sensor Logger app, create a new Study. Note you cannot change the delivery mechanism of an existing Study. 
2. Select Bring Your Own Bucket as the delivery method.
3. Enter your bucket endpoint, access key and secret key.
4. Tap Test Bucket to test the connection. This will write a test file in your bucket. You should manually verify that this file exists before creating the Study. 

### Important to Note
- You **must** enable server-side encryption on your bucket so that recording data is encrypted at rest. Note that data is always transmitted encrypted from the Sensor Logger app, but you are responsible for the encryption at rest.
- You are responsible for monitoring storage usage, managing lifecycle policies, backing up data and deleting data.
- Sensor Logger Cloud does not keep any copies or backups of data (as no recording data is transmitted to Sensor Logger Cloud).
- Sensor Logger will create a folder for each Study based on the Study ID, which you can find when viewing the Study detail. 
- Recording filenames will be the name of the recording with a random UUID prepended, to ensure uniqueness for each upload. 
- Restrict the bucket credentials you provide when creating the study to write-only for maximum security.
- Don't forget that you pay for all storage costs associated with your bucket to your cloud provider.
- Any storage used in your own bucket does not count towards your Sensor Logger Cloud storage.
- Participants can only upload to your bucket for the duration of the study, if you wish to prevent uploads earlier you may delete the study which will immediately prevent further uploads.

### Technical Details
When using BYOB, you provide credentials to access your S3-compatible bucket. These credentials are stored securely by Sensor Logger Cloud and are not distributed to participants. When participants upload a recording, they request a signed upload URL from Sensor Logger Cloud which is generated on the server using your credentials. The signed upload URL is then provided to the participant and the data is uploaded directly from their device to your bucket. We strongly recommend that you only provide write-access credentials to your S3-compatible bucket, if your cloud provider supports this option.
