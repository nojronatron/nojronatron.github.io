# Azure Friday Operational Best Practices

Presented by Scott 'runs everything on Azure AppService' Hanselman.

Guest: Byron Tardif.

## Overview

What is going on with your App Service?

What do you do if something goes wrong?

CloudShell:

- AzCLI is built-in.
- Logstream via AzCli to connect to logs at the AppService instance.
- Can connect to Production or Staging instance.

Azure UI - Metrics:

- Look at Deployment Slots -> Staging (or wherever it is happening).
- Look at Metrics to see Errors raised by the instance.
- Set an alert on a particular Metric.
- Alerts can send an Email based on thresholds.
- Static or Dynamic Alerting can be configured. Dynamic is recommended to avoid alert traffic volume issues.
- Alerting could also call a web-hook or send a text message (instead of email or watching via Azure Portal).

Metrics Splitting:

- Allow viewing instance-specific errors.
- Multi-instance applications are common, so which one is logging the errors? This hones in on those views.
- Multi-instance-capable applications use cookie-affinity, so even a single-instance within an multi-instance deployment will still use the cookie, so that additional instances coming online don't change existing instance behavior.

Stateful vs Stateless:

- Stateful applications should have same conversations context with same session clients. Could be dangerous to make changes while live due to state-corruption risk.
- Stateless apps don't maintain state at any time, but are easier to effect changes while the app is online.

Log Analytics:

- Write queries to look for entries in the App Service Logs.
- Azure Log Analytics can be connected to Splunk and other log analyzers!
- There are *many* log categories and individual logs, so it would be a good idea to get familiar with this (Azure doesn't solve that problem for you).
- Code-generated output logs are also captured in Azure App Service Logs.
- Alerts can be generated based on Logs! Custom message to email, text, webhook, etc. Alert severity can be selected.

Friends Dont Let Friends Publish Directly To Production:

- Enable GitHub Actions to detect PUSH and deal with build and deploy.
- Ensure Actions output changes to a Staging server/farm.
- Commit and Push changes to your remote repo and GH Actions takes care of the rest.
- Test the Staged app to validate fix in place and ensure it is ready for PR to Production.
- Open Deployment Slots and "swap" Staging with Production and Azure takes care of moving affinity to the now-production code.
- Deployment Slots has a 'panic button' to reverse-swap if things are still (or more) broken.

Auto Heal:

- Log Analytic Queries are used to detect a failure situation in Production Slot.
- Custom Auto-Heal Rules define: Conditions (query hit), Actions (recycle app, etc), and Override when Action executes (custom post-action).

## Footer

Return to [Conted Index](./conted-index.html)

Return to [Root README](../README.html)
