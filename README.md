# riverview.geolibre.app

GeoLibre with the [Riverview plugin](https://github.com/mbonnema/riverview-visualization-plugin)
installed and loaded automatically. Published to GitHub Pages at
<https://mbonnema.github.io/riverview.geolibre.app/>.

The app is not developed here. `.github/workflows/deploy.yml` checks out
`opengeos/GeoLibre` and the plugin, installs the plugin into GeoLibre's bundled
drop-in folder (`npm run install:geolibre -- --web <root>`), builds, and deploys.
No sign-in gate and no AI assistant.

## One-time setup

1. Push this repo to GitHub as `mbonnema/riverview.geolibre.app`.
2. Settings > Pages > Source: **GitHub Actions**.
3. Create a fine-grained PAT with read-only **Contents** access to
   `mbonnema/riverview-visualization-plugin` (private) and add it as the secret
   `PLUGIN_REPO_TOKEN`.
4. Add the site origin to the bucket CORS rule. This replaces the whole rule, so
   keep the existing origins:
   `http://localhost:8000`, `https://geolibre.app`, `https://web.geolibre.app`,
   **`https://mbonnema.github.io`**
   (`gcloud storage buckets update gs://riverview-geolibre --cors-file=<file>`).
5. Run **Actions > Deploy riverview.geolibre.app**, or push to `main`.

Redeploys are not triggered by changes in the two source repos; re-run the
workflow (optionally pinning `geolibre_ref` / `plugin_ref`).

## Inputs

The site ships no default data. Choose inputs from Riverview > Select inputs,
or open a saved GeoLibre project (which records its config URL), or use
`?riverview_config=<url>`.
