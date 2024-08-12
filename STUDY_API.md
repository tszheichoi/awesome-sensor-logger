# Study API

As a Study investigator, you can retrieve, delete, and manage all contributed recordings **via a web frontend**, linked directly within your Study page, **or with an API**. The API is useful if you want to automate your large-scale Study. To use the API, you need to have the identifier of your study `studyId` and the `secretCode`. Both can be found or generated within the app under your Study page.   

- For `studyId`, go to the Studies screen and select the As Investigator tab. Tap the Study and tap on the Study ID under the title to copy the identifier.
- For `secretCode`, go to the Studies screen and select the As Investigator tab. Tap the Study and select the Data tab. Tap Generate New Code to generate a new secret code. When using the API, do not include spaces in the secret code. 

> ⚠️ **Important Notice**: The Study API is currently in beta and may undergo changes. While using the API, you might encounter bugs or issues. We recommend testing thoroughly and reporting any problems you find. Please be mindful of the rate limits that apply to all API endpoints.

The example code below is written in Python, but feel free to adapt it to any language or tool of choice.

### Get Study Information

List all recordings and users for the Study with ID `test` and secret code `secret` using the GET method:

```python
import requests

studyId = "test" # replace with real id
secretCode = "secret" # replace with real secret, but be mindful not to commit it to git!
url = f"https://sensorlogger.app/api/study/v1?studyId={studyId}"
response = requests.get(url, headers={"Authorization": secretCode})
print(response.json())
```

Example JSON response is as follows:

```json
{
  "recordings": [
    {
      "uploadId": "97b996e6-7ace-489f-ae65-57bcef27ae47",
      "name": "Tedt-2024-05-15_21-38-32.zip",
      "size": 245407,
      "userId": "98f90cf0f204",
      "questionAnswers": {}
    }
  ],
  "users": [{
      "userId": "98f90cf0f204",
      "questionAnswers": {
        "What is your favourite colour?": "Blue"
      }
    }]
}
```

For more information about the `questionAnswers`schema, see https://github.com/tszheichoi/awesome-sensor-logger/blob/main/QUESTIONNAIRE.md. 

### Download a Specific Recording

Download a specific upload ID `uploadId` for the Study ID `test` and secret code `secret` to a file named `test.zip` using the GET method:

```python
import requests

studyId = "test"
secretCode = "secret"
uploadId = "uploadId"
url = f"https://sensorlogger.app/api/study/file/v1?studyId={studyId}&uploadId={uploadId}"
response = requests.get(url, headers={"Authorization": secretCode})
with open(f"{uploadId}.zip", "wb") as f: # Change the extension if needed
    f.write(response.content)
```

Replace `.zip` with the desired extension if you have configured your Study export not to be Zip (e.g. `.json`) 

### Delete a Specific Recording

Delete a specific upload ID `uploadId` for the Study ID `test` and secret code `secret` using the DELETE method. Please note that deletion requires the Study owner to have a Pro or Ultimate subscription.

```python
import requests

studyId = "test"
secretCode = "secret"
uploadId = "uploadId"
url = f"https://sensorlogger.app/api/study/file/v1?studyId={studyId}&uploadId={uploadId}"
response = requests.delete(url, headers={"Authorization": secretCode})
print(response.json())

```

Example JSON response is as follows:

```json
{
  "success": true
}

```
