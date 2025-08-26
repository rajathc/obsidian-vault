**Mixpanel Project Token:** 0e8237feaad2c70c21cd1e5c7cf95278

### **1. Install Mixpanel**

Add to `pubspec.yaml`:

```
dependencies:
  mixpanel_flutter: ^2.2.0
```

Run:

```
flutter pub get
````

### 2. Initialize Mixpanel (inside `main.dart` )

```
import 'package:flutter/material.dart';
import 'package:mixpanel_flutter/mixpanel_flutter.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await initializeMixpanel();
  runApp(MyApp());
}

late Mixpanel mixpanel;
DateTime? sessionStartTime;

Future<void> initializeMixpanel() async {
  mixpanel = await Mixpanel.init(0e8237feaad2c70c21cd1e5c7cf95278, optOutTrackingDefault: false);
  mixpanel.track("App Opened");  // Track when the app opens
  sessionStartTime = DateTime.now(); // Start session tracking
}

```

### 3. Track Session Duration (inside `dispose()`)

```
@override
void dispose() {
  if (sessionStartTime != null) {
    final sessionEndTime = DateTime.now();
    final sessionDuration = sessionEndTime.difference(sessionStartTime!).inSeconds;
    mixpanel.track("Session Ended", properties: {"Duration (s)": sessionDuration});
  }
  
  mixpanel.flush(); // Ensure all events are sent before closing the app
  super.dispose();
}

```

### 4. Track Neo AI & Memories Tab Opens

#### A. Define Tracking Functions

Add these fucntions to track how many times a user opens these tabs:

```
void trackNeoAITabOpened() {
  mixpanel.track("Neo AI Tab Opened");
}

void trackMemoriesTabOpened() {
  mixpanel.track("Memories Tab Opened");
}

```

#### B. Implement in Bottom Navigation Bar

Modify `onTap` in the `BottomNavigationBar`:

```
BottomNavigationBar(
  currentIndex: _selectedIndex,
  onTap: (index) {
    setState(() {
      _selectedIndex = index;
    });

    if (index == 1) {
      trackNeoAITabOpened();
    } else if (index == 2) {
      trackMemoriesTabOpened();
    }
  },
  items: [
    BottomNavigationBarItem(icon: Icon(Icons."replace with our icons"), label: "Home"),
    BottomNavigationBarItem(icon: Icon(Icons."replace with our icons"), label: "Neo AI"),
    BottomNavigationBarItem(icon: Icon(Icons."replace with our icons"), label: "Memories"),
  ],
);

```

Replace the `"replace with our icons"` with our actual code.

### **5. Track Button Clicks**

Modify and add this to our Tap to reconnect button.

```
void trackButtonClick(String buttonName) {   mixpanel.track("Button Clicked", properties: {"button_name": buttonName}); }
```

**Example usage in UI:**

```
ElevatedButton(   onPressed: () {     trackButtonClick("Subscribe");   },   child: Text("Subscribe"), )
```