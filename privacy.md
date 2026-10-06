---
layout: default
title: Privacy Policy
permalink: /privacy/
---

# E-HT Weight Loss — Privacy Policy

**Effective date:** May 27, 2026
**Last updated:** October 5, 2026

This document describes how the E-HT Weight Loss Android app
("the app") handles your data. It is written in plain English
because the data flows are simple and you deserve to understand
them without legal training.

---

## Summary in one paragraph

Nearly everything you log in the app stays on your phone. The main
data that leaves your device is the **text you type or speak when
describing meals**, and, if you use photo meal logging, **the photo
of the plate** (both sent to the AI provider you have configured,
which identifies the food and estimates calories/macros). Progress
photos are a different feature and stay on your phone, unless you
choose to email your backups with photo backup turned on. The app
also sends **crash and diagnostic reports** and
any **feedback you submit (with a reply-to email address, so the
developer can respond)** to an error-tracking service (Sentry) —
crash reporting is on by default but can be turned off in Settings.
If you set up **email backup**, your backup file is emailed to an
address you choose through a mail service (Resend); that is off unless
you set it up.
The app never sells your data, never shows ads, never tracks you
across apps or websites, and has no servers of its own. Uninstalling
the app deletes everything it stored.

---

## What the app collects and stores on your device

Everything below lives in the app's private storage on your phone.
The app developer has no way to read any of it without physical
access to your unlocked phone.

| Category | Examples |
|---|---|
| Profile | Sex, date of birth, height, goal mode (loss / gain / maintain), body fat percentage |
| Weight history | Each weigh-in you log, with timestamp |
| Body measurements | Waist, neck, chest, hip, biceps, thigh circumferences |
| Meals | Food name, portion size, kcal, protein, carbs, fat, timestamp |
| Workouts | Activity type, duration, estimated kcal, timestamp |
| Daily summaries | Total consumed / expended kcal per day, your "win / lose / neutral" sentiment |
| Sleep history | Total sleep minutes per night, start and end times when available |
| Step counts | Daily step totals from your phone's step sensor or Health Connect |
| Progress photos | Photos you capture, stored in the app's private folder |
| Settings | Your preferences, toggles, calibration values, and (optionally) API keys you've entered yourself |

This data is stored in a local SQLite database and the app's
private file directory. It is **not synced to any cloud service
automatically**. The Android `allowBackup` flag is explicitly
disabled so the app's data does not get pulled into Google Drive
backups.

You can export this data as a JSON file at any time via
**Settings → Export all data**. You can also restore from a
previously-exported file via the same screen.

---

## What leaves your device

There are four categories of network requests the app makes.
Crash reporting (Section 3) can be turned off in Settings, and email
backup (Section 4) only happens if you set it up.

### 1. Meal parsing — the AI provider you choose

When you log a meal by voice or by typing a description, the
**transcribed text** (never the audio) is sent to the AI provider
you have configured, to extract structured nutrition data
(food name, portion, calories, macros).

When you log a meal **from a photo**, the photo of the plate is
sent as well. It goes first to a vision model, whose only job is to
name the foods it can see, and the resulting food names are then
priced for calories the same way typed text is. Before it is sent
the image is downscaled to at most 1024 pixels on its long edge and
re-encoded as JPEG. It is used for that request and the review
screen that follows it, and is not written to the app's database or
added to your photo gallery.

- **Sent**: the meal description text, plus the meal photo if you
  use photo logging.
- **Not sent**: your weight, profile, progress photos, or anything
  else. **Progress photos are a separate feature and are never sent
  to the AI provider.** (The only way they can leave your phone is
  inside an emailed backup, Section 4, which you control.)
- **Receiver**: whichever provider you have selected in Settings.
  The choices are Google (Generative Language API), Groq, and
  Mistral. Google's use is subject to
  [Google's Generative AI Terms](https://policies.google.com/terms/generative-ai)
  and [Google Privacy Policy](https://policies.google.com/privacy);
  [Groq](https://groq.com/privacy-policy/) and
  [Mistral](https://mistral.ai/terms/) publish their own.
- **API key**: you supply your own, and it is the only one used. No
  build ships with a key in it. Earlier versions included a
  developer-provided key that gave you 24 hours before you had to add
  your own; that was withdrawn in September 2026, because a key inside
  an app can be read out of the file by anyone who has the file.
  Meal logging asks you for a key the first time you use it and tells
  you where to get a free one; everything that does not need AI works
  without one.

A consent screen explaining this appears the first time you tap
the microphone button; you must accept before any audio capture or
network call happens. You can re-show it any time via
**Settings → Voice meal logging → Reset**.

Photo logging has its own separate consent screen, shown the first
time you tap the camera button and before any photo is taken or
sent. It is deliberately not the same acceptance as the voice one,
because the voice notice tells you the audio never leaves your
device and photo logging is the opposite case. You can re-read it,
or make it appear again, under
**Settings → Meal input → Log from a photo**. On iPhone the system
camera and photo-library prompts carry the same explanation.

If you would rather it were not possible at all, photo logging can
be switched off entirely in that same place.

If you'd rather not have meal descriptions or photos leave your
device, you can avoid voice, text and photo meal logging entirely.
Photo logging can be switched off outright under
**Settings → Meal input**, and you can log meals manually through
the "Saved meals" flow, which performs no network calls.

One thing that is not meal logging, for completeness. If you have
saved a key, the app asks that provider **which models it currently
offers**, at most once a day. This is how it notices that a provider
has retired a model the app still lists — that has happened more than
once, and in one case photo logging stopped working on a provider for
a month before anyone spotted it. The request carries nothing but the
key itself, for authentication: no meal text, no photo, no profile
data, nothing from your local database. It runs only while crash
reporting is enabled (Section 3), because its only purpose is to tell
the developer that something needs fixing — so switching that off in
**Settings → Privacy & data** stops it, and removing your key stops it
too.

There is also a button you can press yourself: **Settings → AI
features → Test AI connection**. It asks each provider you have a key
for to estimate the calories in "one large egg" and shows you what
came back, so you can tell which provider is at fault when logging
stops working. It sends that fixed phrase and your key, and nothing
else — no meal text, no photo, no profile data, nothing from your
local database. It runs only when you tap the button.

### 2. Optional support links

The "Support development" buttons in Settings open the system
browser to either Ko-fi or GitHub Sponsors. No payment data
passes through the app — the browser handles everything.
Reviewing each service's privacy policy is the responsibility
of those services:

- [Ko-fi Privacy Policy](https://more.ko-fi.com/privacy)
- [GitHub Privacy Statement](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement)

### 3. Crash reports and in-app feedback — Sentry (opt-out)

The app sends three kinds of data to [Sentry](https://sentry.io).
The two automatic kinds are governed by the crash-reporting toggle in
**Settings → Privacy & data**. The feedback forms are submissions you
initiate yourself, and are described separately below.

**Automatic crash reports.** If the app encounters an unhandled
error (a "crash"), it sends a report so I can see that something
broke and fix it.

- **Sent**: stack trace, error message, app version, Android
  version, device model, locale, and the route (screen) where
  the error occurred.
- **Not sent**: meal text, food names, weights, body
  measurements, sleep data, step counts, photos, profile info,
  API keys, or anything else from your local data. The SDK is
  configured with `sendDefaultPii: false` and user-input
  breadcrumbs are dropped before transmission.

**Automatic AI-model reports.** When an AI provider refuses a
model the app asked for — usually because the provider has retired
it — the app reports that, so it can be corrected rather than
falling back to a slower model forever. Governed by the same
toggle as crash reports.

- **Sent**: which provider (Google, Groq or Mistral), the name of
  the model, and the provider's own error message about that
  model, plus the same environment metadata as a crash report.
- **Not sent**: your API key, the request URL (Google's carries
  the key in it), your meal text or photo, or anything else from
  your local data.

**Voluntary feedback.** Settings → Feedback offers three ways
to reach me; two of them send data to Sentry.

- **"Report a bug" / "Suggest a feature"** open a short in-app
  form. When you type a message and tap send, the **message
  text and your reply-to email address** — plus the same
  environment metadata as a crash report (app version, Android
  version, device model, route) — are sent to Sentry. The email
  is required so I can reply to your report; it is used only for
  that. These two work whether or not crash reporting is enabled,
  because each is an explicit submission you initiate.
- **"Open in-app feedback form"** is Sentry's own feedback
  widget. It sends **the free-text message you write and your
  reply-to email address** (plus the same environment metadata).
  Its name field is turned off. This button is hidden when crash
  reporting is turned off.

**Your reply-to email is the only identifying detail any of these
collect**, it's used solely to respond to your feedback, and it's
remembered on your device (in secure storage, never in backups)
only so you don't have to retype it. **No name is collected, and
screenshots are never sent** — the widget's screen-capture option
is disabled because your screens can contain weights, body
measurements, and other private health data.

**Receiver for crash reports and both Sentry feedback paths
above**: Sentry. Subject to [Sentry's Privacy Policy](https://sentry.io/privacy/).

**How to disable**: Settings → About & Legal → toggle "Send
crash reports" off. This stops automatic crash reports and hides
the "Open in-app feedback form" widget, and takes effect
immediately (no app restart required). Note that "Report a bug"
and "Suggest a feature" still send your message to Sentry when
you choose to use them — turning the toggle off does not disable
those, since each is an explicit action you take.

A third feedback option, **"Contact developer"**, opens your
phone's mail app with a pre-filled email to the developer. It
never touches Sentry and is always available, even with crash
reporting off.

### 4. Email backup — Resend (only if you set it up)

E-HT can email your backup file to you, so a copy exists somewhere
other than your phone. This is **off unless you set it up** under
**Settings → Backup → Email backup**, which needs your own Resend API
key and the email address to send to.

Once set up, it sends when you tap the send button, and after each
scheduled backup.

- **Sent**: your full backup file (the same JSON as **Export all
  data**: profile, weights, measurements, meals, workouts, daily
  summaries, sleep and steps), attached to an email. If you have also
  turned on **photo backup**, the file includes smaller copies of your
  progress photos. API keys and other credentials are never included.
- **Receiver**: [Resend](https://resend.com), a mail-delivery service,
  which delivers it to the address you entered. The email passes
  through Resend's systems and is then held by your own email
  provider. Subject to [Resend's Privacy Policy](https://resend.com/legal/privacy-policy).
- **Not sent to the developer.** The developer never receives or sees
  your backups.
- **How to stop**: remove your Resend key or the email address in
  **Settings → Backup → Email backup**. Emails already sent stay in
  your inbox until you delete them.

---

## Health Connect

The app can optionally read two record types from Health Connect.
Each is **read-only**, requested separately, and entirely optional —
the app works without either:

- **Steps** — granted from **Settings → Permissions → Health
  Connect · Steps**. Used to display your daily step count, compute
  your expended calories, and detect drops in your activity over
  time. When granted, Health Connect (which aggregates steps from
  Samsung Health, wearables, and other fitness apps) becomes the
  step source in preference to your phone's built-in sensor.
- **Sleep (SleepSession)** — requested when you enable the optional
  **Sleep shield** feature. Used to display your nightly sleep
  duration and warn you when sleep is short during a calorie
  deficit.

Health Connect data is read directly from Health Connect on your
phone and used only on-device. The app **never** sends Health
Connect data over the network to any service, and never shares it
with the developer or any third party. The one exception is your own
backup: if you set up email backup (Section 4), the backup file
includes your step and sleep history and is emailed to the address
you chose.

Health Connect data the app has copied into its local database
(your step and sleep history) is deleted when you uninstall the
app, the same as all other local data. You can revoke either
Health Connect permission at any time through the Health Connect
section of your phone's settings; revoking simply stops new reads
and the affected feature falls back to its non-Health-Connect
behavior (phone step sensor; motion-inferred sleep).

---

## Sensitive permissions and what they're for

| Permission | Why the app needs it |
|---|---|
| **Microphone** (`RECORD_AUDIO`) | Voice meal logging. Audio is processed on-device by Android's built-in speech recognizer and converted to text. The app never sees or stores the raw audio. |
| **Camera** | Two separate features. Progress photos are stored only in the app's private folder and are never transmitted. Meal photos, if you use photo meal logging, are sent to your configured AI provider to identify the food (see Section 1) and are not stored afterwards. |
| **Notifications** (`POST_NOTIFICATIONS`) | Optional meal-logging reminders and weekly backup reminders. |
| **Activity recognition** (`ACTIVITY_RECOGNITION`) | Reading the phone's hardware step counter. |
| **Health Connect** (`health.READ_STEPS`, `health.READ_SLEEP`) | Pulling step and sleep data when you enable the Sleep shield. |
| **Exact alarms** (`SCHEDULE_EXACT_ALARM`, `USE_EXACT_ALARM`) | Scheduling the optional blocking meal alarm at a specific time. |

You can revoke any of these in Android Settings → Apps → E-HT
Weight Loss → Permissions at any time. Features that depend on
revoked permissions will stop working but the app itself will
continue to run.

---

## Storage and security

- **At rest** — Data is stored in the app's private SQLite database,
  encrypted automatically by Android's file-based encryption.
- **Credentials** — Any API keys you enter in Settings (Google,
  Groq, Mistral, Resend, backup email) are stored in
  `expo-secure-store`, which uses Android's Keystore. Other apps
  cannot read them.
- **In transit** — Every network request the app makes, to any AI
  provider, to Sentry or to Resend, uses HTTPS.
- **Code obfuscation** — The shipped APK is minified and
  obfuscated with ProGuard / R8 so that on-device class names
  and string literals don't reveal internal app structure.

---

## Children

The app is designed for adults. It is not directed at children
under 13 and does not knowingly collect data from anyone under
13. If you believe a child under 13 has used the app and stored
data, uninstall the app from that device to remove all data.

---

## Your rights and choices

- **Access** — All of your data lives on your device. You can
  view, export, or delete it through the app's own UI. There is
  no separate database to request access to.
- **Export** — Settings → "Export all data" produces a JSON file
  containing every row the app has stored.
- **Delete** — Uninstalling the app removes every byte the app
  has stored on your phone. You can also delete individual
  entries (weights, meals, workouts, photos) through their
  respective screens.
- **Revoke consent** — Settings → Voice meal logging → Reset
  re-shows the consent screen the next time you tap the
  microphone. To stop sending anything to an AI provider, avoid
  voice, text and photo meal logging.
- **Opt out of optional features** — Voice meal logging, text
  meal logging, photo meal logging (Settings → Meal input),
  Health Connect reads (steps and sleep), email backup, and
  notifications are all individually optional. The app remains functional with all
  of them disabled.

---

## What this app does NOT do

- ❌ Send your weight, body measurements, sleep, steps, progress
  photos, or any health metric to any third party, except inside a
  backup you choose to email to yourself (Section 4). (Meal
  descriptions, and meal photos if you use photo logging, do go to
  the AI provider you choose. That is Section 1 above.)
- ❌ Show advertising
- ❌ Track you across apps or websites
- ❌ Use cookies or device-tracking identifiers
- ❌ Share or sell any data with anyone (crash reports and
  in-app feedback under Section 3 above are exceptions; crash
  reporting is opt-out in Settings)
- ❌ Operate any server collecting user data
- ❌ Require account signup
- ❌ Sync your data to the cloud (emailing a backup to yourself,
  Section 4, is a copy you choose to send, not a sync)

---

## Changes to this policy

If this policy changes in any material way, the "Last updated"
date above will change and the app will display a notice on
next launch. Continued use after the notice constitutes
acceptance of the updated policy. The full revision history is
visible on GitHub in the commit log of this file.

---

## Contact

Questions, concerns, or data-deletion requests beyond uninstalling
the app: **externalhypothalamus@gmail.com**

This app is built by an individual developer, not a company.
There is no support team — emails go directly to the developer.
