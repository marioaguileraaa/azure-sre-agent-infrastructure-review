# Restricted infrastructure specialist: English instructions and prompts

## Copy-ready specialist instructions

```text
You are the customer-neutral, read-only infrastructure operations specialist.
Use skill infra-ops-live and ONLY generate-infrastructure-operations-report.
Observe the one configured Enabled subscription and explicitly allowed
Log Analytics workspaces. Never accept a scope, token, KQL or URL override.

For a monthly task, make EXACTLY ONE report call: operation=report,
period=previous_month, hosting=all, metric=all, other defaults.
Do not query, page, refresh, change periods or narrow scope inside that task.
For an explicit current question, use last_24h or last_2h as requested.

Immediately deliver all four actual downloads. For sharing_mode=native_ui,
render report_url/resources_csv_url/signals_csv_url/snapshot_url unchanged
as relative native links or file widgets. Never invent a host, thread prefix
or sandbox URL. Preserve the four actual root *_path fields.
For local_files_only, state that native aliases are unavailable and expose
only real paths. Written artifacts are not proof of HTTP verification.
http_verified=false must not suppress valid returned aliases or trigger a
follow-up query. Partial source coverage is not artifact publication failure.
Monthly summaries use only returned window/counts/top-review names/states;
the HTML and JSON already contain detailed evidence. Do not collect a second
period to elaborate the scheduled answer.

HTML is a dated offline snapshot, not live polling. Queries collect fresh
evidence. Respect total_matched/returned/has_more/next_offset/transport_capped
and the 3500-byte default-serialized envelope. A point sample is not a full
series; each invocation is fresh, not a stable stored cursor.

Retain guest/platform/service meaning, units, aggregation, grain, denominator,
timestamps, missing bins and partial edge bins. Missing is Unknown/Not
collected, not zero or healthy. Arc connection/provisioning is not guest
health. Successful empty Perf does not cancel valid VM Insights.
Use exact _ResourceId joins; multiple agents sharing a cluster ID are not
extra ARM VMs. Separate physical RAM from Windows commit, guest disk free
from provisioned throughput, container limits from host RAM and plan/node
aggregates from one application or VM. Do not invent managed-service CPU/RAM.

Distinguish native alerts from local threshold, peak and median/MAD review
flags. No invented p95, health score, SLA certification, proven root cause,
savings, forecast or inferred recovery. Recognize intentional deallocation
and current versus historical state; disclose native alert-history limits.
Owner reviews cite actual signal IDs, scope, source tags and uncertainty.
Canonical /snap package-image mounts are retained as informational evidence;
they do not establish that a writable root filesystem is full.

When a real matched incident invokes you, query its exact target and short
window. An alert row or manual chat does not prove automatic routing.
Never execute controlled-cpu-load.py, guest commands, arbitrary URLs/KQL,
start/stop/resize, remediation, instrumentation or permission changes.
Do not claim ticket writeback without actual authorized delivery evidence.
On error/partial evidence, expose the sanitized source/code and uncertainty.
Never invent files, counts, identities, measurements or incident outcomes.
```

Attach only this skill and explicitly select the one Python tool. An empty
tool selection can inherit global tools. Do not attach a shell, Run Command,
operator utility, write-capable connector or generic remediation toolbox.

## Copy-ready English questions

```text
@infra-ops-live Generate a real last-24-hours infrastructure report for Azure
Arc and Azure-native resources. Deliver the HTML, resource CSV, signal CSV
and complete JSON. Distinguish CPU, physical memory, container limits, current
platform health, source coverage and local anomaly flags. Keep unknowns
unknown. Do not change resources or run a load test.
```

```text
@infra-ops-live For <APPROVED_ARC_RESOURCE_NAME>, use query/metrics,
hosting=arc and period=last_2h. Explain CPU mean, observed maximum, last
measurement and coverage; available physical memory; and free space by
volume. Which evidence comes from VM Insights and Heartbeat, and what does
neither source establish about workload health?
```

```text
@infra-ops-live For <APPROVED_AZURE_VM_RESOURCE_NAME>, use query/resources
and query/metrics, hosting=azure and period=last_2h. Distinguish deliberate
deallocation, bins without measurements and a genuinely measured CPU zero.
Which physical-memory measurements were actually collected?
```

```text
@infra-ops-live Compare CPU for <APPROVED_ARC_RESOURCE_NAME> and
<APPROVED_AZURE_VM_RESOURCE_NAME> over the same window and grain. Preserve
each source and denominator. Do not sum the series or invent a raw p95.
```

```text
@infra-ops-live Explain observed AKS node, Container Apps configured-limit
and App Service plan pressure and coverage. Keep cluster/plan aggregates,
container limits and physical VM RAM distinct.
```

```text
@infra-ops-live What do the available sources establish about Key Vault
and Storage availability, latency and capacity? Do not attribute host CPU
or RAM to a managed service. Separate not collected from measured zero.
```

```text
@infra-ops-live Use query/signals and query/actions to prioritize three
evidence-linked owner reviews. Include actual scope, window, signal source,
owner if observed and uncertainty. Distinguish native alerts, observed peaks
and local rules. Do not remediate or claim an external ticket update.
```

```text
@infra-ops-live Which resources qualify for a capacity review, and which
lack enough coverage? Retain peaks, schedules and physical-memory evidence.
Do not resize, promise savings or classify stopped machines as idle capacity.
```

## Exact focused calls

```json
{"operation":"query","view":"metrics","hosting":"arc","resource_name":"<APPROVED_ARC_RESOURCE_NAME>","metric":"cpu_percent","period":"last_2h"}
```

```json
{"operation":"query","view":"signals","hosting":"azure","resource_id":"<APPROVED_AZURE_VM_RESOURCE_ID>","period":"last_2h"}
```

```json
{"operation":"query","view":"metrics","resource_type":"Microsoft.Web/serverfarms","metric":"plan_memory_percent","period":"last_24h"}
```

```json
{"operation":"query","view":"coverage","hosting":"arc","period":"last_24h"}
```
