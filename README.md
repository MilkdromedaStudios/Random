# Random - AI-Powered Web Experience Generator

> Discover something completely new every time you refresh. One moment it's generative art, the next a mini-game, then a quirky utility — all powered by AI and delivered in a single HTML file.

**Live Demo:** [random.krishnasingh.live](https://random.krishnasingh.live)

## What Is This?

Ever wondered what it would be like to refresh a webpage and see something completely different every single time? This project does exactly that. It's a web page that generates entirely new, fully functional web experiences on the fly using AI.

No backend. No frameworks. No database of pre-built pages. Just one HTML file, some clever JavaScript, and the Gemini API.

## How It Works

### The Concept

Instead of storing thousands of webpage variations, this project uses a single "shell" HTML file that:
1. Shows a loading screen
2. Calls the Gemini AI API with a creative prompt
3. Receives a complete HTML page (with CSS and JavaScript)
4. Renders it in an iframe

Every refresh triggers a new API call, generating something completely unique.

### The Architecture

**Three Core Components:**

1. **The Shell (index.html)**
   - Loading screen with animated progress bar
   - Hidden iframe container for AI-generated content
   - API key management system

2. **The Engine (JavaScript)**
   - API key validation and storage (localStorage)
   - Prompt engineering for diverse outputs
   - Fetch API calls to Gemini
   - Response parsing and iframe injection

3. **The Prompt**
   - Instructs AI to generate complete, self-contained HTML files
   - Enforces variety across 10+ categories (games, tools, art, etc.)
   - Specifies design requirements (responsive, interactive, polished)

## Features

- **Infinite Variety**: Generates unique experiences across multiple categories:
  - 🎨 Generative Art (particle systems, fractals, animations)
  - 🛠️ Utility Tools (calculators, converters, generators)
  - 🎮 Mini Games (Snake, Tetris, puzzles, trivia)
  - 📊 Data Visualizations (charts, trackers, dashboards)
  - 🌟 Interactive Experiences (quizzes, story generators)
  - 🎵 Audio/Visual Tools (beat makers, sound visualizers)
  - And more...

- **Zero Dependencies**: Everything runs in a single HTML file
- **Secure API Key Storage**: Keys stored locally in browser (localStorage)
- **API Key Validation**: Verifies keys before saving
- **Responsive Design**: Works on desktop, tablet, and mobile
- **Smooth Transitions**: Polished loading animations and fade effects

## Getting Started

### Prerequisites

You'll need a Gemini API key (it's free!):
1. Visit [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Sign in with your Google account
3. Generate a new API key

### Usage

1. **Clone or Download**
   ```bash
   git clone https://github.com/krishnasinghprojects/Random.git
   cd Random
   ```

2. **Open the File**
   - Simply open `index.html` in any modern browser
   - Or serve it with a local server:
     ```bash
     python -m http.server 8000
     # Visit http://localhost:8000
     ```

3. **Enter Your API Key**
   - On first visit, you'll be prompted to enter your Gemini API key
   - The key is validated and stored locally
   - It never leaves your browser

4. **Enjoy**
   - Refresh the page to generate a new experience
   - Each refresh creates something completely different

## Technical Deep Dive

### The Prompt Engineering

The magic happens in the prompt. It instructs the AI to:
- Choose randomly from 10+ categories
- Generate complete, self-contained HTML
- Include modern CSS (gradients, animations, shadows)
- Add meaningful interactivity
- Ensure mobile responsiveness
- Use specific fonts (Lora, Young Serif)
- Output raw HTML only (no markdown formatting)

### The Loading Flow

```
Page Load → Check localStorage for API Key
    ↓
    ├─ No Key? → Show API Key Input Form → Validate → Save → Reload
    ↓
    └─ Has Key? → Show Loading Screen → Call Gemini API
                        ↓
                   Parse Response → Clean HTML → Inject into iframe
                        ↓
                   Fade Out Loader → Fade In Content
```

### API Integration

Uses the Gemini 2.5 Flash model via REST API:
```javascript
const GEMINI_API_URL = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=${apiKey}`;
```

The response is cleaned to remove markdown code fences:
```javascript
htmlContent = htmlContent.replace(/^```html\s*|```$/g, '').trim();
```

Then injected into the iframe:
```javascript
contentFrame.srcdoc = htmlContent;
```

### Security Considerations

- API keys stored in localStorage (client-side only)
- No server-side storage or logging
- iframe sandboxing for generated content
- API key validation before storage

## Project Structure

```
Random/
├── index.html          # The entire application
├── CNAME              # Custom domain configuration
└── README.md          # This file
```

Yes, it's really just one HTML file. Everything else is generated on the fly.

## Why This Approach?

**Pros:**
- Zero hosting costs (static file)
- No database needed
- Infinite content without storage
- Easy to deploy (GitHub Pages, Netlify, etc.)
- Fun way to explore AI capabilities

**Cons:**
- Requires API key (but free tier is generous)
- Depends on external API availability
- Generation takes a few seconds
- Quality varies based on AI output

## Customization

Want to modify what gets generated? Edit the `PROMPT` constant in the JavaScript:

```javascript
const PROMPT = `
You are a visionary web developer...
[Customize categories, requirements, style guidelines here]
`;
```

## Browser Compatibility

Works in all modern browsers that support:
- ES6+ JavaScript (async/await, fetch)
- CSS Grid and Flexbox
- iframe srcdoc attribute
- localStorage

Tested on: Chrome, Firefox, Safari, Edge

## Contributing

This is a fun experimental project, but contributions are welcome!

Ideas for improvements:
- Add more prompt categories
- Implement generation history
- Add "favorite" functionality
- Create themed generation modes
- Add social sharing features

## License

This project is open source and available under the MIT License.

## Credits

**Created by:** [Krishna Singh](https://krishnasingh.live)

**Powered by:** Google Gemini AI

**Inspired by:** The idea that the web should be surprising, creative, and fun.

## Learn More

Read the full story behind this project:
- [Blog Post: "I Built an AI-Powered Random Web Page Generator"](https://krishnasingh.live/projects)

## Support

If you encounter issues:
1. Verify your API key is valid
2. Check browser console for errors
3. Ensure you have internet connectivity
4. Try clearing localStorage and re-entering your key

For bugs or feature requests, open an issue on GitHub.

---

**Remember:** Every refresh is a new adventure. You never know what you'll get next. 🎲
