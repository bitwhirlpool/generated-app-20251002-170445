# CogniCore AI Studio
[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/bitwhirlpool/generated-app-20251002-163403)
CogniCore AI Studio is a sophisticated, multi-modal AI chat interface designed for developers, researchers, and creators. It provides a unified frontend to interact with a wide array of AI models, including those from Cloudflare's AI Gateway and external providers like OpenRouter. The application features a stunning, minimalist dark-themed UI with a three-panel layout for seamless workflow: a session manager, a central chat interface, and a detailed model configuration panel.
Built on Cloudflare's serverless stack, it leverages Durable Objects for persistent, stateful agent-based conversations, ensuring a robust, scalable, and high-performance user experience.
## ✨ Key Features
- **Unified Chat Interface**: Interact with multiple AI models from Cloudflare, OpenRouter, and more in one place.
- **Three-Panel Layout**: A professional, responsive layout for managing sessions, chatting, and configuring models efficiently.
- **Session Management**: Create, rename, and delete chat sessions.
- **AI-Assisted Prompt Builder**: Generate effective, well-structured prompts from simple ideas using AI.
- **Comprehensive Prompt Library**: A curated collection of pre-built prompts for various tasks, personalities, and complexities.
- **Stateful Conversations**: Persistent chat sessions powered by Cloudflare Durable Objects via the Agents SDK.
- **Real-time Streaming**: Get instant feedback from AI models with streaming responses.
- **Visually Stunning UI**: A beautiful, minimalist dark theme with smooth animations and a focus on user experience.
- **Vibe Coding Environment**: A real-time, AI-powered code generation and assistance tool.
## ���️ Technology Stack
- **Frontend**: React, Vite, TypeScript
- **Backend**: Hono on Cloudflare Workers
- **State Management**: Zustand (Client-side), Cloudflare Durable Objects (Server-side)
- **Styling**: Tailwind CSS, shadcn/ui
- **Animation**: Framer Motion
- **AI Integration**: Cloudflare Agents SDK, OpenAI SDK (for types)
- **Schema Validation**: Zod
## 🚀 Getting Started
Follow these instructions to get a local copy up and running for development and testing purposes.
### Prerequisites
- [Bun](https://bun.sh/) installed on your machine.
- A [Cloudflare account](https://dash.cloudflare.com/sign-up).
### Installation & Setup
1.  **Clone the repository:**
    ```sh
    git clone https://github.com/your-username/cognicore-ai-studio.git
    cd cognicore-ai-studio
    ```
2.  **Install dependencies:**
    ```sh
    bun install
    ```
3.  **Configure environment variables:**
    Create a `.dev.vars` file in the root of the project for local development. You will need to get your Account ID and create an AI Gateway.
    ```ini
    # .dev.vars
    # Required: Your Cloudflare AI Gateway URL
    # Format: https://gateway.ai.cloudflare.com/v1/ACCOUNT_ID/GATEWAY_NAME/openai
    CF_AI_BASE_URL="https://gateway.ai.cloudflare.com/v1/YOUR_ACCOUNT_ID/YOUR_GATEWAY_ID/openai"
    # Required: An API Key with permission to use the AI Gateway
    CF_AI_API_KEY="YOUR_CLOUDFLARE_API_KEY"
    ```
    **Note:** Never commit your `.dev.vars` file or expose your secrets publicly.
## 💻 Development
To start the local development server, which includes both the Vite frontend and the Cloudflare Worker backend, run:
```sh
bun dev
```
This will start the application on `http://localhost:3000` (or the next available port). The frontend will automatically reload on changes, and the worker is available for API requests.
## ☁️ Deployment
This project is designed for seamless deployment to Cloudflare Pages.
1.  **Login to Wrangler:**
    ```sh
    bunx wrangler login
    ```
2.  **Deploy the application:**
    Run the deploy script, which builds the application and deploys it to your Cloudflare account.
    ```sh
    bun deploy
    ```
    Wrangler will guide you through the initial deployment process. For subsequent deployments, it will update the existing application.
3.  **Configure Production Secrets:**
    After the first deployment, you must add your environment variables as secrets in the Cloudflare dashboard.
    - Go to your Pages project > Settings > Environment variables.
    - Add `CF_AI_BASE_URL` and `CF_AI_API_KEY` with their production values.
### Deployment on Cloudflare Free Plan
**Important**: If you are deploying on the Cloudflare **free plan**, you may encounter an error related to Durable Objects. The free plan requires a specific migration type for Durable Objects.
To fix this, ensure your `wrangler.jsonc` file uses `new_sqlite_classes` for Durable Object migrations instead of `new_classes`. This template has been pre-configured for you, but it's good practice to verify:
```jsonc
// wrangler.jsonc
...
"migrations": [
    {
        "tag": "v1",
        "new_sqlite_classes": ["ChatAgent"]
    },
    {
        "tag": "v2",
        "new_sqlite_classes": ["AppController"]
    }
],
...
```
This change ensures compatibility with the storage backend used by the free tier.
Alternatively, deploy directly from your GitHub repository:
[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/bitwhirlpool/generated-app-20251002-163403)
## 📂 Project Structure
- `src/`: Contains all the frontend React application code.
  - `components/`: Reusable UI components, including shadcn/ui components.
  - `pages/`: Top-level page components for different views.
  - `hooks/`: Custom React hooks for state and logic.
  - `lib/`: Utility functions and client-side libraries.
- `worker/`: Contains the Hono backend code running on Cloudflare Workers.
  - `index.ts`: The entry point for the worker.
  - `agent.ts`: The core `ChatAgent` Durable Object implementation.
  - `app-controller.ts`: The `AppController` Durable Object for session management.
  - `userRoutes.ts`: Defines the API routes for the application.
- `wrangler.jsonc`: Configuration file for the Cloudflare Worker, including bindings.
## 📄 License
This project is licensed under the MIT License. See the `LICENSE` file for details.