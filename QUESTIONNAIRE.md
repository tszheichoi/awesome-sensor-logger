# Questionnaire for Studies

Collect additional information from the participants to support your study. For example, you can use this feature to:

- 📋 Request participants' ages, names, and contact emails upon joining.
- 🔍 Require a participant identifier for joining Sensor Logger data and other research datasets.
- ✅ Obtain additional consent from participants upon enrollment via signatures.
- 🩺 Inquire about participants' physical and mental condition following each data collection session.
- 🤔 Prompt data collectors for any necessary clarifications to facilitate data analysis.
- 📝 Gather demographic information such as gender, occupation, and educational background for a comprehensive understanding of participant profiles.
- 📅 Schedule follow-up surveys or interviews to delve deeper into specific responses or gather longitudinal data.

## When Are Questions Presented?

**Join Study** questions are presented when a user joins a study initially. This is useful for collecting information about the participant — e.g. name, study-specific identifier, contact details etc. Note that once the participant has joined a study, the answers to these questions will not longer be editable. If the same participant leaves and rejoins the study, the latter answers will override the former ones. 

**Recording End** questions are presented every time a recording ends whilst the study is active. This is useful for collecting information that will change across multiple recordings by the same participant — e.g. for a study tracking car journeys, you may want to collect license plate number or the colour of the car; for a medical study, you may want to ask the participant to note down their mood or activity level. These questions can be edited after the fact in the Recordings screen under Study Metadata, up until the recording is uploaded to Sensor Logger Cloud if you opt to use it for your study.

## Question Types
A type, which can be one of the followings.
- Text, where the participants can enter free-form text.
- Number, where the participants can enter numbers in a keypad.
- Email, where the participants can enter text using an email keyboard. Note that this does not validate or guarantee valid email.
- Select, where you provide a list of options where the participants may choose from. There must at least be 2, and up to 10, options per question.
- Sign, where the participants can scribble their signature. *New in version 1.32*

Note: Version 1.31.3 introduced mandatory question fields and multiple-choice selection questions. If you are creating Studies with these features, please make sure your participants are on the latest versions of Sensor Logger, otherwise, they may be able to skip questions and won't see multiple-choice questions entirely, respectively.  

## How Are Questions & Answers Stored?

Both Join Study questions and Recording End questions are packaged and stored as JSON internally. How you access them depends on the data format you have selected for your study. 

| Export Format | Zipped CSV | Combined CSV | JSON | Excel | KML | SQLite |
| --- | --- | --- | --- | --- | --- | --- |
| Part of Recording | ✅ (Complete JSON^) | ❌ | ❌ | ❌ | ❌ | ✅ (Table) |
| View On Sensor Logger Cloud Portal* | ✅ (JSON) | ✅ (JSON) | ✅ (JSON) | ✅ (JSON) | ✅ (JSON) | ✅ (JSON) |
| Download From Sensor Logger Cloud Portal* | ✅ (CSV) | ✅ (CSV) | ✅ (CSV) | ✅ (CSV) | ✅ (CSV) | ✅ (CSV) |

*\*Only if you use Sensor Logger Cloud as your data delivery mechanism. Unavailable if you choose Manual.*

*^Complete JSON includes the entire question -- such as when was the question asked and all options in multiple-choice questions. Simplified JSON includes only the question title and answer.*

Signature is a special type of question where the participants can doodle on a canvas. The availability and presentation of signatures are different to other question types:

| Export Format | Signature |
| --- | --- |
| Part of Recording | As array of coordinates, representing the signature path*  |
| View On Sensor Logger Cloud Portal | Preview as image, and downloadable as SVG |
| Download From Sensor Logger Cloud Portal | Excluded from CSV |

*\*See below for how to read and render this yourself with example Python code.*

## Viewing Questionnaire Answers Online (Recommended) 
When viewing via Sensor Logger Cloud, you get a cleaned version of the questionnaire, where the questions are keys and answers are values. You can view them in a table directly on the website. 

```json
{
   "Which Side Are You On? ":"Left",
   "Row Number":"1",
   "Age": "32"
}
```
In the *Recordings* section of the page, you will see all the Recording End questions. In the *Current Participants* section, you will see all the Join Study questions. 

If your questionnaire has signatures, they will appear in a separate column with a clickable link where you can preview the drawing. This is where you can also download each signature as a separate SVG. 

<img width="1133" alt="signature" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/6c6be467-8b8c-4271-b501-e92b01977fcd">

If you click the "Download Questionnaire" button, then all the answers will be packaged into a CSV. The CSV will be of the following format, where each row is one recording, and the `Questionnaire` column is a json string. Note that signatures, if any, are excluded from this CSV. 

|Download                           |Size     |Questionnaire                                              |Uploader ID|
|-----------------------------------|---------|-----------------------------------------------------------|-----------|
|Recording_2-2024-04-23_22-15-51.zip|158.40 kB|{"Age":"23","Name":"John","Email":"anotherEmail@email.com"}|Study Owner|
|Recording_1-2024-04-23_22-15-30.zip|148.31 kB|{"Age":"33","Name":"Kelvin","Email":"test@test.com"}       |Study Owner|

If you wish to unpack the `Questionnaire` column into a column for each question, you can adapt this simple Python script.

```python
import pandas as pd
import json

df = pd.read_csv('my_recording_questionniares.csv')
df['Questionnaire'] = df['Questionnaire'].apply(json.loads)

for index, row in df.iterrows():
    for key, value in row['Questionnaire'].items():
        df.at[index, key] = json.dumps(value) if isinstance(value, list) else value
```

This yields a Dataframe of the following structure.

|Download                           |Size     |Uploader ID|Age|Name  |Email                 |
|-----------------------------------|---------|-----------|---|------|----------------------|
|Recording_2-2024-04-23_22-15-51.zip|158.40 kB|Study Owner|23 |John  |anotherEmail@email.com|
|Recording_1-2024-04-23_22-15-30.zip|148.31 kB|Study Owner|33 |Kelvin|test@test.com         |

## Viewing Questionnaire Answers As Part of Zipped CSV
If your export format is Zipped CSV, you will get the full questionnaire inside the zip file, as a standalone JSON named `StudyMetadata.json`. For example:

```json
[
   {
      "asked":"Join Study",
      "title":"Is It Raining?",
      "description":"Describe the weather condition",
      "type":"Select",
      "optional":false,
      "selections":[
         "Yes",
         "No"
      ],
      "value":"Yes"
   },
   {
      "asked":"Recording End",
      "title":"Row Number",
      "description":"Approximately, which row were you seating on?",
      "type":"Number",
      "optional":true,
      "selections":[
         
      ],
      "value":"3"
   }
]
```
Unlike the online version, this is more complete -- including the description, type and whether the question was optional. 

## Processing Signatures Yourself
All signatures are stored as vector strokes, and the recommended way to view and retrieve them is via the online portal, where it is. However, if you want to draw it locally yourself, you will have to use a plotting library. To do so, ensure you have either Zipped CSV or SQLite as the export options. This way, all signatures are packaged as part of the recording.

The structure of the value field for a question of signature type is a list of lists representing each distinct stroke. For each stroke, it is an array of two values representing the `x` and `y` coordinates. Divide the integers by 1000 to get the relative coordinates. Note that, following convention, the origin (`(0, 0)`, after dividing by 1000) is at the upper left-hand corner, so the y-axis may be reversed. 

As an example, this Python script reads in 

You can adapt the following script for your needs -- it iterates over the rows and plots out each signature, assuming the signature field is named `signature_field` 

```python
import json
import plotly.graph_objects as go

with open('/work/StudyMetadata.json', 'r') as f:
    study_metadata = json.load(f)

question = study_metadata[0] # array of questions, take the first one
signature_path = question['value'] # we know this is a signature

fig = go.Figure()
for stroke in signature_path:
    x_values = [point[0] * 1000 for point in stroke]
    y_values = [point[1] * 1000 for point in stroke]
    fig.add_trace(go.Scatter(x=x_values, y=y_values, mode='lines', showlegend=False))
fig.update_layout(yaxis_autorange='reversed', xaxis_visible=False, yaxis_visible=False)
fig.show()
```

<img width="820" alt="plotly_signature" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/fd8c085e-cf8b-42cc-a83d-32573c594159">

## Number of Questions

The number of questions you can create for the questionnaire varies based on your subscription tier.
- 1 questionnaire in the Free tier
- 3 questions allowed in the Plus and Pro tiers
- Up to 100 questions allowed in the Ultimate tier
- Need more? *Contact me*.
