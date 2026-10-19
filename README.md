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

## Support console

Open `index.html#admin` (or the "Open support console" link in the demo panel). Every fraud decision is logged with a reference code (`FR-XXXXXX`) that customers see on blocked screens. Agents can search by reference/email/mobile, see score, reasons, OTP result and a talk track, clear a customer for retry, or escalate. The log is stored in the browser's localStorage (prototype only). Use "Load sample data" for demos.

## Fraud ops console

Open `index.html#fraud` (or "Fraud ops" in the demo panel). A deeper view for the fraud team: KPI tiles and score histogram; per-decision score breakdown, every rule evaluated with its input value, raw SDK signals, device and (simulated) network info, linked accounts on the same device, outcome timeline, case status, notes and an audit trail. Analysts can block/unblock a user or device (forces decline), allowlist a user, and edit rule weights and OTP/decline thresholds. IP/geo/ASN are simulated.
