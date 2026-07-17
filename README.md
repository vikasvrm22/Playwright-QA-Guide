# Tech Learn

Android app to learn Playwright, TypeScript, Git, Jenkins, and Java — with
daily quiz, progress dashboard, and personal notes (with camera/gallery photos).

All content is in **English**, and the visual design follows the PathShala-style
reference (indigo/coral/teal/sun/plum palette, Sora + Inter typography, card-based
layout, dot-trail progress bars, bottom tab navigation).

## Features

- **5 tutorials**: Playwright, TypeScript, Git, Jenkins, Java — 32 chapters each (160 total), each chapter has a "Learn" tab (concept + code) and a "Practice" tab (instant-feedback question)
- **Home**: daily-goal ring, streak counter, "continue where you left off" card, horizontal tutorial cards with live progress, most recent note
- **Tutorials**: chip filter across all 5 tutorials + searchable chapter list with progress indicators
- **Quiz**: pass/fail donut chart, average score, per-tutorial quiz start (10 random questions from a 90+ question pool), full answer breakdown with explanations
- **My Notes**: grid of notes with title, text, and an optional photo from camera or gallery
- **Profile**: streak, overall progress, editable name/role, reset-data option
- All screens are **data-driven** — add a tutorial/chapter/question to `lib/data/` and it automatically shows up everywhere (home, tutorials, quiz) with zero UI changes needed
- All data (progress, quiz scores, notes, streak, profile) stored **locally on the device** using `shared_preferences` — nothing leaves the phone, no backend needed

## Building the APK (via GitHub Actions — no local Android Studio needed)

This project includes `.github/workflows/build.yml`, so GitHub Actions will
build the APK automatically:

1. Push this project to a GitHub repository (use GitHub Desktop — see below)
2. GitHub Actions automatically builds the APK on every push to `main`/`master`
3. Go to the **Actions** tab → latest run → **Artifacts** → download `tech-learn-apk`
4. Extract the zip, install `app-release.apk` on your phone

### Uploading with GitHub Desktop (recommended)

1. Install [GitHub Desktop](https://desktop.github.com)
2. Sign in with your GitHub account
3. Create a new repo on GitHub.com, then **File → Clone Repository** in GitHub Desktop
4. Copy all files from this project folder into the cloned folder
5. In GitHub Desktop: write a commit summary → **Commit to main** → **Push origin**
6. Check the **Actions** tab on GitHub.com — the build starts automatically

## Running Locally (optional, for testing)

```bash
flutter pub get
flutter run
```

Requires Flutter SDK installed locally. Everything here is pure Dart or
well-maintained Flutter plugins (`google_fonts`, `shared_preferences`,
`fl_chart`, `image_picker`, `uuid`) — no native build tools needed beyond a
normal Flutter/Android setup.

## What changed in this redesign

- `lib/data/tutorial_content.dart` and `lib/data/quiz_data.dart` — fully
  translated from Hinglish to English (160 chapters, 20+ quiz questions),
  chapter IDs kept identical to the original so progress/quiz-score keys
  still line up if you're upgrading an existing install
- `lib/theme/app_theme.dart` — new design tokens (colors, type scale, card/
  button/chip theming) matching the PathShala-style reference
- `lib/widgets/app_widgets.dart` — new shared components (dot-trail progress,
  goal ring, section headers, avatar, empty states)
- `lib/screens/root_shell.dart` — new bottom-tab navigation shell (replaces
  the old side drawer)
- Every screen was rebuilt: `home_screen.dart` (new dashboard), `tutorials_screen.dart`
  (chip filter + chapter list), `chapter_reader_screen.dart` (Learn/Practice tabs),
  `notes_screen.dart` / `note_form_screen.dart` (grid cards), `quiz_screen.dart`
  (hub) + `quiz_play_screen.dart` (new) + `quiz_result_screen.dart`, `profile_screen.dart` (new)
- `lib/services/profile_service.dart` (new) — streak + daily-goal tracking

## Notes on Content

Tutorial content is written from scratch, in original wording, based on
publicly documented concepts of each technology (Playwright, TypeScript,
Git, Jenkins, Java) — not copied from any single source. Feel free to
expand `lib/data/tutorial_content.dart` and `lib/data/quiz_data.dart` with
more chapters and questions any time — new entries show up automatically
across Home, Tutorials, and Quiz without touching any screen code.
