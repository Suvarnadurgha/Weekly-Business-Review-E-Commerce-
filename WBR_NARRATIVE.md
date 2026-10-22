# Weekly Business Review — week ending 2018-01-28

Olist marketplace, Brazil. All figures traceable to queries in `sql/`.


# Summary

Revenue was R$211.3K in the week ending 28 January 2018, down 5.0% week on
week. The decline was volume, not basket: orders fell 9.7% to 1,566 while
average order value rose 5.2%, so a R$21.5K loss from fewer orders was offset
roughly 54% by an R$11.6K gain from larger ones. That is an unremarkable
post-holiday week and, on its own, would not warrant a review.

The trailing twelve weeks are a different matter. Black Friday drove a 2.3x
demand spike that the fulfilment network could not absorb. On-time delivery
fell 8.9 points in a single week, average delivery time rose by three days, and
review scores dropped 0.33 stars. Recovery took five weeks. The damage was
heavily concentrated: Rio de Janeiro, our second-largest market at 14.1% of
volume, fell 32 points while São Paulo at 38.1% of volume fell only 5. Across
the full history, orders delivered late are 6.7% of volume but account for
roughly a third of every 1–2 star review in the business.

This is a peak-capacity constraint, not a one-off, and it will recur next peak
unless the Rio node is addressed before it.

---

# What moved

Revenue fell R$11.0K week on week. Decomposing that change into its two
drivers — revenue is order count multiplied by average order value — gives a
volume effect of −R$21,540, a basket effect of +R$11,644, and an interaction
term of −R$1,128. The three reconcile to the total change exactly, which is
the check that the decomposition is complete rather than approximately right.

So the week was a volume story. We sold to 168 fewer customers than the week
before, and the customers who did buy spent 5.2% more each, recovering just
over half of what the volume loss cost. Falling orders alongside rising order
value is the signature of marginal buyers dropping out while the higher-intent
core remains — plausible for late January, though this data cannot confirm
the mechanism.

The remaining weekly metrics moved within their normal range and are not
discussed further. On-time delivery at 92.6% was 3.4 points below its early
January level, which is worth watching but is small against the movement
described below.

---

# Root cause

The week ending 26 November 2017 took 2,972 orders against 1,283 the week
before — a 132% increase. In the same week, on-time delivery fell from 91.7%
to 82.7%, average delivery time rose from 13.6 to 16.6 days, and the average
review score fell from 4.13 to 3.81. Every one of those moved in the spike
week itself, not with a lag, which points at immediate capacity saturation
rather than a downstream backlog effect. On-time delivery did not return to
its pre-spike level until the week ending 31 December: five weeks.

The failure was network-wide but very unevenly distributed. Nineteen of
twenty-one states fell below their own nine-week baseline, so the whole network
hit a ceiling. But São Paulo, carrying 38.1% of volume, absorbed the spike with
a 5.2-point decline and delivery times rising only 8.8 to 11.2 days. Rio de
Janeiro, at 14.1% of volume, fell 32.0 points — from 92.9% to 60.9% on-time —
with average delivery time rising from 13.5 to 22.2 days. Weighted by volume,
Rio contributed more than twice São Paulo's share of the network's decline
despite carrying a third of the orders. Rio's baseline was healthy at 92.9%,
so this is a node that broke under load rather than one that was always weak.

That distinction separates two different problems in the same table. States
such as Maranhão, Sergipe and Piauí show the largest percentage-point falls,
but their baselines were already 74–83% with normal delivery times above
nineteen days. Those are structural distribution problems in remote regions,
not peak-capacity failures, and they need a different response. They are also
small: Maranhão's 45.8-point decline rests on 22 orders, and no state below
roughly 25 orders in the spike week is treated as a finding here.

The customer consequence is measurable across the full dataset. Grouping
95,824 reviewed orders by how their delivery compared with the promised date,
the average review score declines at every step from 4.32 stars for orders
arriving eight or more days early to 1.70 stars for those arriving eight or
more days late. The share of 1–2 star reviews rises from 8.9% to 79.2% across
the same range. Late orders are 6.7% of volume and produce approximately 33%
of all 1–2 star reviews.

This is an association measured on observational data, not a controlled
experiment, and remote regions have both later deliveries and plausibly
different expectations. The monotonic gradient across all seven lateness
buckets is difficult to explain by regional confounding alone, which is why
the relationship is treated as real here, but "associated with" remains the
accurate phrase.

One finding inside that curve changes what should be done about it. Moving
from on-time to eight or more days early gains only 0.28 stars, while moving
from on-time to one to three days late costs 0.75 — the penalty for being
slightly late is nearly three times the entire reward for being very early.
Meanwhile 74% of orders already arrive eight or more days early, which means
promised dates are heavily padded and that padding is buying very little.
The business is over-delivering on speed and under-delivering on reliability.

What this data cannot settle is why Rio specifically failed. Carrier identity
is not in the dataset, so seller fulfilment capacity cannot be separated from
carrier performance, and that distinction determines which of the two actions
below is the right one.

---

# Actions

Because this analysis uses historical public data, owners below are stated as
roles rather than named individuals.

The regional fulfilment lead should review Rio de Janeiro's capacity plan
before the next peak period, with the target of holding regional on-time
delivery above 85% through a 2x demand week — Rio's floor this peak was 60.9%.
Success is measured on the on-time rate by state in the spike week itself, not
on the recovery curve afterwards.

Because carrier identity is absent from this data, the first step is
diagnostic rather than corrective: operations should determine whether Rio's
failure originated with seller dispatch or with carrier capacity, since the
two imply different interventions. That answer should be available before
peak-season planning begins, and it should be treated as a blocker on any
capacity commitment made without it.

Separately, the delivery promise itself warrants review. With 74% of orders
arriving eight or more days early and the reward for earliness at 0.28 stars,
the current padding is not earning its cost. Tightening promised dates in
consistently fast regions would improve the customer proposition at no
measurable satisfaction cost, provided the late tail is addressed first —
tightening promises before fixing reliability would convert early deliveries
into late ones and move customers into the buckets that cost 2.6 stars.

---

# What I would measure next, and what this data cannot tell me

Carrier identity is the single most valuable missing field. Without it, Rio's
failure cannot be attributed between seller and carrier, and the recommended
action above is a diagnostic rather than a fix.

Session and traffic data would give a conversion rate and separate a demand
problem from a traffic problem. The January volume decline is currently
undiagnosable for that reason: fewer orders could mean fewer visitors or the
same visitors converting worse, and these are different businesses to run.

Product costs would allow a real margin calculation. Freight as a share of
revenue is used here as the only available cost proxy, and it is a weak one.

Finally, review coverage is incomplete and reviewers are not a random sample
of customers, so every satisfaction figure in this document describes people
who chose to review rather than all buyers. The direction of that bias is
unknown.
