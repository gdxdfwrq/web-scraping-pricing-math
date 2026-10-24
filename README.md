# web scraping services provider: how to choose the right one without overpaying, with full plan prices and real credit math

Searching for a web scraping services provider usually means one of two things: you want someone to hand you clean data, or you want an API that quietly handles proxies, CAPTCHAs, and JavaScript rendering while you keep building your product. Those are different purchases at very different price points, and the fastest way to waste budget is to buy the wrong category. This guide breaks the market into its three real categories, then goes deep on one of the most popular scraping APIs — ScraperAPI — with its current plan lineup, the credit math most articles skip, and the limitations that only show up when you read the fine print.

## Quick picks

> **Most developers and small teams**: ScraperAPI's **Business plan ($299/month, 3M credits, 100 concurrent threads)** is the value inflection point — $269.10/month on annual billing. **Just validating an idea**: start with the free trial (5,000 credits over 7 days, no credit card required). **Over 500K requests/month with existing infrastructure**: raw residential proxies from a provider like Bright Data or Smartproxy will likely cost less than any scraping API.
>
> 👉 [Start the free ScraperAPI trial — 5,000 credits, no credit card](https://www.scraperapi.com/?fp_ref=coupons)

## The three types of web scraping services provider

This is the question to answer first, because "web scraping service" describes at least three different products, and they compete on completely different axes.

**Managed scraping APIs.** ScraperAPI is the clearest example. You send a URL with your API key, and you get HTML or structured JSON back. Proxy rotation, CAPTCHA solving, retries, and optional headless-browser rendering all happen on their side. Your maintenance burden is essentially zero — no proxy lists, no CAPTCHA-solving service to wire up, no retry queue to babysit. Founded in 2017 and headquartered in New York, ScraperAPI advertises a pool of 40M+ IPs covering residential, datacenter, and mobile networks across 50+ countries.

**Fully managed data services (DaaS).** Companies like DataOx, Grepsr, and PromptCloud operate on a "you describe it, we build and run it" model. They write the scrapers, run the pipelines, validate every record against an agreed schema, and deliver cleaned data on your schedule. Third-party roundups put these engagements at roughly **$500+ per site per month**. This fits companies with no developers and long-term, stable data needs.

**Visual scraping platforms.** Octoparse lets non-technical users build extraction tasks in a GUI. Its published pricing runs from a free tier (10 tasks, local only) to Standard at $119/month and Professional at $299/month. Fine for small, low-complexity jobs; awkward at API scale.

If your targets are e-commerce or search sites and someone on your team can write code, the API category is almost always the fastest path from "I need this data" to "I have this data." The rest of this article focuses there.

## ScraperAPI's full plan lineup and pricing

Here is the complete plan table currently shown on ScraperAPI's official pricing page. Monthly price is the baseline; paying annually up front takes a flat 10% off.

| Plan | Monthly price | Annual price/mo | API credits | Concurrent threads | Geo-targeting |
| --- | --- | --- | --- | --- | --- |
| Free trial | $0 (7 days, no credit card) | — | 5,000 | — | — |
| Hobby | $49 | $44.10 | 100,000 | 20 | US & EU only |
| Startup | $149 | $134.10 | 1,000,000 | 50 | US & EU only |
| Business | $299 | $269.10 | 3,000,000 | 100 | Country-level |
| Scaling | $475 | $427.50 | 5,000,000 | 200 | Country-level |
| Professional | $975 | $877.50 | 10,500,000 | 300 | Global |
| Advanced | $1,975 | $1,777.50 | 21,500,000 | 500 | Global |
| Enterprise | Custom | Custom | 22,000,000+ | 500+ | Global |

Every paid plan includes the same core feature set: JS rendering, premium residential and mobile IPs, CAPTCHA and anti-bot handling, automatic retries, custom session support, desktop/mobile user agents, unlimited bandwidth, and a 99.9% uptime guarantee. Higher tiers add things like priority support, a dedicated support team, and Slack support. Signing up also grants a standing 1,000 free credits (max 5 concurrent connections) you can keep using for small tests even before paying anything.

👉 [Check current plan prices on ScraperAPI's pricing page](https://www.scraperapi.com/pricing?fp_ref=coupons)

One honest note on plans: Hobby and Startup only get email/ticket support — no live chat or phone. That's rarely a dealbreaker for solo developers, but if your scraping job is revenue-critical, factor it in.

## Credits are not 1:1 — the cost math most reviews gloss over

ScraperAPI charges in credits, and "one request = one credit" only holds for the simplest possible case. The official documentation lays out the real consumption model:

| Request type | Credits per request |
| --- | --- |
| Normal domain, no extras | 1 |
| E-commerce (Amazon, Walmart, eBay) | 5 |
| SERP (Google, Bing, including all subdomains) | 25 |
| Social (LinkedIn) | 30 |
| JS rendering (`render=true`) | +10 |
| Premium proxy (`premium=true`) | +10 |
| Premium + rendering together | 25 |
| Ultra premium proxy (`ultra_premium=true`) | +30 |
| Cloudflare, Datadome, PerimeterX, or Akamai bypass | +10 each time |

Run the numbers on a realistic job and the gap between headline and actual cost gets big fast. Scraping Amazon search pages with JS rendering on: 5 + 10 = 15 credits per page. Google SERPs with rendering: 35 credits. One reviewer's calculation on the Startup plan — 1,000,000 credits looks like a million pages on paper, but against a protected target needing `render=true` plus `premium=true`, it might only cover 40,000–100,000 actual pages. Budget against your real per-page cost, not the credit count on the pricing page.

There's a documented quote from one independent review that captures this well: *"The credit system punishes exactly the jobs people sign up for."* Harsh, but the counterpoint is that ScraperAPI gives you the tools to see the damage before it happens:

- The **Domain Cost Estimator** in your dashboard returns the exact credit cost for any URL before you start scraping.
- A public endpoint (`api.scraperapi.com/account/urlcost`) does the same thing programmatically, with full parameter support.
- Every response includes a `sa-credit-cost` header showing what that request actually consumed.
- You can set `max_cost` per scrape to cap any single request.

Meanwhile, several parameters cost nothing extra: `country_code`, `session_number`, `device_type`, `autoparse`, `wait_for_selector`, and others. If your targets aren't behind heavy protection like Cloudflare's bot management or Akamai, the default pool usually clears requests without ever touching the expensive premium tier.

👉 [Test your target URLs with the free trial before committing](https://www.scraperapi.com/signup?fp_ref=coupons)

## Real annual cost: monthly vs. annual billing

Annual billing saves exactly 10% across every tier, so the absolute savings scale with plan size:

- **Hobby**: $588/year monthly vs. $529.20 — saves $58.80
- **Startup**: $1,788 vs. $1,609.20 — saves $178.80
- **Business**: $3,588 vs. $3,229.20 — saves $359
- **Scaling**: $5,700 vs. $5,130 — saves $570
- **Professional**: $11,700 vs. $10,530 — saves $1,170

Two overage mechanics are worth knowing before you pick a plan, because they change what "running out" means:

1. **Default behavior**: scraping pauses until your credits renew next cycle. No surprise overage bills.
2. **Opt-in continuation**: Hobby through Professional support **auto-upgrade** — when credits run out, the account automatically moves to the next plan. Scaling and above support **pay-as-you-go**, letting you keep scraping at a fixed per-credit rate up to a monthly spending cap you set yourself.

If your volume swings seasonally (e-commerce holiday peaks, for instance), auto-upgrade beats pre-buying a bigger plan you'll only need two months a year.

## What you're actually paying for: billing fairness and success rates

ScraperAPI only bills requests that return a 200 or 404 status code, plus requests you cancel yourself before their 70-second completion window closes. Blocked requests, timeouts, and internal failures cost nothing. Their documentation states it plainly: "We only charge for successful requests."

Independent testing backs up the underlying reliability. A reviewer who ran 50,000+ requests against Google, Amazon, Zillow, and various e-commerce sites in early 2026 reported a **99.0% success rate**, and separately noted: "Failed requests don't cost credits — you're paying for results, not attempts." Other third-party measurements put average success somewhere between 92% and 99% depending on target difficulty. Whatever the exact number, the combination of "you don't pay for failures" and a mid-90s-plus success rate means your effective per-result cost sits much closer to the headline price than it does with services that bill every attempt.

## The limits that decide whether this fits your project

Concurrency is tiered and enforced: 20 threads on Hobby, 50 on Startup, 100 on Business, 200 on Scaling, 300 on Professional, 500 on Advanced. Exceed your limit and requests come back with a 429 — rejected outright, not queued, and not billed. Your client code needs to back off and retry.

Beyond concurrency, a few constraints don't show up in any pricing comparison table:

- **Latency**: the API adds roughly 2–5 seconds per request. Fine for batch jobs; disqualifying for anything latency-sensitive.
- **Session persistence caps out around one hour**. A `session_number` keeps the same IP for consecutive requests within that window, but ad verification or long-running account workflows that need multi-day sticky IPs need a different kind of provider entirely.
- **No IP-level control**. Everything runs through a single endpoint; there's no dashboard for picking specific IPs or ASNs, and the proxy port mode (`proxy-server.scraperapi.com:8001`) doesn't support the full feature set.
- **Async mode batches up to 10,000 URLs** per submission — great for large jobs where you don't need real-time results.
- **No websockets or real-time streaming**.

The bigger architectural limitation: if you're running Playwright or Puppeteer with custom fingerprinting, an API-based service constrains you by design. And for accounts-and-automation use cases, a scraping API is simply the wrong tool — it's built for pulling data off the open web.

## Where ScraperAPI sits against the alternatives

One comparison worth making before you commit, using only verified figures:

| Category | Example | Pricing model | Best for |
| --- | --- | --- | --- |
| Managed scraping API | ScraperAPI | Credits, from $49/mo | Developers, 20K–500K pages/mo, protected targets |
| Full DaaS | DataOx, Grepsr | Custom, ~$500+/site/mo | Non-technical buyers, ongoing pipelines |
| Visual platform | Octoparse | $0–$299/mo published | Non-coders, small jobs |
| Raw residential proxies | Bright Data, Smartproxy | By bandwidth | 500K+ req/mo, existing infrastructure |

Bright Data operates the largest proxy network in the space — 72M+ residential IPs — and offers city-level geotargeting, where ScraperAPI tops out at country-level routing on Business and above. If city-level precision is a hard requirement, that's a real gap. But raw proxies come with their own bill: you own the rotation logic, the CAPTCHA-solving integration, and every failed request yourself. One reviewer's break-even estimate: below 500K requests/month, ScraperAPI is probably cheaper once you count development time and CAPTCHA costs; above that line with infrastructure already built, raw residential proxies win on cost.

The structured data endpoints deserve a mention here because they're a genuine differentiator in the API category: for Amazon product and search pages, Google Search and Shopping, and Walmart, ScraperAPI returns parsed JSON with titles, prices, reviews, and ratings — no HTML parsing to build or maintain when the target site redesigns.

👉 [Compare plans and structured data endpoints on ScraperAPI](https://www.scraperapi.com/pricing?fp_ref=coupons)

## FAQ

**How much does a web scraping API actually cost per month?** For a managed API like ScraperAPI, plans run from $49/month (100,000 credits, Hobby) to $1,975/month (21.5M credits, Advanced), with a custom-priced Enterprise tier above that. Annual billing takes 10% off every tier.

**Is there a free trial?** Yes. ScraperAPI offers a 7-day trial with 5,000 credits and no credit card required, plus a standing 1,000 free credits on every registered account (max 5 concurrent connections).

**Does ScraperAPI work with Google and Amazon?** Yes, and these are priced as premium domains: Amazon, Walmart, and eBay cost 5 credits per request, Google and Bing (including subdomains) cost 25, and LinkedIn 30. Structured data endpoints for Amazon, Google, and Walmart return parsed JSON directly.

**What happens if I run out of credits mid-month?** By default, scraping pauses until your next billing cycle. You can opt into auto-upgrade (Hobby through Professional), which bumps you to the next plan automatically, or pay-as-you-go on Scaling and above, which continues billing at a fixed per-credit rate up to a cap you set.

**Do failed requests cost credits?** No. Only requests returning 200 or 404 are billed, along with requests you cancel within the 70-second completion window. Timeouts and blocked attempts are free.

## Final call: which route matches your situation

- **Solo dev or small team, 20K–500K pages/month, standard e-commerce or SERP targets** → ScraperAPI Business at $299/month (or Hobby at $49 to start lean). Validate first with the free trial.
- **Mostly plain static pages, tiny volume** → The standing 1,000 free credits might genuinely be all you need. Don't buy a plan until you've exhausted them.
- **Heavy targets like LinkedIn or Instagram at volume** → The ultra-premium multiplier makes a scraping API expensive here; a bandwidth-billed residential proxy plan fits better.
- **Need multi-day sticky IPs for ad verification or account workflows** → Look at dedicated residential or mobile providers instead; a scraping API's one-hour session limit will fight you the whole way.
- **No developers on the team, ongoing data pipeline** → A DaaS provider in the $500+/site/month range is the appropriate buy, even though it costs more.

Before you click purchase on any of these, do one thing: run a handful of your real target URLs through the cost estimator, multiply by your monthly volume, and compare that number to the plan price. It takes five minutes and it's the difference between the sticker price and what you'll actually pay.

👉 [Start your free ScraperAPI trial — 5,000 credits, no credit card](https://www.scraperapi.com/signup?fp_ref=coupons)
