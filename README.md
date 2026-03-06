# Da Nang Language Exchange Club Website

This is the source code for the official website of the Da Nang Language Exchange Club, built with Hugo and the PaperMod theme.

## 🚀 Quick Start (Local Development)

1. **Prerequisites:**
   - Install **Git**
   - Install **Hugo** (Extended version recommended, v0.120.0 or higher)

2. **Clone the repository:**
   ```bash
   git clone --recurse-submodules https://github.com/your-username/danang-language-exchange.git
   cd danang-language-exchange
   ```

3. **Run the local server:**
   ```bash
   hugo server -D
   ```
   The site will be available at `http://localhost:1313/`.

## ✍️ Content Editing Guide (For Admins)

The site is designed to be easily updated by editing simple Markdown files.

### 📅 How to Add a New Event
1. Create a new markdown file in `content/events/` (e.g., `content/events/april-meetup.md`).
2. Add the following at the top (front matter):
   ```yaml
   ---
   title: "Friday Exchange at The Local Bean"
   date: 2026-04-10T19:00:00+07:00
   draft: false
   venue: "The Local Bean, 123 Main St, Da Nang"
   time: "7:00 PM - 9:00 PM"
   summary: "Join our next meetup!"
   ---
   ```
3. Write any additional details below the front matter.

### 📚 How to Add a New Resource
1. Create a markdown file in `content/resources/`.
2. Ensure you have the following front matter:
   ```yaml
   ---
   title: "Ordering Coffee in Vietnamese"
   category: "Beginner"
   download_link: "https://link-to-google-drive-pdf"
   format: "PDF"
   draft: false
   ---
   ```
3. Add a short description below.

### 🗣️ How to Add or Feature a Topic
1. Add a new file in `content/topics/`.
2. Include the front matter:
   ```yaml
   ---
   title: "Topic 4: Hobbies"
   level: "All Levels"
   summary: "Discuss what you do for fun."
   featured: true # Set to true to show this topic on the homepage!
   draft: false
   vocab_prompts: ["sở thích (hobby)", "chơi (to play)"]
   sample_questions: ["What is your favorite hobby?"]
   ---
   ```

## ☁️ Deployment (Cloudflare Pages)

The website is set up to automatically deploy via Cloudflare Pages.

- **Build command:** `hugo --gc --minify`
- **Build output directory:** `public`
- **Root directory:** `/`

*Whenever you push to the `main` branch, Cloudflare will automatically rebuild and deploy the site.*
