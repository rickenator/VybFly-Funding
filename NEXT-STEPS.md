# What you need to do to turn this on

Everything on my side is written and verified. These are the steps only you can
take — they involve identity, tax, and bank details, which I must not touch.

## 1. Enable GitHub Sponsors (required, and not yet done)

I checked: `gh api graphql { viewer { sponsorsListing } }` returns **null** for
`rickenator` — there is no Sponsors listing yet, so nothing can point at it.

1. Go to **https://github.com/sponsors/accounts** and click *Join the waitlist* /
   *Set up your sponsors profile* if prompted.
2. Complete the profile: short description, the tiers from `SPONSOR-PITCH.md`
   (Rung $25 / Replication $100 / Milestone $500 / Embiggenator $1,000+).
3. Complete **tax and bank** details. GitHub handles US 501(c)(3) verification;
   for an individual account you'll do a W-9-equivalent and connect a bank account
   or Stripe. This is the part I deliberately don't automate.
4. Approval can take a few days.

## 2. Once approved, add `FUNDING.yml`

Drop this file at `VybFly/.github/FUNDING.yml`:

```yaml
github: [rickenator]
custom: ["https://github.com/rickenator/VybFly-Funding/blob/main/SPONSOR-PITCH.md"]
```

That puts a **Sponsor** button on the VybFly repo page and surfaces it in the
repo's sidebar.

## 3. Decide where the pitch text lives

Three options, pick one (or several):

- **In the VybFly README** — a short "Sponsorship" section linking to the full
  pitch. Highest visibility, because that's where readers already are.
- **A separate repo** (what I built here: `/usr/export/rick/Projects/VybFly-Funding`)
  — keeps the science repo clean of fundraising material, which some readers prefer.
- **On vyb-lang.org** — if you want a public page outside GitHub.

## 4. Answer two questions I could not decide for you

- **Do you want named sponsor credit?** The pitch currently promises "named credit
  at the Milestone tier and above" — that's your call to keep or drop.
- **Is ~$1,000 the goal you want to state publicly?** My upper-bound model gives
  $467–$1,068. You may prefer to state a round number, or state the GPU-hour target
  (≈1,334 GPU-hr) and let it convert however it converts. Stating a *lower* number
  than you need is worse than stating a range.

## Not done, and why

- I did **not** create a GoFundMe. You chose GitHub Sponsors/Open Collective, and
  GoFundMe is framed around personal hardship — a poor fit for research compute.
- I did **not** open a PR against VybFly. Adding fundraising to the science repo is
  a judgment call about how the project presents itself, and that's yours to make.
- I did **not** guess a dollar figure where the data didn't support one; the model
  and its assumptions are stated in `SPONSOR-PITCH.md` so they can be challenged.
