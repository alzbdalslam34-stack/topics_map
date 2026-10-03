# TopicsMap: Store Approval & Compliance Manual

## 1. Google Play Console Foreground Service Declaration (Android 14+)
Google Play restricts foreground services. For TopicsMap, use the **connectedDevice** category:

### Google Play Console Policy Form Answers:
- **Foreground Service Type**: `connectedDevice`
- **Core Functionality Video**: Record a 30-second screen recording showing:
  1. The user saving a topic for a friend.
  2. The phone locking or switching to home screen.
  3. The target BLE device coming in range and the high-priority alarm notification popping up.
- **Justification Statement (Copy & Paste)**:
  > "TopicsMap is a proximity-based reminder tool that relies on real-time Bluetooth Low Energy (BLE) scanning to notify users when a specific person/colleague is physically nearby. Continuous background scanning via a Foreground Service (type: connectedDevice) is essential because standard background jobs are deferred by Android Doze mode, which causes missed proximity windows when walking past an associate."

---

## 2. Apple App Store Guidelines (Section 2.5.4 & 5.1.1)
Apple strictly audits `UIBackgroundModes` with `bluetooth-central`.

### In App Store Connect Review Notes:
- **How Bluetooth is used**:
  > "TopicsMap uses CoreBluetooth central background mode to continuously monitor for authorized BLE peripherals or device signatures registered by the user. When the specified signature is detected in physical proximity (within ~3 meters), a local notification is triggered containing discussion notes saved for that individual."
- **Privacy Policy**: Ensure your privacy policy states that:
  > "All Bluetooth identifiers and notes remain strictly on-device in local storage. No location coordinates or biometric identifiers are uploaded or shared with 3rd parties."

---

## 3. Battery Optimization Exemption
When onboarding the user on Android:
```dart
import 'package:permission_handler/permission_handler.dart';

// Request battery optimization exemption
if (await Permission.ignoreBatteryOptimizations.isDenied) {
  await Permission.ignoreBatteryOptimizations.request();
}
```