# SARA — Voice Assistant with Full Phone Control (Android)

## Setup (Android Studio)

1. Android Studio kholo → **Open** → is `SaraAssistant` folder ko select karo.
2. Gradle sync hone do (pehli baar thoda time lega, internet chahiye).
3. Phone ko USB se connect karo, USB Debugging on karo (Settings > Developer Options).
4. Run button dabao (▶) — app phone par install ho jayegi.

## First-time app setup (zaroori)

1. App kholte hi permissions maango (mic, calls, SMS) — sab **Allow** karo.
2. **"Enable Full Control (Accessibility)"** button dabao → yeh Settings > Accessibility kholega.
   - List me **SARA** dhoondo → usko **ON** karo.
   - Bina is step ke: back/home/recents/screenshot/click-on-text commands kaam nahi karenge.
   - Yeh Android security ki wajah se manually hi karna padta hai — koi app khud-ba-khud yeh permission nahi le sakti.

## Supported voice commands (abhi ke liye)

| Bolo (English) | Kya hoga |
|---|---|
| "call 9876543210" | Us number par call lagegi |
| "message 9876543210 hello" | SMS app khulega text ke saath |
| "open whatsapp" / "open camera" | Wo app khulega |
| "search cricket score" | Google search khulega |
| "go back" | Back button jaisa kaam |
| "go home" | Home screen par jayega |
| "recent apps" | Recents screen khulega |
| "notifications" | Notification panel khulega |
| "screenshot" | Screenshot le lega |
| "click on Send" | Screen par "Send" likha element dhoond kar tap karega |
| "wifi" / "bluetooth" | Respective settings khulenge |
| "flashlight on" / "flashlight off" | Torch on/off |
| "volume up" / "volume down" | Volume control |
| "set alarm for 7 30" | 7:30 ka alarm set karega |
| "battery" | Battery percentage bolega |

## Naye commands add karna

`CommandProcessor.kt` file me `process()` function ke andar naya `when` branch add karo. Example:

```kotlin
text.contains("play music") -> {
    // apna intent/logic yahan likho
    "Playing music"
}
```

## Important notes

- **Hindi voice input** ke liye `MainActivity.kt` me `EXTRA_LANGUAGE` ko `"hi-IN"` kar do.
- Kuch commands (jaise WiFi/Bluetooth ko seedha ON/OFF karna, bina settings khole) newer Android versions (10+) me apps ko allow nahi hai — security restriction hai, isliye hum settings screen kholte hain.
- "click on X" command sirf tab kaam karega jab woh text screen par visible ho aur Accessibility Service ON ho.
- Yeh ek MVP (starting point) hai — production-ready banane ke liye error handling, wake-word detection ("Hey Sara"), aur offline speech recognition add kar sakte ho.

## Project structure

```
SaraAssistant/
├── app/
│   ├── build.gradle
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/sara/assistant/
│       │   ├── MainActivity.kt              → UI, mic, TTS, speech recognition
│       │   ├── CommandProcessor.kt          → command parsing + actions (the "brain")
│       │   └── SaraAccessibilityService.kt  → deep control (back/home/tap elements)
│       └── res/
│           ├── layout/activity_main.xml
│           ├── values/strings.xml, themes.xml
│           └── xml/accessibility_service_config.xml
├── build.gradle
└── settings.gradle
```
