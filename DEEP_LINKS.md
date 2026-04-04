# Deep Links

Sensor Logger supports deep links via the `sensorlogger://` URL scheme. These work with iOS Shortcuts, Android Tasker, NFC tags, and any app that can open a URL.

## Recording

| URL | Description |
|-----|-------------|
| `sensorlogger://start` | Start recording. No-op if already recording (From Version 1.58). |
| `sensorlogger://stop` | Stop recording. No-op if not recording (From Version 1.58). |
| `sensorlogger://boot` | Toggle recording (start if stopped, stop if started). |

All three navigate to the Logger screen.

## Configuration

| URL | Description |
|-----|-------------|
| `sensorlogger://config/{code}` | Import a configuration (sensors, settings, rules). |

From Version 1.58 and onwards, to get the config code: Settings > Export, Share & Restore > **Copy Deep Link**. This copies a ready-to-use `sensorlogger://config/...` URL.

You can chain config + start to programmatically change settings and begin recording:
1. Open `sensorlogger://config/{code}` to apply settings
2. Open `sensorlogger://start` to begin recording

## Studies

| URL | Description |
|-----|-------------|
| `sensorlogger://study/{studyId}` | Navigate to a specific study. |
| `sensorlogger://joinstudy` | Open the Join Study screen. |

## iOS Shortcuts

1. Open the Shortcuts app
2. Create a new shortcut > Add Action > **Open URLs**
3. Set the URL to any of the above (e.g. `sensorlogger://start`)

Trigger via home screen widget, NFC tag, Siri, location-based automation, or Back Tap.

## Android

Use Tasker, Bixby Routines, MacroDroid, or any automation app that can open a URL. The same `sensorlogger://` links work on both platforms.
