# 📑 Project Documentation: WatchHub App

WatchHub is an Android-based entertainment catalog application that integrates movie and anime data into a dynamic interface ecosystem. This project focuses on the implementation of **Clean UI**, **Fragment State** navigation management, and an advanced **System Localization** engine.

---

## 🏛️ 1. Software Architecture

The application is built using the **Imperative UI** pattern with the **Java** programming language. The core structure is based on the following components:

### A. Fragment Navigation Pattern (Container-Based)
Unlike traditional applications that switch between multiple Activities (which is memory-intensive), WatchHub utilizes a "Single Activity" approach. `MainActivity` acts as a host for a `FrameLayout` container. Content is swapped dynamically without destroying the Activity, ensuring smoother transitions and efficient resource management.



### B. Navigation State Management
The app manages navigation button states manually to ensure synchronized visual feedback. When a user switches tabs, the system executes logic to update text colors, backgrounds, and icons in real-time based on the selected View ID.

---

## 🛠️ 2. Detailed Technical Components

### 📂 MainActivity.java (The Orchestrator)
The central brain of the application that handles the main UI flow.
- **Navigation Logic**: Implements `View.OnClickListener` to detect interactions on Movie, Anime, and Watchlist buttons, triggering the `loadFragment()` function.
- **Optimization**: Uses `if (savedInstanceState == null)` checks in `onCreate` to prevent fragment duplication during screen rotations.
- **UI Refresh**: The `updateButtonState()` method manages `ColorStateList` and `BackgroundTint` dynamically to provide an elegant visual indicator of the active tab.

### 📂 ProfileActivity.java (The Configuration Hub)
Handles user interactions and system configuration preferences.
- **Back Stack Management**: Utilizes `finish()` to return to the previous screen, ensuring the memory stack remains clean.
- **Logout Sequence**: Implements `FLAG_ACTIVITY_NEW_TASK | FLAG_ACTIVITY_CLEAR_TASK` flags during logout to prevent users from navigating back to protected screens after session termination.

### 📂 LocaleHelper.java (The Localization Engine)
An advanced utility component designed to handle on-the-fly language changes without relying on system-wide settings.
- **Context Wrapper**: Uses `createConfigurationContext`. In modern Android APIs, changing the language requires wrapping the Context to ensure that the correct new Resource Strings are loaded into the UI.

---

## 🎨 3. UI/UX Breakdown

### Dynamic Layouting
The app utilizes **ConstraintLayout** as the root element for maximum flexibility.
- **Performance**: Reduces "Nested Layouts," which significantly speeds up UI rendering by the GPU.
- **Responsiveness**: Uses `app:layout_constraintDimensionRatio` and horizontal/vertical bias to ensure the UI remains symmetrical across various screen aspect ratios.



### Visual Elements
- **CardView**: Applied to profile pictures to create a circular clipping effect and provide "Elevation" (shadows), giving elements a modern "floating" look.
- **Selector Drawables**: Implemented on buttons to automatically trigger color transitions during "Pressed" or "Selected" states.

---

## 🌐 4. Localization System

The application is mapped for global scalability. The resource structure is as follows:

| Folder | Target Language | Description |
|---|---|---|
| `values/` | **Default (English)** | Used as a fallback if other languages are unavailable. |
| `values-in/` | **Indonesian** | Customized localization for local Indonesian users. |
| `values-ja/` | **Japanese** | Optimized for Kanji/Kana character rendering. |
| `values-ru/` | **Russian** | Accommodates Cyrillic alphabet characters. |
| `values-de/` | **German** | Handles linguistically longer German compound words. |

---

## 📂 5. Project Directory Structure

```text
WatchHub/
├── .gradle/                  # Automated build configurations
├── app/
│   ├── src/main/
│   │   ├── java/com/example/watchhub/
│   │   │   ├── fragments/    # Modular content (Movie, Anime, Watchlist)
│   │   │   ├── MainActivity  # Main navigation logic
│   │   │   ├── ProfileActivity# User profile & settings logic
│   │   │   └── LocaleHelper  # Language switching engine
│   │   ├── res/
│   │   │   ├── drawable/     # Vector assets (SVG/XML) and images
│   │   │   ├── layout/       # UI definitions (XML)
│   │   │   ├── menu/         # Navigation menu definitions
│   │   │   └── values/       # Colors, Strings, and Themes
│   │   └── AndroidManifest.xml# Activity registration & Permissions
│   └── build.gradle          # Third-party libraries & SDK versions
└── README.md                 # Project documentation
