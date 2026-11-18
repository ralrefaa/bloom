# Bloom — personal dashboard PWA

## What works
- Tasks, medical-study topics, daily habits, mood, journal and workout log.
- Data is saved locally in the browser's localStorage. There is no account, server or cloud backup. Avoid storing highly sensitive information; clearing site data or reinstalling can erase it.
- Calendar currently opens Google Calendar in a separate tab. **Google Calendar API synchronization is not implemented.**

## Try locally
Use a local HTTP server (for example `python3 -m http.server 8000` in this directory), then open http://localhost:8000 on your computer.

## Install on iPhone
Deploy this directory to an HTTPS static host (such as GitHub Pages or Netlify). Open its HTTPS URL in iPhone Safari, tap Share, then Add to Home Screen. Keep the deployment private in the sense of not publishing or advertising the link; note that a public static URL is not access-controlled. Avoid putting secrets in these files.

## Google Calendar OAuth — next phase
1. In Google Cloud Console create a project, enable Google Calendar API, configure OAuth consent screen (External / Testing if appropriate) and add your own Google account as a test user.
2. Create an OAuth 2.0 Web application client and register the exact HTTPS origin used for the hosted app. Do not put a client secret into the PWA.
3. Use Google Identity Services' browser authorization code flow with PKCE where supported, and a small secure backend to exchange/store credentials. Alternatively, browser-only token flow can support a session-limited read-only integration but should not be treated as durable background sync.
4. Start with the least-privileged calendar scope needed (e.g. `https://www.googleapis.com/auth/calendar.events.readonly` for event viewing), request additional scopes only for writing.
5. Store tokens server-side if persistent synchronization is required; never put refresh tokens or client secrets in client-side JavaScript/localStorage. Include sign-out/revoke and handle Google OAuth verification/test-mode limitations.

This starter is a prototype, not a production-ready sensitive-data journal.
