# Zenrows pricing: what the six plans cost, how far 250K credits actually goes, and the billing rules that move your bill (full plan table)

Zenrows publishes six plans. The free one gives you 5,000 credits a month with no card. Paid plans start at **$16/month for 45,000 credits**, and the highest self-serve card on the pricing page is **$458/month for 5,000,000 credits**. Enterprise is quoted on committed volume.

Those credit numbers only become useful once you know the exchange rate, because Zenrows prices by request type rather than by page: a standard page costs 1 credit, JavaScript rendering costs 5, premium proxies cost 10, and both together cost 25. A plan advertised as 250K credits is either 250,000 pages or 10,000 pages depending on which of those you're actually scraping. Everything below works from that multiplier, including the per-1,000-page costs, the plan ladder the pricing page doesn't display, and the rollover and upgrade rules that decide whether your plan survives a busy month.

> **Quick pick:** Launch ($58/mo, 250,000 credits, 50 concurrent requests) is the tier most teams land on, because it's the first one with chat support and enough headroom for a job that runs daily. Skip it if your targets need JavaScript plus premium proxies: 250,000 credits is then only 10,000 pages, and Build's 1,800 protected pages at $8.89 per 1,000 is expensive at any volume. If your mix is mostly protected pages, price the same volume somewhere else before you commit: 👉 [check ScraperAPI's current plans and pricing](https://www.scraperapi.com/?fp_ref=coupons).

## All six Zenrows plans, with the cost per 1,000 pages worked out

The last two columns are the ones that make the tiers comparable. They're calculated from the published monthly price and the 1-credit and 25-credit request weights, so you can see what a page actually costs at each tier instead of comparing credit totals.

| Plan | Price (USD/mo) | Credits/mo | Concurrent requests | Per 1,000 standard pages | Per 1,000 protected pages |
| --- | --- | --- | --- | --- | --- |
| Free | $0 | 5,000 | 5 | $0 | $0 |
| Build | $16 | 45,000 | 20 | $0.36 | $8.89 |
| Launch | $58 | 250,000 | 50 | $0.23 | $5.80 |
| Growth | $166 | 1,200,000 | 100 | $0.14 | $3.46 |
| Scale | $458 | 5,000,000 | 200 to 400 | $0.092 | $2.29 |
| Enterprise | Custom | Above 45M | 500 to 1,000+ | Quoted | Quoted |

All prices are USD on monthly billing, taken from the Zenrows pricing page. The per-1,000 figures are arithmetic, not published by Zenrows.

Support and access scale with the price: community support on Free, email on Build, chat on Launch, priority support from Growth up, and a dedicated account manager plus SLA, SOC 2, ISO 27001 and a DPA on Enterprise. The product set does not scale. Every plan, including Free, carries Fetch, Extract, Crawl, Batch and Browser over the API, SDK, CLI and MCP server, drawn from one shared balance.

## What a credit buys, and what your plan's credits turn into

The multiplier is identical on every tier, so upgrading never changes what a request costs. It only changes how many requests fit.

| Request type | Credits per request | Pages on 45,000 (Build) | Pages on 250,000 (Launch) | Pages on 5,000,000 (Scale) |
| --- | --- | --- | --- | --- |
| Standard page | 1 | 45,000 | 250,000 | 5,000,000 |
| JavaScript rendering | 5 | 9,000 | 50,000 | 1,000,000 |
| Premium proxies | 10 | 4,500 | 25,000 | 500,000 |
| JS + premium (protected) | 25 | 1,800 | 10,000 | 200,000 |

Two other products spend from the same balance at their own rates. Standalone Residential Proxies cost 25,000 credits per GB, which is not available on Free and bills at legacy rates (roughly 18,000 to 54,000 credits per GB) on older plans. The Browser costs 25,000 credits per GB of bandwidth plus 5 credits per minute of session time.

Zenrows' own rule of thumb ties those units together neatly: **1 GB = 25,000 credits = 1,000 protected pages**. So 25,000 credits is 1,000 protected pages, or 1 GB of residential bandwidth, or 5,000 minutes (about 83 hours) of browser session time before bandwidth is counted. On Launch, that bundle represents a tenth of the monthly allowance.

One distinction that catches people: `premium_proxy=true` on a Fetch request routes through a residential IP but bills as a Fetch request at 10 credits, not by bandwidth. Only the standalone Residential Proxies product in the dashboard meters gigabytes.

## Six plan names, sixteen price points

The pricing page shows one card per tier. The internal plan ladder shows more rungs underneath, and this is where the biggest gap between comparison articles and reality sits.

Build runs at 45,000, 80,000 and 120,000 credits (B1 to B3). Launch runs at 250,000, 500,000 and 700,000. Growth runs at 1.2M, 2M and 3M. Scale goes from 5M to 8M, 12.5M, 28M and finally 45M credits at **$2,999/month**. The Scale $458 shown on the pricing page is the starting configuration of that tier, not its ceiling.

Concurrency rises inside Scale too: 200 on S1 through S3, 300 on S4, 400 on S5. Enterprise takes over above 45M credits a month at 500 to 1,000+ concurrent requests.

Two things you cannot buy at any price: extra concurrency on its own, or a cheaper plan limited to a single product. Zenrows states plainly that every plan includes every product and every interface, with limits set by the tier you choose.

A caution before you pick a rung. The documentation's ladder prices some allowances differently from the public pricing page, listing $19 for the 45,000-credit rung and $69 for the 250,000-credit rung, against $16 and $58 on the pricing page cards. Confirm the number your account will actually be charged in the Plans screen before checkout.

## The billing rules that decide your real bill

**You're billed for successful requests only.** Failed attempts and retries don't draw credits. A 404 or 410 counts as a result, because the request completed and returned a real answer. Batch is the exception: it records a 404/410 task as failed but still bills it.

**Crawl has no fee of its own, but it isn't free.** Every page a crawl opens bills as a Fetch request with Adaptive Stealth Mode, at 1 to 25 credits per page depending on the target site. `max_pages` is therefore your cost ceiling as well as your scope limit.

**Extract is currently free on top of the Fetch request it uses.** That's Zenrows' own wording, "currently", so don't build a multi-year budget on it staying that way.

**Response size is capped per request,** covering the whole body whether it's HTML, JSON or a screenshot. Over the cap you get HTTP 413 (RESP005) and no data is delivered, though the request still counts as a success in the billing logic. The cap is set per plan, and the exact megabyte limit is worth checking against your heaviest pages before you commit to a tier.

**Failed payments and pending invoices pause everything,** including plan changes, until the invoice is settled.

## Top-ups, rollover and upgrades: the parts that surprise people

Credits included in your plan do not roll over. They refresh each cycle, and whatever is left at renewal is gone.

Top-ups behave slightly better. You can buy up to 10 in a billing period, each rung has exactly one pack size, and your account can only buy the pack tied to your own rung. Unused top-up credits roll into the next period once, then expire.

Upgrades take effect immediately. Unused credits from your current plan, including base credits, top-ups and anything granted by an admin, carry into the new plan as bonus credits on top of the new allowance. That carry happens once; the bonus doesn't roll again at the following renewal, and nothing carries when you move off Free. Zenrows' worked example: Launch L1 at 250,000 credits with 90,000 left, upgraded to Launch L3 at 700,000, starts the new cycle at **790,000 credits**.

Downgrades land at the end of the current cycle. Unused plan credits expire, unused top-up credits roll once. No penalties, no hidden fees, and no refund of what you didn't use.

Usage warnings fire at 80% and 95% if you enable them in notification settings, and you can turn on automatic top-up purchases with a threshold.

## Annual billing is a 17% discount with one catch

Paying yearly gives you two months free, meaning you pay for 10 and get 12. The credits arrive as one annual balance up front, not as twelve monthly grants. On annual plans the 10-top-up limit and the rollover rule apply per year, and unused plan credits expire at the yearly renewal.

Zenrows doesn't publish an annual monthly-equivalent, so here's the arithmetic on the listed prices:

| Plan | Monthly billing, 12 months | Annual (pay 10, get 12) | Saved |
| --- | --- | --- | --- |
| Build | $192 | About $160 | $32 |
| Launch | $696 | About $580 | $116 |
| Growth | $1,992 | About $1,660 | $332 |
| Scale | $5,496 | About $4,580 | $916 |

The catch is the delivery model. The whole year of credits sits in your balance on day one, so the monthly refresh that normally caps your spending disappears. Burn through it by March and nothing refills until renewal, which means buying top-ups on top of a prepaid year. Test on a monthly plan first: 👉 [see ScraperAPI's plan options before you prepay a year](https://www.scraperapi.com/?fp_ref=coupons).

You can switch between monthly and yearly yourself in the Plans screen, and the confirmation page shows the new price and when it takes effect.

## Free plan, free trial, refunds

The Free plan is the trial. It gives you 5,000 credits a month with no card, everything unlocked except standalone Residential Proxies, 5 concurrent requests, community support, no rollover and no top-ups.

There is no separate free trial. G2 states that Zenrows doesn't offer one, and Capterra's comparison table marks free trial as not available.

Refunds are the weaker spot. Neither the pricing page nor the billing documentation publishes a refund or cancellation-refund policy, so there's no documented route to getting a month back if the site you're targeting turns out to be harder than expected. That's an argument for a month-to-month start over an annual prepay, whatever the 17% discount looks like.

## Payment methods, and the more expensive agent route

A Zenrows account takes credit cards (Visa, MasterCard, American Express and others), Apple Pay, Google Pay and PayPal. Enterprise customers can pay by wire transfer. Crypto and debit cards are not accepted on an account.

AI agents get a separate storefront where Fetch and Extract can be bought with no account and no API key, paying by card, USDC over x402 or MPP. That route costs **$0.50 per 1,000 credits with a 10,000-credit minimum ($5)**, and the plans it sells cover Fetch and Extract only. Compare that to $0.23 per 1,000 credits on Launch and $0.092 on Scale. The storefront is convenient for a one-off agent job and roughly twice the price of a subscription for anything recurring.

## What buyers actually say

G2's pricing page lists six editions starting at $0 and shows a 5.0/5 rating without a review count on that page. Capterra rates Zenrows 4.7 from 103 reviews with a value-for-money score of 4.4.

The Capterra review excerpts split along the same line the pricing does. One data analyst writes "For me the best is the price." A co-founder raises "a few concerns about scalability in terms of pricing," and a VP of products says "It has a lot of functionality, but its high fees and complexity of configuration were a problem for us."

Both directories are showing older price snapshots: G2 and Capterra list Launch, Growth and Scale at $57, $165 and $456 against $58, $166 and $458 on the current pricing page. Treat the pricing page as the checkout figure.

## When Zenrows pricing stops making sense

Three situations where the credit model works against you.

**Almost everything you scrape is protected.** At 25 credits a page, Build delivers 1,800 pages for $16, and even Scale only gets to $2.29 per 1,000. Run that number against your monthly page volume before you look at concurrency.

**You need one product and nothing else.** There's no discounted Fetch-only or Crawl-only plan. You're paying for Browse, Batch, Browser and the rest whether you use them or not.

**You need heavy standalone residential bandwidth.** At 25,000 credits per GB, a terabyte of proxy traffic would cost 25 million credits, which is more than the entire S5 allowance. Buy that from a dedicated proxy provider instead.

If any of those describes your workload, price the same volume with a second vendor before you pick a rung. 👉 [Compare ScraperAPI's plans at your page volume](https://www.scraperapi.com/?fp_ref=coupons).

## FAQ

**Is there a Zenrows coupon code?**
No promo code shows up on the pricing page or in the billing documentation. The only discount Zenrows documents is the annual one: pay for 10 months, get 12.

**What happens when I hit the monthly limit?**
On a paid plan, buy a top-up (up to 10 per billing period) or wait for the refresh. On Free there are no top-ups, so you wait or upgrade. Configuration and data aren't lost either way.

**Can I buy more concurrency?**
No. Concurrency is tied to the tier and the rung, from 5 on Free to 400 on Scale S5 and 500 to 1,000+ on Enterprise.

**Does a 404 burn credits?**
It counts as a successful request, because the server returned a real answer. Failures and retries genuinely don't bill, except 404/410 tasks inside Batch, which are logged as failed and still charged.

**Can I downgrade if I overshoot?**
Yes, effective at the end of the current cycle. Unused plan credits expire and top-up credits roll once. Open invoices block the change.

## Picking a plan without overpaying

Match the tier to your worst month, not your average one, because the rollover rules won't carry the slack for you.

- Testing an idea, under 5,000 credits: stay on Free.
- Steady small job, standard pages, one developer: Build at $16.
- Daily production runs and you want chat support: Launch at $58, or the 500K rung if you're already topping up twice a month.
- 100 concurrent requests or a team sharing the balance: Growth at $166. Above that, the Scale ladder runs to 45M credits at $2,999.
- Mostly protected pages, or a single-product workload: the credit math is against you, and a second quote is the cheaper move.

Three things to confirm before you pay anything. Check the response size cap against your heaviest pages, because a 413 delivers nothing and still counts. Confirm which price your chosen rung actually carries in the Plans screen, given the discrepancy between the ladder and the pricing cards. And start monthly if you're unsure, since no refund policy is published.

When you're ready to compare a second option at the same volume, 👉 [get ScraperAPI's current pricing here](https://www.scraperapi.com/?fp_ref=coupons).
