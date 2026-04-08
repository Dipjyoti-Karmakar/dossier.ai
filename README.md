# Dossier.ai - GitHub Profile Intelligence Dashboard

> Turn any GitHub profile into a full developer intelligence report, powered by Google Gemini AI. No backend. No server. Just open it and go.

![HTML](https://img.shields.io/badge/Built%20With-HTML%20%2F%20CSS%20%2F%20JS-orange?style=flat-square)
![AI](https://img.shields.io/badge/AI-Google%20Gemini-blue?style=flat-square)
![API](https://img.shields.io/badge/Data-GitHub%20REST%20API-black?style=flat-square)
![Deploy](https://img.shields.io/badge/Deployed%20on-GitHub%20Pages-brightgreen?style=flat-square)

---

## Live Demo

**[View Dossier.ai on GitHub Pages](https://dipjyoti-karmakar.github.io/dossier.ai)**

---

## What is Dossier.ai?

Dossier.ai is a single-file, client-side web application that analyzes any GitHub profile and generates a rich, AI-powered intelligence report. Paste a username or GitHub URL, and within seconds you get a full breakdown of that developer including their tech stack, career insights, activity patterns, and a visual representation of their skills.

Built as a side project to bridge data visualization and developer tooling, it runs entirely in the browser with zero backend infrastructure.

---

## Features

### AI Profile Analysis
Powered by Google Gemini, Dossier.ai reads your repositories, languages, stars, bio, and activity to generate:

- A professional developer summary written in plain English
- Your inferred tech stack based on actual code
- Career path suggestions tailored to your current skills
- A full profile audit highlighting what is missing and how to fix it
- A "Code Personality" archetype that describes your coding style
- An optional developer roast for those who want brutal honesty

### Data Visualizations
Five live charts rendered using Chart.js:

- **Skills Radar Chart** — scores you across Frontend, Backend, DevOps, Data/AI, Mobile, and Open Source
- **Language Breakdown Bar** — a colorful segmented bar covering 40+ programming languages with accurate color mapping
- **Star and Fork Trend Line** — plots your top 10 repos across both metrics
- **90-Day Activity Heatmap** — a 13-week grid showing your real GitHub activity intensity per day
- **Live Activity Feed** — your last 15 public GitHub events with timestamps, event type icons, and direct links for push/PR repositories

### Discover Mode
Instead of searching for tools by exact name, describe what you need in plain English.

> Example: "lightweight Python library for scraping websites"

Gemini generates precise search terms, queries the GitHub Search API, and returns the best matching repositories along with an AI explanation of why each one fits your request. A fundamentally different way to explore open source.

### Developer Compare Mode
Enter any second GitHub username and get an instant head-to-head comparison across six metrics: followers, public repos, total stars, total forks, Dossier Score, and Activity Score. Large values are displayed in compact readable notation (for example, 549.1k or 1.2M), and the winner on each metric gets highlighted with a trophy.

### Deep Repository Analysis
Click the Analyze button on any repository to open a detailed modal with:

- Stars, forks, open issues, and watchers at a glance
- A doughnut chart and bar chart showing engagement breakdown
- An AI-generated summary of the README
- A Gemini-powered code quality critique covering architecture and improvement areas
- Repository metadata including creation date, last updated, size, license, and default branch

### Export and Share
- Export your entire dossier as a high-resolution PNG (2x scale) using html2canvas
- Export is stabilized for deterministic capture timing to prevent blank PNG outputs during animation-heavy states
- Share via the native Web Share API on mobile or copy to clipboard on desktop
- Tweet your Dossier Score directly to X with a pre-composed message

### Scoring Rules
Dossier uses deterministic scoring rules so Compare, Share, and Tweet actions all use the same numbers.

- Dossier Score = min(1000, floor(totalStars * 10 + followers * 5 + publicRepos * 2))
- Activity Score = ((publicRepos + followers) % 20) + 2
- totalStars excludes forked repositories
- Metrics are computed during profile load and reused across the app
- Activity Score is a cyclic engagement metric computed from profile stats, not a consecutive-day commit history value
- If cached Dossier Score or Activity Score is missing, the app recalculates before sharing to avoid undefined output

---

## Tech Stack

| Technology | Purpose |
|---|---|
| HTML5 / CSS3 / Vanilla JS | Core application, zero framework dependencies |
| Google Gemini API (gemini-2.5-flash with gemini-2.5-flash-lite fallback) | AI analysis, repo discovery, code critique |
| GitHub REST API v3 | Profile data, repositories, events |
| Chart.js v4.4.0 | All data visualizations |
| html2canvas v1.4.1 | PNG export |
| Google Fonts (Inter) | Typography |

---

## Getting Started

### 1. Clone or Download

```bash
git clone https://github.com/Dipjyoti-Karmakar/dossair.ai.git
cd dossair.ai
```

Or simply download the `index.html` file directly.

### 2. Open in Browser

```bash
open index.html
```

No `npm install`. No build step. No server needed. Just open the file.

### 3. Get Your API Keys

**Gemini API Key (required for AI features)**

1. Go to [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Create a free API key
3. Paste it into the Gemini API Key field in the app

The free tier supports approximately 15 requests per minute, which is more than enough for normal use.

**GitHub Personal Access Token (optional but recommended)**

Without a token, the GitHub API allows 60 requests per hour. With a token, this increases to 5,000 per hour.

1. Go to GitHub Settings → Developer Settings → Personal Access Tokens
2. Generate a token with `public_repo` and `read:user` scopes
3. Paste it into the GitHub Token field in the app

---

## Privacy and API Key Safety

This is important and worth being direct about.

**Your API keys never leave your browser.**

There is no backend server, no database, and no third-party service receiving your keys. When you enter your Gemini API key or GitHub token, they are saved only to your browser's `localStorage`. Every API call is made directly from your browser to Google and GitHub respectively. Nothing passes through any intermediate server.

You can verify this yourself. The entire application is one open HTML file. Open it in any text editor and inspect every network call. There is nothing hidden.

If you are using a shared or public device, clear your browser's local storage after use or use the built-in clear option in the settings panel.

---

## Deployment on GitHub Pages

1. Fork or upload the repository to your GitHub account
2. Go to your repository Settings → Pages
3. Set the source branch to `main` and the folder to `/ (root)`
4. GitHub Pages will publish it at `https://dipjyoti-karmakar.github.io/dossair.ai`

No configuration needed. The app is fully static.

---

## Usage Tips

- You can search by full GitHub URL as well as by username. Both `torvalds` and `github.com/torvalds` work.
- Previous searches are saved in your browser and appear as quick-access pills below the search bar.
- Click any of the legendary developer pills (Torvalds, Guido, Yann LeCun, etc.) to instantly analyze a famous profile.
- The dark/light theme preference is saved automatically between sessions.
- Use the Export PNG button to save a shareable card of your dossier before closing the page.

---

## Project Structure

```
dossair.ai/
├── index.html        # The entire application. HTML + CSS + JS in one file.
└── README.md         # Documentation and project overview.
```

That is the whole project.

---

## Known Limitations

- The activity heatmap is based on public GitHub events, which GitHub limits to the last 300 events per user. Heavy contributors may see an incomplete heatmap.
- The Dossier Score is a relative metric derived from stars, followers, and repositories. It is meant to be a fun comparison tool, not a definitive measure of developer quality.
- The Gemini free tier allows around 15 requests per minute. If you hit this limit, wait a moment and try again.
- Forked repositories are excluded from all stats and visualizations to reflect original work only.

---

## Contributing

Contributions, suggestions, and feedback are welcome. If you find a bug or have a feature idea, open an issue or submit a pull request.

1. Fork the repository
2. Make your changes to `index.html`
3. Test in a browser
4. Open a pull request with a clear description of the change

---

## Author

Built by [Dipjyoti Karmakar](https://github.com/Dipjyoti-Karmakar), a data analytics fresher who loves turning raw data into things that are actually useful.

If you found this helpful or have feedback, feel free to connect on [LinkedIn](https://www.linkedin.com/in/dipjyoti-karmakar-dk) or open an issue here.

---

*If this project helped you, a star on the repository would mean a lot.*
