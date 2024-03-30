# Questionnaire for Studies

Optionally collect additional information from the participants to support your study. For example, you can use this feature to:

- 📋 Request participants' ages, names, and contact emails upon joining.
- 🔍 Require a participant identifier for joining Sensor Logger data and other research datasets.
- ✅ Obtain additional consent from participants upon study enrollment.
- 🩺 Inquire about participants' physical and mental condition following each data collection session.
- 🤔 Prompt data collectors for any necessary clarifications to facilitate data analysis.
- 📝 Gather demographic information such as gender, occupation, and educational background for a comprehensive understanding of participant profiles.
- 📅 Schedule follow-up surveys or interviews to delve deeper into specific responses or gather longitudinal data.

> ⚠️: **Version 1.32.3** introduced mandatory question fields and multiple choice selection questions. If you are creating Studies with these features, please make sure your participants are on the latest versions of Sensor Logger, otherwise they may be able to skip questions and won't see multiple choice questions entirely, respectively. 

## When Are Questions Presented?

**Join Study** questions are presented when a user joins a study initially. This is useful for collecting information about the participant — e.g. name, study-specific identifier, contact details etc. Note that once the participant has joined a study, the answers to these questions will not longer be editable. if the same participant leaves and rejoins the study, the latter answers will override the former ones. 

**Recording End** questions are presented every time a recording ends whilst the study is active. This is useful for collecting information that will change across multiple recordings by the same participant — e.g. for a study tracking car journeys, you may want to collect license plate number or the colour of the car; for a medical study, you may want to ask the participant to note down their mood or activity level. These questions can be changed after the fact in the Recordings screen under Study Metadata, up until the recording is uploaded to Sensor Logger Cloud if you opt to use it for your study.

## How Are Questions & Answers Stored?

Both Join Study questions and Recording End questions are packaged and stored as JSON. How you access them depends on the data format you have opted for your study. 

| Export Format | Zipped CSV | Combined CSV | JSON | Excel | KML | SQLite |
| --- | --- | --- | --- | --- | --- | --- |
| Inside Recording | ✅ (JSON) | ❌ | ❌ | ❌ | ❌ | ❌ |
| View On Sensor Logger Cloud Portal* | ✅ (JSON) | ✅ (JSON) | ✅ (JSON) | ✅ (JSON) | ✅ (JSON) | ✅ (JSON) |
| Download From Sensor Logger Cloud Portal* | ✅ (CSV) | ✅ (CSV) | ✅ (CSV) | ✅ (CSV) | ✅ (CSV) | ✅ (CSV) |

**Only if you use Sensor Logger Cloud as your data delivery mechanism. Unavailable if you choose Manual.* 

When viewing on Sensor Logger Cloud, you get a cleaned version of the questionnaire, where the questions are keys and answers are values. You can view them in a table directly on the website or download them CSV. 

```json
{
   "Which Side Are You On? ":"Left",
   "Row Number":"1",
   "Age": "32"
}
```

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

## Question Types

- A type, which can be one of the followings.
    - Text, where the participants can enter free-form text.
    - Number, where the participants can enter numbers in a keypad.
    - Email, where the participants can enter text using an email keyboard. Note that this does not validate or guarantee valid email.
    - Select, where you provide a list of options where the participants may choose from. There must at least be 2, and up to 10, options per question.

## Number of Questions

- No questionnaire in the Free tier
- 1 question allowed in the Plus tier
- 3 questions allowed in the Pro tier
- 20 questions allowed in the Ultimate tier
- Need more? *Contact me*.
