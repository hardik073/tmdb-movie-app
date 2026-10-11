# UI/UX Design

## Purpose

This document records the current UI/UX direction for the Movie App based on the mock design that I have thought of based on the actual web. It translates the visible screens and patterns into a shared reference for future design and implementation work; it does not prescribe Android implementation details.


## Design Direction

- **Visual style:** Dark, cinematic interface with movie and TV artwork as a major visual element.
- **Information density:** Content-rich screens use clearly separated sections, compact metadata, cards, chips, and horizontal collections.
- **Primary emphasis:** Help users discover content, inspect structured details, track their activity, and explore community information.
- **Themes:** First, we will focus on the primary theme, and then later we will decide to make light and dark themes.

## Primary Navigation

The bottom navigation shown in the design has five destinations:

1. **Home** — featured and curated discovery content.
2. **Discover** — search and browse content, including result filtering.
3. **Watchlist** — access saved content.
4. **Community** — community activity and contribution-related content.
5. **Profile** — personal statistics, ratings, lists, reviews, and account-related options.

## Screen Inventory

### 1. Home

The Home screen is a vertically scrollable discovery feed.

- A top app bar with the app identity, Home destination, notifications, and profile/avatar access.
- A prominent featured-content area.
- A search entry point.
- A Trending section with a time-period selector.
- A Latest Trailers section with content-type or collection controls.
- A What's Popular section with a streaming/on-TV selector.
- A Free to Watch section with movie/TV selection.
- A Leaderboard section with user ranking or progress summaries.
- A community-oriented footer or information area.
- Persistent bottom navigation.


### 2. Discover / Search Results

The supplied search screen shows:

- A search field containing the current query.
- A clear-query control and search action.
- Controls for movie and TV-show result types.
- A result count and a concise description of the current query.
- Sorting and filtering controls.
- A vertically scrolling list of result cards.
- Result cards with poster artwork, title, year or release date, content type, overview text, and relevant actions such as saving.
- A load-more control for additional results.
- Bottom navigation.

### 3. Content Details

The details screen is a vertically scrollable page with a large artwork or backdrop area and multiple information sections. The screenshot shows:

- A backdrop/hero image and poster/title treatment.
- Release or availability information and basic metadata.
- A user score or rating area.
- Quick actions, including rating, marking watched, saving, or sharing where represented.
- An overview section.
- A people/cast-and-crew section.
- A media section with tabs or chips for media types.
- Movie facts and keywords.
- Recommendations.
- A featured list or related collection.
- Bottom navigation.


### 4. Leaderboard

The leaderboard screen shown in the design includes:

- A back navigation control and screen title.
- Sharing and additional-actions controls.
- A highlighted top-ranked user or featured leaderboard entry.
- A follow action and a message action where represented.
- A weekly pace or progress indicator.
- Contribution statistics such as edits, additions, or other contribution totals.
- Contribution impact metrics.
- Badges and milestones.
- Tabs or filters for overview, ratings, watchlist, and lists.
- Recent edits and additions.
- Top-rated content or other user-curated content.

This screen combines rankings with a deeper view of a user's community contributions. The calculations and rules behind scores, ranks, badges, and milestones are product logic and are not defined by the visual layout alone.

### 5. Community Feed / User Activity

The supplied screens show a content-rich activity feed associated with a user or community view. It includes:

- User identity and profile summary.
- Follow and other profile-level actions.
- A list of watched, rated, saved, or otherwise contributed content.
- Content cards with artwork, metadata, review/activity text, and relevant status indicators.
- Actions such as marking watched, rating, saving, or sharing where shown.
- A load-more control.
- Bottom navigation.

### 6. Profile

The profile screen shown in the design includes:

- Profile image, display name, and account summary.
- A profile header with edit and other account-related actions.
- Summary counts for movies, TV shows, ratings, and lists.
- Tabs or sections for overview, watchlist, ratings, and lists.
- Viewing milestones or statistics, such as total time watched and average rating.
- Recently rated content.
- Watchlist queue.
- Curated or public lists.
- Integrations and system/account options, including streaming services, export data and lists, and switching or signing out where shown.

The screen should keep personal statistics and collections organized into clear sections, with links to more detailed views where indicated.

## Shared UI Patterns

The supplied design uses the following recurring patterns:

- Poster cards and larger featured artwork.
- Horizontal carousels for discovery collections.
- Vertical lists for search results and activity feeds.
- Clearly labeled section headings and optional “see all” or similar links.
- Chips and segmented controls for content type, time period, media type, or section selection.
- Compact metadata such as year, rating, runtime, and content type.
- Distinct visual treatment for watched, saved, or rated status.
- Progress bars, counts, and badges for leaderboard or profile statistics.
- Persistent bottom navigation on the main destinations.
- Back navigation for secondary screens such as Content Details or Leaderboard.

Use these patterns consistently across the app. Avoid introducing new patterns without a clear need.

## Theme and Readability

- The reference design uses a dark navy/blue base, contrasting text, bright cyan accents, and occasional green status/progress accents.
- Poster and backdrop imagery should remain visually prominent.
- Text, metadata, icons, and interactive controls should remain legible against their backgrounds.
- Both light and dark themes are in the planned scope. The light theme should preserve the same information hierarchy and interaction patterns; exact light-theme tokens should be documented when the design is available.
- Do not infer exact color codes, font families, spacing values, or corner radii from the overview screenshot. Use the Figma source for exact design tokens.

## Navigation and Interaction Principles

- Selecting a movie or TV show opens its Content Details screen.
- Search results and discovery cards should provide a consistent route to Content Details.
- Watchlist and profile collections should allow users to open the corresponding content.
- User names, leaderboard entries, and community activity can lead to the relevant user or contribution view where shown in the prototype.
- Back navigation should return users to the previous context where practical.
- Tabs, chips, and filters should make the currently selected option clear.
- Actions such as save, watched, rating, follow, and share should provide visible state or feedback consistent with the product rules.

The overview screenshot establishes the presence of these controls but does not fully specify all tap outcomes. Use the Figma prototype to verify detailed interactions before implementation.

## Implementation Boundary

This document describes UI/UX intent only. It does not select Compose components, navigation libraries, state-management APIs, image-loading libraries, or other implementation specifics. Those choices belong in the architecture and implementation work.
There can be more or less addition or removal of the content of data from UI as per the API response and parameters.
