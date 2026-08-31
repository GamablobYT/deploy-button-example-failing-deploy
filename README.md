# Deploy Button example: failing deployment

This disposable fixture is intentionally **ready to dispatch but fails during provider execution**. Publish this folder as its own repository before connecting it to Deploy Button.

## Expected Deploy Button result

- The deploy workflow is manually dispatchable and targets GitHub Pages.
- The `unit-tests` check passes.
- Readiness can pass with `unit-tests` selected and no required secret names.
- The dispatched workflow fails in its build job before artifact upload, letting Deploy Button exercise provider failure polling, events, and terminal UI.

## Try it

1. Grant the Deploy Button GitHub App access to this repository and refresh repositories.
2. In GitHub, set **Settings -> Pages -> Source** to **GitHub Actions**.
3. Select branch `main`, executor **GitHub Actions**, destination **GitHub Pages**, workflow `.github/workflows/deploy-button.yml`, and required check `unit-tests`.
4. Wait for the initial `unit-tests` run to pass, run readiness, then deploy.
5. Confirm the provider run fails at **Produce the intentional provider failure** and Deploy Button reaches an honest failed terminal state.

The failure is confined to the deployment workflow. `npm ci && npm run check` and the push CI check remain healthy.
