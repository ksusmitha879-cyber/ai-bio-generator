# AI Bio Generator

A streamlined web app that transforms basic user inputs into compelling, platform-specific professional biographies using the Claude API.

![AI Bio Generator](https://img.shields.io/badge/Powered%20by-Claude%20AI-7F77DD?style=flat-square) ![Netlify](https://img.shields.io/badge/Deployed%20on-Netlify-00C7B7?style=flat-square) ![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

---

## Demo

> **Input:** Name: Sarah Chen · Job: Graphic Designer · Hobbies: Rock climbing, baking sourdough · Goal: Get freelance clients
>
> **Output:** "Visual storyteller and Graphic Designer helping brands stand out. When I'm not designing, you can find me scaling rock walls or perfecting my sourdough starter. Let's collaborate!"

---

## Features

- 4 target platforms — LinkedIn, Twitter/X, Personal Website, Instagram
- 6 tone options — Professional, Witty, Casual, Bold, Warm, Minimal
- Adjustable character limit (80–500 characters)
- Quick-fill example presets to get started instantly
- One-click copy to clipboard
- Regenerate button for fresh variations
- `Cmd/Ctrl + Enter` keyboard shortcut
- Full dark mode support
- Mobile responsive

---

## Project Structure

```
my-bio-app/
├── index.html                  # Frontend — form, UI, and API call
└── netlify/
    └── functions/
        └── generate.js         # Serverless function — proxies Anthropic API
```

---

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18 or higher
- [Netlify CLI](https://docs.netlify.com/cli/get-started/) — `npm install -g netlify-cli`
- An [Anthropic API key](https://console.anthropic.com/)

### Local Development

```bash
# Clone the repository
git clone https://github.com/yourusername/ai-bio-generator.git
cd ai-bio-generator

# Log in to Netlify
netlify login

# Start local dev server (runs functions + frontend together)
netlify dev
```

Open [http://localhost:8888](http://localhost:8888) in your browser.

### Environment Variables

Create a `.env` file in the root folder for local development:

```
ANTHROPIC_API_KEY=sk-ant-your-key-here
```

> Never commit `.env` to GitHub. It is already excluded by the Node `.gitignore`.

---

## Deployment

### Deploy to Netlify

```bash
# One-time setup
netlify login
netlify init

# Deploy to production
netlify deploy --prod
```

When prompted:
- **Publish directory:** `.` (just a dot)

### Add API Key on Netlify

1. Go to [netlify.com](https://netlify.com) → your site
2. **Site configuration → Environment variables → Add variable**
3. Key: `ANTHROPIC_API_KEY` · Value: `sk-ant-...your key...`
4. Redeploy: `netlify deploy --prod`

### Auto-deploy via GitHub

1. Push your code to GitHub
2. Go to **Netlify Dashboard → Site → Build & Deploy → Link to Git repository**
3. Select your GitHub repo

Every `git push` will now trigger an automatic redeploy.

---

## How It Works

```
User fills form (name, job, hobbies, goal, platform, tone, char limit)
        ↓
index.html builds a prompt and sends it to /.netlify/functions/generate
        ↓
generate.js adds the API key and forwards the request to Anthropic
        ↓
Claude returns a tailored bio
        ↓
index.html displays the result with character count and copy button
```

The serverless function keeps your API key secure — it never touches the frontend.

---

## Prompt Template

```
You are an expert copywriter specializing in personal branding.
Write a bio for [Platform] using these details:

Name: [Name]
Job/Role: [Job]
Hobbies & Interests: [Hobbies]
Goal: [Goal]

Keep the tone [Tone] and strictly under [X] characters.
Write only the bio — no intro, no explanation, no quotes.
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript |
| Icons | Tabler Icons |
| AI Model | Claude Sonnet (claude-sonnet-4-6) |
| Backend | Netlify Serverless Functions |
| Hosting | Netlify |

---

## Customization

**Add a new platform** — in `index.html`, add a button to `#platformGrid`:
```html
<button class="platform-btn" data-val="GitHub">
  <i class="ti ti-brand-github"></i>GitHub
</button>
```

**Add a new tone** — add a button to `#toneGrid`:
```html
<button class="tone-btn" data-val="Inspirational and motivating">
  <i class="ti ti-rocket"></i> Inspire
</button>
```

**Change the model** — in `index.html`, update the model name in the fetch body:
```js
model: 'claude-opus-4-6'  // swap to a different Claude model
```

---

## License

MIT — free to use, modify, and distribute.

---

## Acknowledgements

- [Anthropic](https://anthropic.com) for the Claude API
- [Tabler Icons](https://tabler.io/icons) for the icon set
- [Netlify](https://netlify.com) for hosting and serverless functions
