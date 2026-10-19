# Fraud-score signup prototype

Homecentre-style sign-up page that calls a (mock) partner fraud-score API and acts on the score.

Run: just open `index.html` in a browser (no Node/server needed).

| Score | Action |
|-------|--------|
| < 30  | Allow |
| 30–69 | Challenge with OTP (shown in modal) |
| ≥ 70  | Decline |

Everything is in one file: a mock partner SDK (signal collection), a mock partner scoring function, the decision engine, and an in-memory OTP check (3 attempts, 5 min expiry). Replace `partnerScore` with a real vendor API call to productionise.

Use the demo panel on the page to force low/medium/high, or try a `@mailinator.com` email.