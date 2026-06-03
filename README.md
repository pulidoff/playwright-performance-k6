# k6 Performance Testing Suite

[![k6 Performance Tests](https://github.com/your-username/playwright-performance-k6/actions/workflows/k6.yml/badge.svg)](https://github.com/your-username/playwright-performance-k6/actions/workflows/k6.yml)

Performance testing suite for [Task Bliss App](https://task-bliss-app-82.lovable.app) built with [k6](https://k6.io/).

## Stack

- **[k6](https://k6.io/)** — open-source load testing tool
- **GitHub Actions** — CI pipeline running smoke tests on every push/PR

## Test Scenarios

| Test | VUs | Duration | Purpose |
|------|-----|----------|---------|
| `smoke.js` | 1 | 30s | Verify the system works under minimal load |
| `load.js` | 10 | 1m | Validate performance under expected normal load |
| `stress.js` | ramp to 50 | ~2.5m | Find the breaking point with increasing load |
| `spike.js` | spike to 100 | ~1m | Test system reaction to sudden traffic bursts |
| `soak.js` | 5 | 10m | Detect memory leaks and degradation over time |

## Thresholds

All tests enforce the following thresholds:

- **p(95) response time** < 2000ms
- **Error rate** < 10%

## Project Structure

```
tests/
  smoke.js        # 1 VU, 30s
  load.js         # 10 VUs, 1 minute
  stress.js       # ramp up to 50 VUs
  spike.js        # sudden spike from 0 to 100 VUs and back
  soak.js         # 5 VUs, 10 minutes
.github/
  workflows/
    k6.yml        # CI pipeline (smoke test only)
.gitignore
README.md
```

## Prerequisites

Install k6: https://k6.io/docs/get-started/installation/

```bash
# macOS
brew install k6

# Windows (Chocolatey)
choco install k6

# Windows (winget)
winget install k6
```

## Running Tests

```bash
# Smoke test — quick sanity check
k6 run tests/smoke.js

# Load test — normal expected traffic
k6 run tests/load.js

# Stress test — ramp up to find limits
k6 run tests/stress.js

# Spike test — sudden burst of traffic
k6 run tests/spike.js

# Soak test — sustained load over time
k6 run tests/soak.js
```

## CI

The GitHub Actions workflow runs `smoke.js` automatically on every push and pull request to `main`. To trigger the other scenarios manually, run them locally or extend the workflow.
