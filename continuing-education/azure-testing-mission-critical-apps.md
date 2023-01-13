# Continuous Testing and Validation of Azure Workloads

Host: Scott Hanselman

Guests:

- Heyko Oelrichs
- Martin Simicek

*Note*: I need to review how to support locale-specific character sets in markdown.

## Overview

Increase confidence in things you build in Azure by continuously evaluating the Azure App.

## Content

Continuous Validation

- Azure Pipelines -> Deploy -> Test
- Tests include Azure Load Testing, targeting Azure Front Door (edge or ingress/egress boundary?).
- Tests include Azure Chaos Studio, targeting AKC clusters.
- Unittests and integration tests are still part of the pipeline.
- Simulated failures are injected in an automated way to the deployed environment.

Azure DevOps pipeline definitions can be customized:

- YAML files, of course.
- UI Pipeline "Run" modal window.

Implementation Notes:

- This is an advanced topic, and takes some time and is challenging to configure.
- Many steps are involved to get a true test of your Azure App.

Application Insights can be helpful in viewing the Azure App status and statistics.

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
