# Azure Billing Reporting and Costs

Notes about Azure Billing, how to manage costs, and usage costs reports.

## Azure Friday Episode

[Source](https://learn.microsoft.com/en-us/shows/azure-friday/managing-reporting-and-reducing-your-costs-in-azure)

Host: Scott Hanselman
Guest: Barry Lujibregts @AzureBarry

Originally aired 19-Dec-2022

### General Notes

Costs:

- Services: Azure VMs, AppServices; Tier of each service.
- Storage: DBs, Blob and File storage; Amount of storage used; Tier.
- Network Traffic: Ingress usually free; Egress almost always; Internal comms are free; Between Regions might have a cost.
- Software Licenses: VMs running with licensed OS such as Server.

Managing:

- Azure Cost Management and Billing.
- Azure Advisor: Looks at all things that costs money and provides alerts re: pricing tier utilization, unused services, etc.

Billing: Invoices; Payment methods; Billing address; Tax ID.

Cost Management: Cost Analysis; Budgets; Alerts; Connect to AWS; Export billing data.

Cost Alerts:

- Budget:
- Credit:
- Dept spending quota: Enterprise-agreement customers.

### Azure Portal Views

Drill-down to Cost Management, Cost Analysis.

'Slice-and-dice' all resources to discover what is costing money.

Drill-down to Cost Management, Budgets.

Dill-down to Cost Management, Cost Alerts.

### Reduce Costs in Azure

- Cost reductions: Scale to right-sized Tiers; Policies; Clean-up unused resources (see Azure Advisor); Scale-down.
- Use Discounts: Visual Studio Subscription benefit; MSP (Managed Service Provider); EA (Enterprise Agreements, sometimes include pre-paid discounts).
- Azure Spot VM: Pricing option "Run this with an Azure Spot discount" during VM creation, saves over pay-as-you-go, auto-eviction, no SLA.
- Reserved Capacity: Period could be 1 to 3 years; Locked to specific SKU; Upfront/monthly payment.
- BYO License: SQL Server, Windows Server, Software Assurance (Azure Hybrid, set up in Licensing section when creating a VM).
- Auto Start/Stop Services.

## Resources

Optimize your [Azure Costs](https://azure.microsoft.com/en-us/solutions/cost-optimization/).

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [Root README](../README.html)
