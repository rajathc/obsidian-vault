## 1. Problem Statement

Users sometimes forget to carry the Neo 1 device but still need to capture important conversations. Currently, there is no seamless fallback mechanism to record audio via the mobile app. This gap leads to lost memory opportunities and reduces the perceived reliability of the product.

## 2. Objective

Introduce a fallback recording experience—**Forget Mode**—within the Neo mobile app that activates when the Neo 1 device is not connected. This mode will:

- Let users record high-importance conversations using the phone microphone.
- Automatically transcribe and generate a memory, similar to Neo 1 workflows.
- Preserve the “connect and forget” promise by always being ready with a backup.
## 3. Core Functionality

### 3.1 Trigger

- Automatically detect a lack of Neo 1 connection on app launch.
- Show a non-intrusive prompt: **“Forgot Neo 1?”**
- Users can also access Forget Mode manually via the settings.
### 3.2 Recording Interface

- Request microphone permissions if not granted.
- Display a simple interface: mic waveform and stop button.
- Visual indicator must show that the mic is on and actively recording.
### 3.3 Audio Handling & Memory Generation

- The memory starts generating on the backend when I press “Save”.
- Transcribe and generate structured memory with tags    
- Display on Home screen & Memory list post-processing.

## 4. UX/UI Requirements

- Show a persistent recording notification while app is backgrounded.
- Provide proactive reminders if user has a calendar event but no connected Neo 1.
- Alert at the start on impact of playing media while recording(the volume is reduced), impact on the battery if the device is transcribing and how phone calls can interrupt the transcribing.
- Handle phone call interruptions with ease using auto-resume capability.
## 5. Test Cases

| TC ID | Description                                | Expected Outcome                                                                                                                                                                                                                        |
| ----- | ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| TC01  | Open app without Neo 1 connected           | “Forgot Neo 1?” cta shown                                                                                                                                                                                                               |
| TC02  | Enter Forget Mode and grant mic permission | Recording UI appears with the popup asking with instructions on how continous recording will imoact battery life, phone calls can inturuppt the recording and playing media while recording will impact the recording and media volume. |
| TC03  | Deny mic permission                        | Show error and retry option                                                                                                                                                                                                             |
| TC04  | Save recording                             | Memory generated and appears in list                                                                                                                                                                                                    |
| TC05  | Screen locked during recording             | Recording continues with persistent banner                                                                                                                                                                                              |
| TC06  | Phone call during recording                | Recording paused, prompt to resume post-call                                                                                                                                                                                            |
| TC07  | Audio playback detected                    | Alert shown that the recording will be impacted                                                                                                                                                                                         |
| TC08  | Calendar event + no Neo                    | Push: “Start Forget mode?” sent if device is not connected                                                                                                                                                                              |
| TC09  | Forget mode reminder                       | Forgot your Neo 1? Try using your phone to record your important meetings                                                                                                                                                               |
## Forget mode reminder logic:
- Daily active user (active for 2/5 working days each in the past 2 weeks)
- Has not connected to the app on a weekday
- Around the time the user normally connects the device. Go by the average time they are going to connect
## 6. Analytics & Instrumentation

| Event Name                     | When It Triggers                    | Properties                                |
| ------------------------------ | ----------------------------------- | ----------------------------------------- |
| `forget_mode_prompt_displayed` | On app load when Neo 1 not detected | user_id, timestamp                        |
| `forget_mode_started`          | User taps “Forgot Neo 1?”           | device_status, session_id                 |
| `transcibing_started`          | Tap on Start                        | permission_status, device_model           |
| `transcribing_stopped`         | Tap on Stop                         | duration, interruption_flags              |
| `memory_generated`             | Audio successfully transcribed      | memory_id, length_sec, source = "phone"   |
| `forgot_mode_abandoned`        | User exits without started          | reason (denied_permission, cancel, error) |
| `calendar_based_reminder_sent` | Event starts, no Neo connected      | event_time, user_action_taken             |
|                                |                                     |                                           |
subcategory of mixpanel events too
---

## 7. Constraints

| Scenario                    | UX/Tech Response                                       | Notes                                                                          |
| --------------------------- | ------------------------------------------------------ | ------------------------------------------------------------------------------ |
| Device not connected        | Show fallback prompt                                   | Triggered only if user has prior Neo history                                   |
| Phone call during recording | Auto pause and resume logic                            | OS-level interruptions                                                         |
| App backgrounded            | Persistent OS notification                             | Ensure recording does not stop and remonds user that the recording is underway |
| Mic permissions denied      | Error prompt with retry                                | Onboarding edge case                                                           |
| Playback detection          | Alert user that the recording quality will be affected | Prevent                                                                        |


## 9. 📈 Success Metrics

- **< 5% failure rate** in audio upload or transcription.
    
- **> 80% completion rate** for fallback recordings started.
    
- **20% adoption** by active users with calendar integrations.
    
- **< 3 sec** median latency from tapping "Start" to recording start.