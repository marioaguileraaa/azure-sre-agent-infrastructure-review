# Infrastructure operations evidence

## Platform

web

## Users

Infrastructure operators reviewing a hybrid estate, and customers watching an
Azure SRE Agent demonstration. They need to distinguish an observed operational
problem from a monitoring blind spot, locate its evidence, and decide who should
review it.

## Product Purpose

Scenario 03 makes real CPU, memory, utilization, health, capacity and anomaly
evidence understandable across Azure Arc machines and Azure-native services.
The deliverable pairs source-grounded chat questions with a monthly interactive
HTML snapshot and machine-readable exports.

## Positioning

One restricted read-only SRE subagent explains comparable operational signals
without pretending that Arc guest telemetry, Azure platform metrics and managed
service metrics have identical semantics. The absence of evidence remains
visible rather than becoming zero or a healthy status.

## Operating Context

The report is reviewed monthly and can be generated on demand. It is a dated,
self-contained offline artifact, not a live-polling portal. Fresh chat queries
collect scoped evidence for real-time demonstrations. A separately approved,
bounded operator load exercise demonstrates an actual Azure Monitor alert
invoking the subagent; the report, skill and scheduled task never apply load.

## Capabilities and Constraints

- Use real lab observations only for deployed demonstrations.
- Keep source, resource identity, unit, aggregation, grain, observation time,
  coverage and uncertainty attached to measurements.
- Support resource filters, time series, comparisons, chronological events,
  resource drilldowns and complete filtered exports.
- Collect only from one configured subscription and explicitly allowed log
  workspaces using the agent's managed identity.
- Return compact, complete structured chat responses. Full normalized evidence
  belongs in guarded runtime-owned files.
- Missing guest monitoring is Unknown / Not collected. Arc connection and ARM
  provisioning are not guest health. Anomaly flags are not root-cause proof.
- No automatic remediation, resource changes, workload stops, secrets, OOM
  exercises, disk filling or unbounded stress.
- No external frontend libraries, fonts, CDN calls, tokens or analytics.
- Publish case03 code and documentation only, without other scenarios or private
  repository history.

## Brand Commitments

Customer-neutral and reusable. The report's operations-ledger personality avoids
a generic dashboard without replacing evidence with decoration. No customer
data, branding, copied customer assets or simulation belongs in this scenario.

## Evidence on Hand

The public package contains the standalone case03 tool and its documentation,
not a private telemetry dataset. The original guide and owner-reviewed lab
screenshots record historical observations from October 10, 2026. They are not
proof of current availability or another deployment's permissions and behavior.
Offline tests may use explicitly synthetic, source-shaped fixtures that are
never deployed as lab observations. Private raw handoffs and deployment/privacy
receipts remain outside the public package.

## Product Principles

1. Evidence before confidence: preserve unknowns and disclose source errors.
2. Comparable only when semantics match: never hide units or aggregation.
3. Read-only by construction: operator actions are separate and explicit.
4. Useful decisions over decorative scores: prioritize explainable owner reviews.
5. Snapshot honesty: recorded time and coverage travel with every export.

## Recorded Decisions and Runtime Evidence

The implemented operations-ledger direction is recorded in [DESIGN.md](DESIGN.md).
This public documentation restoration does not redesign the report or alter its
runtime.

The historical lab verified real Arc/native telemetry, deployed restricted
components, final monthly/current native downloads, actual automatic incident
invocations, bounded operator CPU measurements, worker cleanup and original
power-state restoration. The [README](README.md#verified-lab-outcomes) records
their dated scope and limitations; no private raw telemetry dataset is published.
The Arc exercise honors its observed command CPU quota rather than claiming
host-wide saturation. Offline tests and replay checks remain distinct from
these historical runtime facts.
