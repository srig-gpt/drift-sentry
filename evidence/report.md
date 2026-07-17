# drift-sentry report

14-day replay. HTTP availability never dropped below 99.983%: **zero uptime alerts**. Flag threshold 0.444 (top 1.5% of reference scores); quality SLO precision >= 0.34.

| injected event | when | caught by | detection | lag |
|---|---|---|---|---|
| data_drift: MX market launch shifts input mix (25% new traffic) | day 6.0 (h144) | PSI:country | day 6.1 (h146) | 2h |
| concept_drift: fraud flips to account-takeover pattern | day 9.0 (h216) | quality-SLO | day 11.7 (h280) | 64h |
| pipeline_bug: schema change zeroes device_age for all traffic | day 12.0 (h288) | PSI:device_age (+1 more) | day 12.1 (h290) | 2h |

## The point

The uptime line was green for all 336 hours. Every one of these failures was invisible to availability monitoring and would have surfaced as slowly-eroding business metrics weeks later. Label-free monitors (PSI on inputs and scores) caught the pipeline bug and the market shift within hours; only the label-based quality SLO could catch the concept drift, and it is structurally late by the 48h label lag. You need both.
