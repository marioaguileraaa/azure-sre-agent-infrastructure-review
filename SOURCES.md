# Sources and attribution

This repository publishes the case03 implementation and customer-neutral
documentation, including the complete original English walkthrough, its two
inline Mermaid diagrams and nine original lab screenshots reviewed and
authorized for public reuse by their owner. The illustrations retain their
original pixels, numbered red callouts and historical/date/stage qualifications;
they are not newly collected telemetry or recreated setup UI.

No customer documents, customer branding, private raw captures, raw datasets,
deployment identities, credentials, private provenance/privacy receipts or
other-case material are published. Generic lab labels in the reviewed
illustrations are historical examples, not approved deployment targets.
The historical facts in README describe a controlled lab on October 10, 2026;
they are not corporate claims or proof that another deployment will behave
identically.

The implementation uses Azure APIs and standard Python packages. Their services,
packages, documentation and trademarks retain their own terms and licenses.
The repository's MIT license applies to this implementation, not to third-party
assets, Microsoft portal UI or the Azure services themselves. The lab
screenshots illustrate the owner's use of those services; they do not transfer
ownership of Microsoft UI, names or trademarks.

## Existing public companion media

- [English LinkedIn/video package, v2](https://github.com/marioaguileraaa/azure-sre-agent-infrastructure-review/releases/tag/case03-linkedin-v2)
- [70-second case03 video, v2](https://github.com/marioaguileraaa/azure-sre-agent-infrastructure-review/releases/download/case03-linkedin-v2/case03-linkedin-final.mp4)
- [Original video release, v1](https://github.com/marioaguileraaa/azure-sre-agent-infrastructure-review/releases/tag/case03-linkedin-v1)

The releases retain their own dated, identity-redacted film/caption context.
Restoring the original guide images does not replace those media assets, create
new lab evidence or claim that a post has been published to LinkedIn.

## First-party technical references

- [Azure SRE Agent overview](https://learn.microsoft.com/azure/sre-agent/overview)
- [Python tools](https://learn.microsoft.com/azure/sre-agent/python-code-execution)
- [Skills](https://learn.microsoft.com/azure/sre-agent/skills)
- [User roles](https://learn.microsoft.com/azure/sre-agent/user-roles)
- [Incident response plans](https://learn.microsoft.com/azure/sre-agent/incident-response-plan)
- [Automate workflows](https://learn.microsoft.com/azure/sre-agent/automate-workflows)
- [VM platform metrics](https://learn.microsoft.com/azure/azure-monitor/reference/supported-metrics/microsoft-compute-virtualmachines-metrics)
- [InsightsMetrics table](https://learn.microsoft.com/azure/azure-monitor/reference/tables/insightsmetrics)
- [Perf table](https://learn.microsoft.com/azure/azure-monitor/reference/tables/perf)
- [Heartbeat table](https://learn.microsoft.com/azure/azure-monitor/reference/tables/heartbeat)
- [Connected Machine agent resource governance](https://learn.microsoft.com/azure/azure-arc/servers/agent-overview#agent-resource-governance)
- [Logs API request format](https://learn.microsoft.com/azure/azure-monitor/logs/api/request-format)
- [Metric definitions](https://learn.microsoft.com/rest/api/monitor/metric-definitions/list)
- [Metric values](https://learn.microsoft.com/rest/api/monitor/metrics/list)
- [Resource Health](https://learn.microsoft.com/rest/api/resourcehealth/availability-statuses/list-by-subscription-id)
- [Alerts API lookback options](https://learn.microsoft.com/javascript/api/@azure/arm-alertsmanagement/alertsgetalloptionalparams)
- [Linux cgroup v2 CPU semantics](https://www.kernel.org/doc/html/latest/admin-guide/cgroup-v2.html#cpu)

The Python-tool documentation was consulted on October 13, 2026. Runtime
filesystem and sharing details in this example follow its observed guarded
output contract; verify these details for the SRE version you use.
