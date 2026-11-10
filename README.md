# aws-tracker

The page for a personal learning tracker, served at <https://ash-agarwalcs.github.io/aws-tracker/>.

This repository is public and holds only the page (`index.html`). The page contains no plan and no progress. After you connect it with a token, it reads `plan-data.js` and `progress.json` from a private repository through the GitHub API and writes `progress.json` back as you tick.

## How it works

- **Connect:** the page asks for a fine-grained GitHub token with **Contents: Read and write** on the one data repository. The token is kept in the browser's local storage and sent only to `api.github.com`.
- **Read:** it fetches `plan-data.js` (which defines the plan) and `progress.json` from the data repository.
- **Save:** about 2.5 seconds after the last change it commits `progress.json` to the data repository. The top bar shows Saving, Saved, Offline or Not saved.
- **Other devices:** when the page regains focus or comes back online it checks for a newer `progress.json`. If both sides changed, it asks which copy to keep.
- **Offline:** it starts from the copy cached in the browser and saves when GitHub can be reached.

The page loads no third-party code, and its content security policy allows network requests to `api.github.com` only.

## Changing the page

Edit `index.html` and push to `main`; GitHub Pages republishes in a minute or two. There is no build.

Two URL parameters exist for testing: `?today=YYYY-MM-DD` overrides today's date, and `?branch=name` reads and writes another branch of the data repository.
