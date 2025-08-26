**Northstar of the Product Experience:** Work seamlessly. Connect and forget.

### **Current Issues:**
**Disconnects**
- App freezes randomly, and users don’t even realise it, it just quietly stops working and they think the product is faulty.
- The app gets killed, especially on Android. People assume it’s a hardware issue, not a background execution problem.
- Regular activities like running, sitting in a car, or riding a bike are enough to disconnect the device. That's not okay.

**Battery**
- Devices are disconnecting mid-meeting because the battery indicator isn’t accurate.
- No battery level is shown on the device itself, this is causing serious battery anxiety. Users are constantly opening the app just to check. If the battery is adequate during important meetings.

**Memory Generation**
- Memory creation has been spotty. A bunch of different things are going wrong:
    - Longer meetings are getting split into multiple memories.
    - Contextual accuracy of names and numbers is off.
    - Transcript quality is poor, especially for people who aren’t the main speaker. They’re often just garbled or missed.

### **Improvements (App-side – doable on existing V1 hardware):**

**Disconnects**
- App freeze needs to go. We need more robust state handling.
- Use AlarmManager, FCM, and WorkManager properly to keep the Android app alive.
- Adjust the IMU sensor thresholds to account for real-world motion. We can also add a low-pass filter to reduce rapid/noisy inputs.

**Battery**
- Accurate battery reporting is non-negotiable.
- Push battery level alerts and low-battery warnings to the app so the user isn't left guessing.

**Memory**
- We _must_ aim for 95%+ transcript accuracy. It's a key part of perceived product quality.
- Handle disconnects better. We must store short-term audio chunks locally before streaming (if this isn’t already being done).
- Improve name and number parsing. These tiny contextual things are what make or break the trust in memory quality.

### **Improvements (Hardware-side for V2):**

**Disconnects**
- A physical toggle to turn the device on gives users more confidence that it's working.
- Adding flash storage can help with short-term offline mode. So temporary disconnects don’t ruin the experience.

**Battery**
- Add an RGB LED with a standard light pattern to indicate battery status. This lets people glance and know. No screen is needed.
- A bigger battery is a must. Some users are out for 12+ hours. Right now they’re limiting usage to work hours. If we can hit 20+ hours, people will use the device throughout the day and charge overnight, which will help people to use their device beyond the work settings.

**Memory**
- Flash memory is essential, especially for cases where users move out of Bluetooth range or when the users are not in a network zone.
- Better mic array to catch _everyone_ in the room. Needs to handle bigger rooms and multiple voices, not just the closest speaker.

**Other nice-to-have hardware improvements for a truly seamless experience:**
- **IP rating:** Just removes the mental load of being careful all the time. People can use it like any other daily device.
- **Alternative mounting options (tentative):** A few users want different mounting styles during meetings. Might be a symptom of poor mic pickup, so fix the mic and this becomes irrelevant. But still worth thinking about.