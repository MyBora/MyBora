# Bora Karatepe

I build production software for small Turkish businesses, mostly alone: product,
backend, frontend, database, deployment, and the person who installs it on site.

Most of my repositories are private because they are live commercial systems.
Short descriptions are below, and I am happy to give access on request.

---

## Quarr — a menu that learns to sell

**[quarr.app](https://quarr.app)** · live in production · private repo · TypeScript, PL/pgSQL

My latest and the only in-production project. A restaurant menu that rearranges itself from how that venue's own tables order,
and measures whether doing so actually earns money.

- **Guest side:** scan at the table, order from a phone. No app, no login, no
  account, and no payment step; the bill is settled at the table as it always was.
- **Venue side:** the whole service runs inside Telegram, with no dashboard to
  learn. Orders arrive as cards, pending orders sit in a pinned board, one tap
  marks an order as taken, and typed commands mark a dish sold out, close a table
  or rotate a table's QR. An hourly watchdog re-sends anything that did not arrive.
- **Measurement, not assertion:** one in ten table visits is held out from every
  suggestion, so the suggestion layer is compared against a control group every
  month instead of being claimed. The unit is the table visit rather than the
  phone, because a suggestion taken up by one guest reaches the whole table.
- **Security posture:** row-level security on every table, prices computed only
  on the server and never trusted from the client, unguessable table tokens,
  Postgres-based rate limits, and no payment surface at all.
- **Scale of the work:** 265 commits between July and September 2026, 121 SQL
  migrations, 45 automated verification suites covering ordering, security,
  delivery, panel actions and the guest experience.

Stack: Next.js (App Router, React Server Components), Supabase / Postgres,
Vercel, Tailwind, Zod, Telegram Bot API.

## Boreai — Instagram customer service for small businesses

Private repo · workflow automation

Went live with 2 customers, after a review of Meta restrictions and not being a tech provider for Meta was too risky, the project delayed until the requirements for being a Tech Provider for Meta are fullfilled. Around-the-clock automated replies in the owner's own voice for boutiques,
salons and restaurants, built on Instagram messaging and n8n workflows. The system answers the questions of the clients' behalf; by booking appointments, remembering past conversations, comprehending voice messages from clients' customers and also can see the images sent on instagram plus working with a vector database for the clients' products (such as clothing butiques' clothing inventory), and pulling the infos from the inventory if needed / asked by the customer from instagram. Beyond the automation itself, I wrote the system's data-protection documentation:
data flows, retention periods, third-party processors, user rights, a breach
procedure, and the client onboarding handbook.

## NEFES — a retention brain for pilates studios

Private repo · Python

Not a commercial one. Did to teach myself some python and deterministic if's. Sits on top of a studio's existing system: remembers every member, shows who is
drifting away and why, and drafts the message the owner sends.

- The risk engine is plain deterministic Python with **no LLM**, deliberately:
  anything that computes money and risk has to be testable, and hallucination is
  not an affordable failure mode there.
- The LLM only drafts the message, behind a validator, with an offline fallback
  so the product still works when the model does not.
- The owner approves and sends from their own channel; the system never sends
  on its own.
- Health notes are encrypted at rest (Fernet) to meet Turkish data-protection law.

---

## How I work

- **One measured number beats five confident claims.** Every product I build
  has a way to tell whether it worked, and I would rather ship the instrument
  before the marketing sentence.
- **Tests with negative controls.** After fixing something, I temporarily put
  the bug back to prove the new test actually fails, then restore the fix. A
  test that has never been red is not a test.
- **Determinism where money is involved, models where language is.** Prices,
  risk and eligibility are computed by code that can be read and tested; models
  write sentences, behind validators and fallbacks.
- **Turkish-first.** The people who use what I build are venue owners and staff
  on the floor, on a phone, mid-service. The interface has to survive that.
