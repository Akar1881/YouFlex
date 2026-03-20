# YouFlex — Complete Project Wiki

> Last updated: March 2026  
> Platform: **Android** (iOS and Desktop planned — see roadmap at the bottom)  
> Built with: React Native / Expo

---

## Table of Contents

1. [What Is YouFlex?](#1-what-is-youflex)
2. [Is This Legal?](#2-is-this-legal)
3. [How to Install on Android](#3-how-to-install-on-android)
4. [The App at a Glance — Navigating the UI](#4-the-app-at-a-glance--navigating-the-ui)
5. [Home Screen — Everything That Loads on Startup](#5-home-screen--everything-that-loads-on-startup)
6. [Search — How to Find Anything](#6-search--how-to-find-anything)
7. [Movies Tab](#7-movies-tab)
8. [TV Shows Tab](#8-tv-shows-tab)
9. [Anime Tab](#9-anime-tab)
10. [Profile Tab — TMDB Account Integration](#10-profile-tab--tmdb-account-integration)
11. [Settings Tab — Full Breakdown of Every Option](#11-settings-tab--full-breakdown-of-every-option)
12. [Details Page — Everything About a Title](#12-details-page--everything-about-a-title)
13. [Actor / Person Pages](#13-actor--person-pages)
14. [The Watch Screen — Before You Press Play](#14-the-watch-screen--before-you-press-play)
15. [The Scraping System — How Streams Are Found](#15-the-scraping-system--how-streams-are-found)
    - [Alpha — Vidlink](#alpha--vidlink)
    - [Omega — YFlix](#omega--yflix)
    - [Neon — Videasy](#neon--videasy)
    - [4K — 4KHDHub](#4k--4khdhub)
    - [Gamma — Castle](#gamma--castle)
    - [Anime — AnimeKai](#anime--animekai)
    - [HiAnime](#hianime)
16. [The Video Player — Deep Dive](#16-the-video-player--deep-dive)
17. [HLS Caching System](#17-hls-caching-system)
18. [Subtitle System — Full Breakdown](#18-subtitle-system--full-breakdown)
    - [Original / Embedded Subtitles](#original--embedded-subtitles)
    - [OpenSubtitles via Wyzie API](#opensubtitles-via-wyzie-api)
    - [AI Translation Engine](#ai-translation-engine)
19. [Caption Appearance Customization](#19-caption-appearance-customization)
20. [Continue Watching & Progress Tracking](#20-continue-watching--progress-tracking)
21. [Lists — Watchlist, Favorites, Custom Lists](#21-lists--watchlist-favorites-custom-lists)
22. [Release Calendar](#22-release-calendar)
23. [Offline / Weak Connection Handling](#23-offline--weak-connection-handling)
24. [Update System](#24-update-system)
25. [Full File & Folder Structure](#25-full-file--folder-structure)
26. [Data Sources and APIs Used](#26-data-sources-and-apis-used)
27. [Tech Stack & Key Dependencies](#27-tech-stack--key-dependencies)
28. [Style Guide & Design Language](#28-style-guide--design-language)
29. [Platform Availability & Roadmap](#29-platform-availability--roadmap)
30. [FAQ](#30-faq)

---

## 1. What Is YouFlex?

YouFlex is a free, open streaming client built for Android. It lets you browse, discover, and watch movies, TV shows, and anime without a subscription. Think of it as an interface — a very polished, very capable one — that connects you to streaming content that already exists on the internet.

The app uses The Movie Database (TMDB) as its source for metadata: posters, backdrops, overviews, ratings, cast info, trailers, release dates, everything visual you see in the app comes from TMDB. The actual video streams? Those come from independent streaming providers scattered across the web. YouFlex does not store a single frame of video. It never has. It just knows where to look.

YouFlex is designed to feel like a premium streaming app. The entire UI is cinematic — pure black backgrounds, crisp white text, smooth animations, a hero banner that scrolls through trending content, organized sections for every genre and provider. It doesn't feel like a piracy tool from 2012 with a broken search bar. It feels like something you'd pay for. Except you don't.

Some of the key things YouFlex can do:

- Stream any movie or TV episode in up to 4K quality from multiple providers
- Search for movies, TV shows, anime, and actors all in one place
- Watch anime with subbed or dubbed audio through AnimeKai and HiAnime
- Display subtitles — either the ones that come bundled with the stream, or fetched fresh from OpenSubtitles via the Wyzie API
- Translate any subtitle track into 30+ languages in real time using Google Translate's AI engine, right on your device, no account needed
- Cache HLS streams locally so you can keep watching even if your connection drops mid-episode
- Track your watch progress across every movie and show, even down to the specific season and episode
- Browse actor filmographies, tap any film in their list to go directly to that title
- Connect your TMDB account to sync your watchlist and favorites
- Create custom lists and organize your content your way
- See upcoming release dates on a calendar that highlights which days have new stuff dropping

---

## 2. Is This Legal?

This is probably the first question anyone asks, and it deserves a real answer, not a one-liner.

**YouFlex does not host, store, encode, or distribute any video content.**

Let that sit for a second. YouFlex is a client application. Its job is to find publicly accessible streaming URLs that exist on third-party websites and play them in a video player. That's it. The app itself contains zero video files, zero CDN infrastructure, zero media servers. There is nothing on any server controlled by YouFlex that contains copyrighted video.

Think about how web browsers work. When you open Chrome and visit a website that embeds a YouTube video, Chrome finds the video URL and plays it. Chrome didn't host the video. Chrome didn't reproduce it. Chrome is a client. YouFlex works the same way — it's a mobile client that retrieves publicly accessible URLs and plays them.

The third-party providers that YouFlex connects to — Vidlink, YFlix, Videasy, Castle, 4KHDHub, AnimeKai, HiAnime — are independent services. They operate their own infrastructure, make their own legal decisions, and are responsible for the content they make available. YouFlex doesn't operate any of those services. YouFlex just knows their public API endpoints.

**If you have a copyright concern, you need to contact the streaming providers themselves, not YouFlex.** They are the ones serving the video. They are the ones who would need a DMCA notice. They are the ones who would need to remove content. YouFlex is just reading publicly available data from their APIs — the same thing any web scraper or automated tool does every day.

The legal landscape for this kind of software has been debated extensively. The most relevant precedent in most countries is that the act of *streaming* (as opposed to *downloading and distributing*) is treated differently under copyright law. Many legal scholars argue that a viewer who streams content doesn't create a permanent copy and therefore isn't liable in the same way a distributor would be. YouFlex's HLS caching system does create temporary local copies of video segments, but these are held in the system's temporary cache directory and are automatically deleted when you close the player.

To summarize the legal position:

- YouFlex does not host content → **Not liable as a host**
- YouFlex does not distribute content → **Not liable as a distributor**
- YouFlex connects to third-party public URLs → **Same as a browser**
- The third-party providers are responsible for what they serve → **They bear the legal risk, not you and not YouFlex**

That said — laws vary by country. In some jurisdictions, even streaming copyrighted content without authorization may have legal implications for the end user. We are not lawyers. Do your own research about your local laws and make your own decisions.

YouFlex is provided as-is, for educational and personal use.

---

## 3. How to Install on Android

YouFlex is built with Expo and distributed as an APK. iOS requires an Apple Developer account ($99/year) which we don't have yet, so for now Android is the only supported mobile platform. Desktop support is planned but not here yet either.

### Method 1: Build from Source

If you're technically inclined and have Node.js and the Expo CLI installed:

```bash
git clone <repo-url>
cd youflex
npm install
npx expo run:android
```

You'll need Android Studio with an AVD set up, or a physical Android device with USB debugging enabled.

### Method 2: Install the APK

Download the latest APK release from the project's releases page. On your Android device:

1. Go to **Settings → Security** (or **Settings → Apps → Special App Access** depending on your Android version)
2. Enable **Install unknown apps** for your browser or file manager
3. Open the downloaded APK file
4. Tap **Install**

That's it. The app will appear in your launcher.

### Permissions the App Needs

YouFlex requests the following permissions:

- **Internet** — Obviously required to stream video and fetch metadata
- **Network state** — Used to detect when you go offline so it can switch to the local cache
- **External storage (read/write)** — Used by the HLS caching system to save video segments temporarily

The app does not access your contacts, camera, microphone, location, or any other sensitive data. It doesn't phone home. It doesn't track you.

---

## 4. The App at a Glance — Navigating the UI

YouFlex has a bottom tab bar with six tabs:

| Tab | Icon | What It Does |
|-----|------|-------------|
| Home | House | Main feed with trending, new releases, Netflix/Disney/Prime sections, Top 10, calendar |
| Movies | Film reel | Browse and filter movies by genre, release date, region |
| TV Shows | Television | Browse and filter TV shows |
| Anime | Play circle | Browse anime via AniList — seasonal, trending, popular |
| Profile | Person | Your TMDB account, watchlist, favorites, custom lists |
| Settings | Gear | Quality preference, subtitle mode, AI language, caption style |

There's also a search bar in the header at the top of the Home screen. Tap on it to go to the search results page, which has its own filter tabs (All, Movie, TV, Anime, Actor).

From any poster card, details page, or cast section, you can tap through to deeper levels of the app:

- **Poster → Details page** (full info, trailers, cast, gallery, recommendations)
- **Details page → Watch screen** (episode selector for TV, play button for movies)
- **Watch screen → Streaming player** (actual video playback)
- **Cast card → Actor page** (bio, filmography grid)
- **Recommendation card → Details page** (same flow, different title)
- **Calendar day → Release modal** (list of what dropped that day)

---

## 5. Home Screen — Everything That Loads on Startup

The home screen is a scrollable feed that loads a lot of content in parallel when the app starts. Here's exactly what happens:

### What Loads on Startup

The home screen fires off eleven simultaneous API requests to TMDB when it mounts:

1. **Trending Movies (Week)** — The most popular movies of the past week globally
2. **New Movies** — Recently released movies sorted by release date
3. **New TV Shows** — Recently premiered TV shows
4. **Top Rated Movies** — All-time highest rated movies on TMDB
5. **Trending TV (Week)** — Most watched TV shows of the past week
6. **Top Rated TV** — Highest rated TV shows of all time
7. **Netflix Movies** — Movies available on Netflix (provider ID 8)
8. **Disney+ Movies** — Movies on Disney+ (provider ID 2739)
9. **Prime Video Movies** — Movies on Amazon Prime (provider ID 9)
10. **Pixar** — Pixar content (provider/company ID 3)
11. **Disney Studio** — Disney animated/studio content (company ID 2)

All of these run at the same time with `Promise.all()`, so the whole thing typically resolves in 1–2 seconds depending on your connection.

### The Hero Banner

At the very top of the home screen is a horizontally scrollable hero banner. It alternates between trending movies and TV shows — one movie, one TV show, one movie, one TV show — up to 10 items. Each card is a full-width backdrop image with the title and "MUST WATCH" badge overlaid. You can swipe through them. Tapping any of them goes to the details page.

### Continue Watching

Right below the hero is the Continue Watching row, but only if you have any watch history. This section reloads every time you navigate to the Home tab (using `useFocusEffect`) so it's always up to date. Each card shows:

- A thumbnail (backdrop image if available, poster otherwise)
- Title
- Progress info: either a timestamp (for movies), or "S1 E3" for TV shows, or "Episode 5" for anime
- A white progress bar showing how far you've watched
- A green "WATCHED" badge if you've hit 95% or more of the runtime
- A trash icon in the corner to delete that entry from your history

Tapping a Continue Watching card takes you directly to the watch screen with the correct season and episode pre-selected.

### Content Sections

After Continue Watching, the home screen shows these horizontal scrolling sections in order:

- Trending Movies Now
- Netflix Originals
- Disney+ Favorites
- Prime Video Hits
- **Top 10 This Week** — A special numbered list with large landscape cards showing rankings (No 1, No 2, etc.)
- New Movies
- New TV Shows
- Global Top Rated
- Binge Worthy TV

Each of these uses the `PosterCard` component — portrait poster image, title below, tappable to go to details.

### Release Calendar

At the very bottom of the home screen is the Release Calendar. It's a monthly calendar grid that highlights which days have movies or TV shows releasing. When you navigate to the calendar, it automatically fetches data for every day in the current month in parallel. Days that have releases show with a white background and black text. Tap any highlighted day and a modal slides up showing all the titles releasing that day with their poster, title, and type (MOVIE or TV SHOW). Tapping a title from the modal takes you to its details page.

You can navigate forward and backward through months using the chevron arrows. Each time you change the month, it refetches release data for the entire new month.

---

## 6. Search — How to Find Anything

The search bar lives in the Header component which is pinned to the top of the Home screen. Typing in it and submitting navigates you to the dedicated search screen.

### Search Screen

The search screen fires two parallel requests:

1. **TMDB Multi-Search** — Searches movies, TV shows, and people all in one call using `/search/multi`. This is the same endpoint Netflix and most major apps use for their search.
2. **AniList Search** — Simultaneously searches AniList's GraphQL API for anime matching your query, fetching up to 20 results.

Results from both are merged into a single list.

### Filter Tabs

The search screen has five filter tabs along the top:

- **All** — Shows everything: movies, TV, anime, and actors together
- **Movie** — Only movies
- **TV** — Only TV shows  
- **Anime** — Only AniList anime results
- **Actor** — Only people (actors, directors, crew)

### How Actor Search Works

Previously the app filtered out `media_type: 'person'` results from TMDB's multi-search. Now it keeps them. When you search for "Tom Hanks" or "Christopher Nolan", their cards appear in the grid right alongside movie and TV cards. Actor cards show:

- Their profile photo in the same poster aspect ratio
- Their name below
- Their department (Acting, Directing, etc.)
- If they don't have a profile photo, a silhouette placeholder is shown

Tapping an actor card goes to the Actor / Person page (see section 13).

### Content Cards in Search

All results use the same 3-column grid with cards that are `(screenWidth - 32) / 3` wide — the same formula used on the home screen's poster sections. Each card has a poster or profile photo at the top, the title/name below, and a small metadata line (type + year for media, department for actors).

---

## 7. Movies Tab

The Movies tab is a dedicated browsing screen for movies. It lets you filter by genre, sort by different criteria, and browse with infinite scroll or pagination. The movies come from TMDB's discover API with various filter parameters applied.

Genre chips at the top let you narrow down to Action, Comedy, Drama, Horror, Sci-Fi, Romance, and other major genres. The full movie list is displayed in the same 3-column `PosterCard` grid.

---

## 8. TV Shows Tab

Same structure as the Movies tab but for TV shows. Genre filtering, sorting options, and a grid of poster cards. TV show results route to the details page with `type: 'tv'` so the app knows to show the episode selector instead of a direct play button.

---

## 9. Anime Tab

The Anime tab is completely separate from the TMDB-powered tabs. It uses AniList's GraphQL API instead. AniList has arguably the most comprehensive anime database on the internet, covering everything from mainstream shonen to obscure seasonal OVAs.

### What's in the Anime Tab

The anime tab typically shows:

- **Trending Now** — What the AniList community is watching most this week
- **Popular This Season** — Currently airing anime ranked by popularity
- **All Time Popular** — The legendary titles that have stood the test of time
- **Top Rated** — Sorted by mean score across all AniList users

Each anime card shows the cover image, title (English if available, falls back to Romaji, then Native), and tapping it goes to the AniList Details page rather than the TMDB Details page.

### AniList Details Page

The AniList details page is specifically built for anime. It shows:

- Cover image and banner backdrop
- Title, status (Ongoing, Finished, etc.)
- Score, episodes, format (TV, Movie, OVA, ONA, Special)
- Genres as chips
- Description / overview
- Studios
- Airing schedule (next episode date if still airing)

From the AniList details page you can tap **Watch** to go to the Watch screen for anime.

### Anime Watch Screen

The anime watch screen is `app/watch/anilistIndex.js`. It handles anime differently from regular TV shows because episode numbering in AniList can be complex (split cours, different season numbering conventions, etc.). The scrapers (AnimeKai and HiAnime) use AniList IDs to find the correct anime.

---

## 10. Profile Tab — TMDB Account Integration

### Logging In

YouFlex lets you connect your TMDB account. TMDB is free — anyone can make an account at themoviedb.org. Once you connect your account to YouFlex, you get access to:

- Your existing TMDB watchlist
- Your TMDB favorites
- Any custom lists you've created on TMDB
- The ability to add movies and shows to any of these from within YouFlex

The login flow works like this:

1. Tap the **Login** button on the Profile tab
2. The app generates a TMDB request token via the `/authentication/token/new` endpoint
3. It opens the TMDB authentication page in your system browser, with a redirect URL pointing back to the app via the `youflex://` deep link scheme
4. You approve the access on TMDB's website
5. TMDB redirects back to the app with the authorized token
6. The app exchanges the token for a session ID via `/authentication/session/new`
7. Your session ID and account details are saved to AsyncStorage
8. You're logged in and your lists load automatically

The app uses the custom URL scheme `youflex://` registered in `app.json` for the OAuth redirect to work on Android.

### Profile Screen Features

Once logged in, the profile screen shows:

- Your TMDB username and avatar
- Watchlist (movies + TV shows combined, sorted by date added)
- Favorites (same structure)
- Custom lists — you can create new ones, see item counts, tap to browse them
- Logout button

From any details page, you can tap **Add** to add that title to your watchlist, favorites, or any custom list. If you're not logged in, tapping Add shows a notification nudging you to log in.

---

## 11. Settings Tab — Full Breakdown of Every Option

The settings screen has one main section: **Playback Preferences**. Every setting here is saved to AsyncStorage under the key `player_preferences` and persists across app restarts.

### Preferred Sources

This is probably the most important setting. YouFlex has multiple stream providers, each with different strengths, and you pick which one to try first when you press play.

**TMDB Sources (for movies and TV shows):**

| Source Name | Internal Name | Provider | Notes |
|-------------|--------------|----------|-------|
| Alpha (Global) | Alpha | Vidlink | The default and most reliable general-purpose source. Runs against Vidlink's API, supports movies and TV shows worldwide. Usually the fastest. |
| Omega (Netflix) | Omega | YFlix | Tuned specifically for Netflix-originated content. If you're watching a Netflix original and Alpha gives a lower quality stream, try Omega. |
| Neon (Global) | Neon | Videasy | Uses the Videasy streaming network's MyFlixer/UpCloud backend. Good fallback for content that Alpha doesn't find. |
| 4K (HIGH QUALITY) | 4K | 4KHDHub | Specifically targets high-quality encodes. If you want the best possible video quality and don't mind potentially slower loading, use this. |
| Gamma (Castle) | Gamma | Castle | Uses the Castle streaming platform (api.fstcy.com). Different content library, different encryption, worth trying if the other sources fail on something. |

**AniList Sources (for anime):**

| Source Name | Internal Name | Provider | Notes |
|-------------|--------------|----------|-------|
| Animekai | Anime | AnimeKai | The default and recommended anime source. Supports sub and dub, has most seasonal anime. |
| HiAnime | HiAnime | HiAnime | Alternative anime source at hianime.to. Different content availability, useful as a backup. |

### Default Quality

Options: **Auto**, **1080**, **720**, **360**

When set to Auto, the player uses whatever stream is at the top of the list (typically the highest quality available from the chosen provider). When you pick a specific quality, the app looks through the available streams and selects the one that matches. The quality comparison normalizes the 'p' suffix — so '720p' from the scraper matches '720' from settings. If no exact match is found, it falls back to the first stream.

### Subtitle Mode

Two options:

- **Original Subtitles** — Uses the subtitle tracks that come bundled with the stream from the provider. Automatically selects English if available, otherwise picks the first available track.
- **AI Subtitles** — Ignores the bundled subtitles and instead translates the subtitle text in real time to your chosen AI language.

### AI Language

Only visible when Subtitle Mode is set to AI Subtitles. Opens a scrollable list of ~35 languages organized by region. Select your target language and the AI translation engine will translate every subtitle line into that language as you watch. Your selection here is saved globally and applies to every video you play.

Supported language groups:
- **Middle East / Regional**: Kurdish (Sorani), Kurdish (Kurmanji), Arabic, Persian, Turkish, Hebrew
- **Global / Western**: English, Spanish, French, German, Italian, Portuguese, Russian, Dutch
- **Eastern Europe**: Polish, Ukrainian, Romanian, Czech, Greek, Hungarian
- **Nordic**: Swedish, Danish, Finnish, Norwegian
- **East Asia**: Chinese Simplified, Chinese Traditional, Japanese, Korean
- **South / Southeast Asia**: Hindi, Thai, Vietnamese, Indonesian, Malay
- **Africa**: Swahili

### Caption Appearance

Opens a full caption customization panel (the same one you can access in the player). Settings include:

- **Text Color** — White, Yellow, Green, or other preset colors
- **Text Size** — XS, S, M, L, XL (maps to 14px, 16px, 20px, 26px, 34px)
- **Background Opacity** — How dark/transparent the black box behind the subtitle text is (0% to 100%)
- **Vertical Position** — How far from the bottom the subtitles sit (percentage of screen height)
- **Delay** — Shift the subtitle timing forward or backward in seconds (useful when subtitles are slightly out of sync)

All caption settings are saved separately under the `caption_config` AsyncStorage key and are read by the player on every launch.

---

## 12. Details Page — Everything About a Title

When you tap any movie or TV show poster anywhere in the app, you go to the Details page. This page loads everything TMDB knows about that title in a single API call using `append_to_response` to bundle multiple endpoints:

- Basic info (title, overview, genres, release date, rating)
- Credits (full cast and crew)
- Videos (trailers and clips from YouTube)
- Images (backdrop gallery)
- Recommendations (similar titles)
- Season information (for TV shows)

### Layout

**Backdrop** — A wide landscape image from TMDB fills the top of the screen, slightly transparent.

**Poster + Action Row** — Below the backdrop (overlapping it slightly) is the poster thumbnail on the left, and on the right:
- **WATCH** button — Takes you to the watch screen
- **Add** button — Opens the lists modal (if you're logged in) or shows a login prompt

**Title, Year, Rating, Genres** — Displayed as text metadata below the action buttons.

**For TV Shows specifically** — Season count and episode count are shown in the metadata.

**Trailers** — A horizontally scrollable list of trailer thumbnails from YouTube. Tapping one opens a fullscreen WebView player that autoloads the video. The trailer plays in YouTube's embedded player. There's an X button to close it.

**Overview** — The synopsis/description from TMDB.

**View Collection** — If a movie is part of a collection (like the Avengers saga or the Harry Potter series), a button appears to view all titles in that collection.

**Gallery** — A horizontal scroll of backdrop images. Up to 10 images are shown.

**Cast** — A horizontal list of up to 15 cast members. Each card shows:
- Circular profile photo
- Actor's name
- Character name in gray italic below their name
- Tapping a cast card goes to the Actor page

**Recommended** — A horizontal row of poster cards for similar titles, each tappable to their own details page.

### Back Button

The back button is positioned absolutely in the top-left, overlaying the backdrop. It uses `navigation.goBack()` rather than `router.back()` to properly handle the navigation stack.

### Anime Redirect

If a details page is opened with `type: 'anime'`, it immediately redirects to the AniList Details page instead. This handles the case where anime results appear in search or on the home screen.

---

## 13. Actor / Person Pages

Tapping any cast member from the Details page takes you to their Actor page at `/person?id=<tmdb_person_id>`.

### What's on the Actor Page

**Hero Section** — A full-width photo of the actor at the top (using their TMDB profile image at w500 resolution). Their name and department (e.g., "Acting", "Directing") overlay the bottom of the photo with a dark gradient.

**Stats Row** — Pill-shaped chips showing:
- Birthday and age (calculated from today's date, shows "†X" if they're deceased)
- Place of birth
- Number of movies they've been in
- Number of TV shows they've been in

**Biography** — Their TMDB biography text, collapsed to 4 lines by default with a "Read more" toggle to expand the full text.

**Filmography Filter** — Three filter tabs:
- **All [count]** — Every credit combined
- **Movie [count]** — Movies only
- **TV Show [count]** — TV shows only

**Filmography Grid** — A 3-column grid showing all their credits. Each card follows the exact same format as the search results page:
- Poster image at `2:3` aspect ratio
- Title below
- Year below the title

Cards are sorted newest first. Duplicate entries (where the same title appears multiple times due to appearing in different episodes) are deduplicated. Tapping any card takes you to that title's details page.

### Data Source for Actor Pages

The `fetchPersonDetails` function in `services/tmdbApi.js` calls `/person/{id}?append_to_response=combined_credits`. The `combined_credits` response includes both `cast` and `crew` credits, with each item tagged with `media_type: 'movie'` or `media_type: 'tv'`. The actor page only shows cast credits (not crew) to keep the filmography clean.

### Navigation

The back button on the actor page uses `navigation.goBack()` wrapped in a circular floating button (black with white arrow, 42px diameter) positioned at the top-left, same style as the details page back button.

---

## 14. The Watch Screen — Before You Press Play

Before you actually start watching, you land on the Watch screen. For movies it's pretty simple — there's a poster with a play button. For TV shows it becomes a full episode browser.

### Movie Watch Screen

Shows the movie poster as a large card. Centered on it is a white circular button with a play icon and "WATCH" text. Tapping it starts the scraping process.

### TV Show Watch Screen

For TV shows, the watch screen is much richer:

**Episode Navigation Bar** — Left/right arrow buttons to step through episodes, with the current "S:X E:Y" shown in the center. The forward arrow is disabled on the last episode of a season.

**Season Selector** — A dropdown button showing "Season X". Tapping it opens a bottom sheet modal listing all available seasons (excluding season 0 / specials). Selecting a season switches the episode list and resets to episode 1.

**Episode List** — A vertical list of all episodes in the selected season, each showing:
- Episode thumbnail (still image from TMDB, or the show poster as fallback)
- Episode number and title ("Episode 3: The Long Road")
- Rating (star icon + decimal score) and runtime in minutes
- For episodes that haven't aired yet: the air date plus a countdown ("will air in 12d" or "Airing today")
- Unaired episodes are dimmed and disabled — you can't tap them

The currently selected episode has a white border and slightly different background to indicate it's active.

**The Play Button**

When you tap the play button (or the big WATCH button for movies), the scraping process begins. The play button changes to a spinning loader icon. During this time, the app is contacting the selected streaming provider and extracting playable URLs. This typically takes 2–10 seconds.

If no streams are found (the provider doesn't have this content), an alert tells you the content isn't available and to check back later.

When streams are found, the app pushes you to the streaming screen, passing along:
- The list of streams (URL, quality, provider, headers)
- The subtitle list
- The episode title (formatted as "S1E3 The Long Road" for TV, or just the movie title)
- The mediaInfo object (id, type, season, episode, poster, resumeTime from previous progress)

---

## 15. The Scraping System — How Streams Are Found

This is the most technically interesting part of the app and the part that makes everything else possible. When you hit play, one of the scrapers runs. Here's exactly what each one does.

### Alpha — Vidlink

**File:** `scraper/providers/vidlink.js` (Node.js) + `vidlinkUtil.js` (wrapper)

Vidlink is the primary and most reliable source. It accesses the Vidlink Pro API at `https://vidlink.pro/api/b`.

**The flow:**
1. Look up the title on TMDB to get the IMDB ID and other metadata
2. Construct the Vidlink API request with the TMDB ID, IMDB ID, media type, season, and episode
3. The Vidlink API returns an encrypted response (they use their own encryption format)
4. The encrypted data is sent to a decryption service at `enc-dec.app/api` which returns the actual JSON
5. The decrypted JSON contains an M3U8 playlist URL for the video stream
6. That M3U8 URL is fetched and parsed — if it's a master playlist (containing multiple quality variants), the parser extracts all variant streams with their resolution/bandwidth info
7. The extracted streams are returned with quality labels like "1080p", "720p", "480p", "360p"
8. Subtitle tracks (VTT/SRT format) embedded in the stream response are also extracted and returned

The streams come back with proper Referer and Origin headers for Vidlink, which are passed along to the video player so the CDN doesn't reject the requests.

**Quality parsing:** Vidlink streams have `RESOLUTION=1920x1080` or similar in the M3U8 `#EXT-X-STREAM-INF` tags. The parser extracts the height (1080, 720, 480, 360) and uses that as the quality label.

### Omega — YFlix

**File:** `scraper/providers/yflix.js` (Node.js) + `yflixUtil.js` (wrapper)

YFlix targets `yflix.to`, a streaming aggregator that particularly excels with Netflix content. It uses a more complex multi-step process:

1. Uses a database lookup API at `enc-dec.app/db/flix` to find the YFlix internal ID for the title
2. Once it has the internal ID, fetches the AJAX endpoint at `https://yflix.to/ajax`
3. The response contains encrypted stream data
4. Decrypts using the `enc-dec.app/api` decryption service
5. Extracts M3U8 URLs from the decrypted payload
6. Returns streams with quality labels

YFlix tends to have better quality for Netflix originals and fresh theatrical releases because of how its backend indexes content.

### Neon — Videasy

**File:** `scraper/providers/videasy.js` (Node.js) + `videasyUtil.js` (wrapper)

Videasy operates on a completely different model. It's a streaming aggregation API at `api.videasy.net` that acts as a broker for multiple backend streaming services.

**The Neon server config:**
```
Neon: {
  url: 'https://api.videasy.net/myflixerzupcloud/sources-with-title',
  language: 'Original'
}
```

The code comments show there were many more server configurations at one point (Sage, Cypher, Yoru, Reyna, Omen, Breach, Vyse, German Killjoy, Italian Harbor, French Chamber, Hindi Fade, Latin Gekko, Spanish Kayo, Portuguese Raze/Phoenix/Astra) but Neon is the stable one right now.

**The flow:**
1. TMDB lookup to get title, year, IMDB ID
2. Build a Videasy URL with all metadata as query parameters
3. The Videasy endpoint returns encrypted data
4. Decrypt via `enc-dec.app/api/dec-videasy` (different decrypt endpoint from Vidlink)
5. The decrypted data contains sources array with video URLs and a subtitles array
6. Quality extraction uses a combination of explicit quality fields and URL pattern matching (looking for things like `/1080p/`, `/720p/`, base64-encoded resolution strings like `MTA4MA==` = 1080)
7. Language detection is built in — if a stream has an explicit language field (English, Hindi, German, etc.), it's noted in the stream name

The language normalization function is comprehensive, mapping both ISO codes (`en`, `eng`) and full names (`english`, `English`) to readable display names.

**Subtitle extraction for Videasy:**
- Checks `subtitles` array in the decrypted response
- Checks `tracks` array for items with `kind: 'subtitles'` or `kind: 'captions'`
- Normalizes language codes the same way as for streams

### 4K — 4KHDHub

**File:** `scraper/providers/4khdhub.js` + `4khdhubUtil.js`

4KHDHub is specifically tuned for high-definition content. It targets a different backend infrastructure that tends to have higher quality encodes (true 4K where available, or the best available version of older content).

The scraping approach is similar to the others — TMDB lookup, API call with encrypted response, decryption, stream extraction — but the source it targets consistently returns high-bitrate streams.

When you have a good connection and want the best possible picture quality, 4K is the source to use. The tradeoff is that it can be slower to load and may buffer more on weaker connections.

### Gamma — Castle

**File:** `scraper/providers/castle.js` + `castleUtil.js`

Castle is the most complex scraper. It connects to `api.fstcy.com`, which appears to be a large international streaming platform (based on details like `CHANNEL = 'IndiaA'` and `PKG = 'com.external.castle'`). The system suggests it's designed to scrape a mobile streaming app's backend.

**The Castle flow is unique:**

1. **Get Security Key** — Every session starts by fetching a dynamic security key from `${CASTLE_BASE}/v0.1/system/getSecurityKey/`. This key changes, so it has to be fetched fresh every time.

2. **Search** — Uses `searchByKeyword` endpoint with the title and year, returns an encrypted response

3. **Decrypt** — Castle uses AES-CBC encryption. The encrypted data is base64-encoded. It's sent to a separate decryption service at `https://aesdec.nuvioapp.space/decrypt-castle` along with the security key. The decryption service handles the actual AES-CBC math and returns the plaintext JSON.

4. **Find the Castle Movie ID** — The search results are fuzzy-matched against the title to find the Castle-internal ID. It tries exact matches first, falls back to partial matches, falls back to the first result.

5. **For TV Shows** — It navigates Castle's season structure. Castle represents TV shows differently — each season may have a different `movieId`. So for TV show scraping, it fetches the top-level show, finds the right season within it, and potentially re-fetches with the season's specific ID.

6. **Get Episode ID** — Within the season, it finds the specific episode ID needed for the video request.

7. **Get Video (v2 and v1)** — It tries two different video API versions. The v2 endpoint uses POST with a body including `apkSignKey`, `androidVersion`, `woolUser`, and other fields that mimic an Android app. The v1 endpoint supports language selection via `languageId`.

8. **Extract Streams and Subtitles** — The decrypted video response contains `videos` array, `subtitles` array, `captions` array, and `tracks` array. Castle's subtitle extraction is the most thorough in the codebase — it checks five different possible subtitle locations in the response and has a sophisticated language detection system:
   - Direct `label`, `language`, `languageName`, `lang`, `name`, `title` fields on subtitle objects
   - Falls back to extracting language from the subtitle URL itself (e.g., `English.vtt` → English, `/en/` path segment → English)
   - Maps two-letter ISO codes, three-letter ISO codes, and full language names

**Why Castle exists:** Because its content library is different from Vidlink and Videasy. Some content that's hard to find on other sources turns up easily through Castle.

### Anime — AnimeKai

**File:** `scraper/providers/animekai.js` + `animekaiUtil.js`

AnimeKai is the primary anime source. It operates at `animekai.to` and has a sophisticated backend.

**The AnimeKai flow:**

1. **AniList Lookup** — Given an AniList ID, queries AniList's GraphQL API to get the anime title (both English and native/romaji versions), episode count, and other metadata.

2. **Episode Count Verification** — Optionally queries Jikan (MAL's unofficial API) to verify episode counts, with rate limit handling (retries after 1 second on 429).

3. **AnimeKai Search** — Searches `animekai.to/ajax` with the anime title to find AnimeKai's internal ID for the series.

4. **Episode List** — Fetches the episode list from AnimeKai using their AJAX endpoint.

5. **Server Selection** — AnimeKai has multiple server types: `sub` (hard-coded subtitles), `softsub` (soft subtitles, separable), and `dub` (English or other language audio). The scraper tries to find the requested episode on the preferred server type.

6. **Source Extraction** — The server page contains encrypted source data. The app uses `enc-dec.app/api` to decrypt it.

7. **M3U8 Parsing** — The decrypted source contains an M3U8 URL. The playlist is fetched and parsed for quality variants.

AnimeKai is recommended over HiAnime for most cases because it has broader coverage of seasonal anime and supports more server types.

### HiAnime

**File:** `scraper/providers/hianime.js` + `hianimeUtil.js`

HiAnime targets `hianime.to`, one of the most popular anime streaming sites. The technical challenge with HiAnime is that its video player uses Megacloud (a CDN with its own encryption), and the decryption key changes periodically.

**The HiAnime flow:**

1. **Get Decryption Key** — Fetches the current Megacloud decryption key from a community-maintained GitHub repository at `https://raw.githubusercontent.com/ryanwtf88/megacloud-keys/refs/heads/master/key.txt`. The key is cached in memory for the session.

2. **Anime Search** — Searches HiAnime for the anime by title using their search endpoint.

3. **Episode Navigation** — Finds the specific episode from the episode list.

4. **Player Extraction** — The episode page embeds a Megacloud player. The scraper uses Cheerio (a server-side HTML parser) to extract the player URL from the page source.

5. **Token Extraction** — The Megacloud player page has a token embedded in various ways — in script variables (`window.something = 'token'`), in meta tags, in data attributes. The scraper tries multiple extraction patterns.

6. **AES Decryption** — Uses `crypto-js` to perform AES decryption on the encrypted stream source using the fetched key. Supports both string and hex key formats.

7. **Source Extraction** — The decrypted JSON contains the actual M3U8 stream URLs, subtitle tracks, and other metadata.

HiAnime tends to have slightly better quality for older, classic anime where Megacloud archives high-quality encodes.

---

## 16. The Video Player — Deep Dive

The player is built in `components/Player/VideoPlayer.js` using `react-native-video`. This is a native video player component that wraps ExoPlayer on Android and AVFoundation on iOS. It's the most reliable option for React Native video playback.

### Player Props

```javascript
VideoPlayer({
  streams,         // Array of stream objects from the scraper
  subtitles,       // Array of subtitle objects
  title,           // String shown in the top bar (e.g., "S1E3 The Long Road")
  onBack,          // Function called when back button is pressed
  mediaInfo        // JSON string with id, type, season, episode, poster, resumeTime
})
```

### Buffer Configuration

The player uses an aggressive buffer configuration:

```javascript
const BUFFER_CONFIG = {
  minBufferMs: 60000,        // Minimum 60 seconds always in buffer
  maxBufferMs: 180000,       // Try to buffer up to 3 minutes ahead
  bufferForPlaybackMs: 2500, // Only need 2.5s to start playing
  bufferForPlaybackAfterRebufferMs: 5000,  // Need 5s after a rebuffer
};
```

This is tuned to prevent buffering interruptions. The tradeoff is slightly more initial load time, but you should almost never see a "buffering..." spinner after playback starts on a decent connection.

### Screen Orientation and Navigation Bar

When the player opens:
- Screen is locked to landscape mode via `expo-screen-orientation`
- On Android, the navigation bar (the system buttons at the bottom) is hidden and set to sticky-immersive mode via `expo-navigation-bar`

When the player closes, both are restored to their defaults.

### Controls UI

Controls are overlaid on top of the video. Tapping anywhere on the player toggles controls on/off with a simple boolean state. The status bar also hides when controls are hidden for a true fullscreen experience.

**Top bar** (visible when controls are showing):
- Back arrow (left side) — calls `onBack`
- Title text (right of back arrow) — the episode or movie title

**Center controls:**
- Skip back 10 seconds (left)
- Play/Pause (center) — large button
- Skip forward 10 seconds (right)

**Bottom controls:**
- Current time / total duration
- A scrubbing slider (react-native-community/slider) for seeking
- Volume icon (left side bottom) — toggles mute
- Right side has four icon buttons: Subtitles, Quality, Source Layers, Settings

### Quality Switching

When you switch quality, the player records the current playback time, switches the stream source, and when the new video loads, seeks to the recorded time. This is done via the `timeToRestore` state variable.

### Error Handling and Recovery

If the video fails to play (`onError` callback fires), the player first tries a fallback to the locally cached M3U8 file (if the HLS cache system has already downloaded some segments). If the local cache path exists and recovery hasn't been attempted yet, it switches to that local file and restores the current playback position.

If that also fails (or no cache exists), it shows an error modal with:
- The error message
- A **Copy Error Log** button that copies a detailed JSON object to the clipboard including stream URL, headers, provider, quality, platform, and timing info — useful for debugging and reporting

---

## 17. HLS Caching System

**File:** `services/hlsCache.js`

This is one of the more sophisticated pieces of engineering in the app. HLS (HTTP Live Streaming) is the dominant streaming protocol — M3U8 playlists pointing to hundreds of short `.ts` segment files. The caching system downloads those segments to local storage in the background while you watch, so you have a local copy as a fallback if your connection drops.

### How It Works

**Step 1: M3U8 Fetch**

When a stream starts, the HLS cache is initialized with the stream URL. It fetches the M3U8 file.

**Step 2: Master vs Variant Playlist Detection**

If the M3U8 is a master playlist (contains `#EXT-X-STREAM-INF` or `#EXT-X-MEDIA:`), it means it lists multiple quality variants. The cache picks the highest bandwidth variant (the one with the highest `BANDWIDTH=` value) and fetches that variant's M3U8 instead.

If it's already a variant playlist (contains `#EXTINF:` tags pointing directly to segments), it uses it as-is.

**Step 3: Segment Parsing**

All segment URLs are extracted from the playlist. Relative URLs are resolved against the playlist's base URL. The result is a list of absolute HTTPS URLs for every `.ts` (or `.m4s` for CMAF) segment.

**Step 4: First 12 Segments Download**

The first 12 segments are downloaded immediately in batches of 6 simultaneous downloads. This gives you roughly 60–120 seconds of cached video before the background downloader takes over.

**Step 5: Local M3U8 Generation**

A modified version of the M3U8 playlist is written to the app's cache directory, where every segment URL that has been downloaded is replaced with its local file path. Segments not yet downloaded keep their remote URL as a fallback.

**Step 6: Background Download**

The rest of the segments continue downloading in the background while you watch. Every 20 segments, the local M3U8 is rewritten to include the newly cached segments.

### Recovery Trigger

In the `VideoPlayer`, there's a `LOW_BUFFER_THRESHOLD = 8` seconds constant. If your connection drops (`isConnected` becomes false from NetInfo) AND the amount of buffered video ahead of your current position drops below 8 seconds, the offline banner appears.

If playback fails while offline and a local M3U8 exists, the player switches to it automatically. You can then continue watching from the cached content until the segments run out.

### Cache Cleanup

When you leave the player (`useEffect` cleanup function), `clearStreamCache()` is called. This:
- Stops all background downloads
- Clears the in-memory segment map
- Deletes the entire cache directory from disk

So the cache is strictly per-session. It doesn't persist between playback sessions.

---

## 18. Subtitle System — Full Breakdown

The subtitle system in YouFlex is probably its most feature-rich aspect. There are three completely separate subtitle sources, all accessible from the subtitle button in the player.

### Subtitle Menu Architecture

The subtitle menu has three tabs: **Original**, **OpenSubs**, and **AI**.

It's implemented in `components/Player/menus/subtitlesMenu.js` and receives:
- `subtitles` — The array from the scraper
- `currentSubtitle` — Currently active subtitle object
- `onSelectSubtitle` — Callback when user picks a subtitle
- `media` — The media info object (needed for OpenSubtitles TMDB ID lookup)
- `aiSourceSub` — The subtitle that AI mode is translating (can be overridden by user)
- `onSetAiSource` — Callback when user picks a different source for AI translation

### Original / Embedded Subtitles

These are the subtitle tracks that come bundled with the stream from whichever provider you're using. Not all providers include subtitles — Vidlink tends to have the most, Castle has comprehensive multi-language subtitle sets when it finds content.

The Original tab shows a scrollable list of all available subtitle tracks. Each track shows its language name. Tapping one activates it. An **Off** option is always at the top to disable subtitles entirely.

**Auto-selection:** On player startup, the `findEnglishSubtitle` function runs through the available subtitles and looks for one with "english" in its label or language field. If found, it's automatically selected. If not, the first subtitle in the list is selected.

**How subtitles are rendered:**

YouFlex renders subtitles itself rather than using the video player's built-in subtitle support. This was a deliberate choice because it allows for:

1. Custom styling (text color, size, background, position)
2. AI translation (you can't modify the video player's native subtitle text)
3. Timing delay adjustment
4. SRT support (the native player prefers VTT/M3U8 embedded tracks)

The process:

1. When a subtitle is selected, its URL is fetched
2. The response text (SRT or VTT format) is parsed line by line
3. Each subtitle cue is extracted: start time, end time, and text lines
4. Timecodes in both `HH:MM:SS,mmm` (SRT) and `HH:MM:SS.mmm` (VTT) formats are parsed to seconds
5. On every video progress update (which fires roughly every 250ms), the active cues are filtered from the parsed list (cues where `now >= start && now <= end`)
6. The text of those cues is displayed in a View positioned absolutely over the video, with configurable bottom position

HTML tags in subtitle text are stripped with a regex before display.

### OpenSubtitles via Wyzie API

The second tab fetches subtitles from OpenSubtitles, the largest subtitle database on the internet, through the Wyzie API.

**File:** `services/wyzieSubtitles.js`

**Wyzie API endpoint:**

For movies:
```
https://sub.wyzie.io/search?id={tmdbId}&source=opensubtitles&key={apiKey}
```

For TV episodes:
```
https://sub.wyzie.io/search?id={tmdbId}&source=opensubtitles&key={apiKey}&season={s}&episode={e}
```

The API returns an array of subtitle results. Each result has:
- `display` — Human-readable language name
- `language` — ISO language code
- `flagUrl` — URL to a flag image for that language
- `download` — Download URL for the SRT/VTT file
- `hearingImpaired` — Boolean flag
- `downloadCount` — How many times it's been downloaded (popularity indicator)

**UI in the OpenSubs tab:**
- Results are grouped by language (English first, then alphabetical)
- Each language group has a flag image and the language name as a header
- Under each language, individual files are listed with their download count and a hearing-impaired badge (🦻) if applicable
- A "Use for AI" button appears next to each subtitle — see the AI source section

**Error handling and retry:**
If the Wyzie API returns an error (e.g., for anime which may not have TMDB IDs), a retry button is shown. The API returns HTTP 400 for invalid or missing IDs, which is caught and displayed.

**Fetch deduplication:**
A `hasFetchedRef` prevents the API from being called multiple times when switching between the OpenSubs tab and the AI tab (since AI also uses OpenSubs files as source).

### AI Translation Engine

The third tab is where you translate subtitles into any of the 35+ supported languages in real time.

**The Translation Service:**
`services/translator/translator.js`

The app uses Google Translate's public single-translation API endpoint (`translate.googleapis.com/translate_a/single`) with the `gtx` client identifier. This is the same endpoint that powers the Google Translate extension and many other translation tools. It doesn't require an API key or account.

On web (due to CORS), requests are routed through corsproxy.io. On Android (no CORS restriction), requests go directly.

The response format is an array of arrays — `response.data[0]` is an array of translated segments. The segments are joined to form the complete translated text.

**Translation Cache:**
Every translation is cached in memory using a key format: `{languageCode}_{cueStart}_{cueEnd}`. This means each subtitle cue is only translated once per session. The cache is cleared when you change the AI language or switch the AI source subtitle.

**Batch Translation:**
The app doesn't translate one cue at a time — that would create a waterfall of 500+ requests. Instead, it looks at cues that are "visible" (within a 65-second window of the current playback position) and translates batches of up to 15 cues at a time using `Promise.all()`. This creates efficient parallelism while staying within reasonable API limits.

**Line-aware translation:**
Dialogue subtitles often have multiple characters speaking simultaneously, with each line starting with a dash (`-`). The translation engine handles this by translating each dashed line separately to preserve the multi-speaker structure. Single-block subtitles are translated as one string and then redistributed across the original line count.

**AI Source Selection:**
By default, AI mode translates from the best available embedded subtitle (English preferred). But you can override this — in the OpenSubs tab, each subtitle file has a "Use for AI" button. Selecting it sets that specific subtitle file as the AI's source material. This is useful when:
- The stream has no embedded English subtitles but OpenSubtitles has one
- You want higher quality source text than what came bundled with the stream
- You want to translate from a non-English original subtitle file

When you change the AI source, the translation cache is cleared and re-translation begins from the new source.

---

## 19. Caption Appearance Customization

The caption customization panel lives in `components/Player/menus/captionsMenu.js` and is accessible both from Settings and from within the player's settings menu.

### Settings

**Text Color** — Preset swatches. Default is white. Other options include yellow (classic subtitle color), green, cyan. The color is applied directly to the Text style.

**Text Size** — Five options: XS (14px), S (16px), M (20px), L (26px), XL (34px). The default M gives a readable size for most phone screens.

**Background Opacity** — A slider from 0% to 100% controlling the transparency of the black box behind subtitle text. 0% = fully transparent (no background, text only), 100% = solid black box. 50% is the default — visible enough to read against any background without being obtrusive.

**Vertical Position** — Slider controlling how far from the bottom the subtitle sits. 0% = at the very bottom, 50% = middle of the screen, 100% = near the top. Default is 10% from the bottom.

**Delay** — Positive or negative seconds to offset the subtitle timing. Useful for subtitles that are consistently early or late. The delay is added to `currentTime` when checking which cues to display.

All settings are saved to `AsyncStorage` under the `caption_config` key and applied immediately on both the preview (in settings) and in the player.

---

## 20. Continue Watching & Progress Tracking

**File:** `services/progressService.js`

Progress is saved to AsyncStorage under the key `continue_watching`. This is a JSON object keyed by TMDB ID.

### When Progress Is Saved

The player saves progress every 5 seconds via a `setInterval` timer, but only when:
- The video is playing (not paused)
- The video is not loading
- The video is not buffering
- There is actual playback time to record (`currentTime > 0`)

Progress is also saved one final time when the player unmounts (e.g., you press the back button mid-episode).

### What's Stored

For **movies:**
```json
{
  "id": "550",
  "type": "movie",
  "title": "Fight Club",
  "poster_path": "/pB8BM7pdSp6B6Ih7QZ4DrQ3PmJK.jpg",
  "progress": {
    "watched": 3421.5,
    "duration": 8100.0,
    "percentage": 42.2
  },
  "last_updated": 1711234567890
}
```

For **TV shows:**
```json
{
  "id": "1399",
  "type": "tv",
  "title": "Game of Thrones",
  "last_season_watched": "7",
  "last_episode_watched": "6",
  "show_progress": {
    "s7e6": {
      "season": "7",
      "episode": "6",
      "progress": { "watched": 2145.3, "duration": 4200.0, "percentage": 51.1 }
    }
  },
  "progress": { "watched": 2145.3, "duration": 4200.0, "percentage": 51.1 },
  "last_updated": 1711234567890
}
```

### Resume on Play

When you press play on something you've watched before, the app calls `getMediaProgress(id, type, season, episode)` to check if there's an existing progress entry for that specific content. If there is, the `resumeTime` (the `watched` value in seconds) is passed to the player as part of `mediaInfo`.

The player then seeks to `resumeTime` when the video first loads — handled in the `onLoad` callback.

### "Watched" Threshold

When progress reaches 95% or higher, the Continue Watching card shows a green "WATCHED" badge with a checkmark. The progress bar turns green as well. The item stays in Continue Watching even after being marked as watched so you can rewatch easily.

### Deleting History

Each Continue Watching card has a trash icon in its corner. Tapping it calls `deleteHistoryItem(id)` which removes that entry from AsyncStorage and immediately refreshes the list.

---

## 21. Lists — Watchlist, Favorites, Custom Lists

**File:** `services/listService.js` and `services/authService.js`

All list functionality requires a TMDB account (it's free to create one).

### Watchlist and Favorites

These are TMDB's default lists. Every TMDB account has them automatically. The app reads and writes them via:

- `GET /account/{account_id}/watchlist/movies`
- `GET /account/{account_id}/watchlist/tv`
- `POST /account/{account_id}/watchlist` (to add/remove)
- Same pattern for `/favorite`

Both movies and TV are fetched separately and combined. Pagination is handled (up to 15 pages, so up to 300 items per list) to load large lists.

### Custom Lists

TMDB also supports user-created custom lists. The app can:

- Create a new custom list: `POST /list` with a name and description
- Fetch all your lists: `GET /account/{account_id}/lists`
- Add items: `POST /list/{list_id}/add_item` with `media_id`
- Remove items: `POST /list/{list_id}/remove_item` with `media_id`
- Delete a list: `DELETE /list/{list_id}`
- View list contents: `GET /list/{list_id}`

### The "Add" Button Flow

On any details page, the **Add** button opens the `ListsModal` component. This modal:
1. Loads your watchlist, favorites, and custom lists from TMDB
2. Shows checkboxes or buttons for each list
3. Shows which lists the current item is already in
4. Lets you toggle items in/out of any list
5. All changes are synced immediately to TMDB

---

## 22. Release Calendar

The release calendar at the bottom of the Home screen is one of the more clever features. It's not just a static calendar — it actually queries TMDB for every single day of the displayed month to determine which days have content releasing.

### How It Works

When the calendar renders (and whenever you navigate to a different month), it calls `checkMonthReleases`:

1. For every day in the month (up to 31), it creates two promises:
   - `fetchByDate(dateStr, 'movie')` — TMDB discover with primary_release_date filter
   - `fetchByDate(dateStr, 'tv')` — TMDB discover with first_air_date filter
2. All of these promises (up to 62 simultaneous API calls) are fired in parallel with `Promise.all()`
3. Any day that returns at least one result gets marked as `releases[day] = true`
4. The calendar renders with those days highlighted (white cell, black text)

Days with no releases render in the default dark style.

### Tapping a Day

When you tap a highlighted day, the app re-fetches both movies and TV shows for that specific date and combines them into a list. A modal slides up showing:
- Poster thumbnail for each title
- Title and type (MOVIE or TV SHOW)
- Tapping a title closes the modal and goes to the details page

### Navigation

Left/right chevron arrows change the displayed month. Each month change triggers a full refetch of release data for the new month. A loading spinner overlays the calendar grid while data loads.

---

## 23. Offline / Weak Connection Handling

The app has a multi-layer approach to connectivity issues using `@react-native-community/netinfo`.

### Connection Monitoring

At player startup, the app subscribes to NetInfo events. When connection state changes:

- `isConnected = true` — Normal operation
- `isConnected = false` — Triggers offline logic

### Offline Banner

The full-screen offline overlay appears when **both** conditions are true:
- No internet connection (`isConnected = false`)
- Buffer ahead is less than 8 seconds (`bufferedAhead < LOW_BUFFER_THRESHOLD`)

If you're offline but have more than 8 seconds buffered, the overlay doesn't appear — just a small pill indicator at the top showing "Offline — Xs buffered".

### The Offline Banner Shows:

- A WiFi-off icon (semi-transparent)
- "No internet connection" title
- A message showing either:
  - "Cache available (X% downloaded)" if HLS cache has content
  - "Waiting for connection to resume..." if no cache
- A Retry button that manually re-checks the connection state

### HLS Cache Fallback

If playback fails (connection drop mid-stream) and the HLS cache has been building segments, the player automatically switches from the remote M3U8 to the locally cached M3U8 playlist. This is transparent to the user — playback just continues from the cached segments.

### Non-Player Offline Behavior

Outside the player, the app doesn't have a special offline mode. If you're offline on the home screen, the TMDB API calls will fail silently and sections will just be empty. No special UI is shown for this case since most interactions require internet anyway.

---

## 24. Update System

**File:** `services/updateService.js`

YouFlex has a built-in update checker. On every app startup (in the root `_layout.js`), it calls `checkForUpdates()`.

The update check pings a remote endpoint (likely a GitHub releases API or a custom JSON file) to see if there's a newer version available than what's currently installed. If there is, an `UpdateModal` component slides up showing the update information.

The modal presents the update and gives the user the option to download it or dismiss. Users can choose to ignore the update and continue with the current version.

This system is particularly important for an app like this because stream providers sometimes change their APIs, encryption, or endpoints. A forced update mechanism ensures users can always be pushed to a version with working scrapers.

---

## 25. Full File & Folder Structure

```
youflex/
│
├── app/                          # Expo Router screens
│   ├── _layout.js                # Root layout — Stack navigator, update modal
│   ├── (tabs)/                   # Bottom tab screens
│   │   ├── _layout.js            # Tab bar config (Home, Movies, TV, Anime, Profile, Settings)
│   │   ├── index.js              # Home screen — hero, continue watching, content sections, calendar
│   │   ├── movies.js             # Movies browse/filter page
│   │   ├── tvshows.js            # TV shows browse/filter page
│   │   ├── anime.js              # Anime browse via AniList
│   │   ├── profile.js            # TMDB account — watchlist, favorites, custom lists
│   │   └── settings.js           # Playback preferences, subtitle config, caption style
│   │
│   ├── details.js                # Movie/TV details page
│   ├── person.js                 # Actor/person page with filmography grid
│   ├── search.js                 # Search results with multi-type filters
│   ├── anilistDetails.js         # AniList anime details page
│   │
│   ├── watch/
│   │   ├── index.js              # Watch screen — episode selector, poster, scraping trigger
│   │   ├── streaming.js          # Streaming screen — loads VideoPlayer with stream data
│   │   └── anilistIndex.js       # Anime-specific watch screen
│   │
│   ├── collection/
│   │   └── [id].js               # Movie collection page (e.g., MCU, Harry Potter)
│   │
│   └── profile.js                # (also exists as a tab)
│
├── components/
│   ├── Header.js                 # Top search bar (pinned to home screen)
│   ├── PosterCard.js             # Reusable poster card for 3-column grids and horizontal lists
│   ├── ListsModal.js             # "Add to list" modal for watchlist/favorites/custom lists
│   ├── UpdateModal.js            # Update notification modal
│   │
│   └── Player/
│       ├── VideoPlayer.js        # Full video player with controls, subtitles, HLS cache
│       └── menus/
│           ├── settingsMenu.js   # Settings icon → opens sub-menus
│           ├── playbackSpeedMenu.js  # 0.5x, 0.75x, 1x, 1.25x, 1.5x, 2x
│           ├── captionsMenu.js   # Caption appearance (color, size, opacity, position, delay)
│           ├── subtitlesMenu.js  # 3-tab subtitle picker (Original / OpenSubs / AI)
│           └── qualityMenu.js    # Stream quality selection
│
├── scraper/
│   └── providers/
│       ├── vidlink.js            # Alpha — Vidlink scraper (primary movie/TV source)
│       ├── vidlinkUtil.js        # Wrapper with getPlayableStreams() interface
│       ├── yflix.js              # Omega — YFlix scraper (Netflix-optimized)
│       ├── yflixUtil.js          # Wrapper
│       ├── videasy.js            # Neon — Videasy scraper (MyFlixer/UpCloud backend)
│       ├── videasyUtil.js        # Wrapper
│       ├── 4khdhub.js            # 4K — High quality scraper
│       ├── 4khdhubUtil.js        # Wrapper
│       ├── castle.js             # Gamma — Castle scraper (AES-CBC encrypted, international)
│       ├── castleUtil.js         # Wrapper
│       ├── animekai.js           # Anime — AnimeKai scraper
│       ├── animekaiUtil.js       # Wrapper
│       ├── hianime.js            # HiAnime — alternative anime source (Megacloud decryption)
│       └── hianimeUtil.js        # Wrapper
│
├── services/
│   ├── tmdbApi.js                # TMDB API client — fetch, search, details, seasons, persons
│   ├── anilistApi.js             # AniList GraphQL client — browse, search, details
│   ├── authService.js            # TMDB OAuth — request tokens, sessions, watchlist, favorites
│   ├── listService.js            # TMDB custom lists CRUD
│   ├── progressService.js        # Watch history and progress tracking via AsyncStorage
│   ├── hlsCache.js               # HLS segment downloader and local M3U8 builder
│   ├── wyzieSubtitles.js         # Wyzie/OpenSubtitles API integration
│   ├── updateService.js          # Version check and update notification
│   └── translator/
│       ├── translator.js         # Google Translate API wrapper
│       └── translatorUtil.js     # Subtitle pre-processing utilities
│
├── CONTRIBUTION.md               # Style guide and development standards
├── WIKI.md                       # This file
├── package.json                  # Dependencies and scripts
└── app.json                      # Expo config — app name, icon, deep links, permissions
```

### Test Files

There are also several test scripts at the root level:
- `test-vidlinkUtil.js`
- `test-yflixUtil.js`
- `test-videasy.js`
- `test-4khdhub.js`
- `test-castle.js`
- `test-hianime.js`
- `test-animekai.js`

These are Node.js scripts you can run directly with `node test-vidlinkUtil.js` to test a specific scraper without launching the full app. Useful when a scraper stops working and you need to debug the API flow in isolation.

---

## 26. Data Sources and APIs Used

### TMDB (The Movie Database)

The foundation of all movie and TV show data. Used for:
- Trending content (week/day)
- New releases
- Top rated
- Provider-specific catalogs (Netflix, Disney+, Prime)
- Search (multi-search endpoint)
- Full title details with credits, videos, images, recommendations
- Season and episode details
- Person/actor details and combined credits
- Release calendar queries
- Authentication (OAuth token flow)
- Watchlist, favorites, custom lists

**API Key:** Multiple TMDB API keys are used across different scrapers. TMDB's free tier allows up to 40 requests per second which is more than enough.

**Rate limiting:** The home screen fires ~11 requests on startup. TMDB handles this fine. The calendar feature fires up to 62 requests (2 per day × 31 days) but these are parallelized and TMDB handles it.

### AniList GraphQL API

Used for all anime content. AniList's GraphQL API is public and doesn't require authentication for read operations.

Used for:
- Browsing anime by trending, popular, seasonal, top rated
- Searching anime by title
- Fetching full anime details (including airing schedule, studios, relations)
- Episode count lookup for scraper matching

### Jikan API (MyAnimeList Unofficial)

Used specifically within the AnimeKai scraper to verify episode counts. MyAnimeList often has accurate episode counts for completed series. The Jikan API is the unofficial MAL REST API.

Rate limit: Jikan limits to 60 requests/minute and 3 requests/second. The AnimeKai scraper handles 429 (rate limit) responses by waiting 1 second and retrying.

### OpenSubtitles via Wyzie API

Wyzie (`sub.wyzie.io`) is a subtitle aggregation service that wraps OpenSubtitles' database. OpenSubtitles is the largest community-maintained subtitle database in the world with subtitles in every language for virtually every movie and TV show.

The Wyzie API simplifies access by accepting TMDB IDs directly instead of requiring IMDB IDs or file hashes. The API key (`wyzie-195d06cff3a794da0fab3450dd99c491`) is included in the query string.

### Google Translate API

The public `translate.googleapis.com/translate_a/single` endpoint used by the AI translation system. No key required, client is set to `gtx`. This is the same endpoint used by many open source translation tools.

### enc-dec.app

A custom decryption service used by Vidlink, YFlix, Videasy, AnimeKai, and other scrapers. This service handles the actual cryptographic operations (decrypting stream data that the providers have encrypted to protect against automated scraping).

The service has different endpoints for different providers:
- `/api/dec-videasy` — Videasy
- `/api` — General purpose (Vidlink, YFlix)

### aesdec.nuvioapp.space

Used specifically by the Castle scraper for AES-CBC decryption. Castle uses a dynamic security key that changes, and this service handles the actual decryption when given the encrypted data and the security key.

### megacloud-keys (GitHub)

HiAnime uses Megacloud for its video delivery, and Megacloud rotates its AES decryption key periodically. The key is tracked by the community and kept updated at:
`https://raw.githubusercontent.com/ryanwtf88/megacloud-keys/refs/heads/master/key.txt`

The HiAnime scraper fetches this key at runtime and caches it in memory for the session.

---

## 27. Tech Stack & Key Dependencies

### Core Framework

| Package | Version | Purpose |
|---------|---------|---------|
| `expo` | ~54.0.x | Build tooling, native module access |
| `expo-router` | ~6.0.x | File-system based navigation |
| `react-native` | 0.76.x | Cross-platform UI framework |
| `react` | 18.3.x | Component library |

### Navigation

| Package | Purpose |
|---------|---------|
| `expo-router` | File-based routing (like Next.js but for mobile) |
| `@react-navigation/native` | Navigation primitives used by expo-router |

### Video Playback

| Package | Purpose |
|---------|---------|
| `react-native-video` | Core video player — wraps ExoPlayer on Android |
| `expo-screen-orientation` | Lock/unlock screen rotation |
| `expo-navigation-bar` | Hide/show Android nav bar |

### Storage

| Package | Purpose |
|---------|---------|
| `@react-native-async-storage/async-storage` | Persistent key-value storage (preferences, history, auth) |
| `expo-file-system` | File I/O for HLS cache segment storage |

### Network

| Package | Purpose |
|---------|---------|
| `axios` | HTTP client for TMDB API and translator |
| `node-fetch` | HTTP client in scraper Node.js files |
| `@react-native-community/netinfo` | Network connectivity monitoring |

### UI & Interactions

| Package | Purpose |
|---------|---------|
| `lucide-react-native` | Icon library (all icons throughout the app) |
| `@react-native-community/slider` | Seek bar in video player |
| `expo-clipboard` | Copy error logs to clipboard |

### Anime-Specific

| Package | Purpose |
|---------|---------|
| `cheerio-without-node-native` | HTML parsing in HiAnime scraper |
| `crypto-js` | AES decryption in HiAnime scraper |
| `qs` | Query string serialization in Videasy |

### Auth

| Package | Purpose |
|---------|---------|
| `expo-web-browser` | Opens TMDB OAuth page |

---

## 28. Style Guide & Design Language

YouFlex follows a strict **cinematic black & white** aesthetic. No colors, no gradients, no pastels. Pure cinema.

### Color Palette

| Variable | Value | Used For |
|----------|-------|---------|
| Primary Background | `#000` | All screen backgrounds |
| Secondary Background | `#0a0a0a` | Section backgrounds, modals |
| Tertiary Background | `#1a1a1a` | Cards, buttons, inputs |
| Text Primary | `#fff` | Main titles, important text |
| Text Secondary | `#d4d4d4` | Body text, descriptions |
| Text Tertiary | `#999` | Metadata, secondary labels |
| Border | `#333` or `#1a1a1a` | Card borders, dividers |
| Overlay Light | `rgba(0,0,0,0.5)` | Gradient overlays on images |
| Overlay Heavy | `rgba(0,0,0,0.92)` | Modal backgrounds |

### Typography

- **Screen titles**: 20–26px, `fontWeight: '800'`, `letterSpacing: 0.3–0.5`
- **Section headers**: 18px, `fontWeight: '800'`
- **Body text**: 14–15px, `fontWeight: '400'`, `lineHeight: 24`
- **Labels/metadata**: 12–14px, `fontWeight: '500'–'600'`, `lineHeight: 16`
- **Small text**: 11–12px

### Spacing

All spacing uses multiples of 4: 4, 8, 12, 16, 18, 20, 24, 28. Major section vertical margins use `marginVertical: 20–28`.

### Border Radius

- Cards/Posters: 12–14px
- Buttons: 10–12px
- Circular buttons: `borderRadius: 50%` of the button's width
- Modal/sheet: 24–28px (top corners only)

### Interactive Elements

All buttons have `activeOpacity={0.75}` or use `Animated.View` with scale animations. Press animations compress the element to 0.92 scale over 180ms. Release returns to 1.0.

### Card Widths

The `PosterCard` component calculates width for a 3-column grid:
```javascript
const columnSpacing = 16;
const horizontalPadding = 12;
const cardWidth = (screenWidth - (horizontalPadding * 2) - columnSpacing) / 3;
```

The search and actor pages use a slightly different formula:
```javascript
const cardWidth = (width - 32) / 3;  // 8px list padding on each side + 16px leftover
```

### What Must NOT Change

Per `CONTRIBUTION.md`, the search bar and search results overlay in `Header.js` are off-limits. They've been carefully tuned for UX and should not be touched.

---

## 29. Platform Availability & Roadmap

### Current: Android Only

YouFlex currently supports Android only, and that's not changing for now. Here's why each other platform is unavailable:

**iOS:**
Apple requires an Apple Developer Program membership ($99/year) to distribute apps, even for sideloading. Additionally, iOS distribution outside the App Store (via AltStore, sideloading, etc.) has significant limitations and user friction. App Store distribution is out of the question for obvious reasons. Until there's funding for a developer account and the willingness to navigate Apple's restrictions, iOS isn't happening.

The React Native codebase is mostly cross-platform so the iOS build would be straightforward technically — it's purely a business/distribution problem. When iOS support eventually comes, it will likely be through sideloading or TestFlight with a limited number of testers.

**Windows / macOS / Linux:**

Desktop support is planned but not started. Expo supports building for web (via Metro/React Native Web) and there's a React Native for macOS project. The main blockers are:

1. The scrapers are written as Node.js modules (`require()` style) and assume a Node.js environment. They use packages like `node-fetch`, `cheerio`, and `crypto-js` that are not available in the browser context. Making scrapers work on web requires either a proxy server (which introduces hosting complexity) or significant refactoring.

2. The HLS caching system uses `expo-file-system` for file I/O, which isn't available on web.

3. Screen orientation and navigation bar APIs are mobile-only.

Desktop support would likely mean either a native Electron wrapper around the app or a dedicated desktop rebuild. Either way it's a significant undertaking. It's on the roadmap but with no ETA.

### What's Planned

- **iOS sideloading** — Once/if funding for a developer account is available, or if a community-built IPA distribution system is set up.

- **Desktop (Windows/macOS/Linux)** — In planning. Most likely via Electron wrapping the web build, with a separate backend service for the scrapers.

- **More stream sources** — The scraper system is designed to be extensible. Adding a new source is a matter of writing a new provider module and adding it to the source selector in settings.

- **Subtitle source improvements** — OpenSubtitles via Wyzie covers most languages well, but other subtitle databases (Subscene, Addic7ed, etc.) could be added as additional tabs.

- **Download for offline** — Full episode downloads (not just the in-session HLS cache). This would require significant storage management UI and legal is even murkier than streaming.

- **Chromecast / AirPlay support** — react-native-video has some cast support but it's not implemented yet.

- **Notifications for new episodes** — When a show you've watched has a new episode drop, you could get a push notification. Needs a backend component.

---

## 30. FAQ

**Q: The video won't play / I get a black screen.**

A: Try switching to a different source in Settings. Go to Settings → Preferred Sources and try Alpha, then Omega, then Neon, then 4K, then Gamma. Different sources work for different content. Also try changing Default Quality to "Auto" in case a specific quality is failing.

**Q: Audio is out of sync with the video.**

A: This is usually a stream issue, not an app issue. Try a different source. If audio/video sync is fine but subtitles are off, use the Caption Appearance settings to add a positive or negative delay to subtitles.

**Q: Subtitles aren't showing.**

A: Make sure a subtitle is selected (tap the Subtitle button in the player). If the embedded subtitles aren't working, try the OpenSubs tab to fetch subtitles from OpenSubtitles. If you want any language, use the AI tab.

**Q: The AI translation looks wrong / is in the wrong language.**

A: Go to Settings → AI Language and make sure you've selected the right target language. Also make sure the source subtitle it's translating from is actually English or another language the translator handles well. If the source subtitle is in a language with unusual character sets (Arabic, Chinese), translation quality may vary.

**Q: The app crashes when opening a specific movie/show.**

A: This might be a scraper failure. Try a different source in Settings. If the crash happens on the details page (before you even press play), it might be a TMDB API issue — the content might have incomplete metadata. Rarely, some TMDB IDs return malformed responses for certain edge cases.

**Q: Why isn't [specific movie/show] available?**

A: Coverage depends entirely on the stream providers. New theatrical releases typically appear within a few days to a week of their digital release. Very old or obscure content may not be indexed by any of the providers. Try different sources — a title that's not on Alpha might be on Gamma or Neon.

**Q: The anime scraper is failing.**

A: AnimeKai and HiAnime's backends change periodically. These require the most maintenance of all the scrapers because anime streaming sites get DMCA'd and change infrastructure more frequently than general streaming aggregators. Check if there's an app update available.

**Q: Can I download content to watch later?**

A: Not currently. The HLS caching system keeps a temporary local copy while you watch, but it's deleted when you close the player. Full download support is planned for the future.

**Q: Does the app log in anywhere or send my data anywhere?**

A: No. The only network calls the app makes are to TMDB (for metadata), AniList (for anime data), the stream providers (to get video URLs), Wyzie/OpenSubtitles (if you use the OpenSubs subtitle tab), Google Translate (if you use AI subtitles), and whatever URL serves the video itself. No analytics, no tracking, no phone-home.

**Q: Is there a Telegram channel / Discord server?**

A: Check the repository's README for current community links.

**Q: Can I add a new stream source?**

A: Yes. Write a new provider module following the pattern of the existing ones — it needs to export a `getPlayableStreams({ tmdbId, mediaType, season, episode })` function that returns `{ streams, subtitles }`. Then add it to the `scraperMap` in `app/watch/index.js` and add a source option in `app/(tabs)/settings.js`. See the existing util wrappers for the expected interface.

**Q: The release calendar is slow to load.**

A: It fires up to 62 API requests at once. On a good connection this takes about 2–3 seconds. On a slow connection it can take considerably longer. The calendar shows a loading spinner while it's working. This is an area that could be improved with caching or a backend aggregator, but it works fine on typical mobile connections.

**Q: How do I report a bug?**

A: Use the error reporting system built into the player — when a stream fails, the error modal has a "Copy Error Log" button that puts a full diagnostic JSON onto your clipboard. Share that log with a bug report.

---

*YouFlex — Stream everything. Host nothing.*
