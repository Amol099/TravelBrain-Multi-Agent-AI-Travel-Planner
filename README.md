<div align="center">

<!-- ✈️ ───────────────────────────────────────────── ✈️ -->

# 🧠 TravelBrain

### *Your trip, planned by a team of AI specialists.*

Describe the trip you want in plain English — get back **flights, hotels, weather
and a day-by-day itinerary**, researched for you in about a minute.

<br>

[![Live Demo](https://img.shields.io/badge/✨_Live_Demo-Open_App-6366f1?style=for-the-badge)](https://travelbrain-multi-agent-ai-travel-planner-yq5a.onrender.com)
&nbsp;
[![Status](https://img.shields.io/badge/Status-Done-22c55e?style=for-the-badge)](#)
&nbsp;
[![License](https://img.shields.io/badge/License-GPL--3.0-3b82f6?style=for-the-badge)](LICENSE)

[![Issues](https://img.shields.io/github/issues/KalyanM45/TravelBrain-Multi-Agent-AI-Travel-Planner?style=flat-square&color=f59e0b)](https://github.com/KalyanM45/TravelBrain-Multi-Agent-AI-Travel-Planner/issues)
[![Pull Requests](https://img.shields.io/github/issues-pr/KalyanM45/TravelBrain-Multi-Agent-AI-Travel-Planner?style=flat-square&color=ec4899)](https://github.com/KalyanM45/TravelBrain-Multi-Agent-AI-Travel-Planner/pulls)
![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Groq](https://img.shields.io/badge/Groq-F55036?style=flat-square&logoColor=white)

<br>

[**Features**](#-features) •
[**How it works**](#-how-it-works) •
[**Quick start**](#-quick-start) •
[**Usage**](#-usage) •
[**Troubleshooting**](#-troubleshooting) •
[**Contributing**](#-contributing)

</div>

<br>

<!--
  💡 TIP: Drop a screenshot or GIF of the app here for maximum wow-factor:
  <p align="center"><img src="docs/screenshot.png" width="85%" alt="TravelBrain preview"></p>
-->

---

## 🌍 About

Planning a trip usually means juggling half a dozen browser tabs — one for flights,
another for hotels, a third for the weather, and a notes app where you try to
squeeze it all into a sensible order.

**TravelBrain collapses all of that into a single conversation.**

Tell it what you want, the way you'd tell a friend:

> 💬 *"Plan a 10 day Europe trip from India in April, mid-range budget"*

A team of AI specialists goes off and researches it. One looks into flights,
another finds places to stay, another checks the weather while you're there.
Their findings are pulled together into **one plan you can actually act on** —
a day-by-day schedule and a cost estimate, in about a minute instead of an
afternoon.

---

## ✨ Features

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>✈️ Flights</h3>
      Likely airports, airlines on the route, typical duration and fare range.
    </td>
    <td width="50%" valign="top">
      <h3>🏨 Hotels</h3>
      Accommodation options matched to your destination and budget.
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h3>🌤️ Weather</h3>
      Current conditions and forecast, with practical travel advice.
    </td>
    <td width="50%" valign="top">
      <h3>🗺️ Itinerary</h3>
      A realistic day-by-day plan you can actually follow.
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h3>💰 Budget</h3>
      An estimated breakdown of what the trip will cost.
    </td>
    <td width="50%" valign="top">
      <h3>💾 Saved Trips</h3>
      Plans are saved as you go — reopen a trip later and ask follow-ups without starting over.
    </td>
  </tr>
</table>

---

## 🔭 How it works

```mermaid
flowchart LR
    A([💬 Your request]) --> B{{🧠 Planner}}
    B --> C[✈️ Flights agent<br/><sub>AviationStack</sub>]
    B --> D[🏨 Hotels agent<br/><sub>Tavily</sub>]
    B --> E[🌤️ Weather agent<br/><sub>OpenWeather</sub>]
    C --> F{{🧩 Synthesis<br/><sub>Groq LLM</sub>}}
    D --> F
    E --> F
    F --> G([🗺️ Itinerary + 💰 Budget])
    G --> H[(🐘 PostgreSQL)]
```

---

## 🚀 Quick start

### 📋 Prerequisites

| | Requirement | Notes |
|:-:|---|---|
| 🐍 | **Python 3.11** | |
| ⚡ | **[uv](https://docs.astral.sh/uv/)** | Used to install dependencies |
| 🐘 | **PostgreSQL database** | A free [Render](https://render.com/) instance works great |
| 🔑 | **API keys** | All have free tiers — see below |

<details>
<summary><b>🔑 Where to get the API keys</b></summary>

<br>

| Service | Used for | Get a key |
|---|---|---|
| **Groq** | AI planning | [console.groq.com](https://console.groq.com/) |
| **Tavily** | Hotel search | [tavily.com](https://tavily.com/) |
| **AviationStack** | Airports & airlines | [aviationstack.com](https://aviationstack.com/) |
| **OpenWeather** | Weather & forecasts | [openweathermap.org/api](https://openweathermap.org/api) |

</details>

### 📦 Installation

**1. Clone the repository**

```bash
git clone https://github.com/KalyanM45/TravelBrain-Multi-Agent-AI-Travel-Planner.git
cd TravelBrain-Multi-Agent-AI-Travel-Planner
```

**2. Install dependencies**

```bash
uv sync
```

**3. Add your keys** — create a `.env` file in the project root:

```dotenv
# ── Required ──────────────────────────────────────
GROQ_API_KEY=your_groq_key
DATABASE_URL=postgresql://user:password@host:5432/dbname

# ── Service keys ──────────────────────────────────
TAVILY_API_KEY=your_tavily_key
AVIATIONSTACK_API_KEY=your_aviationstack_key
OPENWEATHER_API_KEY=your_openweather_key

# ── Optional ──────────────────────────────────────
GROQ_MODEL=openai/gpt-oss-20b
```

| Variable | Required | What it's for |
|---|:---:|---|
| `GROQ_API_KEY` | ✅ | Powers the AI planning |
| `DATABASE_URL` | ✅ | Saves your trips so you can return to them |
| `TAVILY_API_KEY` | ✅ | Hotel search |
| `AVIATIONSTACK_API_KEY` | ✅ | Airport and airline information |
| `OPENWEATHER_API_KEY` | ✅ | Weather and forecasts |
| `GROQ_MODEL` | ➖ | Switch the AI model without editing any code |

> [!WARNING]
> Your `.env` file is ignored by Git. **Never commit real keys.**

**4. Launch the app**

```bash
uv run python app.py
```

Then open the app in your browser (or try the
[**live demo**](https://travelbrain-multi-agent-ai-travel-planner-yq5a.onrender.com)).
If you see the planner with a green **API connected** dot at the bottom of the
sidebar — you're ready to go! 🎉

---

## 🎈 Usage

### 🧳 Planning a trip

Type your request into the box at the bottom and press **Enter**. Anything
conversational works:

> 🇪🇺 *Plan a 10 day Europe trip from India in April, mid-range budget*

> 🇮🇹 *I want a relaxed 5 day trip to Rome and Florence in September for two people*

Not sure where to start? Click one of the **suggestion cards** on the home screen.

> [!NOTE]
> A plan takes **30–90 seconds** to build, and you'll see each stage as it progresses.

### 🎛️ Using the trip builder

Prefer fields over sentences? Click the **sliders icon** to the left of the
message box, then fill in:

`Origin` · `Destination` · `Dates` · `Duration` · `Travellers` · `Budget` · `Interests`

Hit **Write my prompt** and your request is composed for you — ready to send or edit.

### 📑 Reading your plan

Results are split into tabs so you can jump straight to what you need:

| 📋 Plan | 🗺️ Itinerary | ✈️ Flights | 🏨 Hotels | 🌤️ Weather |
|:-:|:-:|:-:|:-:|:-:|

### 💾 Saving, exporting & revisiting

- 🗂️ Every trip is **saved to the sidebar** automatically — click any one to reopen it
- 🧠 Ask **follow-up questions** on an open trip — it remembers the context
- 📤 Use the icons at the top of a result to **copy**, **download as Markdown**, or **print**
- ➕ Click **New trip** to start fresh
- 🌗 Toggle **light / dark mode** with the sun/moon icon at the bottom of the sidebar

---

## 🛠️ Troubleshooting

<details>
<summary><b>🔌 The page loads but planning fails</b></summary>

<br>

Check the status indicator at the bottom of the sidebar. If it says
*API unreachable*, the app has stopped — restart it:

```bash
uv run python app.py
```

Otherwise, check the terminal you started the app in for the error.

</details>

<details>
<summary><b>🤖 An error says the model does not exist</b></summary>

<br>

AI providers retire models over time. List the ones your key can use:

```bash
curl -s https://api.groq.com/openai/v1/models \
  -H "Authorization: Bearer $GROQ_API_KEY"
```

Pick one from the list and set it as `GROQ_MODEL` in your `.env` file.

</details>

<details>
<summary><b>🐘 An error says DATABASE_URL is missing</b></summary>

<br>

The app needs a PostgreSQL database to save your trips. Add a connection string
to your `.env` file — see [Installation](#-installation).

</details>

<details>
<summary><b>⏳ Plans take a long time</b></summary>

<br>

This is expected. Several specialists research your trip in turn, and each step
involves live data and AI calls. **30–90 seconds is normal.**

</details>

---

## 🤝 Contributing

Contributions are welcome! The project is actively being developed, so there's
plenty to pick up.

**1. Fork** the repo and clone your fork, then follow [Quick start](#-quick-start).

**2. Create a branch**

```bash
git checkout -b feature/your-feature-name
```

**3. Make your changes**

- 🎯 Keep each pull request focused on one thing
- 🎨 Match the style of the code around you
- ✅ Check the app still runs end to end before opening a PR
- 🔐 Never commit your `.env` file or any API keys

**4. Commit & push**

```bash
git commit -m "Add support for multi-city trips"
git push origin feature/your-feature-name
```

**5. Open a pull request** against `main`, describing what you changed, why,
and how you tested it.

> [!TIP]
> Found a bug or have an idea? Open an [issue](https://github.com/KalyanM45/TravelBrain-Multi-Agent-AI-Travel-Planner/issues).
> For bugs, include what you did, what you expected, what happened instead, and any terminal error output.

---

## ✍️ Authors

<a href="https://github.com/KalyanM45">
  <img src="https://img.shields.io/badge/Made_by-@KalyanM45-181717?style=for-the-badge&logo=github" alt="KalyanM45">
</a>

---

## 💖 Acknowledgements

| | |
|---|---|
| ⚡ [**Groq**](https://groq.com/) | Blazing-fast AI inference |
| 🔎 [**Tavily**](https://tavily.com/) | Live hotel search |
| ✈️ [**AviationStack**](https://aviationstack.com/) | Airport & airline data |
| 🌦️ [**OpenWeather**](https://openweathermap.org/) | Weather & forecasts |

---

<div align="center">

### ⭐ If TravelBrain helped you plan a trip, give it a star!

Licensed under the **GNU General Public License v3.0** — see [LICENSE](LICENSE).

<sub>Built with ☕ and a love for travel 🌏</sub>

</div>
