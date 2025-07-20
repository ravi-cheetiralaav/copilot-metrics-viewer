# Copilot Instructions for GitHub Copilot Metrics Viewer

## Overview
The GitHub Copilot Metrics Viewer is a Nuxt-based application designed to visualize metrics related to GitHub Copilot usage. It integrates with the GitHub Copilot Metrics API to provide insights into acceptance rates, language breakdowns, chat metrics, and seat analysis for organizations and enterprises.

## Architecture
- **Frontend**: Built with Nuxt.js, located in the `app/` directory. Key components include:
  - `MainComponent.vue`: The entry point for rendering metrics.
  - `AgentModeViewer.vue`: Displays detailed statistics for GitHub Copilot features.
  - `MetricsViewer.vue`: Handles the visualization of metrics data.
- **Backend**: The app relies on GitHub APIs for data. Authentication can be configured using GitHub OAuth or Personal Access Tokens (PAT).
- **Infrastructure**: Deployment configurations are defined in the `infra/` directory using Bicep templates.

## Key Files and Directories
- `app/`: Contains the Nuxt application code.
- `infra/`: Infrastructure as Code (IaC) files for deploying the application.
- `.env`: Environment variables for configuring the application.
- `README.md`: Detailed setup and deployment instructions.
- `e2e-tests/`: End-to-end tests using Playwright.

## Environment Variables
- `NUXT_PUBLIC_SCOPE`: Defines the scope of API calls (`enterprise`, `organization`, or `team`).
- `NUXT_PUBLIC_GITHUB_ORG`: Specifies the GitHub organization for metrics.
- `NUXT_PUBLIC_IS_DATA_MOCKED`: Enables mocked data for testing.
- `NUXT_SESSION_PASSWORD`: Required for session encryption (minimum 32 characters).

## Developer Workflows
### Setup
1. Install dependencies:
   ```bash
   npm install
   ```
2. Run the development server:
   ```bash
   npm run dev
   ```
3. Build the Docker image:
   ```bash
   docker build -t copilot-metrics-viewer .
   ```
4. Run the Docker container:
   ```bash
   docker run -p 8080:80 --env-file ./.env copilot-metrics-viewer
   ```

### Testing
- Unit tests are located in the `tests/` directory.
- End-to-end tests are in `e2e-tests/` and can be run using Playwright.

### Deployment
- Use the `infra/main.bicep` file for Azure deployments.
- For one-click Azure deployment, refer to `DEPLOYMENT.md`.

## Patterns and Conventions
- **Component-based Architecture**: Each feature is encapsulated in a Vue component (e.g., `AgentModeViewer.vue`).
- **TypeScript Models**: API responses are strongly typed using interfaces in `app/model/`.
- **Chart.js Integration**: Used for rendering visualizations in components like `AgentModeViewer.vue`.
- **Environment-driven Configuration**: Public variables (prefixed with `NUXT_PUBLIC_`) are exposed to the frontend.

## External Dependencies
- **GitHub API**: For fetching Copilot metrics.
- **Vue Chart.js**: For data visualization.
- **Playwright**: For end-to-end testing.

## Tips for AI Agents
- Follow the patterns in `app/components/` for creating new features.
- Use the TypeScript models in `app/model/` to ensure type safety.
- Refer to `README.md` and `DEPLOYMENT.md` for setup and deployment details.
- Mock data can be enabled via `NUXT_PUBLIC_IS_DATA_MOCKED` for testing without API calls.

For further details, consult the `README.md` or reach out to the maintainers listed in the `SUPPORT.md` file.
