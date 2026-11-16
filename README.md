# FairSplit: Split Smart. Settle Easy. Stay Fair.
Group expense tracker where **a payment only counts once the receiver approves it**.

**Stack:** React + Vite, React Router, Lucide, Recharts · FastAPI, SQLAlchemy, SQLite (Decimal money) · no API keys.

## Run
```bash
# terminal 1
cd backend && pip install -r requirements.txt && uvicorn main:app --reload      # http://127.0.0.1:8000
# terminal 2
cd frontend && npm install && npm run dev                                       # http://localhost:5173
```
The SQLite file (`backend/fairsplit.db`) is created and seeded on first start. Delete it to reset. Needs Python 3.10+.
A random signing secret is generated once into `backend/.secret` (or set `FAIRSPLIT_SECRET`). Sessions last 7 days.

**Tests:** `cd backend && pip install httpx && python test_api.py` (uses a throw-away database).

## Demo logins (password `demo123`)
aarav@demo.com · meera@demo.com · rohan@demo.com · isha@demo.com (or tap a demo chip on the login page).
Try: sign in as Aarav → Approvals → approve Isha's ₹500 (partial payment, +20 XP). Then sign in as Rohan to approve Meera's rent payment.

## Workflows
- **Add expense:** equal or custom split (amounts: numbers only, max 2 decimals, up to ₹1,00,00,000; leftover paise go to the first person so shares always add up exactly); payer never owes themselves; participants get notified.
- **I've paid:** amount, method, reference → status "Awaiting Receiver Confirmation". Debt unchanged. You can never have more awaiting than you actually owe that person.
- **Approve/Reject:** only the receiver. Approve settles oldest shares first (partials supported), awards XP/badges, notifies both. Reject needs a reason; debtor can resubmit. Each payment can be decided exactly once, even with double-clicks or two tabs.
- **Leaving a group:** only when you owe nothing, nobody owes you, and no payment of yours is awaiting.
- **Budget Baba:** debt simplification, shown as suggestions only.
- **Weekly summary:** computed on demand; a background thread creates weekend reminders only while the server runs.

## Layout
`backend/main.py` (models, API, logic) · `backend/seed.py` · `frontend/src/App.jsx` (all pages) · `frontend/src/styles.css`
