Northstar of the App: Work seamlessly. Connect and forget

Issues facing right now:
- Disconnects
	- App freeze, and customers are not realising it and thinking it is a product issue
	- App kill, espcailly on android. This is making people think that issue is with the device connectivity
	- Simple running, travelling by car, travelling by motorcycle can turn off the device
- Battery
	- Device disconnected mid-meeting because the battery indicator is not accurate
	- No battery indicator on the device, leading to batteyr anxeity for the customer and they have to check in the application frequently
- Memory Generating:
	- Memory generations have been iffy due to multiple reasons.
	- Memories are being split into multiple memories
	- The name and number contextual accuracy has been poor
	- Transcript accuracy has been bad
	- Transcript of non speaker are bad

Improvements (app side can be implemented on V1 hardware):

Disconnects: 
- App freeze should not exist. we need to handle the states better
- Implementing Alarm manager, fcm and work manager to keep the android app from being killed.
- Modifying the sensitivity of the sensor IMU sensor based on the real world usage. Turning the threshold and add low-pass filter to remove the rapid changes.
Battery:
- Getting the accurate battery levels is a must.
- In addition we can offer battery warnings of the device on the phone.
Memory:
- Transcript accuracy must be close to 95%. The transcript accuracy must impress people only then will our product perception will be good.
- Better handling of disconnects and if possible we can try to store some chunks of data locally before streaming(if not implemented already)
- The name and number needs to be 

Improvements (Hardware)
Disconnects:
- Toggle to turn the device on, offers confidence for the users. They can be sure that the device is on
- We can add flash memory to let the device run in offline more, so that the slight disconnect doesn't impact the device experience.
Battery:
- Having RGB led with existing standard for light indicators will benifit people from not looking at the screen to check for the battery
- Bigger battery would be a plus, because some of our customers have 12+ hours of day. Due to the short battery life people are using it only during their office hours, if we have the battery benchmark of 20+ hours. We would see people use the device beyond their office hours and charge the device while they go to sleep.
Memory:
- the device needs to have flash memory to handle the issues when people go out of range of Bluetooth.
- Better mic array to capture the audio of rest of the speakers, if the microphone can capture the larger meeting rooms that would be ideal too.
- 

Other good to-have hardware improvements which can help with device working seemlessly:
- IP rating so that people have less anxiety while using the product on a day-to-day basis
- Different mounting methods(debatable) Due to the limitations of the mic the customers are asking for different mounting methods for the device during the meeting. This should not be an issue if we fix our microphone

