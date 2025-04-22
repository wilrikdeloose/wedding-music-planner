# Wedding Playlist Organizer

A single-page web application built with pure HTML, CSS, and JavaScript to organize a specific Spotify wedding playlist (`2S0g60Pj6okGDTvSUBgBs5`) into timed chapters, allowing reordering and saving back to Spotify.

## Features

*   Loads tracks from a specific Spotify playlist.
*   Organizes tracks into chapters based on a predefined wedding schedule.
*   Calculates and displays track start times, accounting for crossfade.
*   Adjustable crossfade duration (0-12 seconds) via a slider.
*   Drag-and-drop reordering of songs within and between chapters.
*   "Move to Chapter" buttons for quick relocation of songs.
*   Collapsible chapter sections.
*   Automatic saving of the playlist order to Spotify (debounced 5 seconds after changes).
*   Manual "Save" button for immediate saving to Spotify.
*   Manual "Reload" button to fetch the latest playlist state from Spotify.
*   Floating chapter markers on the right for easy navigation and visual context during scroll.
*   Remote playback control: Initiates playback of a selected track on the user's active Spotify device (requires `user-modify-playback-state` permission and an active Spotify client).
*   Uses Spotify Authorization Code Flow with PKCE for secure authentication.
*   Built entirely with vanilla HTML, CSS, and JavaScript (no external libraries or frameworks).
*   Includes `robots.txt` to discourage search engine indexing.

## Setup

1.  **Spotify Developer Account:** You need a Spotify account and must create an application on the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/).
2.  **Get Client ID:** From your Spotify application dashboard, copy the **Client ID**.
3.  **Configure Redirect URI:** In your Spotify application settings (under "Edit Settings"), add a **Redirect URI**. This URI **must** match the exact URL where you will host or access this `index.html` file. 
    *   For local development using a simple server (like Python's), this is often `http://localhost:8000/` or `http://localhost:8000/index.html` (use the specific address you intend to access the app with).
4.  **Edit `index.html`:** Open the `index.html` file in a text editor.
5.  Find the line containing `const CLIENT_ID =`. 
6.  Replace the placeholder value (if present, or the existing ID) with your actual **Client ID** obtained in step 2.

## Usage

1.  **Serve the File:** This application needs to be served by a web server because of Spotify API requirements (CORS, Redirect URI). You cannot simply open the `index.html` file directly in your browser from your filesystem.
    *   A simple way to run a local server is using Python:
        *   Open your terminal or command prompt.
        *   Navigate (`cd`) to the directory containing the `index.html` file.
        *   Run the command: `python -m http.server` (for Python 3) or `python -m SimpleHTTPServer` (for Python 2).
        *   The server will usually start on port 8000.
2.  **Access the App:** Open your web browser and navigate to the address provided by the server (e.g., `http://localhost:8000/` or `http://localhost:8000/index.html`). Ensure this URL exactly matches the Redirect URI you configured in the Spotify Developer Dashboard.
3.  **Login:** Click the "Login with Spotify" button and follow the prompts to authorize the application. You may need to grant permissions including reading playlists, modifying playlists, and controlling playback state.
4.  **Organize:** 
    *   Drag and drop songs to reorder them.
    *   Click the move icon (`↔️`) next to a song and select a destination chapter.
    *   Click chapter headers to collapse/expand them.
    *   Use the slider to adjust the crossfade.
    *   Use the chapter markers on the right to navigate.
5.  **Saving:** Changes are saved automatically to Spotify 5 seconds after you stop making modifications (dragging, moving). Use the floating manual save button (`💾`) for an immediate save.
6.  **Playback:** Click the play icon (`▶️`) next to a song title to request playback on your currently active Spotify device (Desktop app, Web Player, Mobile app, etc.). Make sure a device is active.
7.  **Reload:** Click the floating reload button (`🔄`) to discard local changes and reload the current playlist order from Spotify.

## Important Notes

*   **Permissions:** To successfully save changes to the playlist, the logged-in Spotify user **must** be the owner of the playlist or have been invited as a collaborator via Spotify.
*   **Playback Control:** Remote playback requires an active Spotify client to be running and may require a Spotify Premium account. If playback fails, try interacting (play/pause) with your desired Spotify client first.
*   **Hardcoded Values:** The specific Spotify Playlist ID and the wedding chapter schedule (names and times) are hardcoded within the `<script>` section of `index.html`. Modify the `PLAYLIST_ID` and `chapters` constants if you need to adapt this for a different playlist or schedule.
*   **No Dependencies:** Requires only a modern web browser with JavaScript enabled. 