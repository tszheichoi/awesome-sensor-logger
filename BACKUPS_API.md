# Backups API

If you have Backups enabled, you can list, download, and delete your backed up recordings programmatically via an API as follows:

- Sign in to https://sensorlogger.app/backups with the email you verified in the Sensor Logger app.
- Under API Access, tap Generate Key.
- To revoke a key, tap Generate New Key. The old key stops working immediately.

This key covers every device verified with that email. 

### List Backups

List all backed up recordings for the API key `secret` using the GET method:

```python
import requests

apiKey = "secret" # replace with real key, but be mindful not to commit it to git!
url = "https://sensorlogger.app/api/backup/v1"
response = requests.get(url, headers={"Authorization": apiKey})
response.raise_for_status()
print(response.json())
```

Example JSON response is as follows:

```json
{
  "backups": [
    {
      "backupId": "3f2a9c1e7b8d4f60",
      "deviceId": "8A1F3C2E-5B6D-4E7F-9A0B-1C2D3E4F5A6B",
      "name": "Morning Run",
      "fileName": "Morning Run-2026-08-30_07-12-05.zip",
      "size": 1834592,
      "createdOn": "2026-08-30T07:12:05.000Z",
      "uploadedOn": "2026-08-30T07:41:18.000Z",
      "duration": 1795000,
      "tags": ["studyName:Gait Study"],
      "meta": {
        "platform": "iOS",
        "platformVersion": "19.0",
        "deviceModel": "iPhone 17 Pro",
        "appVersion": "1.64.0",
        "timezone": "Europe/London",
        "sensors": ["Accelerometer", "Gyroscope", "Location"]
      }
    }
  ]
}
```

- `duration` is in milliseconds.
- `meta` is only present for recordings backed up from recent app versions; older backups may omit it or include only some fields.
- `tags` prefixed with `studyName:` indicate the recording was also contributed to a Study.

### Download a Specific Backup

Download a specific backup ID `backupId` for the API key `secret` to a file named `backupId.zip` using the GET method:

```python
import requests

apiKey = "secret"
backupId = "backupId"
url = "https://sensorlogger.app/api/backup/file/v1"
with requests.get(
    url,
    params={"backupId": backupId},
    headers={"Authorization": apiKey},
    stream=True,
) as response:
    response.raise_for_status()
    with open(f"{backupId}.zip", "wb") as f:
        for chunk in response.iter_content(chunk_size=65536):
            f.write(chunk)
```

Backups are always stored as Zip, regardless of the export format configured in the app.

### Delete a Specific Backup

Delete a specific backup ID `backupId` for the API key `secret` using the DELETE method. This removes the recording from the cloud and frees up the storage against your quota. Any copy on your device in Sensor Logger is unaffected.

```python
import requests

apiKey = "secret"
backupId = "backupId"
url = "https://sensorlogger.app/api/backup/file/v1"
response = requests.delete(
    url,
    params={"backupId": backupId},
    headers={"Authorization": apiKey},
)
response.raise_for_status()
print(response.json())
```

An example JSON response is as follows:

```json
{
  "success": true
}
```

### Errors

All errors are returned as JSON with an `error` field. 

- An incorrect or revoked API key returns HTTP 404 with `"The API key is incorrect"`.
- A `backupId` that does not exist, or that belongs to a different email address, returns HTTP 404 with `"Backup not found"`.
