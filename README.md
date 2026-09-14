# Home Base — the @unwelcomedata front door

This is the one site that's **yours**. Not a per-project Pages site — the single
place a stranger who liked one chart can go to find everything else and subscribe.
Every post you ever make points back here.

It's a single self-contained `index.html` (no build step, no framework). Edit it
by hand, commit, push. That's the whole workflow.

---

## What it does

- Introduces `@unwelcomedata` and the mission in one screen.
- Links all live project Pages sites (the "projects" grid).
- Captures email — the **only** audience channel no platform can take from you.
- States the principles (public data, sources cited, methodology shown).

When you publish a new project, add one `<a class="card">` block to the grid in
`index.html`. That's the only maintenance.

---

## Deploy it (pick one)

Both use GitHub Pages, both are free, both keep the identity clean (no real name).

### Option A — the profile repo (recommended, doubles as your GitHub landing page)

A repo named exactly `unwelcomedata` renders its README as your GitHub profile
page, AND a repo named `unwelcomedata.github.io` serves as your root user site at
`https://unwelcomedata.github.io/`. Use the root user site for this:

```bash
# create the root user-site repo (public — it's a public landing page)
gh repo create unwelcomedata/unwelcomedata.github.io --public

# from this home-base/ folder:
git init
git add index.html README.md
git commit -m "feat: home base landing site"
git branch -M main
git remote add origin https://github.com/unwelcomedata/unwelcomedata.github.io.git
git push -u origin main

# enable Pages from main / root
gh api -X POST repos/unwelcomedata/unwelcomedata.github.io/pages \
  -f 'source[branch]=main' -f 'source[path]=/'
```

Live at **https://unwelcomedata.github.io/** in ~1–2 minutes. This becomes the URL
you put in every social bio and every post.

### Option B — a normal project repo

If you'd rather not use the root user site yet:

```bash
gh repo create unwelcomedata/home-base --public
# ...push index.html... then enable Pages
```

Live at `https://unwelcomedata.github.io/home-base/`. Fine, but the root URL in
Option A is cleaner for a bio link.

> Identity check before pushing: `git config user.name` should be `unwelcomedata`
> and `user.email` the noreply address. Same rule as every other repo.

---

## Email — deliberately deferred (not a TODO for now)

**Decision (owner):** no email list yet. Rationale: an empty list you never mail
leaves a bad first impression on early subscribers, and the priority is getting
comfortable with **one** new thing (posting) before adding another. The site ships
with a **"Follow along"** button instead of a signup form — nothing to sign up for,
nothing to unsubscribe from.

`unwelcomedata@proton.me` is a **mailbox**, not a list tool — it can't collect or
broadcast to subscribers on its own. When a newsletter *is* wanted later, that
Proton address is what you register the list provider with (and send "from"), so
the identity stays clean.

**When you're ready to add email later** (only once posting is a comfortable habit):

| Provider | Free tier | Why it fits |
| --- | --- | --- |
| **Buttondown** | ~100 subscribers free | Indie, privacy-friendly, dead simple. Best fit for "low-key." |
| **MailerLite** | ~1,000 subscribers free | More features, still simple, generous free tier. |

Steps at that point: register with `unwelcomedata@proton.me`, grab the provider's
form endpoint, swap the "Follow along" button back to a `<form action="...">`, test
by subscribing yourself. Not before you'll actually send something.

## Point the "Follow along" button at your real channel

The button currently links to the GitHub profile as a placeholder. Once your social
channel is live (Bluesky is the planned first channel), update the `href` on the
`.follow-btn` in `index.html` to that profile URL. That's the one edit the site
needs before it's fully wired for the posting habit.

---

## What NOT to do here

- Don't add analytics that phone home with personal data, or anything that leaks
  identity. Keep it clean.
- Don't turn this into a big framework/site-generator project — that's the "build
  instead of ship" trap. It's one HTML file on purpose.
- Don't wait for it to be perfect to deploy. A live plain site beats a perfect
  local one.
