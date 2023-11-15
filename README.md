# RustSec Advisory Database
[![security status](https://qa.meterian.com/badge/pb/f9d3ac33-ade4-4f98-b125-fa5ff530ebe4/security)](https://qa.meterian.com/projects/?pid=f9d3ac33-ade4-4f98-b125-fa5ff530ebe4) [![stability status](https://qa.meterian.com/badge/pb/f9d3ac33-ade4-4f98-b125-fa5ff530ebe4/stability)](https://qa.meterian.com/projects/?pid=f9d3ac33-ade4-4f98-b125-fa5ff530ebe4) [![licensing status](https://qa.meterian.com/badge/pb/f9d3ac33-ade4-4f98-b125-fa5ff530ebe4/licensing)](https://qa.meterian.com/projects/?pid=f9d3ac33-ade4-4f98-b125-fa5ff530ebe4)

[![Build Status][build-image]][build-link]
![Maintained: Q1 2021][maintained-image]
[![Project Chat][chat-image]][chat-link]

The RustSec Advisory Database is a repository of security advisories filed
against Rust crates published via https://crates.io. A human-readable version
of the advisory database can be found at https://rustsec.org/advisories/.

The following tools consume this advisory database and can be used for auditing
and reporting (send PRs to add yours):

* [cargo-audit]: Audit `Cargo.lock` files for crates with security vulnerabilities
* [cargo-deny]: Audit `Cargo.lock` files for crates with security vulnerabilities,
  limit the usage of particular dependencies, their licenses, sources to download
  from, detect multiple versions of same packages in the dependency tree and more.

## Reporting Vulnerabilities

To report a new vulnerability, open a pull request using the template below.
See [CONTRIBUTING.md] for more information.

<a href="https://github.com/RustSec/advisory-db/blob/main/CONTRIBUTING.md">
  <img alt="Report Vulnerability" width="250px" height="60px" src="https://rustsec.org/img/report-vuln-button.svg">
</a>

## Advisory Format

See [EXAMPLE_ADVISORY.md] for a template.

Advisories are formatted in [Markdown] with [TOML] "front matter".
Below is the schema of the "front matter" section of an advisory:

```toml
# Before you submit a PR using this template, **please delete the comments**
# explaining each field, as well as any unused fields.

[advisory]
# Identifier for the advisory (mandatory). Will be assigned a "RUSTSEC-YYYY-NNNN"
# identifier e.g. RUSTSEC-2018-0001. Please use "RUSTSEC-0000-0000" in PRs.
id = "RUSTSEC-0000-0000"

# Name of the affected crate (mandatory)
package = "mycrate"

# Disclosure date of the advisory as an RFC 3339 date (mandatory)
date = "2019-10-01"

# URL to a long-form description of this issue, e.g. a GitHub issue/PR,
# a change log entry, or a blogpost announcing the release (optional)
url = "https://github.com/mystuff/mycrate/issues/123"

# Optional: Categories this advisory falls under. Valid categories are:
# "code-execution", "crypto-failure", "denial-of-service", "file-disclosure"
# "format-injection", "memory-corruption", "memory-exposure", "privilege-escalation"
categories = ["crypto-failure"]

# Optional: a Common Vulnerability Scoring System score. More information
# can be found on the CVSS website, https://www.first.org/cvss/.
#cvss = "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H"

# Freeform keywords which describe this vulnerability, similar to Cargo (optional)
keywords = ["ssl", "mitm"]

# Vulnerability aliases, e.g. CVE IDs (optional but recommended)
# Request a CVE for your RustSec vulns: https://iwantacve.org/
#aliases = ["CVE-2018-XXXX"]

# Related vulnerabilities (optional)
# e.g. CVE for a C library wrapped by a -sys crate)
#related = ["CVE-2018-YYYY", "CVE-2018-ZZZZ"]

# Optional: metadata which narrows the scope of what this advisory affects
[affected]
# CPU architectures impacted by this vulnerability (optional).
# Only use this if the vulnerability is specific to a particular CPU architecture,
# e.g. the vulnerability is in x86 assembly.
# For a list of CPU architecture strings, see the "platforms" crate:
# <https://docs.rs/platforms/latest/platforms/target/enum.Arch.html>
#arch = ["x86", "x86_64"]

# Operating systems impacted by this vulnerability (optional)
# Only use this if the vulnerable is specific to a particular OS, e.g. it was
# located in a binding to a Windows-specific API.
# For a list of OS strings, see the "platforms" crate:
# <https://docs.rs/platforms/latest/platforms/target/enum.OS.html>
#os = ["windows"]

# Table of canonical paths to vulnerable functions (optional)
# mapping to which versions impacted by this advisory used that particular
# name (e.g. if the function was renamed between versions). 
# The path syntax is `cratename::path::to::function`, without any
# parameters or additional information, followed by a list of version reqs.
functions = { "mycrate::MyType::vulnerable_function" = ["< 1.2.0, >= 1.1.0"] }

# Versions which include fixes for this vulnerability (mandatory)
[versions]
patched = [">= 1.2.0"]

# Versions which were never vulnerable (optional)
#unaffected = ["< 1.1.0"]
```

## License

All content in this repository is placed in the public domain.

[![Public Domain](http://i.creativecommons.org/p/zero/1.0/88x31.png)](https://github.com/RustSec/advisory-db/blob/main/LICENSE.txt)

[//]: # (badges)

[build-image]: https://github.com/rustsec/advisory-db/workflows/Validate/badge.svg
[build-link]: https://github.com/rustsec/advisory-db/actions
[maintained-image]: https://img.shields.io/maintenance/yes/2021.svg
[chat-image]: https://img.shields.io/badge/zulip-join_chat-blue.svg
[chat-link]: https://rust-lang.zulipchat.com/#narrow/stream/146229-wg-secure-code/

[//]: # (general links)

[EXAMPLE_ADVISORY.md]: https://github.com/RustSec/advisory-db/blob/main/EXAMPLE_ADVISORY.md
[Markdown]: https://www.markdownguide.org/
[TOML]: https://github.com/toml-lang/toml
[cargo-audit]: https://github.com/rustsec/cargo-audit
[cargo-deny]: https://github.com/EmbarkStudios/cargo-deny
[CONTRIBUTING.md]: https://github.com/RustSec/advisory-db/blob/main/CONTRIBUTING.md
