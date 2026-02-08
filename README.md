# News App

An Android news reader that fetches top headlines from [NewsAPI.org](https://newsapi.org). Users can browse news by category, search by keyword, and view full article details.

---

## Features

- **Top Headlines** — Load latest news for India on launch
- **Category Filter** — business, entertainment, general, health, science, sports, technology
- **Search** — Search news by keyword
- **Article Details** — Tap any headline to view full article (title, author, time, description, content, image)
- **Edge-to-edge UI** — Full-screen layout with proper system bar handling

---

## Tech Stack

| Technology | Purpose |
|------------|---------|
| **Retrofit** | REST API calls & JSON parsing (Gson) |
| **Picasso** | Image loading from URLs |
| **RecyclerView** | Scrollable list of headlines |
| **NewsAPI.org** | News data source |

---

## Android Concepts Implemented

### Core Topics

- **Activities** — MainActivity (launcher), DetailsActivity (article details)
- **Intents** — Passing `NewsHeadlines` between activities via `putExtra` / `getSerializableExtra`
- **Layouts** — LinearLayout, HorizontalScrollView, CardView, RecyclerView, SearchView
- **RecyclerView** — CustomAdapter, CustomViewHolder, GridLayoutManager
- **Manifest** — Activity registration, launcher intent-filter, INTERNET permission
- **Resources** — strings, colors, themes, drawables, layouts
- **Build (Gradle)** — Dependencies, SDK versions, build types

### Advanced Topics

#### 1. Edge-to-Edge Display & Window Insets

Full-screen content with proper handling of system bars (status bar, navigation bar), notches, and gesture navigation using `EdgeToEdge.enable()` and `ViewCompat.setOnApplyWindowInsetsListener`.

#### 2. Retrofit Declarative API Definition

Interface-based API definition with annotations (`@GET`, `@Query`). Retrofit generates the implementation via dynamic proxy—no manual HTTP code.

#### 3. Callback/Listener Pattern for Async Updates

- `OnFetchDataListener` — Decouples `RequestManager` from `MainActivity`
- `SelectListener` — Handles headline click events
- Network runs off main thread; callbacks update UI on main thread

#### 4. RecyclerView Optimization

- `setHasFixedSize(true)` for layout optimization
- ViewHolder pattern for view recycling and avoiding repeated `findViewById`

#### 5. Resource Qualifiers (Night Mode)

`res/values/themes.xml` and `res/values-night/themes.xml` allow automatic dark theme switching based on system settings.

#### 6. Build Configuration & ProGuard

- Build variants (debug/release)
- ProGuard rules for release builds
- Version catalog (`libs.versions.toml`) for dependency management

#### 7. Serialization

`NewsHeadlines`, `Source`, and `NewsApiResponse` implement `Serializable` for passing data between activities via Intents.

---

## Project Structure

```
app/src/main/java/com/example/newsapp/
├── MainActivity.java          # Main screen (categories, search, list)
├── DetailsActivity.java       # Article detail screen
├── RequestManager.java        # Retrofit API calls
├── CustomAdapter.java         # RecyclerView adapter
├── CustomViewHolder.java      # RecyclerView ViewHolder
├── OnFetchDataListener.java   # API callback interface
├── SelectListener.java        # Item click interface
└── Models/
    ├── NewsApiResponse.java   # API response wrapper
    ├── NewsHeadlines.java     # Article model
    └── Source.java            # News source model
```

---

## Setup

1. Clone the repository
2. Open in Android Studio
3. Add your NewsAPI.org API key in `app/src/main/res/values/strings.xml`:
   ```xml
   <string name="api_key">YOUR_API_KEY</string>
   ```
4. Get a free API key at [newsapi.org](https://newsapi.org)
5. Build and run

---

## Requirements

- Android Studio
- minSdk 24
- targetSdk 34
- Java 8+

---

## API

Uses [NewsAPI.org Top Headlines](https://newsapi.org/docs/endpoints/top-headlines) endpoint with country set to India (`in`).
