---
layout: default
title: Download E-HT Weight Loss
permalink: /downloads/
---

# Download

## Android

**[Download the APK](https://github.com/Father-Sherman/eht-privacy/releases/latest/download/eht-weight-loss.apk)**
&nbsp;&nbsp;<small>currently v2.37.9</small>

<!-- The asset filename is deliberately unversioned. A "latest"
     download URL has to name the file exactly, so a versioned
     filename here would 404 the moment the next release lands.
     The version label above is prose and can go stale harmlessly;
     the link cannot. -->


Installing it takes a couple of taps more than the Play Store, because
Android quite reasonably does not let a web page install software
without asking:

1. Open the downloaded file. Android will say it cannot install from
   this source.
2. Tap the prompt through to settings and allow your browser to
   install apps, then go back and open the file again.
3. Play Protect may warn that the app is unrecognised. It is
   unrecognised because it did not come from the Play Store, not
   because anything is known to be wrong with it. Install anyway if
   you are comfortable with that.

You can turn the install permission back off afterwards. It is not
needed again unless you update the same way.

### You need your own AI key

**No build includes an API key**, deliberately. A key baked into an app
sits in the file in plaintext, and anyone with the file can read it out
in seconds, so shipping one would mean handing my key to whoever wanted
it.

So the first thing to do after installing is add your own. It is free:

- **[Google AI Studio](https://aistudio.google.com/apikey)** is the
  one the app is tuned for. Sign in, create a key, paste it into
  Settings → API keys.
- **[Groq](https://console.groq.com/keys)** and
  **[Mistral](https://console.mistral.ai/api-keys/)** also have free
  tiers and work as alternatives or backups.

Until a key is in, everything that does not need AI still works:
weight, steps, workouts, measurements, sleep, the charts and the
streak. Only reading a meal from text, voice or a photo needs one.

The Play Store build works the same way. It used to include a
developer key for the first 24 hours so you could try things before
signing up for anything, but that was withdrawn in September 2026:
a key shipped inside an app can be read out of the file by anyone who
has the file, which is not a thing you can fix by asking nicely.

## iPhone

Not yet, and not because the app does not run. It does. The blocker
is distribution: Apple will not let an iPhone install an app from a
web link the way Android will. An app has to come through the App
Store or TestFlight, and both need a paid Apple Developer account
that does not exist for this project yet.

If that changes, this is where the TestFlight link will go.

## Which build should I use?

Use the Play Store if the app is listed there and you just want it to
work. Use this download if you want it without a Google account in
the loop, or you want the version with the full-screen meal alarm,
which Play's policy does not allow for an app in this category.

---

[Privacy Policy](./privacy/) · [Home](./)
