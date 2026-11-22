# Open source and AI security work

Contributions to supply chain, detection and AI security projects. I follow one routine: reproduce locally, check for existing work, open an issue, wait for the maintainer, then write code. Status is as of 22 November 2026, and I update it as things merge.

## Supply chain hardening

**Docker Hardened Images catalog**
* Issue [#302](https://github.com/docker-hardened-images/catalog/issues/302): hardened images for the Kyverno policy reporter plugins. I submitted three image definitions, PRs [#462](https://github.com/docker-hardened-images/catalog/pull/462), [#463](https://github.com/docker-hardened-images/catalog/pull/463) and [#464](https://github.com/docker-hardened-images/catalog/pull/464). A Kyverno maintainer confirmed in the issue that the PRs look good and that the images should become the policy reporter chart defaults. Status: open, and I have committed to the follow up chart PR once they merge.
* Issue [#732](https://github.com/docker-hardened-images/catalog/issues/732): requested hardened images for the Falco ecosystem after finding it had no coverage in the catalog. Status: awaiting maintainer.

## Detection

**Chainguard malcontent**
* Issue [#1813](https://github.com/chainguard-dev/malcontent/issues/1813): proposed detection rules for cloud instance metadata endpoints beyond the existing AWS and GCP rules (Azure, Oracle Cloud, Alibaba Cloud, DigitalOcean). I checked each endpoint and required header against the provider documentation first. Status: awaiting maintainer.

**Falco prempti (coding agent runtime rules)**
* Issue [#49](https://github.com/falcosecurity/prempti/issues/49) and PR [#60](https://github.com/falcosecurity/prempti/pull/60): rules for agents fetching instance metadata endpoints and known indicators of compromise through web fetch tools. Status: open, in review with a maintainer.

## AI and agent security

**NVIDIA garak (LLM vulnerability scanner)**
* Issue [#2502](https://github.com/NVIDIA/garak/issues/2502): proposed a probe and detector for agents steered into requesting cloud metadata endpoints. I confirmed the gap first by searching the codebase, and separated it from related SVG/XXE proposals and the generic agent_breaker probe. Status: awaiting maintainer.
* Review of PR [#1779](https://github.com/NVIDIA/garak/pull/1779) (context compliance probe): found and reproduced robustness bugs in the generated variant, using a stub attacker model. Valid JSON that is not an object crashes the probe, null values are accepted, single line fenced replies are dropped, and total generation failure is silent. The probe also had no tests for that path.
* Review of PR [#1849](https://github.com/NVIDIA/garak/pull/1849) (data structure injection probe): answered the maintainer's request for reproducible testing with offline control runs and a live run against a small open model (10 of 30 prompts flagged), then inspected every flagged output by hand. Found that the detector matches the trigger anywhere in the JSON, so a mention inside a note field counts as an attack success, demonstrated with a short script.

## How I work
* Check existing issues and code before proposing anything.
* Reproduce locally and keep the commands, so maintainers can rerun them.
* Report what I verified and what I did not, including when my own prediction was wrong.
* No pull request until a maintainer confirms the direction.
