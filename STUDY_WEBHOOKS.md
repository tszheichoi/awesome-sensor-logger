# Study Webhooks
When participants contribute recordings to a Study, it is often useful to provide timely analysis results and feedback based on the collected data. You may also want to trigger advanced automation based on participant's recordings. Both of these can be done via Studies Webhooks. 

With Webhooks, you can get notified whenever a participant uploads a recording, and you can optionally send an analysis report back to the participant, which can be viewed in-app alongside the recording. There are three modes:

1. **Do Nothing** -- This is the default (Just A)
2. **Notify** -- You provide a URL Sensor Logger will call whenever a participant uploads a recording, along with the necessary codes to download the recording (A, B and C). 
3. **Notify & Respond** -- Like Notify, but additionally, you can post results back to the users as either a PDF or a Markdown document (All of A, B, C, D, E and F)

<img width="788" height="392" alt="Screenshot 2025-11-17 at 23 16 56" src="https://github.com/user-attachments/assets/5cbfcebf-3fa6-40d6-84f3-00b7aa15c09a" />

## Possible Use Cases
- Automatically run quality checks (length, sensor completeness, phone orientation) the moment a recording arrives.
- Auto-ingest recordings into your dataset by downloading, normalising, and storing them in your cloud storage.
- Send operational notifications to Slack/Discord/Teams whenever key participants submit new data.
- Return personalised feedback reports (PDF/Markdown) directly to participants inside the app.
- Deliver gamified responses like badges, streaks, or performance scores after each upload.
- Guide participants with adaptive next steps (“Please redo the test”, “Try Test B next”) based on analysis.

## Important Notes
- Webhooks only work for Studies where you use **Sensor Logger Cloud** as the data delivery mechanism.
- Webhooks require you to run your own analysis server, some expertise is needed. See below for examples. 
- Webhooks work for all Studies, even on the free tier 🎉! 

## Webhook API Reference

> Note: A simple Python implementation of this API is available with instructions on deployment in the README.

You will need to create a HTTP endpoint that Sensor Logger Cloud will POST to _for every recording uploaded to your Study_. It should be able to receive a JSON payload as the body:

```json
{
  "studyId": "string",
  "uploadId": "string",
  "secretCode": "string"
}
```

`studyId` is the ID of the study. `uploadId` The ID of the uploaded recording. `secretCode` is the authorization code for API access to ultimately download the recording. Sensor Logger will attempt to reach this endpoint once per uploaded recording and you should return status code 200 to indicate success.

With these three pieces of information, you can then download the uploaded recording with GET `https://sensorlogger.app/api/study/file/v1?studyId={studyId}&uploadId={uploadId}`. You must also put the `secretCode` in the HTTP GET request with the header `Authorization: {secretCode}`. This is in fact part of the wider set of APIs available with Studies. See https://github.com/tszheichoi/awesome-sensor-logger/blob/main/STUDY_API.md for more information.

Once downloaded, you can extract and analyze the data as needed and output either a markdown document or PDF, which you can POST back to the users via `https://sensorlogger.app/api/study/webhook/v1?studyId={studyId}&uploadId={uploadId}` with header

```
{
    "Authorization": secret_code,
    "Content-Type": "text/markdown"
},
```
or
```
{
    "Authorization": secret_code,
    "Content-Type": "application/pdf"
},
```
depending on whether you are posting the results back as markdown or PDF, respectively. 

## Creating a Study with Webhooks
Create a new Study in Sensor Logger. In the Webhooks section, you can select whether you want to enable Notify or Notify & Respond webhooks, as shown in A. Specify the Webhook URL in B. 

<img width="662" height="477" alt="Screenshot 2025-11-18 at 14 40 56" src="https://github.com/user-attachments/assets/0dc24436-a11a-4d7b-a7da-081d45288a8a" />

Tap C to make sure Sensor Logger can reach the endpoint. Sensor Logger will attept to call your endpoint with dummy information that can be used to download a testing zipped recording. If you see a tick, that means it was sucessful. After you create your Study, both you as the investigator and all your Study participants can see that Webhooks are enabled, as shown in D.
