# SECURITY-NOTES.md — Log4Shell (CVE-2021-44228)

## Summary

Log4Shell is a critical remote code execution vulnerability in Apache Log4j 2. An attacker who can control log messages or log message parameters can exploit JNDI lookups to execute arbitrary code loaded from LDAP and other JNDI-related endpoints. Only the `log4j-core` JAR is impacted; applications using only `log4j-api` without `log4j-core` are not affected.

## CVE Identifier

- **CVE-2021-44228**

## Affected Versions

- Apache Log4j 2.0-beta9 through 2.14.1
- Precise range: `[2.0-beta9, 2.3.1) ∪ [2.4, 2.12.2) ∪ [2.13.0, 2.15.0)`

## Fixed Versions

- **2.3.1** (Java 6)
- **2.12.2** (Java 7)
- **2.15.0** (Java 8 and later — initial fix for CVE-2021-44228)
- **2.16.0** (Java 8+, disables JNDI lookups by default; also addresses CVE-2021-45046)
- **2.17.1** (Java 8+, addresses CVE-2021-45105); 2.12.4 (Java 7) and 2.3.2 (Java 6) are the final backports.

## Severity

- **CVSS 3.x base score: 10.0 — CRITICAL**
- Vector: `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H`
- GitHub Advisory Database (GHSA-jfh8-c2jp-5v3q): Critical

## Remediation Highlights

1. Upgrade `log4j-core` to 2.15.0+ (prefer 2.16.0+/2.17.1 for Java 8+).
2. Detect vulnerable deployments via dependency trees (`mvn dependency:tree`, `gradle dependencyInsight`), scanning tools, and runtime version checks.
3. Hardening: set `-Dlog4j2.formatMsgNoLookups=true` or remove the `JndiLookup` class from the jar as an interim measure.
4. Automated dependency scanning: enable GitHub Dependabot alerts, OWASP Dependency-Check, and Snyk in CI.

## Sources

- Apache Logging Services Security page: https://logging.apache.org/log4j/2.x/security.html
- NVD CVE-2021-44228: https://nvd.nist.gov/vuln/detail/CVE-2021-44228
- GitHub Advisory Database (GHSA-jfh8-c2jp-5v3q): https://github.com/advisories/ghsa-jfh8-c2jp-5v3q
- JPCERT/CC alert (Update Jan 4, 2022): https://www.jpcert.or.jp/english/at/2021/at210050.html
