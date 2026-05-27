---
layout: default
title: Privacy Policy
permalink: /privacy/
---

# E-HT Weight Loss — Privacy Policy

**Effective date:** May 27, 2026
**Last updated:** May 27, 2026

This document describes how the E-HT Weight Loss Android app
("the app") handles your data. It is written in plain English
because the data flows are simple and you deserve to understand
them without legal training.

---

## Summary in one paragraph

Nearly everything you log in the app stays on your phone. The only
data that leaves your device is the **text you type or speak when
describing meals** (sent to Google's Gemini API for nutrition
parsing) and **food-name lookups** (sent to the USDA FoodData
Central API). The app never sells your data, never shows ads,
never tracks you across apps or websites, and has no servers of
its own. Uninstalling the app deletes everything it stored.

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

There are three categories of network requests the app makes.

### 1. Meal parsing — Google Gemini API

When you log a meal by voice or by typing a description, the
**transcribed text** (never the audio) is sent to Google's
Generative Language API to extract structured nutrition data
(food name, portion, calories, macros).

- **Sent**: the meal description text only.
- **Not sent**: your weight, profile, photos, or anything else.
- **Receiver**: Google. Subject to [Google's Generative AI Terms](https://policies.google.com/terms/generative-ai)
  and [Google Privacy Policy](https://policies.google.com/privacy).
- **API key**: by default a developer-provided trial key is used
  for the first 24 hours after install. After that you must add
  your own Google AI Studio key in Settings — your queries then
  go against your own quota.

A consent screen explaining this appears the first time you tap
the microphone button; you must accept before any audio capture
or network call happens. You can re-show the consent screen any
time via **Settings → Voice meal logging → Reset**.

If you'd rather not have meal descriptions leave your device, you
can avoid using voice and text meal logging entirely — log meals
manually through the "Saved meals" flow instead, which performs
no network calls.

### 2. Food lookups — USDA FoodData Central API

When a food name isn't in the app's local cache, the name is
queried against the public [USDA FoodData Central API](https://fdc.nal.usda.gov)
for a reference identifier. This is a US-government service.

- **Sent**: the food name text only.
- **Receiver**: USDA. Subject to [USDA's privacy notice](https://www.usda.gov/privacy-policy).

### 3. Optional support links

The "Support development" buttons in Settings open the system
browser to either Ko-fi or GitHub Sponsors. No payment data
passes through the app — the browser handles everything.
Reviewing each service's privacy policy is the responsibility
of those services:

- [Ko-fi Privacy Policy](https://more.ko-fi.com/privacy)
- [GitHub Privacy Statement](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement)

---

## Health Connect

If you enable the optional **Sleep shield** feature, the app
requests **read-only** access to two Health Connect record types:

- **Steps** — used to display your daily step count and compute
  expended calories.
- **SleepSession** — used to display your nightly sleep duration
  and warn you when sleep is short during a calorie deficit.

Health Connect data is read directly from the Health Connect app
on your phone. The app does **not** send Health Connect data over
the network. You can revoke the app's Health Connect permissions
at any time via the Health Connect app on your phone.

---

## Sensitive permissions and what they're for

| Permission | Why the app needs it |
|---|---|
| **Microphone** (`RECORD_AUDIO`) | Voice meal logging. Audio is processed on-device by Android's built-in speech recognizer and converted to text. The app never sees or stores the raw audio. |
| **Camera** | Capturing progress photos. Photos are stored only in the app's private folder. |
| **Notifications** (`POST_NOTIFICATIONS`) | Optional meal-logging reminders and weekly backup reminders. |
| **Activity recognition** (`ACTIVITY_RECOGNITION`) | Reading the phone's hardware step counter. |
| **Health Connect** (`health.READ_STEPS`, `health.READ_SLEEP`) | Pulling step and sleep data when you enable the Sleep shield. |
| **Exact alarms** (`SCHEDULE_EXACT_ALARM`, `USE_EXACT_ALARM`) | Scheduling the optional blocking meal alarm at a specific time. |
| **Full-screen intent** (`USE_FULL_SCREEN_INTENT`) | Showing the blocking meal alarm as a full-screen notification when it fires. |

You can revoke any of these in Android Settings → Apps → E-HT
Weight Loss → Permissions at any time. Features that depend on
revoked permissions will stop working but the app itself will
continue to run.

---

## Storage and security

- **At rest** — Data is stored in the app's private SQLite database,
  encrypted automatically by Android's file-based encryption.
- **Credentials** — Any API keys you enter in Settings (Gemini,
  USDA, Resend, backup email) are stored in `expo-secure-store`,
  which uses Android's Keystore. Other apps cannot read them.
- **In transit** — All network requests to Gemini and USDA use
  HTTPS.
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
  microphone. To stop sending data to Gemini entirely, simply
  avoid using voice and text meal logging.
- **Opt out of network features** — Voice meal logging, text
  meal logging, USDA food lookups, Health Connect sync, and
  notifications are all individually optional. The app remains
  functional with all of them disabled.

---

## What this app does NOT do

- ❌ Send your weight, body measurements, sleep, steps, photos,
  or any health metric to any third party
- ❌ Show advertising
- ❌ Track you across apps or websites
- ❌ Use cookies or device-tracking identifiers
- ❌ Share or sell any data with anyone
- ❌ Operate any server collecting user data
- ❌ Require account signup
- ❌ Sync your data to the cloud

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
