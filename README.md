# Render Status Badge 🛠️🟢

[![npm version](https://img.shields.io/npm/v/render-status-badge)](https://www.npmjs.com/package/render-status-badge)
[![GitHub License](https://img.shields.io/github/license/nia-cloud-official/render-status)](https://github.com/nia-cloud-official/render-status-badge/blob/main/LICENSE)
[![Render Status](https://img.shields.io/badge/Render-Live-brightgreen?logo=render&style=for-the-badge)](https://github.com/nia-cloud-official/render-status-badge)

A dynamic status badge generator for Render.com deployments. Automatically displays your service's deploy status (Live, Failed, Deploying) in your README or docs using Shields.io and Render's API.

![Example Badges](https://img.shields.io/badge/Render-Live-brightgreen?logo=render&style=for-the-badge)
![Example Badges](https://img.shields.io/badge/Render-Failed-red?logo=render&style=for-the-badge)
![Example Badges](https://img.shields.io/badge/Render-Deploying-blue?logo=render&style=for-the-badge)

## Features ✨

- **Real-time Status**: Automatically updates based on Render's deploy status.
- **Customizable**: Supports Shields.io styles (flat, plastic, etc.).
- **Multi-Project Ready**: Use across multiple repos/services via `.env` config.
- **CI/CD Integration**: Built-in GitHub Actions workflow for auto-updates.
- **Open Source**: MIT licensed — modify and distribute freely!

## Installation 📦

```bash
npm install render-status-badge
# or
yarn add render-status-badge
```

## Usage 🚀

### 1. Configure Environment Variables
Create a `.env` file in your project root:
```env
RENDER_API_KEY="your_render_api_key_here"
RENDER_SERVICE_ID="your_service_id_here"
```

### 2. Generate the Badge URL
Run the script to get your dynamic badge URL:
```bash
npx render-status-badge
# Output: https://img.shields.io/badge/Render-Live-brightgreen?logo=render&style=for-the-badge
```

### 3. Add to README.md
Paste the generated URL into your markdown:
```markdown
![Render Status](YOUR_BADGE_URL_HERE)
```

## GitHub Actions Automation 🤖
Add this workflow (`.github/workflows/update-badge.yml`) to auto-update your badge:
```yaml
name: Update Render Status Badge
on:
  schedule:
    - cron: '*/5 * * * *' # Runs every 5 minutes
  workflow_dispatch:

jobs:
  update-badge:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Generate Badge
        env:
          RENDER_API_KEY: ${{ secrets.RENDER_API_KEY }}
          RENDER_SERVICE_ID: ${{ secrets.RENDER_SERVICE_ID }}
        run: npx render-status-badge >> badge-url.txt
      - name: Update README
        run: |
          sed -i "s|https://img.shields.io/badge/Render-Unknown-lightgrey?logo=render
          git commit -am "Update Render status badge" && git push
```

## Configuration ⚙️
| Environment Variable | Required | Description                          |
|-----------------------|----------|--------------------------------------|
| `RENDER_API_KEY`      | Yes      | Render API key ([get it here](https://render.com/docs/api#authentication)) |
| `RENDER_SERVICE_ID`   | Yes      | Your Render service ID               |

## Contributing 🤝
Contributions are welcome! Here’s how:
1. **Report Issues**: Open a GitHub issue for bugs or feature requests.
2. **Suggest Features**: Propose improvements via Discussions.
3. **Submit PRs**: Fork the repo, create a branch, and open a PR.

## License 📄
MIT License — see [LICENSE](LICENSE) for details.

---

**Made by [Milton Vafana](https://github.com/nia-cloud-official)**  
*Credits to [Render](https://render.com) and [Shields.io](https://shields.io)*
