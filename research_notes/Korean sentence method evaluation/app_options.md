# Building a Personal Android Sentence-Shadowing + Spaced-Repetition App vs. Using Existing Apps (as of Nov 2026)

Research note: several primary hosts could not be fetched from this research session (android-developers.googleblog.com, androidauthority.com, developer.chrome.com, docs.ankiweb.net, whatpwacando.today were outside the sandbox's allowed network). Findings for those come from search-result summaries of the pages, not full reads. developer.android.com and github.com were fetched directly.

## 1. Sideloading APKs in 2026 and Google's developer verification

### Takeaway
A personal APK still installs on the user's own phone. `adb install` from the laptop is exempt from developer verification, and nothing is enforced outside Brazil, Indonesia, Singapore and Thailand until 2027. Two other routes also work: Google's free "limited distribution" hobbyist account (up to 20 devices, no ID or fee), or the one-time "advanced flow" (Developer Options toggle, restart, 24-hour wait). For a trip starting within days, set up the advanced flow or ADB **before** leaving, because the 24-hour wait can't be hurried.

### Cited Findings
- Official timeline: in August 2026, developer APIs, limited distribution accounts and the power-user "advanced flow" launch. On **September 30, 2026**, protections begin for installs from participating stores in **Brazil, Indonesia, Singapore and Thailand** on certified devices running Android 7+. In "2027 and beyond", verification expands globally. — [Android Developers: Developer verification](https://developer.android.com/developer-verification)
- "Students, teachers, and hobbyists can share apps with up to 20 devices without a government-issued ID or registration fee" (limited distribution account). — [Android Developers: Developer verification](https://developer.android.com/developer-verification)
- The official landing page itself does **not** mention an ADB exemption. — [Android Developers: Developer verification](https://developer.android.com/developer-verification)
- Google's June 2026 blog post (summary seen via search only) says unregistered apps can be sideloaded "with Android Debug Bridge (adb) or advanced flow". A free limited distribution account needs only an email address. — [Android Developers Blog, June 2026](https://android-developers.googleblog.com/2026/06/android-developer-verification.html)
- Gadget Hacks reports that Google's verification FAQ confirms ADB remains exempt. — [Gadget Hacks](https://android.gadgethacks.com/news/google-android-sideloading-rules-2026-changes-explained/)
- Advanced flow steps: Developer Options, then "Allow apps from unverified developers". Authenticate with the screen lock and confirm nobody is pressuring you. Restart, wait 24 hours, re-authenticate, then choose to allow unverified installs for 7 days or indefinitely. It is a **one-time** process, not a per-APK timer. If the flow is disabled, a 10-minute grace period applies. Turning it off also blocks updates to unverified apps. ADB is not part of the advanced flow. — [The Hacker News](https://thehackernews.com/2026/03/google-adds-24-hour-wait-for-unverified.html); [9to5Google, Aug 18 2026](https://9to5google.com/2026/08/18/google-gradually-rolling-out-androids-advanced-sideloading-ahead-of-developer-verification/); [XDA](https://www.xda-developers.com/googles-controversial-advanced-flow-sideloading-rolling-out-ahead-of-stricter-developer-verification/)
- The advanced flow is "rolling out gradually", so some devices may not show it yet. — [9to5Google](https://9to5google.com/2026/08/18/google-gradually-rolling-out-androids-advanced-sideloading-ahead-of-developer-verification/)
- Secondary sources conflict on details, for example whether the verifier is active or still dormant in non-launch regions. — [Android Authority (first-wave rollout)](https://www.androidauthority.com/android-sideloading-developer-verification-first-wave-rollout-3717921/); [primetestlab](https://primetestlab.com/blog/sideload-apk-after-developer-verification)

### Inferences
- Korea and the user's home country are presumably not among the four September 2026 launch countries. So in Nov–Dec 2026 a self-built APK probably installs with the classic "install unknown apps" prompt, with no verification check at all. The ADB and advanced-flow notes matter mainly as future-proofing for 2027. (The user's home country wasn't stated, so confirm it.)
- Safest dev loop for a beginner: USB debugging plus `adb install app.apk`, or `flutter run` / `npx expo run:android`, which use ADB under the hood. It is exempt in every announced phase and needs no Google account.
- A PWA avoids the APK question entirely: it installs from Chrome and is not an APK sideload.

### Gaps
- I could not read Google's FAQ directly to confirm the ADB exemption in its own words. It relies on the June 2026 blog summary and Gadget Hacks.
- Whether Samsung/OEM skins add their own extra prompts was not researched.

## 2. PWA vs Flutter vs React Native/Expo vs native Kotlin

### Takeaway
The make-or-break requirement is **looping a playlist with the screen off for 30+ minutes**. That is the weakest point for a PWA, and even Expo's audio module has reported Android cutoffs. A native-shell app with a proper media foreground service (Flutter + `just_audio`/`audio_service`, or Kotlin + Media3) is the most reliable. Either one costs a beginner more setup (Android Studio/SDK) than a PWA. For "usable in a few days", a PWA is fastest to build, but the user must test background audio on their own phone on day 1.

### Cited Findings
- PWA/web: Chrome for Android disables audio autoplay, so `play()` must follow a user gesture. — [Chrome Developers: Media Session](https://developer.chrome.com/blog/media-session/) (via search summary)
- The Media Session API supports next/previous handlers from the media notification. Chrome's sample loops a playlist with `index = (index + 1) % playlist.length`. — [Chrome Developers: Media Session](https://developer.chrome.com/blog/media-session/)
- Mobile browsers "pause media, throttle, or freeze background tabs" when the screen is off or the user switches apps. Chrome has no in-app background-audio toggle, and the suggested workaround is the per-app battery setting. — [Androxus](https://androxus.com/blogs/play-music-from-any-website-background) (secondary, low authority)
- Anecdote (June 2026): a PWA stopped after two tracks or about 11 minutes with the screen locked, even with battery restrictions removed. A commenter suggested an app bug. Unverified. — [Reddit snapshot](https://reddit.sentinel-team.org/posts/1u15l75/snapshots/2026-06-09T23%3A37%3A29.450403Z)
- Expo: `enableBackgroundPlayback` adds a media-playback foreground service. Lock-screen controls (`setActiveForLockScreen`) are "required for sustained background playback" on Android, and without them audio stops after about 3 minutes (OS limitation). — [Expo docs: expo-audio](https://docs.expo.dev/versions/latest/sdk/audio/)
- Expo bug report: background playback stopped after about 10–15 minutes with the screen locked, because ActivityManager reaped AudioControlsService as "app idle". — [expo/expo #49906](https://github.com/expo/expo/issues/49906)
- An expo-audio maintainer called the module "still experimental" when asked about custom Previous/Next lock-screen callbacks (early 2026). — [expo/expo discussion #43351](https://github.com/expo/expo/discussions/43351)
- Background-audio changes in Expo need a native build (EAS Build or prebuild with a dev client) and can't be tested in Expo Go. — [xolace_app issue #366](https://github.com/xolace-official/xolace_app/issues/366)
- react-native-track-player is the more mature alternative to expo-audio for playlist/background use. — [LogRocket](https://blog.logrocket.com/react-native-track-player-vs-expo-audio/)

### Inferences
These come from general platform knowledge, not sources fetched in this session. Verify them.
- **PWA:**
  - Fastest to iterate: one HTML/JS codebase, edits test instantly on the laptop, and it can be hosted free on GitHub Pages.
  - Offline: a Service Worker plus the Cache API or IndexedDB can store MP3s.
  - Microphone: `MediaRecorder` + `getUserMedia` works in Chrome Android over HTTPS.
  - Risks: background looping playback, and Chrome evicting storage under pressure (call `navigator.storage.persist()`).
- **Flutter:**
  - One Dart codebase. `flutter build apk` produces a sideloadable APK locally with no cloud account.
  - Mature packages: `just_audio` (gapless and looping playlists) with `audio_service` (foreground service and lock-screen controls), `record` (mic), `sqflite` or `drift` (SQLite), `flutter_tts`.
  - Needs the Android SDK/Android Studio installed, which takes a few GB and about an hour of setup.
  - Dart port of FSRS: the FSRS org lists Dart among its implementation languages ([longtermemory](https://longtermemory.com/b/fsrs-vs-sm2/)).
- **React Native/Expo:**
  - JS/TS, a good fit if the AI assistant writes TS. ts-fsrs drops in.
  - Background audio has the caveats above.
  - EAS cloud builds have a free tier with queues. Local builds (`npx expo run:android` or `eas build --local`) still need the Android SDK. Free-tier limits were not verified this session.
- **Native Kotlin:**
  - Most reliable: Media3 ExoPlayer + MediaSessionService for screen-off loops, plus built-in TextToSpeech and SpeechRecognizer.
  - Steepest curve for a beginner. Android Studio is mandatory.
- **Hybrid option worth flagging:** a PWA wrapped with Capacitor or a Trusted Web Activity. This keeps web code and adds native background audio plugins, but adds toolchain complexity. Not researched in depth.

### Gaps
- Could not fetch Chrome's or MDN's docs on PWA background playback, so there is no authoritative statement on screen-off duration limits.
- EAS free-tier build quotas for late 2026 were not verified.
- No first-hand source compared Flutter `audio_service` reliability on recent Android (15–17).

## 3. Spaced repetition: SM-2 vs FSRS

### Takeaway
FSRS predicts recall better than SM-2 and usually needs fewer reviews. It is free and MIT-licensed in TypeScript (ts-fsrs) and many other languages. Using a library makes it about a day's integration. Hand-coding SM-2 is roughly 20 lines and fine for an MVP.

### Cited Findings
- ts-fsrs: TypeScript FSRS toolkit, MIT license, ESM/CJS/UMD builds. Supports FSRS versions 3, 4.5, 6 and 7, and `DefaultScheduler()` uses FSRS-7. Example API: `const scheduler = await DefaultScheduler(); const card = scheduler.newCard({ now }); scheduler.review({ card, grade: Rating.Good, now })`. ts-fsrs v6 requires Node.js ≥ 24 for its tooling. — [GitHub: open-spaced-repetition/ts-fsrs](https://github.com/open-spaced-repetition/ts-fsrs)
- FSRS implementations exist in "Python, Go, Rust, TypeScript, Swift, Dart, and a dozen other" languages. — [longtermemory.com](https://longtermemory.com/b/fsrs-vs-sm2/)
- A mid-2025 benchmark cited by a blog put FSRS prediction error at about 4% vs 13–15% for SM-2. The source is commercial, so treat it as indicative. — [studyglen](https://studyglen.com/guides/best-spaced-repetition-apps)
- SM-2 often shows new cards at unnecessarily short intervals, and FSRS avoids many unneeded reviews. Another blog says FSRS is more conservative for mature cards. — [mindomax](https://www.mindomax.com/fsrs-vs-sm2-spaced-repetition-algorithm); [smartrecallai](https://smartrecallai.com/blog/fsrs-vs-sm2-deep-dive)
- AnkiDroid supports FSRS from version 2.17 onward (since about February 2024). It is a per-collection setting, and SM-2 remains Anki's default. — [slidetoanki](https://slidetoanki.com/blog/how-to-use-fsrs-anki-guide); [fsrs4anki tutorial](https://github.com/open-spaced-repetition/fsrs4anki/blob/main/docs/tutorial.md)
- A Hacker News user reports using ts-fsrs "without problems". — [HN](https://news.ycombinator.com/item?id=42908863)

### Inferences
- The hard part is the data model and UI, not the algorithm: store card state and review logs, build the "due today" queue, and add 4-button grading. A custom app should save review logs from day 1 so FSRS parameters can be optimised later. The repo includes a binding package for training parameters from logs.
- The ts-fsrs README snippet above reflects the current major version. Older tutorials use `fsrs()`, `createEmptyCard()` and `repeat()`, so an AI assistant may produce outdated API calls. Pin the version.

### Gaps
- I didn't confirm whether the ts-fsrs browser bundle needs a build step, or whether Node ≥ 24 applies only to tooling or also to the runtime.

## 4. On-device Korean TTS and speech recognition

### Takeaway
Korean TTS and recognition can both run offline on Android, but only after language packs are downloaded in advance. Download them **before** the trip, over Wi-Fi. Pre-generated MP3s from a good TTS or native recordings stay the more reliable primary audio. Device TTS is a free fallback, and on-device recognition can give rough "did I say it right" feedback.

### Cited Findings
- Android `SpeechRecognizer`:
  - `createOnDeviceSpeechRecognizer()` and `isOnDeviceRecognitionAvailable()` require API 31 (Android 12).
  - `triggerModelDownload()` (API 33+) "attempts to download the support" for a language and may need user approval.
  - `ERROR_LANGUAGE_UNAVAILABLE` means the language is "supported, but not available currently (e.g. not downloaded yet)".
  - The default (non-on-device) implementation "is likely to stream audio to remote servers" and needs the RECORD_AUDIO permission.
  - Source: [Android Developers: SpeechRecognizer](https://developer.android.com/reference/android/speech/SpeechRecognizer)
- Web Speech API recognition is server-based by default and doesn't work offline. — [MDN: Using the Web Speech API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API/Using_the_Web_Speech_API)
- Chrome 139 added on-device recognition via `processLocally: true`, with a one-time language-pack download per language. After that it works offline. ko-KR is listed as a supported on-device locale. `available()` and `install()` are gated by the "on-device-speech-recognition" permissions policy. — [W3C/WebAudio explainer](https://github.com/WebAudio/web-speech-api/blob/main/explainers/on-device-speech-recognition.md); [Medium: On-Device Speech UIs in Chrome 139](https://medium.com/@roman_fedyskyi/on-device-speech-uis-in-chrome-139-4b9f0397b9c9)
- Chrome Android support for Web Speech recognition is inconsistent across sources: "since Chrome 25 (webkit-prefixed)" vs "Partial (v134)". There is also an open bug report that it doesn't work in Chrome on Android. — [addpipe](https://blog.addpipe.com/a-deep-dive-into-the-web-speech-api/); [mdn/browser-compat-data #25794](https://github.com/mdn/browser-compat-data/issues/25794)
- For `speechSynthesis`, voices load asynchronously (wait for `voiceschanged` before `getVoices()`). Whether a voice is local is shown by its `localService` flag. — [webreflection](https://webreflection.medium.com/taming-the-web-speech-api-ef64f5a245e1); [W3C Web Speech spec](https://webaudio.github.io/web-speech-api/)
- AnkiDroid manual: card text can be read with the Android TTS engine. Google's built-in engine "should work" and third-party engines "may or may not". `<tts>` tags need `service="android"` and a voice/language attribute. — [AnkiDroid User Manual](https://docs.ankidroid.org/)

### Inferences
- Pre-trip checklist:
  - Install Google "Speech Recognition & Synthesis" Korean voice data.
  - Download Korean for offline speech recognition (Settings > Languages/Voice input, depending on OEM).
  - Verify both in airplane mode.
- Speech-recognition scoring for pronunciation is crude: it returns text, not phoneme accuracy. Record-and-compare (play the native clip, then your own clip) is the more useful shadowing feedback and needs no recognition at all.

### Gaps
- I found no source confirming offline Korean `speechSynthesis` voices in Chrome Android specifically. It needs a device test.
- Quality of Google's offline Korean TTS voice vs cloud TTS was not assessed.

## 5. Existing alternatives compared to the custom idea

### Takeaway
**AnkiDroid already covers about 80% of the custom app**: free, offline, FSRS, audio fields, Android TTS, a built-in record-and-playback "Check Pronunciation" toolbar, CSV import and AnkiWeb sync. The parts it does badly are hands-free looping sentence playlists with the screen off, and a frictionless "add a niche sentence list" flow on the phone. Commercial apps (Glossika, Migaku) are sentence-based but expensive, and none let you load your own skateboarding sentence list as easily as a CSV in Anki.

### Cited Findings
- **AnkiDroid:**
  - FSRS from 2.17 ([slidetoanki](https://slidetoanki.com/blog/how-to-use-fsrs-anki-guide)).
  - "Check Pronunciation" in the manual is "a temporary audio recorder toolbar" with play, stop and record, for hearing your own voice. A separate "Record audio" option saves a recording into a note field. ([AnkiDroid User Manual](https://docs.ankidroid.org/))
  - GitHub issues propose simplifying it and adding "hold to record" (tagged for 2.18) ([#16185](https://github.com/ankidroid/Anki-Android/issues/16185), [#16282](https://github.com/ankidroid/Anki-Android/issues/16282)).
  - AnkiDroid syncs with AnkiWeb ([alternativeto](https://alternativeto.net/software/ankidroid/about)).
- **AnkiDroid TTS caveat:** older guides and reviews say desktop add-on `<tts>` tags (AwesomeTTS) don't play on Android. The recommended route is to generate MP3s on the desktop (AwesomeTTS or HyperTTS) and sync them. Reviewers report mixed Korean results, e.g. a HyperTTS Naver voice returning 403. — [memo.cards](https://www.memo.cards/blog/how-to-create-audio-cards-in-anki); [AwesomeTTS](https://ankiweb.net/shared/info/1436550454); [HyperTTS](https://ankiweb.net/shared/info/111623432). (These conflict somewhat with the AnkiDroid manual, which documents Android-service TTS tags. Likely the add-on's own tag format is unsupported, while Anki's native `{{tts}}` works.)
- **Desktop Anki add-on "Record own voice buttons on card":** record and replay buttons on the card. Needs a separate template snippet for mobile. — [AnkiWeb add-on](https://ankiweb.net/shared/info/556226822)
- **Glossika:**
  - Sentence-based spaced-repetition audio drills.
  - Price varies by source: about $16.99/mo for one language or $30.99 for all; Basic about $20/mo or $199/yr; Pro about $40/mo or $399/yr. Check the official site.
  - The Android listing ("Glossika Legacy") says content can be downloaded for offline reps.
  - Reviews call drills monotonous with thin grammar, but some call it excellent for Korean listening.
  - You cannot add your own skateboarding sentences (inferred from its fixed-course model; not explicitly confirmed).
  - Sources: [langoly](https://www.langoly.com/glossika-review/); [kojiilanguages 2026](https://kojiilanguages.com/glossika-review-2026/); [AppBrain listing](https://www.appbrain.com/app/glossika-language-learning/com.glossika.ai); [mezzoguild](https://www.mezzoguild.com/glossika-review/)
- **Migaku:** has iOS/Android apps, flashcards and daily reviews. Courses and cards are available offline and sync. It has a Korean course and is "pricey for casual learners". — [Migaku App Store](https://apps.apple.com/us/app/migaku-really-learn-languages/id1664096855?l=ko); [Chrome Web Store](https://chromewebstore.google.com/detail/migaku-really-learn-langu/lkhiljgmbeecmljiogckofcalncmfnfo?hl=de)
- **Language Reactor:** desktop browser extension. There's no mobile version because mobile browsers don't support the extension interface. — [lingosive](https://lingosive.com/en/blog/best-language-reactor-alternative); [uptogo](https://uptogo.com.tw/科技/language-reactor-有手機版嗎？/)
- **LingQ:** 30+ languages, Free / $12.99 per month. I found no confirmation of Korean offline mobile use. — [comprehensibleinput.it.com](https://comprehensibleinput.it.com/blog/best-comprehensible-input-apps-2026)
- **Korean shadowing apps:**
  - "Learn Korean: Shadowing TOPIK" (Google Play): sentence-by-sentence audio, line repeat, 0.5–1.0x speed, romanization, free, offline. Fixed content. — [Google Play](https://play.google.com/store/apps/details?id=com.ciesoft.shadowing_korean)
  - SayHo (iOS only): turns Korean YouTube videos into 3-sentence shadowing chunks with pronunciation feedback. — [App Store](https://apps.apple.com/us/app/sayho-korean-shadowing/id6797679626)
- **Mikel (NLL) method:**
  - Mikel Telleria Mujika's "Natural Language Learning" combines active recall, shadowing and mnemonics.
  - Shadowing protocol: listen to each sentence 5 times on first encounter, 1 rep on reviews.
  - Targets a bank of about 10,000 words plus 10,000 sentences.
  - Sources: [nll.coach routine](https://www.nll.coach/blog/mikel-hyperpolyglot-45-minute-language-learning-routine); [nll.coach AI](https://www.nll.coach/blog/Mikel%20Hyperpolyglot:%20How%20to%20learn%20Russian%20x10%20faster); [hyperlingua.app/mikel](http://hyperlingua.app/mikel/)
- No dedicated Mikel-branded Korean shadowing Android app was found. hyperlingua.app and nll.coach appear to be associated coaching/AI products, but their features were not verified. — [hyperlingua.app/mikel](http://hyperlingua.app/mikel/)
- A Korean teacher warns against shadowing without comprehension: listen to the whole clip first, then chunk it. — [deliciouskorean](https://deliciouskorean.com/blog/daily-korean/shadowing-korean-dont-just-mimic)

### Inferences
- **Speak** and **Talk To Me In Korean** apps were not researched in this session (no sources retrieved). Speak is an AI conversation tutor, and TTMIK is a fixed-curriculum lesson app. Neither is likely to support custom sentence lists. Treat this as unverified.
- The custom app's real differentiator is a **"Mikel-style session runner"**: play sentence 5x with gaps, record, compare, then grade with FSRS, plus a hands-free looping listening mode. AnkiDroid can approximate this by putting the audio 5 times on a card or using its auto-advance feature. An approximation is still not the same as a dedicated flow.

### Gaps
- Speak, TTMIK, and LingQ's Korean offline support have no sources here.
- I didn't verify whether AnkiDroid's auto-advance or "play audio N times" can produce a screen-off hands-free loop.

## 6. Common pitfalls for hobby learning apps

### Takeaway
The biggest risks for this user are (a) building instead of studying during a one-month trip, (b) losing review history on a phone with no backup, and (c) leaking or racking up costs on a TTS API key embedded in a client app. All three can be largely avoided by keeping content in a CSV on the laptop, generating audio offline, and exporting progress to a file.

### Cited Findings
- Syncing generated TTS audio between devices "might not always be straightforward". — [memo.cards](https://www.memo.cards/blog/how-to-create-audio-cards-in-anki)
- Mobile background playback is killed by OS battery/idle management unless a foreground service with lock-screen controls is used. — [Expo docs](https://docs.expo.dev/versions/latest/sdk/audio/); [expo/expo #49906](https://github.com/expo/expo/issues/49906)
- The advanced flow toggle also blocks updates to unverified apps when switched off, which matters if you rebuild the APK while travelling. — [9to5Google](https://9to5google.com/2026/08/18/google-gradually-rolling-out-androids-advanced-sideloading-ahead-of-developer-verification/)

### Inferences
These are reasoned from general engineering practice. I found no single source for them.
- **Scope creep:** limit the MVP to import CSV, play/loop, record/compare and FSRS grading. Defer accounts, sync, AI sentence generation and stats.
- **Data loss:**
  - PWA IndexedDB can be evicted, and uninstalling or reinstalling an APK with a different signing key wipes app data.
  - Keep the same debug keystore and add a JSON export/import button from day 1.
  - Keep the master sentence list as CSV in git or cloud on the laptop.
- **Audio management:**
  - Name files by a stable sentence ID (`sk-0001.mp3`), not by sentence text.
  - Bundle them as a zip or in the APK assets.
  - A few hundred short MP3s at about 20–50 KB each is small.
- **API keys:** never embed a cloud TTS or LLM key in the APK or PWA, because it is extractable. Generate audio on the laptop with a script and ship only the MP3s.
- **Sync:** for one user, manual export/import or a shared folder (e.g. Drive/Syncthing) beats building a backend. AnkiWeb solves this for free if using Anki.
- **Patchy connectivity:** everything must be local-first. Test in airplane mode before departure.

### Gaps
- No published post-mortems of hobby learning apps were reviewed.

## 7. Recommended MVP and phased plan; is building worth it?

### Takeaway
**For the trip, use AnkiDroid now and build later.** In 1–2 days the user can have a working offline Korean skateboarding/daily-life deck with native-quality audio, FSRS and record-and-compare. A self-built app is unlikely to be as reliable within a few days, especially for screen-off looping audio. Building is worth it afterwards as a learning project and for the Mikel-style session flow and niche list sharing. A PWA is fastest for that. Flutter is more robust if screen-off loops matter most.

### Cited Findings
- AnkiDroid: FSRS, audio fields, Android TTS, Check Pronunciation recorder, offline use, AnkiWeb sync. — [AnkiDroid User Manual](https://docs.ankidroid.org/); [slidetoanki](https://slidetoanki.com/blog/how-to-use-fsrs-anki-guide)
- Generating MP3s on the desktop and syncing them is the reliable cross-device audio route. — [memo.cards](https://www.memo.cards/blog/how-to-create-audio-cards-in-anki)
- ADB install is exempt from verification, and the advanced flow needs a 24-hour wait. — [Gadget Hacks](https://android.gadgethacks.com/news/google-android-sideloading-rules-2026-changes-explained/); [The Hacker News](https://thehackernews.com/2026/03/google-adds-24-hour-wait-for-unverified.html)
- ts-fsrs provides FSRS as an MIT library. — [GitHub ts-fsrs](https://github.com/open-spaced-repetition/ts-fsrs)
- Mikel's protocol is 5 listens on first encounter and 1 on review. — [nll.coach](https://www.nll.coach/blog/mikel-hyperpolyglot-45-minute-language-learning-routine)

### Inferences (proposed plan)
**Phase 0, before departure (days 1–2): AnkiDroid**
1. Write about 100–200 sentences in a CSV on the laptop (columns: id, korean, english, romanization, tags such as `skate` or `daily`, audio).
2. Generate Korean MP3s with a laptop script or the Anki desktop add-ons HyperTTS/AwesomeTTS. Reference them as `[sound:sk-0001.mp3]`.
3. Import into Anki desktop, enable FSRS, sync to AnkiWeb, then sync AnkiDroid.
4. Create a card template with the audio on the front (listen, then recall meaning or shadow) and Korean/English on the back. Use Check Pronunciation to record and compare.
5. For hands-free looping listening, also export the MP3s into one folder or playlist and play them in any offline music player with repeat. This gets a reliable screen-off loop at zero dev cost.
6. Download offline Korean TTS and speech packs on the phone, then test everything in airplane mode.

**Phase 1, optional during the trip (evenings, 2–4 days): PWA prototype**
- Static HTML/JS hosted on GitHub Pages.
- Loads the same CSV and MP3 zip and caches them with a Service Worker.
- Uses IndexedDB for card state and ts-fsrs for scheduling.
- Mikel-style session: play ×5 with a gap, record via MediaRecorder, play back, grade.
- Has an export button for JSON backup.
- Accept that screen-off looping may be unreliable. Keep the music-player loop as a fallback.

**Phase 2, after the trip: robust app if still wanted**
- Use Flutter (`just_audio` + `audio_service` + `record` + `sqflite` + a Dart FSRS port) or Kotlin with Media3.
- Build locally and install with `adb install`. Use a limited-distribution account if sharing with up to 20 friends' devices, or for 2027+ verification.
- Add a "deck pack" format (CSV + audio zip) so any learner or niche can be loaded.

**Minimal viable feature set**
1. Import CSV + audio pack.
2. Sentence list with tap-to-play and loop.
3. Shadow mode: N repeats with a pause.
4. Record-and-compare.
5. Recall card with 4-button FSRS grading.
6. Offline-first storage.
7. Export/import backup.

Everything else (speech-recognition scoring, AI-generated sentences, sync server, stats) is phase 2+.

**Honest verdict:** for the stated goal of learning Korean on this trip, building is **not** worth it before departure. AnkiDroid plus a music-player loop covers the core needs offline and free, today. Building becomes worthwhile when (a) the user wants the specific Mikel-style session UX, (b) they want shareable niche sentence packs for other learners, or (c) the coding practice itself is a goal.

### Gaps
- Not verified: whether AnkiDroid's current auto-advance can replicate a hands-free shadowing loop.
- Not tested: the time estimates for a beginner with an AI assistant. They are judgement calls.
