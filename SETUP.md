# Configure the read-only case03 workflow

This is a configuration guide, not an instruction to deploy resources, grant
roles, create schedules or run a CPU exercise automatically. Use an approved
lab and your own explicitly authorized scope.

This concise checklist accompanies the [complete original illustrated
walkthrough](README.md#contents), including its setup/runtime diagrams, detailed
explanations and nine dated original lab screenshots. Follow that guide for
the original Step 0-6 order; the existing checklist headings below remain stable.

## 1. Configure the fixed scope

Full walkthrough: [Step 0 - Fixed scope and read access](README.md#step-0---fixed-scope-and-read-access).

Edit only the deployment copy of the report tool's top-level constants:

```python
SUBSCRIPTION_ID = "<YOUR_SUBSCRIPTION_ID>"
TENANT_ID = "<YOUR_TENANT_ID>"
MANAGED_IDENTITY_CLIENT_ID = "<YOUR_AGENT_CLIENT_ID>"
LOG_WORKSPACE_IDS = ["<YOUR_APPROVED_WORKSPACE_GUID>"]
COMPANY_LOGO_DATA_URI = ""
COMPANY_LOGO_ALT_TEXT = "Company logo"
```

Use the managed identity's **Client ID**, not its Object/Principal ID. The
subscription must be Enabled and its tenant must match. Only explicitly allowed
workspace GUIDs are queried. Do not paste identifiers, access tokens, secrets,
customer logos or raw API responses into a public fork.

Verify existing approved read permissions for inventory, metric definitions
and values, Resource Health, native alerts and required workspace tables.
Human SRE author/chat permissions are separate from the managed identity's
resource reads. Consult current [SRE roles](https://learn.microsoft.com/azure/sre-agent/user-roles).
The tool never installs monitoring or expands permissions to hide a blind spot.

## 2. Create the Python tool in an authorized SRE environment

Full walkthrough: [Step 1 - Create and test the Python tool](README.md#step-1---create-and-test-the-python-tool),
including the [optional company-logo configuration](README.md#optional-company-logo).

Name it `generate-infrastructure-operations-report`. Paste the complete
configured Python source. Use its typed `main()` signature and the exact
parameter schema. Make the direct requirements available in the runtime.

Do not add arbitrary KQL, URLs, paths, credential or subscription inputs.
Test a short approved query and verify the actual source statuses, counts and
units before creating the tool. Syntax validation alone does not establish
access or downloadable files.

```json
{"operation":"query","view":"metrics","hosting":"arc","resource_name":"<APPROVED_ARC_RESOURCE_NAME>","metric":"cpu_percent","period":"last_2h"}
```

## 3. Attach one skill and explicitly select one tool

Full walkthrough: [Step 2 - Create the skill](README.md#step-2---create-the-skill)
and [Step 3 - Restrict the subagent](README.md#step-3---restrict-the-subagent).

Create `infra-ops-live` from [SKILL.md](skills/infra-ops-live/SKILL.md).
Create the restricted specialist using the instructions in
[subagent-instructions-and-prompts.md](subagent-instructions-and-prompts.md).

Attach only that skill and explicitly select only the report tool. Do not
leave the tool selection empty: portal versions can then inherit global tools.
Do not attach a shell, guest Run Command, stress utility, write-capable
connector or generic remediation toolbox. A prompt is not a permission control.

## 4. Request a report and inspect its evidence

Full walkthrough: [Step 4 - Reports and fresh questions](README.md#step-4---reports-and-fresh-questions).

```text
@infra-ops-live Generate a real last-24-hours infrastructure report for both
Azure Arc and Azure-native resources. Return the HTML, resource CSV, signal CSV
and complete JSON. Preserve sources, units, measurement semantics, missing
data and coverage. Do not change resources or run a load test.
```

```json
{"operation":"report","hosting":"all","period":"last_24h"}
```

`period="auto"` selects the previous complete UTC month for reports and the
last 24 hours for queries. Request a short window explicitly for a current
question. A downloaded HTML file is a dated offline snapshot, not live polling.

The normal four output paths belong to the guarded runtime-owned report
directory. If `sharing_mode="native_ui"`, render the four returned relative
native aliases unchanged. Do not invent a host, thread prefix or sandbox link.
If aliases are unavailable, show only the actual local paths and state that
limitation. `artifact_status="written"` does not mean an HTTP download was
verified; `http_verified=false` does not justify hiding otherwise valid aliases.

The artifact-directory and native-alias contracts were verified in a particular
SRE runtime. Portal/runtime versions evolve; validate the returned paths in your
own deployment rather than assuming a documentation example's filesystem is
identical. Do not broaden storage permissions to work around a failure.

## 5. Keep a monthly review to one complete report call

Full walkthrough: [Step 5 - Monthly task and run now](README.md#step-5---monthly-task-and-run-now).

The optional monthly configuration uses the previous UTC calendar month and
`0 9 1 * *` (day 1, 09:00 UTC). Read [monthly-task-prompt.md](monthly-task-prompt.md).
Create a schedule only with separate authorization; these files do not create
one. The monthly run makes one report call and immediately shares the four
returned artifacts. Fresh follow-up questions belong in a separate explicit
chat, not hidden additional calls in the monthly run.

Use the full Arc-and-Azure scope. Do not turn an artifact-size failure into
success by shortening the month, removing resources or dropping sources.
Lossless codec 2.0 retains nested records and exact timestamps/numbers; the
HTML and Python decoder also accept codec 1.0. Plain artifacts are bounded to
4,800,000 bytes and compact chat results to 3,500 default-serialized bytes.
Query paging is not a stable stored cursor: each live call collects fresh data.

## 6. Understand an incident without changing the machine

Full walkthrough: [Step 6 - Real alert to subagent demonstration](README.md#step-6---real-alert-to-subagent-demonstration).
The separate historical operator exercise in that section is not part of this
read-only handler configuration.

An isolated, authorized response plan can route an actual Azure Monitor incident
to `infra-ops-live` in Review mode. Verify the real incident, response-plan
mapping, selected handler and completed investigation separately from the
alert record. Preserve unrelated existing plans and do not silently change a
broad handler to make a demonstration route differently.

The handler queries the exact approved target and a short window. It distinguishes
native alert conditions from local review flags, discloses uncertainty and
provides evidence-linked owner checks. It does not start/stop/resize a resource,
run guest commands, apply load or update an external ticket.

## Separate operator-only CPU utility

See the original guide's [safety gate](README.md#safety-gate) and
[operator-only bounded CPU command](README.md#operator-only-bounded-cpu-command).

`controlled-cpu-load.py` is included for code completeness and offline safety
tests. It is **not** part of the SRE tool, skill, monthly task or incident handler.
It makes no Azure calls and creates no memory/disk-pressure exercise.

Before any operator use, obtain exact host, duration, load, startup/restoration
and cost approvals; establish a separate stop channel and recovery plan.
The utility supports only an inspectable Linux cgroup v2 environment, exact
hostname confirmation, bounded workers/duration, baseline and memory-reserve
checks, a reachable CPU target, per-worker duty limits, sampled host CPU
protection and cleanup of its own PIDs. It fails closed when the required
environment or counters cannot be established.

The hard limits are 480 seconds, at most eight workers, target at most 82%,
per-worker duty at most 85% and a sampled 85% host-CPU stop ceiling. These are
not an instantaneous host-wide guarantee, an OOM guarantee or permission to
change a cgroup quota. A 0.3-core quota on two vCPUs allows about 15% host CPU;
never rescale the reported values or bypass governance to claim saturation.

No operator load, Azure operation or new scheduled run is needed to run the
repository's synthetic offline tests.
