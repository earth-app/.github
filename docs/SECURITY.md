# Security Policy

The Earth App takes the security of its users, contributors, and infrastructure
seriously. This document describes how to report vulnerabilities and what to
expect from us in return.

## Reporting a Vulnerability

**Do not open a public GitHub issue for a security vulnerability.**

If you believe you have found a security issue in any Earth App repository,
service, mobile app, or piece of infrastructure, please report it privately
using one of the following channels:

1. **Primary**: email
   [support@earth-app.com](mailto:support@earth-app.com) with the subject line
   `SECURITY: <short description>` so the support team can escalate.
2. **Critical / sensitive**: for issues that need to reach ownership directly,
   contact [gregory@earth-app.com](mailto:gregory@earth-app.com).
3. **Coordinated disclosure**: use GitHub's private
   [Security Advisories](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing/privately-reporting-a-security-vulnerability)
   feature on the affected repository under the
   [earth-app](https://github.com/earth-app) organization.

Please include, if you can:

- A description of the vulnerability and its impact.
- The repository, service, endpoint, or app version affected.
- Steps to reproduce, ideally with a minimal proof of concept.
- Any relevant logs, screenshots, or request / response payloads (with any
  personal data of others redacted).
- Your name or handle so we can credit you, if you want credit.

We support responsible disclosure and will work with you in good faith to
investigate and resolve the issue.

## Response Timeline

We aim to respond to security reports on the following schedule. Actual
response times depend on complexity and severity.

| Stage                        | Target                          |
| ---------------------------- | ------------------------------- |
| Initial acknowledgment       | Within **72 hours**             |
| Triage and severity decision | Within **7 days**               |
| Fix or mitigation in place   | Within **30 days** for high / critical severity |
| Public disclosure            | After a fix is deployed and users have had time to update |

For actively exploited or catastrophic issues, we may act faster and issue an
out-of-band advisory.

## Scope

### In Scope

- All repositories under the [earth-app](https://github.com/earth-app) GitHub
  organization, including but not limited to `crust`, `sky`, `mantle2`,
  `cloud`, `ocean`, `blog`, `website`, `moon`, `verdant`, `recess`, `rain`,
  `moho`, `shovel`, `CollegeDB`, `doc2lora`, and `smoke`.
- Production services:
  [earth-app.com](https://earth-app.com),
  [app.earth-app.com](https://app.earth-app.com),
  [api.earth-app.com](https://api.earth-app.com),
  [cloud.earth-app.com](https://cloud.earth-app.com),
  [support.earth-app.com](https://support.earth-app.com),
  [blog.earth-app.com](https://blog.earth-app.com), and any other
  `*.earth-app.com` service.
- The Earth App iOS and Android applications distributed through Apple's App
  Store and Google Play.
- Published packages, including `@earth-app/*` on GitHub Packages, npm, and
  Maven.

### Out of scope

- Automated scanner output that has not been manually verified.
- Denial-of-service by volume alone (e.g., raw traffic floods).
- Rate-limit or CAPTCHA bypass without a concrete downstream impact.
- Social engineering of staff, contributors, or users.
- Findings that require physical access to a user's unlocked device.
- Findings that only affect obsolete browsers, unpatched operating systems, or
  unsupported Ionic / Capacitor versions.
- Missing security headers on pages with no sensitive functionality.
- Vulnerabilities in third-party dependencies without a demonstrated path to
  exploitation in an Earth App surface.

## What We Consider High Severity

Reports that touch these areas will be prioritized:

- Authentication and authorization: bearer-token issuance and validation,
  OAuth linking (Google, Microsoft, Discord, GitHub, Facebook, Apple),
  admin-key gated endpoints on `mantle2` and `cloud`, session and reauth
  windows on the delete-account flow.
- Privacy: leakage of user data across privacy tiers (`PUBLIC`, `UNLISTED`,
  `PRIVATE`, `CIRCLE`, `MUTUAL`), profile field disclosure, cache-key
  poisoning that could return one user's data to another.
- Quest integrity: forging or spoofing quest evidence (image, audio, article
  quiz, structured steps), bypassing device or metadata anti-spoofing checks,
  or tampering with binary quest artifacts stored in R2.
- Payment and subscription: any way to obtain a paid feature without an
  active subscription, or to escape a refund workflow.
- Content moderation: bypassing the email verification gate on content
  creation, evading obscenity / NSFW moderation, or content injection through
  AI-generated pipelines.
- WebSocket safety: replaying or forging one-time tickets used to establish
  the `/ws/users/:id/notifications` channel.
- Cross-service integrity: any way to make Cloud act on behalf of a Mantle2
  user without valid session context.

## Handling User Data

If your report demonstrates access to real user data, please:

- Access only the minimum data required to prove the issue.
- Do not save, share, or publish user data beyond what is necessary for the
  report.
- Delete any copies of user data you obtained as soon as we confirm receipt.

Failing to respect user privacy will disqualify a report from safe-harbor
treatment.

## Safe Harbor

We consider security research conducted in good faith and in accordance with
this policy to be:

- Authorized concerning any applicable anti-hacking laws, and we will not
  initiate or support legal action against you for accidental, good-faith
  violations.
- Authorized concerning any relevant anti-circumvention laws, and we will not
  bring a claim against you for circumvention of technology controls.
- Exempt from restrictions in our Terms of Service that would interfere with
  conducting security research, and we waive those restrictions on a limited
  basis for work done under this policy.

If you cannot determine whether your intended action is in scope, please ask
before you start.

## Credit

With your permission, we are happy to publicly credit you in a repository
security advisory, in release notes, or on our security acknowledgments page.
If you prefer to stay anonymous, that is fine too.

## Data Handling and Compliance

Details on how The Earth App collects, stores, and processes user data are in
our [Privacy Policy](https://earth-app.com/privacy-policy). The Earth App is
registered in Cook County, Illinois, USA. We support GDPR and CCPA rights;
requests can be sent to
[support@earth-app.com](mailto:support@earth-app.com).

---

Thank you for helping keep The Earth App and its users safe.
