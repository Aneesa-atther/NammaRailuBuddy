# NammaRailuBuddy 🚂

> A community-powered Android application designed to assist local passenger train commuters in navigating small and mid-size railway stations with real-time platform information, coach-position guidance, and crowd-sourced delay updates.

**Platform:** Android (API 26+) | **Track:** GenAI | **Category:** Infrastructure  
**Version:** 1.0 | **Status:** In Development

---

## 📋 Table of Contents

- [About](#about)
- [Problem Statement](#problem-statement)
- [Key Features](#key-features)
- [Vision & Impact](#vision--impact)
- [Tech Stack](#tech-stack)
- [Installation](#installation)
- [Usage & User Flow](#usage--user-flow)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Development Timeline](#development-timeline)
- [Success Criteria](#success-criteria)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## 🚀 About

**NammaRailuBuddy** is an Android application built specifically for first-time and infrequent train travellers, particularly rural-to-city workers who struggle with navigating small and mid-size railway stations in India.

The app addresses the critical gap where local passenger trains lack clear digital signage, reliable announcements, and coach-position information. By combining **Firebase real-time database**, **GPS geofencing**, and **crowd-sourced intelligence**, NammaRailuBuddy makes railway navigation accessible to everyone—regardless of literacy or technical familiarity.

This is a **public-service utility** project, not a commercial product, and positions itself as a critical tool for improving the daily commute experience.

---

## 🎯 Problem Statement

Local passenger trains are the lifeline for millions of rural-to-city workers in India, yet the station experience is riddled with friction:

- **Confusing Platforms** — Small stations rarely have clear digital displays
- **Inaudible Announcements** — Crowd noise and poor PA systems make announcements unreliable
- **No Coach-Position Data** — Passengers don't know where the General or Ladies coach will stop
- **Missed Trains** — Sleeping commuters on long journeys miss their destination stops
- **Information Gap** — No app specifically addresses rural/suburban passenger train travel

**NammaRailuBuddy solves these pain points** with accessible, offline-first technology.

---

## ✨ Key Features

### MVP (Must-Have)

✅ **Destination Alarm**
- GPS-triggered alarm fires when user is within 5 km of destination
- Works with screen off
- Uses Android Geofencing API + FusedLocationProviderClient
- Includes audible alert + vibration
- < 200 m GPS accuracy required

✅ **Platform Ping**
- Community members post the platform number for arriving trains
- Other users confirm (upvote) in real-time
- Live confirmation counter shows validation count
- Powered by Firebase Realtime Database
- Anonymous contributions allowed

✅ **Coach Position Viewer**
- Visual, scrollable diagram of train coach layout
- Colour-coded by type: General (Blue), Ladies (Pink), Sleeper (Green)
- Clear position labels: "General Coach — Front (Engine Side)"
- Works offline with cached data

✅ **Station & Train Search**
- Search any Indian local railway station by name or code
- Look up trains for selected route within 2 hours
- Integrated with NTES/IRCTC APIs (fallback to cached data)

### Phase 2 (Good-to-Have)

⭐ **GenAI Journey Assistant**
- Natural-language queries: "Which coach should I board for Mandya?"
- Powered by Google Gemini API with on-device reasoning
- RAG (Retrieval-Augmented Generation) on coach layout data

⭐ **Smart Crowd Alerts**
- ML prediction of crowding levels based on historical data
- Time-of-day based alerts
- Powered by Firebase ML

⭐ **Visual Coach AR Overlay**
- Augmented reality arrow pointing to correct coach position
- Uses device camera + ARCore

⭐ **Offline Speech Announcements**
- Text-to-speech in user's language (Kannada, Tamil, Hindi, English)
- Works without internet

⭐ **Delay Heatmap**
- Visual heatmap of frequently delayed trains by route
- Built from crowd-sourced data

⭐ **Station Community Board**
- Hyperlocal message board per station
- Passengers share tips, lost-and-found, cautions

---

## 🎯 Vision & Impact

NammaRailuBuddy envisions a future where **any commuter—regardless of literacy, technology familiarity, or language—can board the right coach, on the right platform, without stress.**

| Goal | Impact |
|------|--------|
| **Efficient Transport** | Reduce missed trains and platform confusion for daily workforce |
| **Public Service** | Improve station experience of common citizens |
| **Digital Inclusion** | Accessible to first-time and infrequent travellers |
| **Community Power** | Leverage crowd-sourcing to fill data gaps where official APIs absent |

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Language** | Kotlin 1.9+ | Primary Android development |
| **Architecture** | MVVM + Clean Architecture | Separation of concerns, testability |
| **UI** | Jetpack Compose / XML Layouts | High-contrast coach visualization, Station screens |
| **Location** | Google Fused Location + Geofencing API | Destination alarm trigger at 5 km radius |
| **Real-time DB** | Firebase Realtime Database | Platform Ping crowd-sourcing |
| **Authentication** | Firebase Anonymous Auth | Allow contributions without forced sign-up |
| **Local DB** | Room (SQLite) | Offline station and train data cache |
| **Networking** | Retrofit 2 + OkHttp | NTES / IRCTC API calls |
| **Background** | WorkManager | Persistent alarm even after app killed |
| **Dependency Injection** | Hilt | Dependency injection across modules |
| **Testing** | JUnit 5 + Mockk + Espresso | Unit + UI tests for alarm and ping modules |
| **GenAI** | Google Gemini API | Natural-language journey assistant |

### Minimum Requirements
- **Android:** API 26 (Android 8.0) and above
- **RAM:** 2 GB (mid-range device target)
- **Connectivity:** Works offline; Firebase sync when connected

---

## 📦 Installation

### Prerequisites

- Android Studio (latest version)
- Android SDK API 26+
- Kotlin 1.9+
- Git
- Firebase project credentials (see setup below)

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/Aneesa-atther/NammaRailuBuddy.git
   cd NammaRailuBuddy
   ```

2. **Open in Android Studio**
   - File → Open → Select the project directory
   - Let Gradle sync automatically

3. **Firebase Setup**
   - Create a Firebase project at [console.firebase.google.com](https://console.firebase.google.com)
   - Download `google-services.json`
   - Place in `app/` directory
   - Enable Firebase Realtime Database and Anonymous Authentication

4. **Gemini API Setup (Optional for Phase 2)**
   - Get API key from [Google AI Studio](https://makersuite.google.com/app/apikey)
   - Add to `local.properties`:
     ```properties
     GEMINI_API_KEY=your_api_key_here
     ```

5. **Build and Run**
   ```bash
   ./gradlew build
   ./gradlew installDebug
   ```
   Or directly from Android Studio: **Run → Run 'app'**

---

## 💻 Usage & User Flow

### 1. Launch & Station Select
```
User opens app → Searches for boarding station (e.g., Mandya, Birur) → Selects train
```

### 2. View Coach Position
```
App displays vertical coach layout diagram
General/Ladies/Sleeper coaches are colour-coded
Label shows: "General Coach — Front (Engine Side)"
```

### 3. Platform Ping
```
Community posts: "Train arriving on Platform 2"
Other users confirm (+1)
Counter displays: "Confirmed by 7 users"
Updates in real-time
```

### 4. Set Destination Alarm
```
User selects destination station → Arms proximity alarm
App runs in background
```

### 5. Alarm Triggers
```
Device enters 5 km geofence of destination
Loud alarm + vibration fires (even screen off)
User wakes and gets off at correct station
```

---

## 🏗️ Architecture

### MVVM + Clean Architecture

```
├── Data Layer
│   ├── Local (Room DB)
│   ├── Remote (Firebase, Retrofit APIs)
│   └── Repository (abstraction)
│
├── Domain Layer
│   ├── Use Cases (business logic)
│   └── Entities
│
├── Presentation Layer
│   ├── ViewModels (state management)
│   ├── UI Screens (Compose/XML)
│   └── Navigation
```

### Key Design Patterns

- **MVVM:** ViewModel + LiveData for state management
- **Dependency Injection:** Hilt for loose coupling
- **Repository Pattern:** Unified data access
- **Offline-First:** Local Room DB with Firebase sync
- **WorkManager:** Background alarm execution

---

## 📂 Project Structure

```
NammaRailuBuddy/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── kotlin/
│   │   │   │   └── com/namma_railu_buddy/
│   │   │   │       ├── data/              # Repositories, API, Room DB
│   │   │   │       ├── domain/            # Use cases, entities
│   │   │   │       ├── presentation/      # ViewModels, UI
│   │   │   │       │   ├── screens/       # Composables/Activities
│   │   │   │       │   └── components/    # Reusable UI components
│   │   │   │       ├── service/           # Background services
│   │   │   │       └── utils/             # Helpers, extensions
│   │   │   └── res/
│   │   │       ├── layout/                # XML layouts
│   │   │       ├── values/                # Strings, colors, styles
│   │   │       └── drawable/              # Icons, images
│   │   └── test/ & androidTest/           # Unit & UI tests
│   ├── build.gradle.kts                   # App-level dependencies
│   └── google-services.json                # Firebase config
│
├── build.gradle.kts                       # Project-level config
├── settings.gradle.kts                    # Module configuration
├── gradle.properties                      # Gradle settings
├── README.md                              # This file
├── PDR.pdf                                # Product Design & Requirements
└── LICENSE
```

---

## 🎬 Development Timeline

| Week | Milestone | Deliverable |
|------|-----------|------------|
| 1–2 | **Foundation** | Project setup, MVVM architecture, Room DB with station data, UI skeleton |
| 3–4 | **Core Features** | Station search, coach layout visualization, offline data sync |
| 5–6 | **Platform Ping** | Firebase integration, anonymous auth, real-time confirmation counter |
| 7–8 | **Destination Alarm** | Geofencing setup, WorkManager service, alarm UI |
| 9 | **GenAI Integration** | Gemini API — natural-language journey assistant (good-to-have) |
| 10 | **Polish & Test** | Accessibility audit, WCAG contrast check, unit + UI tests, performance profiling |
| 11 | **Submission** | APK build, demo video, final README, PDR submission |

---

## ✅ Success Criteria

### Destination Alarm Accuracy
- Alarm MUST trigger within 5 km radius with < 200 m GPS error
- 95% success rate on at least 3 device types
- Vibration + sound work with screen off

### Platform Ping Confirmation Count
- Real-time display of confirmation count
- Update within < 3 seconds across devices
- Clear visual feedback on upvote

### UI Contrast & Readability
- All primary text meets WCAG AA contrast ratio (4.5:1 minimum)
- Font size ≥ 16sp for key labels
- Usable in bright outdoor sunlight (100% brightness)

### Offline Fallback
- Coach position data available without internet
- Graceful degradation on network loss
- No crashes on connectivity interruption

### Performance
- Cold start < 2 seconds on 2 GB RAM device
- Platform Ping list loads < 1.5 seconds on 4G
- Battery drain < 3% per hour with active alarm

### Accessibility
- Screen-reader (TalkBack) support for all interactive elements
- High-contrast mode toggle in settings
- All strings externalized (no hard-coded UI text)

---

## 🚨 Known Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|-----------|
| GPS inaccuracy in tunnels/rural areas | Medium | High | Fallback to cell-tower/WiFi; expand geofence to 7 km in low-signal zones |
| Firebase rate limits with large concurrent users | Low | High | Client-side debouncing; Firebase rules to throttle writes per user |
| Spam/fake Platform Pings | High | Medium | Require anonymous auth; auto-expire after 30 min; flag outliers |
| IRCTC/NTES API unavailability | Medium | High | Cache last-known data locally; fallback to community-entered timetables |
| Background alarm killed by battery optimization | High | High | Use WorkManager with FOREGROUND service; prompt to disable battery optimization |

---

## 🤝 Contributing

We welcome contributions from developers, testers, and the community!

### How to Contribute

1. **Fork** the repository
2. **Create** a feature branch
   ```bash
   git checkout -b feature/YourFeature
   ```
3. **Commit** your changes with clear messages
   ```bash
   git commit -m "Add: [Feature description]"
   ```
4. **Push** to your branch
   ```bash
   git push origin feature/YourFeature
   ```
5. **Open** a Pull Request

### Guidelines

- Follow Kotlin style guide ([kotlinlang.org](https://kotlinlang.org/docs/coding-conventions.html))
- Write unit tests for new features (target > 60% coverage)
- Update documentation
- Test on API 26+ devices
- Use meaningful commit messages

### Areas We Need Help

- UI/UX design and testing
- Backend optimization (Firebase rules)
- Localization (new language support)
- Accessibility improvements
- Performance optimization

---

## 📝 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

This project is intended for educational purposes and community benefit.

---

## 👤 Contact & Contributors

**Project Lead:** Aneesa Atther
- **GitHub:** [@Aneesa-atther](https://github.com/Aneesa-atther)
- **Email:** [Your email here]

**Track:** GenAI Android Development | **Category:** Infrastructure  
**Submission Deadline:** April 2026

---

## 📚 Additional Resources

- **Product Design & Requirements Document:** See [PDR.pdf](./PDR.pdf)
- **Android Geofencing API:** [developer.android.com](https://developer.android.com/training/location/geofencing)
- **Firebase Realtime Database:** [firebase.google.com/docs/database](https://firebase.google.com/docs/database)
- **Google Gemini API:** [ai.google.dev](https://ai.google.dev)
- **WCAG 2.1 Accessibility:** [w3.org/WAI/WCAG21](https://www.w3.org/WAI/WCAG21/quickref/)
- **Namma Railu Campaign:** [praja.in](https://www.praja.in/)

---

## 🙏 Acknowledgments

- **Namma Railu Community** — For the vision of better public transport in Bengaluru
- **First-time Commuters & Rural Workers** — Whose struggles inspired this solution
- **Open Source Community** — Firebase, Android Jetpack, Kotlin developers
- **Accessibility Advocates** — For guidance on inclusive design

---

## 📌 Quick Start Checklist

- [ ] Clone the repository
- [ ] Set up Firebase credentials
- [ ] Build project in Android Studio
- [ ] Install APK on test device
- [ ] Test Station Search feature
- [ ] Test Destination Alarm with GPS
- [ ] Test Platform Ping real-time updates
- [ ] Verify offline functionality

---

**Status:** 🔨 **In Active Development**

For questions or support, open an issue on GitHub or reach out to the development team.

**Last Updated:** April 2026 | **PDR Version:** 1.0

