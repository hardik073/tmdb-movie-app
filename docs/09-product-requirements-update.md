# Product Requirements Update

## Purpose

This document records the updated product scope reflected in the current Figma design. It supplements the original Phase 1 product documents rather than replacing them. The original documents remain as the record of the initial product direction; this update captures the expanded scope to guide the next design and implementation phases.

The Figma design is the current visual reference for the screens and capabilities listed here. Details that are not clearly established by the design are intentionally left open rather than treated as confirmed requirements.

## Product Direction

The Movie App is a movie and TV-show discovery and tracking experience. It helps users discover content, explore structured information, keep track of what they watch, and engage with a community of other users.

## Updated Scope

All screens represented in the supplied Figma design are included in the intended product scope.

### 1. Home and Discovery

- Present featured content and curated discovery sections.
- Show collections such as trending content, popular titles, free-to-watch content, and latest trailers.
- Support discovery of both movies and TV shows.
- Include leaderboard or community highlights where represented in the design.
- Provide entry points to search and explore content.

### 2. Search and Results

- Search for movies and TV shows by title.
- Allow users to distinguish or filter movie and TV-show results.
- Display matching content in a structured results list.
- Include sorting and filtering controls shown in the design.
- Provide a way to open a result's content details.

### 3. Content Details

- Provide a dedicated details screen for a movie or TV show.
- Show relevant artwork and key metadata, such as title, release information, content type, runtime or episode information where available, and ratings.
- Include an overview or synopsis.
- Present related information sections represented in the design, including cast and crew, media, facts, keywords, recommendations, and featured lists where applicable.
- Provide actions represented in the design, such as rating, marking content as watched, saving content, or sharing it.
- The information displayed may vary depending on whether the selected item is a movie or a TV show.

### 4. Watchlist and Watched Content

- Provide a destination for saved content.
- Distinguish saved content from content marked as watched where the design indicates.
- Show content in organized lists or cards.
- Support access to the relevant content details from these collections.

### 5. Community

- Present user activity and contributions, including activity or review-style content.
- Support community-oriented content discovery.

### 6. Leaderboard

- Present ranked users and leaderboard information.
- Show user contribution or activity metrics, including scores and progress indicators where represented.
- Include user profile entry points from leaderboard items.
- Present contribution impact, badges, milestones, and recent edits or activity where shown.

### 7. User Profile

- Can be designed based on the real profile of the Use in TMBD Web

### 8. User Content Activity

The design represents several ways for a user to track or contribute information about content, including:

- Marking content as watched.
- Saving content to a watchlist.
- Rating content.
- Creating or viewing lists.
- Writing or viewing reviews and activity entries.
- Viewing contribution scores, badges, milestones, or edit history where available.

The exact rules for these actions, including permissions, validation, and persistence, remain to be specified where the Figma design does not establish them.

## Primary Navigation

The supplied design shows five bottom-navigation destinations:

1. Home
2. Discover
3. Watchlist
4. Community
5. Profile

This supersedes the earlier working assumption of four destinations (Home, Search, Categories, and Watchlist). Search and category/filter exploration should be represented within the relevant screen flows unless the design is later updated to show them as separate top-level destinations.

## Product Content Types

- Movies
- TV shows / series

The interface should make the content type clear where users browse, search, or view details.

## Requirements Boundaries

This update captures product capabilities visible in the current mock design. It does not, by itself, settle:

- The data provider, API contracts, or availability of specific metadata.
- Authentication provider or account-creation flow.
- The backend and persistence strategy for ratings, reviews, lists, watch history, and community activity.
- Exact business rules for contribution scores, badges, leaderboard calculations, or milestones.
- Moderation, reporting, privacy, or abuse-prevention rules for community features.
- Exact offline behavior and synchronization rules.
- Loading, empty, error, and permission states not represented in the supplied design.
- Exact responsive behavior, accessibility specifications, and interaction details not evident in the screenshot.

These should be decided only when needed and documented in the relevant product, system design, or implementation documents.

## Relationship to Existing Documents

- The original Phase 1 documents remain unchanged.
- This document records the expanded requirements inferred from the current mock design.
- `10-ui-ux-design.md` describes the visible screen structure, navigation, visual direction, and user flows.
- If a conflict arises between the original scope and this update, this update is the current working scope for Phase 2 onward, subject to later explicit decisions.

## Status

Draft based on the supplied mock design.
