# Site manual — Zi Ze (Kevin) Lin

**Live at: https://kevinzizelin.github.io**
Repo: `github.com/kevinzizelin/kevinzizelin.github.io`

Plain HTML. No build step, no framework, no dependencies. You edit a file, you upload it,
it's live. Nothing in here can break, which is why sites built this way last twenty years.

```
index.html          the homepage — the list of memos lives here
about.html          who you are
disclaimer.html     the legal boilerplate
style.css           every visual choice, in one short file
feed.xml            RSS, so people can subscribe
memos/              one HTML file per memo
```

To preview changes before uploading, open a terminal in this folder and run
`python3 -m http.server`, then visit `localhost:8000`. (Double-clicking `index.html` sort
of works, but links starting with `/` won't resolve outside a real server.)

---

## 1. Publishing a memo

1. Copy `memos/2026-07-31-cascade-bearing.html` to a new file named
   `YYYY-MM-DD-company-name.html`. Dated filenames sort themselves and stay unambiguous.
   **Keep it inside the `memos` folder** — the homepage links expect it there.
2. Write the memo.
3. Add an entry to the `<ul class="memos">` list in `index.html`, newest at the top.
4. Add a matching `<item>` block to `feed.xml`, newest at the top.
5. Upload the changed files to GitHub: open the repo → **Add file → Upload files** → drag
   them in → **Commit changes**. Live in about a minute.

To upload into the `memos` folder, click into that folder first, *then* Upload files.

Steps 3 and 4 are manual, and after fifteen or twenty memos that gets old. When it does,
say the word and I'll set up a static site generator that builds the index and feed
automatically. Not worth the complexity before then.

**Delete the sample memo** once you have a real one. It's a fictional company with invented
numbers, kept only as a formatting template. Remove `memos/2026-07-31-cascade-bearing.html`,
its entry in `index.html`, its `<item>` in `feed.xml`, and the `.sample` rule in `style.css`.

---

## 2. Adding linzize.com (~$10/year)

The site already works at `kevinzizelin.github.io`. A custom domain is optional but worth
it — it reads as serious, and if you ever change hosts your links don't break.

**Buy at Cloudflare Registrar** — sells at cost, about **$10.44/year** for a `.com`, no
first-year-cheap-then-triple pricing, free WHOIS privacy. Namecheap is a fine alternative.
As of July 2026 `linzize.com` appeared unregistered; confirm at checkout.

Once you own it, in **Cloudflare → your domain → DNS**, add:

**Four A records**, name `@`, pointing to:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**One CNAME record**, name `www`, pointing to `kevinzizelin.github.io`

> **Important:** set all five to **DNS only** (click the orange cloud so it turns grey).
> If they're proxied, GitHub can't issue your HTTPS certificate and visitors get a
> security warning. You can enable the proxy later once HTTPS is working.

Then in the repo: **Settings → Pages → Custom domain**, type `linzize.com`, **Save**. Wait
for the DNS check to pass, then tick **Enforce HTTPS**. Usually lands within an hour,
occasionally up to 24.

`feed.xml` already points at `https://linzize.com/` — so RSS links will only be correct
once the domain is connected. If you decide against the domain, change those three URLs in
`feed.xml` to `https://kevinzizelin.github.io/`.

---

## 3. Email distribution (later)

RSS is dying and most readers won't use it. If you want people to actually receive your
memos:

- **Buttondown** — free under 100 subscribers, plain-text look that matches this site, and
  you own your list. The natural fit.
- **Substack** — free, bigger built-in audience, but it brands your work and makes it
  harder to move later.

Common setup for investment writers: memos live permanently on your own site, email goes
out as a short note with a link. Site is the archive, email is distribution.

---

## Three things worth thinking about

**Timestamps are your credibility.** The value of a memo archive is that it's an unedited
public record of your thinking, including the calls that went wrong. Resist the temptation
to quietly revise. If you update a memo, add a dated note at the bottom saying what changed
and why. GitHub keeps every version permanently, which is the point.

**Be careful with tickers and disclosures.** A memo naming a real ticker, stating a price,
and saying "I own shares" is a public claim about a real security. Make sure each of those
is true before it goes up. Check that any ticker you use belongs to the company you think
it does — `CBRG`, used in the original sample, turned out to be a live NASDAQ listing.

**The disclaimer page is a starting point, not legal advice.** If you ever manage outside
money, or become registered or licensed anywhere, have a securities lawyer read it. The
rules on public commentary about securities are stricter than most people expect.
