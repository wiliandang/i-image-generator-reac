# i-image-generator-reacgit init
git remote add origin https://github.com/wiliandang/ai-image-generator-react.git
git add .
git commit -m "Initial commit"
git push -u origin master
# AI Image Generator with Gemini + OpenAI

This app enhances prompts using Gemini Pro (Google AI) and generates realistic images using OpenAI's DALL·E.

## 🚀 Features
- Prompt enhancement (Gemini)
- Image generation (DALL·E 3)
- PDF export
- Tailwind UI

## 🧪 Setup
1. Clone this repo
2. Create `.env.local` and fill:
   ```
   VITE_OPENAI_API_KEY=your_openai_key
   GEMINI_API_KEY=your_gemini_key
   ```
3. Install & run:
   ```bash
   npm install
   npm run dev
   ```
4. Deploy to [Vercel](https://vercel.com)

MIT License
