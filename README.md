# Azure SRE Agent: an evidence-led infrastructure review

One read-only workflow for Azure Arc guests and Azure-native services, without
pretending that their measurements mean the same thing.

The tool collects source-qualified CPU, physical memory, capacity, utilization,
platform-health and alert evidence. It creates a self-contained, interactive
HTML snapshot, resource CSV, signal CSV and losslessly encoded JSON. A restricted
`infra-ops-live` specialist answers scoped questions and supports a monthly
review. **Missing evidence stays Unknown / Not collected, not zero or healthy.**

This repository contains **case03 infrastructure code only**. It contains no
customer data, private deployment configuration, raw lab telemetry, screenshots,
cloud credentials or history from another repository. This is a personal,
reusable example, not an official Microsoft product or support commitment.

## What was actually observed

These are **historical lab observations from October 10, 2026**, not current
availability claims, guaranteed performance or a production benchmark.

| Lab check | Observed result |
|---|---|
| Fixed inventory | 63 resources: 10 Arc resources, comprising eight machines and two connected clusters; 53 Azure-native resources. |
| Two-hour snapshot | 253 series and 6,023 retained points, collected at 11:54:41 UTC. |
| Previous complete month | September 1-October 1, 2026 UTC: 269 series and 171,059 retained points. |
| Final monthly artifacts | HTML 1,261,116 bytes; JSON 1,200,185 bytes; resource CSV 61,456 bytes; signal CSV 60,847 bytes. All four historical downloads returned HTTP 200. |
| Native VM operator exercise | Separate, approved 480-second CPU-only exercise: 479 host samples, 71.95% mean and 74.5% maximum. A 65% teaching alert fired at 11:10:30 UTC and its monitor condition resolved at 11:19:36 UTC. |
| Arc operator exercise | Separate, approved 480-second CPU-only exercise: 479 host samples, 14.01% mean and 25% maximum. Its unchanged 0.3-core command quota on a two-vCPU host implies about 15% host CPU budget, not 72% host saturation. A 10% teaching alert fired at 11:33:15 UTC and its monitor condition resolved at 11:56:54 UTC. |
| Automatic investigations | Both real alerts routed to the restricted read-only specialist and the investigations completed. No remediation or external ticket writeback was performed. |
| Historical cleanup | Created load workers stopped and the temporarily started lab machines were verified back in their original deallocated state at the time. This is not a statement about their state today. |

Operator host-sample averages are **not** the report's five-minute metric-bin
averages. The two teaching thresholds are not production SLOs. Source alert
resolution, investigation completion, worker cleanup and power-state
restoration are distinct observations. A manual chat or an alert row alone does
not prove automatic routing. The report can be `partial` because coverage is
partial while all four exports remain complete.

## Start here

Read [SETUP.md](SETUP.md) before configuring the tool. Run offline tests first:

```text
python -m unittest discover -s tests -p "test_*.py"
```

Tests use explicitly synthetic fixtures and make no cloud calls. Optional
private-source replay tests skip when the deliberately excluded
`handoff-inputs` directory is absent. Linux-only stop-channel tests skip on
Windows; neither those tests nor the report should be mistaken for permission
to apply load to a machine.

Install runtime dependencies in your own environment when you need to configure
the SRE tool:

```text
python -m pip install -r requirements.txt
```

The unconfigured tool fails explicitly with `configuration_required`.
Authentication uses the specifically configured managed identity, not a cached
CLI account or a token supplied in chat.

The two canonical Python utilities retain their original bytes through the
included `.gitattributes`. Do not normalize their line endings when verifying
source hashes.

## Package

| File | Purpose |
|---|---|
| [generate-infrastructure-operations-report.py](generate-infrastructure-operations-report.py) | Standalone read-only collector, scoped queries, interactive report and lossless evidence exports. |
| [tool-parameters.schema.json](tool-parameters.schema.json) | Exact typed inputs, filters, enums and bounds. |
| [requirements.txt](requirements.txt) | Direct runtime dependencies. Pillow validates an optional authorized raster logo. |
| [skills/infra-ops-live/SKILL.md](skills/infra-ops-live/SKILL.md) | Evidence semantics, one-call monthly contract and incident-investigation boundaries. |
| [subagent-instructions-and-prompts.md](subagent-instructions-and-prompts.md) | Restricted agent instructions and copy-ready English questions. |
| [chatprompt.txt](chatprompt.txt) | Copy-and-paste English read-only demo prompt. |
| [monthly-task-prompt.md](monthly-task-prompt.md) | Monthly UTC review prompt. The file does not create or run a schedule. |
| [controlled-cpu-load.py](controlled-cpu-load.py) | Separate, approval-gated Linux operator utility. **Never install it as an SRE tool, skill asset or scheduled action.** |
| [tests](tests) | Synthetic offline contract tests; no private datasets are included. |
| [SOURCES.md](SOURCES.md) | First-party source references and attribution boundaries. |
| [LICENSE](LICENSE) | MIT license for this code, not for Microsoft services or third-party packages. |

## Interpretation and safety

Arc connection is not guest health. VM Insights, supported guest counters,
native platform metrics and managed-service measurements retain their source,
units, aggregation, denominator, grain, timestamps and missing bins. Container
limits, Windows commit and physical RAM are different concepts. A deliberately
deallocated VM with absent measurements is not automatically an outage or an
idle-capacity recommendation.

Local threshold and median/MAD flags are owner-review aids, not proof of root
cause. No composite health score, invented p95, SLA certification, savings,
automatic resize, restart, self-healing or ticket update is promised.
Existing monitoring and SRE/log-query usage can have costs.

The optional logo defaults to an empty configuration and a neutral placeholder.
Only a locally validated, single-frame PNG/JPEG of at most 100,000 bytes and
2048 by 2048 pixels is accepted. Do not embed a customer brand without permission.

For an authorized local PNG, this Windows command emits short Python string
chunks for the configuration constant; it does not upload the file:

```powershell
python -c "import base64, sys, textwrap; from pathlib import Path; b = Path(r'C:\path\company-logo.png').read_bytes(); 0 < len(b) <= 100000 or sys.exit('Use a logo of 1 to 100000 bytes'); u = 'data:image/png;base64,' + base64.b64encode(b).decode('ascii'); print('COMPANY_LOGO_DATA_URI = (\n' + '\n'.join('    ' + repr(s) for s in textwrap.wrap(u, 88)) + '\n)')"
```

For JPEG use `data:image/jpeg;base64,` instead. The tool verifies the complete
raster before embedding it and returns explicit errors for invalid images,
missing validation dependencies or exceeded size bounds. No remote image fetch,
customer logo, external font or CDN is needed.

Public reuse requires your own approved scope and read access. Configuring
roles, monitoring, schedules, alert rules, incident routing or an operator
exercise is a separate action, not something this repository performs on import.
