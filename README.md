# Nija

An Android browser built on the system WebView. No Google Play Services, no account,
no telemetry.

Package `in.nijatva.browser` · Android 7 and up · about 9 MB · free

---

## What it is

Most Android browsers either ship their own copy of Chromium or are a thin shell around a
WebView with an address bar. Nija is the second kind, taken seriously: the engine is the
one already on your phone, and everything around it — blocking, tabs, containers, reading,
speech, downloads — is written here.

Because the engine is the system's, the install is a few megabytes and security fixes
arrive with the operating system rather than with an app update. The trade is real and is
listed under [What it does not do](#what-it-does-not-do).

## What it does

**Blocking.** Network and cosmetic filter rules are applied on the device from lists
inside the APK — nothing is sent to a filtering service. There is a per-site allow list, a
blocked counter, and an element picker for the boxes a rule cannot catch. Tracking
parameters are stripped from a link before it loads.

**Tabs and containers.** Named, colour-coded containers hold their own tab sets, so work
and personal browsing do not share one pile. Each container can carry its own user agent.

**Reading.** Reader mode scores the page for the densest block of text, strips the
navigation and furniture, and rewrites the article in place with its own typography:
light, sepia or dark, 13–28px, optional bionic text, optional vertical writing for CJK.
Articles can be saved to a local reading list.

**Speech.** Pages are read aloud through Android's own TTS engine — no cloud voice. Rate,
pitch, a pronunciation dictionary, a sleep timer, and a highlight that follows the
sentence being spoken.

**Downloads.** Media links are fetched by the browser itself, including HLS playlists,
with AES-128 decryption where the playlist asks for it.

**The rest.** Bookmarks, history with per-row delete, tab groups that survive a restart,
a private mode that keeps extensions out unless you turn them on, HTTPS-only, a per-site
zoom and dark-mode setting, and a settings screen with search over 34 screens.

## Extensions

Nija installs small scripts from its own store — 39 of them, each with an icon, a
version, a category and the permissions it asks for. The catalogue is a JSON file with a
signature and a sha256 per script; both this browser and the store page read it, and a
script that changed under you is refused rather than installed.

These are scripts, not Chrome extensions. See the next section for why.

Store: <https://vasudev-work.github.io/nijatva-web-store/>

## What it does not do

Being clear about this is more useful than a longer feature list.

- **No Chrome extensions.** The system WebView has no `chrome.*` API, no `webRequest` and
  no background page. Anything that needs those cannot work here, whatever the store says.
- **No DRM video.** Widevine is not available to WebView apps, so subscription streaming
  services that require it will not play.
- **No custom request headers or DNS-over-HTTPS.** WebView exposes neither.
- **Containers are not yet a privacy boundary.** All containers currently share one cookie
  store, so a site you are signed into in one is signed into in another. Treat them as tab
  groups until isolation lands.
- **No sync and no account.** Nothing leaves the device, which also means nothing follows
  you to another phone.

## Where your data lives

Bookmarks, history, containers, passwords, saved articles, settings and the filter lists
are plain files in the app's own storage. There is no server to send them to. Clearing
site data from Settings removes cookies and storage; uninstalling removes everything.

## Install

Download the APK from [Releases](https://github.com/vasudev-work/nijatva-browser/releases)
and open it. Android will ask you to allow installing from this source — the build is
signed with a debug key, which is why that prompt appears.

## Build

```bash
./gradlew assembleDebug
```

The APK lands in `app/build/outputs/apk/debug/`. GitHub Actions builds one on every push
to `main` and keeps it as a workflow artifact.

## Layout

```
app/src/main/java/in/nijatva/browser/   activities, engine, stores
app/src/main/assets/                    filter lists, new-tab page, keep-alive
app/src/main/res/                       layouts, drawables, strings
desktop/                                JavaFX build for macOS, Windows and Linux
docs/                                   the landing page served by GitHub Pages
tools/                                  store index and signing helpers
```

## Licence

No licence file is included yet, which under copyright means all rights reserved. If you
want to reuse part of this, open an issue and ask.

## Contact

Issues and feature requests: <https://github.com/vasudev-work/nijatva-browser/issues>

Email: vasudev.work@rediffmail.com
