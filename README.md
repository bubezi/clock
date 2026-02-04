# ⏱️ Market Clock & Session Dashboard

A zero-dependency, single-file trading dashboard that answers one core question:

> **“What time is it — across markets — *in my own timezone*?”**

This project is designed for traders who care about **sessions, kill zones, and market opens**, not UI frameworks.

**No frameworks. No build step. No external libraries.**

---

## ✨ Features

* ⏳ Fixed event countdown
* 🌍 Multi-timezone world clock
* 🕒 User-configurable local timezone
* 📈 Trading session timeline bar
* 🎯 Precise kill zones (London & NY)
* 🚨 Next major market open countdown
* 🧪 Built-in time travel testing (URL-based)

All in **one HTML file**.

---

## 📂 Project Structure

```text
.
├── clock.html              # Main application
├── config.js               # Optional user overrides (gitignored)
└── README.md               # You are here
```

---

## 🌍 Timezones Used

| Market       | Timezone ID        |
| ------------ | ------------------ |
| New York     | `America/New_York` |
| London       | `Europe/London`    |
| User / Local | `EAT`(configurable)|

---

## ⚙️ User Timezone Configuration

### Option 1: Edit the default (simple)

Inside `clock.html`:

```js
const DEFAULT_USER_TIMEZONE = "Africa/Nairobi";
```

Change to any valid IANA timezone, e.g.:

```js
"Asia/Tokyo"
"Europe/Berlin"
"America/Chicago"
```

---

### Option 2: External override (recommended for public GitHub)

Create an optional file called **`config.js`**:

```js
window.MARKET_CLOCK_CONFIG = {
  userTimezone: "Asia/Tokyo"
};
```

Include it **before** the main script:

```html
<script src="config.js"></script>
<script src="clock.js"></script>
```

* If `config.js` is missing → app still works
* Add `config.js` to `.gitignore`
* Users can customize without editing core logic

---

## 🎯 Kill Zones Configuration

Kill zones are defined in **minutes since midnight** in the market’s **local time**.

```js
const KILL_ZONES = {
  london: {
    tz: "Europe/London",
    start: 7 * 60,      // 07:00
    end:   9 * 60,      // 09:00
  },
  ny: {
    tz: "America/New_York",
    start: 9 * 60 + 30, // 09:30
    end:   9 * 60 + 45, // 09:45
  },
};
```

### Customizing kill zones

* Change **only the numbers**
* No UTC math
* DST handled automatically by the browser

---

## 📊 Session Timeline Bar

The timeline visualizes:

* Asian session
* London session
* New York session
* Current session highlight
* Kill zone overlays

Sessions are computed using **real exchange time**, not your local clock.

---

## ⏰ Next Major Market Open

The dashboard automatically detects:

* Upcoming London Open
* Upcoming New York Open
* Countdown updates every second

Displayed in your **local timezone**, sourced from exchange time.

---

## 🧪 Testing & Time Travel (Important)

You can simulate *any moment in time* using a URL parameter.

### Format

?test=YYYY-MM-DDTHH:MM:SSZ

### Example: Test NY Kill Zone

?test=2026-02-05T14:31:00Z

This simulates:

* **09:31 New York**
* NY kill zone → ACTIVE
* London → CLOSED

### Remove testing

Just remove the `?test=` parameter — real time resumes.

This is invaluable for:

* Verifying kill zones
* Checking session transitions
* Debugging edge cases

---

## 🔒 No Dependencies. No Tracking

* No external APIs
* No cookies
* No analytics
* No frameworks

Everything runs **locally in the browser**.

---

## 🧠 Design Philosophy

* **Trader-first**
* Configurable without code rewrites
* DST-safe
* Fork-friendly
* Honest time math

This tool exists to reduce cognitive load — not add dashboards for the sake of dashboards.

---

## 🚀 Deployment

* Open `clock.html` locally
* Or host on:

  * GitHub Pages
  * Netlify
  * Any static server

Zero configuration required.

---

## 📜 License

MIT — fork it, modify it, trade with it.

---
