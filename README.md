## Introduction

Thank you for using my Spotify app. This app was created with minimal dependencies, using Vue.js and Vite (modern replacement for the Vue.js CLI).

## Installation

To run the app, please ensure you have at least Node.js v16 or higher installed along with Node Package Manager (npm).

To install dependencies, run "npm install" in the "unherd-technical-assessment" folder and allow the installation to finish. This should the ideal environment to inspect the assessment.

Then to run locally with Vite, run "npm run dev" to launch a local development server.

ctrl/command click to open the app at a local URL in your default browser.

## App features

This app allows your to query the Spotify API via an text search across a range of types. The types are selectable via the dropdown menu. The available types are:

Artist, Album, Playlist, Track, Show, Episode, Audiobook.

There is also an option to configure the quantity of results your search will return, but the further down the results, the less accurate the Spotify search typically is.

The app shows the title, along with some extra information if it exists, such as album art, album release date, genre or narrators for audiobooks.

The results link to the correct content on the Spotify web player when clicked (title or album art).
