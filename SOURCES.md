# Sources and attribution

This repository publishes the case03 implementation and customer-neutral
documentation. It does not redistribute Microsoft portal assets, customer
documents, private screenshots, raw datasets or deployment receipts.
The historical facts in README describe a controlled lab on October 10, 2026;
they are not corporate claims or proof that another deployment will behave
identically.

The implementation uses Azure APIs and standard Python packages. Their services,
packages, documentation and trademarks retain their own terms and licenses.
The repository's MIT license applies to this implementation, not to third-party
assets or the Azure services themselves.

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
