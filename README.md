# Fraud-score signup prototype

Homecentre-style sign-up page that calls a (mock) partner fraud-score API and acts on the score.

**Live demo:** https://divek-landmark.github.io/fraud-score-checkout-prototype/

Run locally: open `index.html` in a browser (no Node/server needed).

| Score | Action |
|-------|--------|
| < 30  | Allow |
| 30–69 | Challenge with OTP (shown in modal) |
| ≥ 70  | Decline |

Everything is in one file: a mock partner SDK (signal collection), a rule-based mock partner scoring function, the decision engine, and an in-memory OTP check (3 attempts, 5 min expiry). Replace `partnerScore` with a real vendor API call to productionise.

## Customer journey

Starts at the cart (`#cart`), then sign in / sign up / forgot password, then checkout and payment. Fraud checks run on sign-in, sign-up, forgot password, add/edit/delete/default address, Shukran redemption, checkout load (Cash on Delivery is greyed out unless the decision is Allow) and Pay Now.

- OTP is verified once per session; medium-risk address and Shukran steps then skip it. Pay Now always re-challenges. High risk always declines.
- Declines never reveal the reason: customers see a vague "Something went wrong" message plus a reference code.

## Demo controls

Use the demo panel to force low/medium/high, or use emails: `@mailinator.com` scores 45 (OTP), `@blocked.test` scores 75 (decline). Tick "show fraud score" to display scores in popups. Run the tests with `cd tests && npm install && npm test`.

## Support console

Open `index.html#admin` (or the "Open support console" link in the demo panel). Every fraud decision is logged with a reference code (`FR-XXXXXX`) that customers see on blocked screens. Agents can search by reference/email/mobile, see score, reasons, OTP result and a talk track, clear a customer for retry, or escalate. The log is stored in the browser's localStorage (prototype only). Use "Load sample data" for demos.

## Fraud ops console

Open `index.html#fraud` (or "Fraud ops" in the demo panel). A deeper view for the fraud team: KPI tiles and score histogram; per-decision score breakdown, every rule evaluated with its input value, raw SDK signals, device and (simulated) network info, linked accounts on the same device, outcome timeline, case status, notes and an audit trail. Analysts can block/unblock a user or device (forces decline), allowlist a user, and edit rule weights and OTP/decline thresholds. IP/geo/ASN are simulated.
