# Java Web Application · Security Case Study

A focused refactor of a supplied Spring application demonstrating **SHA-256 checksum generation, local HTTPS configuration, certificate tooling, and dependency review**.

**Read the [security report (PDF)](docs/security-report.pdf)** · [Editable Word version](docs/security-report.docx)

## My contribution

I added a route that returns a fixed string and its SHA-256 digest, generated a self-signed certificate and keystore, and configured the application to serve the route over HTTPS. I checked the output manually and reviewed the dependencies with OWASP Dependency-Check.

Working within an existing application required keeping the change controlled and distinguishing the purpose of each security mechanism. AES-256 was a recommendation in the report; the demonstrated work concerned hashing and HTTPS configuration.

## Results

![Checksum output at the local HTTPS endpoint](screenshots/localhost-checksum.png)

The visible string and digest match an independent SHA-256 calculation. The browser warning reflects the local self-signed certificate setup.

| Evidence | Result |
|---|---|
| [Checksum output](screenshots/localhost-checksum.png) | Fixed string and SHA-256 digest at `https://localhost:8443/hash` |
| [Certificate project tree](screenshots/certificate-project-tree.png) | Certificate and keystore files in the original project |
| [Dependency report](screenshots/dependency-check.png) | 49 dependencies scanned, 29 unique, 13 vulnerable dependencies, and 160 findings |

## Scope

This is a documented academic exercise using a supplied Spring starter application and fictional Artemis Financial scenario. The report and screenshots record the April 19, 2026 work; application source and a reproducible build are not included.

The dependency scan retained high and critical findings, and remediation is not demonstrated. The self-signed setup was not publicly trusted. A plain checksum also does not authenticate data if an attacker can replace both the value and digest. The report explains these limits and distinguishes the implemented work from recommendations.

## What I learned

A narrow change is easier to inspect and test, but inherited dependency issues still need attention. The practices I would carry forward are using established cryptographic tools, testing after meaningful changes, and recording unresolved findings so the next development step is clear.

See [credits and acknowledgments](CREDITS.md). The report includes references to NIST, Oracle, and OWASP documentation.
