# Qoruz AI

A React and Vite chat prototype for creator discovery, campaign research and planning, content strategy, and influencer marketing questions. It uses OpenUI to render structured assistant responses and stores conversation threads in browser local storage.

## Local setup

1. Use Node.js 22.23.3 (`nvm use`).
2. Copy `.env.example` to `.env.local`.
3. Configure the providers you want to use:
   - **Gemini:** set `VITE_GEMINI_API_KEY`. Optionally set `VITE_GEMINI_MODEL` (defaults to `gemini-3.6-flash`).
   - **Ollama Cloud:** set `OLLAMA_API_KEY`. Optionally set `VITE_OLLAMA_MODEL` (defaults to `gpt-oss:120b`).
   - **Groq:** set `GROQ_API_KEY`. Optionally set `VITE_GROQ_MODEL` (defaults to `openai/gpt-oss-120b`).
   - **Qoruz campaigns:** set `VITE_QORUZ_API_KEY` to enable live campaign lookups. Optionally set `VITE_QORUZ_API_URL` (defaults to `https://api.qoruz.com/v1`).
4. Optionally set `VITE_PROFILE_NAME` and `VITE_PROFILE_EMAIL` for the workspace profile.
5. Run `npm run dev` and open the Vite URL, normally `http://localhost:5173`.

Choose the AI provider and model from the model controls. Available models are loaded from the selected provider, and provider/model preferences are saved in local storage. Ollama Cloud and Groq use same-origin Vite proxies at `/ollama` and `/groq`.

## Qoruz data and limitations

The app can fetch campaigns from the configured Qoruz `/campaigns` endpoint when a prompt asks for the user's campaigns. Other creator discovery, research, planning, and content responses are AI-generated guidance; they are not live Qoruz data. The app does not use external web search or a database. Treat generated examples and recommendations as illustrative, and verify them before acting.

## Security

This is a local prototype, not a production deployment. `VITE_` variables are embedded in the browser bundle, so `VITE_GEMINI_API_KEY` and `VITE_QORUZ_API_KEY` are visible to users. Use restricted development credentials and rotate them if exposed. Never commit `.env.local`.

`OLLAMA_API_KEY` and `GROQ_API_KEY` are attached by the Vite server-side proxies during development and Vite preview. A static production build does not include these proxies; production hosting needs a secured backend proxy for these providers and for any secrets that must remain private.

## Build and checks

- `npm run dev` starts the development server.
- `npm run lint` runs Oxlint.
- `npm run build` creates the production site in `dist/`.
- `npm run preview` serves the production build locally.

The production build uses Rolldown code splitting for dependencies to keep JavaScript chunks below the configured 450 KiB target where possible. The generated `dist/` directory is build output and should not be committed.
