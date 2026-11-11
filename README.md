# Payouts and Cross-Border Payments

The common payout vocabulary -- the recipients or beneficiaries paid, their bank accounts, and the payouts or transfers sent to them -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Payouts, Cross-Border Payments, Remittances, Mass Payouts, International Payments, Money Transfer, Disbursements in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| beneficiary | 27 | 24 | id 71% | beneficiaries 12, recipients 8, counterparties 3, beneficiary 2 |
| payout | 55 | 53 | status 72%, amount 68%, id 66%, created_at 53% | payouts 26, transfers 17, transfer 11, payout 9 |

Cohort: 100 providers with harvested OpenAPI, 62 crosswalks. Of the providers exposing a beneficiary: 67% create, 85% list, 52% fetch, 33% update, 37% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Payouts agree on status, amount, id and created_at; currency reaches 42% and the reference 40%, because single-currency providers leave the currency implicit.
- Beneficiaries agree only on id: entity_type, name and status each reach 42%, and the bank details are a country-specific object (IBAN, sort code, routing number, CLABE) at every provider.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- beneficiary is the market word for the party paid (over recipient and payee) in cross-border payments, and it does not collide with a concept in another context.
- Bank details are left as an object: their fields are set by each country's clearing system, not by the providers.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
