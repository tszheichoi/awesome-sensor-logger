# Deep Links

Sensor Logger supports deep links via the `sensorlogger://` URL scheme. These work with iOS Shortcuts, Android Tasker, NFC tags, and any app that can open a URL.

## Recording

| URL | Description |
|-----|-------------|
| `sensorlogger://start` | Start recording. No-op if already recording (From Version 1.58). |
| `sensorlogger://stop` | Stop recording. No-op if not recording (From Version 1.58). |
| `sensorlogger://boot` | Toggle recording (start if stopped, stop if started). |

All three navigate to the Logger screen.

## Annotations

| URL | Description |
|-----|-------------|
| `sensorlogger://annotate?text=pothole` | Record an annotation with free text "pothole". |
| `sensorlogger://annotate?preset=1` | Record an annotation using the preset at index 1 (0-based). |
| `sensorlogger://annotate` | Record an annotation using the first preset (index 0). |

A recording must already be in progress. If not, an alert is shown. If both `text` and `preset` are provided, `text` takes priority. Navigates to the Logger screen on success. From Version 1.59.

**Notes:**
- Commas in annotation text are automatically stripped to ensure CSV export compatibility.
- Spaces and special characters in `text` must be URL-encoded — for example, `speed bump` should be `sensorlogger://annotate?text=speed%20bump`. When in doubt, stick to simple alphanumeric text (e.g. `pothole`, `station_1`) to avoid encoding issues.

Because annotations don't require looking at the phone screen, they pair well with hands-free triggers. See the [Automation](#automation) section below for how to set up Siri, Action Button, Back Tap, NFC tags, widgets, Tasker and more. For example:
- Stick NFC tags along a route, each written with a different `annotate?text=...` URL — tap as you pass each one
- Assign `sensorlogger://annotate?text=pothole` to Siri and say "Hey Siri, pothole" while driving
- Add a Shortcuts widget with buttons for "Bus", "Train", "Walk" — each opening a different annotation URL

## Configuration

| URL | Description |
|-----|-------------|
| `sensorlogger://config/{code}` | Import a configuration (sensors, settings, rules). |

From Version 1.58 and onwards, to get the config code: Settings > Export, Share & Restore > **Copy Deep Link**. This copies a ready-to-use `sensorlogger://config/...` URL.

You can chain config + start to programmatically change settings and begin recording:
1. Open `sensorlogger://config/{code}` to apply settings
2. Open `sensorlogger://start` to begin recording

By default, Sensor Logger will ask you to confirm before importing the new configuration, as the existing configuration (including settings, selected sensors, rules, streaming configuration and more) will all be overridden. If this is in the way of your automation, you can add `skipConfirmation` to bypass this safeguard: `sensorlogger://config/{code}?skipConfirmation=true`.

## Studies

| URL | Description |
|-----|-------------|
| `sensorlogger://study/{studyId}` | Navigate to a specific study. |
| `sensorlogger://joinstudy` | Open the Join Study screen. |

## Automation

Any app or system feature that can open a URL can trigger Sensor Logger deep links. Below are platform-specific ways to integrate.

### iOS Shortcuts

1. Open the **Shortcuts** app
2. Create a new shortcut > Add Action > **Open URLs**
3. Set the URL to any `sensorlogger://` link (e.g. `sensorlogger://start`)

Once created, a Shortcut can be triggered from many places:

| Trigger | How to set up |
|---------|---------------|
| Siri voice command | Shortcut settings > "Add to Siri" — assign a custom phrase like "Start logging" or "Mark pothole". |
| Action Button | Settings > Action Button > Shortcut (iPhone 15 Pro and later). |
| Back Tap | Settings > Accessibility > Touch > Back Tap > choose Double or Triple Tap > select your Shortcut. |
| Home screen icon | Long-press the Shortcuts app > tap your shortcut > "Add to Home Screen". |
| Lock screen widget | Add a Shortcuts widget to the lock screen (iOS 16+). |
| Control Centre | Settings > Control Centre > add a Shortcuts toggle (iOS 18+). |
| NFC tag | Automations > Create Personal Automation > NFC > scan a tag > add "Open URL" action. Tap your phone to the tag to trigger — no confirmation needed. |
| Location-based | Automations > Arrive/Leave a location > "Open URL". Automatically start recording when you arrive at a trailhead or lab. |
| Time of day | Automations > Time of Day > "Open URL". Start a daily commute recording at 8am. |
| CarPlay / Bluetooth connect | Automations > CarPlay or Bluetooth > "Open URL". Start recording when your phone connects to your car. |
| Apple Watch | The Shortcuts app syncs to Apple Watch — run deep links from your wrist. |
| Focus mode | Automations > When Focus turns on > "Open URL". Start recording when Driving Focus activates. |

You can chain multiple URLs in a single Shortcut to configure and start in one tap:
1. Open URLs: `sensorlogger://config/{code}?skipConfirmation=true`
2. Wait 1 second
3. Open URLs: `sensorlogger://start`

### Android

The same `sensorlogger://` links work on Android via any automation app or system feature that can open a URL.

| App / Feature | How to set up |
|---------------|---------------|
| Tasker | Task > Net > Browse URL > enter the `sensorlogger://` URL. Trigger from profiles (location, time, Bluetooth, sensor state, etc.), widgets, or Quick Settings tiles. |
| Bixby Routines (Samsung) | Create Routine > add condition (e.g. Bluetooth connected) > add action "Open app or URL". |
| MacroDroid | Add Action > Open Website > enter URL. Trigger from geofence, NFC, shake, widget, notification, and more. |
| Google Assistant Routines | Add action > "Open URL" (availability varies by region). Say "Hey Google, start logging". |
| Home screen shortcut | Most automation apps (Tasker, MacroDroid) let you place a single-tap shortcut/widget on the home screen. |
| Quick Settings tile | Tasker and MacroDroid can add custom Quick Settings tiles that open a URL — accessible from the notification shade without unlocking. |
| NFC tag | Use NFC Tools or Tasker to write a URL to a tag. Tap to trigger. |
| Wear OS | Tasker tasks can be triggered from a Wear OS watch face or complication. |

### Multi-step Workflows

Combine deep links for more powerful automations:

- **Drive logging**: CarPlay/Bluetooth connect → `config` (enable GPS + accelerometer) → `start` → on disconnect → `stop`
- **Lab experiment**: NFC tag at each station → `annotate?text=station_1`, `annotate?text=station_2`, etc.
- **Transportation study**: Shortcuts widget with buttons for "Bus", "Train", "Walk", "Car" — each opens `annotate?text=bus`, etc.
- **Daily routine**: Time-of-day automation at 8am → `start`, at 6pm → `stop`
