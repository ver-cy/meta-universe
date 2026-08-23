# Security Policy

## Scope

Meta-Universe is a **specification** with reference tooling. "Security" here means
two things:

1. **Specification security** — a flaw in the standard that would let a conforming
   implementation be attacked (for example a gap in the
   [Security Model](03-federation/Security-Model.md), the
   [Trust Model](03-federation/Trust-Model.md), or the
   [Consent and Disclosure](03-federation/Consent-and-Disclosure.md) rules).
2. **Tooling security** — a flaw in the reference tools under [`tools/`](tools/).

## Reporting a vulnerability

Please report privately. Do **not** open a public issue or pull request for a
suspected vulnerability.

- Email the maintainers at **to@ver.cy** (or the address listed on the
  repository's security advisory page).
- Include: the affected document or tool, the threat, and — for specification
  issues — which [Security Model threat](03-federation/Security-Model.md) (T1–T10)
  it relates to or extends.

We aim to acknowledge reports promptly, agree a disclosure timeline, and credit
reporters who wish to be credited.

## Handling

Specification security fixes are processed as **Corrective** Change Requests with
priority and a clear migration note where behavior changes. Confirmed threats are
folded into the [Security Model](03-federation/Security-Model.md) threat table and
the [Semantic Test Kit](tests/).
