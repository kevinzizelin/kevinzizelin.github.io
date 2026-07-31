# linzize.com — site manual

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

Setup is done — your name, email, and domain are already filled in everywhere.

To preview locally, open a terminal in this folder and run `python3 -m http.server`, then
visit `localhost:8000`. (Double-clicking `index.html` sort of works, but links that start
with `/` won't resolve until the site is on a real server.)

---

## 1. Put it online (about 15 minutes, free)

**GitHub Pages.** Free forever, custom domains, automatic HTTPS, and every version of every
memo is saved permanently. That last part matters more than you'd think when you publish
dated opinions about securities — nobody can accuse you of quietly editing a call after the
fact when there's a public timestamped history.

1. Make an account at **github.com**. Whatever username you pick becomes part of your URL,
   so choose something you're happy to be seen — `linzize` if it's free.
2. Click **+** (top right) → **New repository**.
3. Name it exactly `YOURUSERNAME.github.io`, using the username from step 1. So if your
   username is `linzize`, the repo is `linzize.github.io`. This exact naming is what tells
   GitHub to treat it as your personal site. Set it to **Public**. Click **Create**.
4. On the empty repo page, click **uploading an existing file**. Drag in everything from
   this folder — all four HTML/CSS/XML files *and* the `memos` folder. Then **Commit changes**.
5. **Settings** → **Pages** (left sidebar) → under Source pick **Deploy from a branch**,
   branch **main**, folder **/ (root)** → **Save**.
6. Wait about a minute, then visit `https://YOURUSERNAME.github.io`. That's your site.

Check every page and link before moving on. If something looks unstyled, you probably
missed `style.css` in the upload.

---

## 2. Point linzize.com at it (~$10/year)

Worth doing. `linzize.com` reads as serious in a way `linzize.github.io` doesn't, and if you
ever change hosts your links don't break.

**Buy it at Cloudflare Registrar** — they sell at cost, currently about **$10.44/year** for
a `.com`, with no first-year-cheap-then-triple pricing and free WHOIS privacy. Namecheap is
a fine alternative. As of today `linzize.com` appears unregistered, but confirm at checkout.

Once you own it, in **Cloudflare → your domain → DNS**, add these records:

**Four A records**, name `@`, pointing to:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**One CNAME record**, name `www`, pointing to `YOURUSERNAME.github.io`

> **Cloudflare-specific:** set all five records to **DNS only** (click the orange cloud so
> it turns grey). If they're proxied, GitHub can't issue your HTTPS certificate and you'll
> get a certificate error. You can turn the proxy on later once HTTPS is working.

Then back in GitHub: **Settings → Pages → Custom domain**, type `linzize.com`, **Save**.
Wait for the DNS check to pass, then tick **Enforce HTTPS**. DNS usually lands within an
hour, occasionally up to 24.

---

## 3. Publishing a memo

1. Copy `memos/2026-07-31-cascade-bearing.html` to a new file named
   `YYYY-MM-DD-company-name.html`. Dated filenames sort themselves and stay unambiguous.
2. Write the memo.
3. Add an entry to the `<ul class="memos">` list in `index.html`, newest at the top.
4. Add a matching `<item>` block to `feed.xml`, newest at the top.
5. Upload the changed files to GitHub. Live in about a minute.

Steps 3 and 4 are manual, and after fifteen or twenty memos that gets old. When it does,
say the word and I'll set up a static site generator that builds the index and feed
automatically. Not worth the complexity before then.

---

## 4. Email distribution (later)

RSS is dying and most readers won't use it. If you want people to actually receive your
memos:

- **Buttondown** — free under 100 subscribers, plain-text look that matches this site, and
  you own your list. The natural fit.
- **Substack** — free, bigger built-in audience, but it brands your work and makes it
  harder to move later.

The common setup for investment writers: memos live permanently on your own site, email
goes out as a short note with a link. Site is the archive, email is distribution.

---

## Two things worth thinking about

**Timestamps are your credibility.** The value of a memo archive is that it's an unedited
public record of your thinking, including the calls that went wrong. Resist the temptation
to quietly revise. If you update a memo, add a dated note at the bottom saying what changed
and why.

**Be careful with tickers and disclosures.** A memo that names a real ticker, states a
price, and says "I own shares" is a public claim about a real security. Make sure each of
those is actually true before it goes up, and delete or clearly label anything that's a
template or an exercise.

**The disclaimer page is a starting point, not legal advice.** If you ever manage outside
money, or become registered or licensed anywhere, have a securities lawyer read it. The
rules on public commentary about securities are stricter than most people expect.
