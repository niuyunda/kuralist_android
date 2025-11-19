# Kuralist Android

**Kuralist** is a New Zealand school information platform built for Android. It provides a comprehensive offline-first experience for exploring and managing school data.

## Features

*   **Offline-First Architecture**: Browse and search for schools without an internet connection.
*   **School Directory**: Access detailed information for ~2,500 New Zealand schools.
*   **Interactive Maps**: View school locations on an integrated Google Map.
*   **Authentication**: Secure user login and data synchronization via Supabase.
*   **Modern UI**: Built with Jetpack Compose and Material 3 for a fluid, native experience.

## Tech Stack

*   **Language**: [Kotlin](https://kotlinlang.org/)
*   **UI Toolkit**: [Jetpack Compose](https://developer.android.com/jetpack/compose) (Material 3)
*   **Architecture**: MVVM (Model-View-ViewModel) with Repository pattern
*   **Local Database**: [Room](https://developer.android.com/training/data-storage/room)
*   **Backend & Auth**: [Supabase](https://supabase.com/)
*   **Networking**: [Ktor](https://ktor.io/) (Supabase client) & [Retrofit](https://square.github.io/retrofit/)
*   **Maps**: [Google Maps Compose](https://github.com/googlemaps/android-maps-compose)
*   **Asynchronous**: Kotlin Coroutines & Flow

## Prerequisites

To build and run this project, you will need:

*   **Android Studio**: Koala or newer is recommended.
*   **JDK**: Version 11 or newer.
*   **Android SDK**: API Level 35 (Target), API Level 29 (Min).

## Configuration

> [!NOTE]
> **Important**: API keys for Supabase and Google Maps are currently configured directly in `app/build.gradle.kts`.

Ensure you have the following keys configured in your build environment (already present in the repository for this version):
*   `SUPABASE_URL`
*   `SUPABASE_ANON_KEY`
*   `GOOGLE_MAPS_API_KEY`

## Build & Run

1.  **Clone the repository**:
    ```bash
    git clone <repository-url>
    cd kuralist_android
    ```

2.  **Open in Android Studio**:
    Open the `kuralist_android` directory as an existing Android Studio project.

3.  **Build the project**:
    You can build the project using the Gradle wrapper from the command line:
    ```bash
    ./gradlew assembleDebug
    ```

4.  **Run on Device/Emulator**:
    Select your connected device or emulator in Android Studio and click **Run** (Shift+F10).

## Architecture Overview

The app follows a strict **Offline-First** principle:

1.  **UI Layer**: ViewModels observe data from Repositories and expose UI State (via `StateFlow`) to Compose screens.
2.  **Data Layer**:
    *   **Repositories** act as the single source of truth.
    *   **Local Data**: The app primarily reads from the local Room database (`SchoolDatabase`).
    *   **Remote Sync**: The `SupabaseManager` handles background synchronization to fetch updates from the remote Supabase instance and update the local database.

## Project Structure

*   `app/src/main/java/com/kuralist/app/`
    *   `features/`: Contains UI screens and ViewModels, organized by feature (e.g., `auth`, `schoollist`, `map`).
    *   `core/`: Shared components, models, and services.
        *   `models/`: Data classes and entities.
        *   `services/`: Business logic and data repositories.
        *   `database/`: Room database configuration and DAOs.
