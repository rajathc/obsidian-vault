**Husain: 1.3.2(1)**: 
**Rajath: 1.3.2(6)**: The backend is not receiving data or going into the transcribe state upon reconnecting
**Manas: App Store**:
**Priyanshu: 1.3.2(9)**:


- Transcribing mode directly after sleep mode. The previous state will persist.
- Epoch Timestamp from the app

Tasks:
- App:
	- update the opus decoder logic to send packets in 10 second interval. make sure that there are no frame drop related issues