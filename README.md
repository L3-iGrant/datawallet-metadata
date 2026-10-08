# datawallet-metadata
Hosts public metadata for Data Wallet app. For e.g. Support ledger networks, PkPass schema metadata e.t.c

## unsigned_request_policy.json

Unsigned presentation requests (no request JWS, or a request object with `alg: none`) the Data Wallet apps may serve without a trust-list check. Change detection uses the `unsigned_request_policy` timestamp in `last_updated.json`.

One entry per permitted (URI scheme, credential type):

| Field | Meaning |
| --- | --- |
| `scheme` | URI scheme the request must arrive on, without `://`, matched case-insensitively. Example: `av`. |
| `allow_all_schemes` | `true` lets the entry match every URI scheme. `scheme` may then be left out. |
| `doctype` | mdoc doctype the request may ask for (DCQL `meta.doctype_value`). |
| `vct` | SD-JWT `vct` the request may ask for (DCQL `meta.vct_values`). |

Each entry needs `scheme` or `allow_all_schemes`, and `doctype` or `vct`. An unsigned request is served only when every credential it asks for has an entry covering the scheme it arrived on. An empty list serves no unsigned request.

Current entry: the age verification attestation `eu.europa.ec.av.1` on every scheme.
