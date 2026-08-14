# Step 6: Datadog Monitoring & Alerting
## Objective

A Datadog monitoring and notification workflow was configured to monitor CPU utilization and send alerts to Slack.

## 1. Create Notification Rule

A notification rule was created to deliver monitoring alerts to the Slack channel.

## 2. Create CPU Utilization Monitor

A CPU Utilization monitor was configured.

The monitor tracks CPU utilization on the monitored EC2 instances.

## 3. Attach the Notification Rule

The CPU monitor was attached to the notification rule.

## 4. Generate High CPU Load

A high CPU workload was generated to test the monitoring system.

## Validation

Verify that:

* Datadog receives the CPU metrics.
* The monitor detects the configured threshold.
* The monitor triggers.
* The notification rule executes.
* Slack receives the alert.

