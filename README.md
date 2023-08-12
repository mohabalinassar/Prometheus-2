# Prometheus-2

## 1- How do I trigger a Prometheus alert?
In Prometheus, alerts are triggered based on defined alerting rules that monitor certain conditions or thresholds in your metrics data. When these conditions are met, Prometheus generates alerts and sends them to an alert manager, which then takes further actions, such as sending notifications to designated recipients. Here's a general overview of the process to trigger a Prometheus alert:

* Define Alerting Rules: In your Prometheus configuration, you define alerting rules using PromQL (Prometheus Query Language). These rules specify the conditions that need to be met for an alert to be triggered. For example, you might define a rule to trigger an alert when the CPU usage of a server exceeds a certain threshold for a specified duration.
   * Open your Prometheus configuration file (prometheus.yml) for editing.
   * Define alerting rules using PromQL syntax. Each rule consists of a name, condition, labels, and annotations. For example:
    ```shell
    rule_files:
      - alert.rules.yml
    ```
      
* Configure Alertmanager: Configure the Prometheus Alertmanager to receive alerts from Prometheus and handle alert notifications. This can involve specifying notification methods (like email, Slack, PagerDuty, etc.) and their corresponding settings.

*Alert Evaluation: Prometheus periodically evaluates the defined alerting rules against the collected metrics data. If the conditions of a rule are met, the rule's alert state changes to firing.

*Alert Generation: When an alerting rule transitions to the firing state, Prometheus generates an alert instance containing details about the alert, such as the rule name, labels, and annotations.

*Alert Forwarding: The generated alert instances are forwarded to the conIn the Prometheus configuration (prometheus.yml), specify the Alertmanager's URL.figured Alertmanager.

*Alert Handling: The Alertmanager receives the alerts and applies grouping and deduplication based on labels. It then sends notifications to the specified external services (like email, chat, etc.) or integrates with incident management systems.

*Notification: The Alertmanager sends notifications to the designated recipients based on the configured notification methods. Recipients are informed about the triggered alerts.

*Resolution: Once the conditions of an alerting rule are no longer met (i.e., the problem is resolved), Prometheus updates the alert instance's state to resolved. The Alertmanager then sends notifications indicating that the alert has been resolved.

## 2- What is the difference between node exporter and mysql exporter ?
*Node Exporter:

Purpose: Node Exporter is a Prometheus exporter that collects and exposes hardware and operating system-level metrics from the host system where it is running. It provides insights into the overall health and resource usage of the system.
Metrics: Node Exporter collects metrics related to CPU usage, memory usage, disk space, network activity, system load, and other system-related information.
Usage: Node Exporter is used to monitor the performance and resource utilization of servers, virtual machines, containers, and other host systems.

*MySQL Exporter:

Purpose: MySQL Exporter is a Prometheus exporter specifically designed for collecting metrics from MySQL databases. It provides visibility into the performance and health of MySQL database instances.
Metrics: MySQL Exporter gathers metrics related to database activity, query performance, connections, replication status, table statistics, and other MySQL-specific information.
Usage: MySQL Exporter is used to monitor the behavior and performance of MySQL databases, helping database administrators optimize query performance, identify bottlenecks, and ensure the reliability of the database infrastructure.

## 3- What is the maximum retention period to save data in Prometheus and how to increase it ?
The maximum retention period for data storage in Prometheus is determined by the configured retention time in the Prometheus server's storage configuration. The retention time specifies how long data will be retained in the storage before being automatically pruned to free up space. By default, Prometheus retains data for 15 days.

To increase the retention period in Prometheus, you need to adjust the storage.tsdb.retention.time configuration option in your Prometheus configuration file. 

## 4- What are the different PromQL data types available in Prometheus Expression language?
PromQL (Prometheus Query Language) in Prometheus uses a limited set of data types for handling metrics and performing queries. The main data types available in PromQL are:

*Scalar: A scalar is a single numeric value representing a metric measurement. Scalars can be integers or floating-point     numbers. Examples of scalar values are metric values like CPU usage, memory usage, etc.

*Vector: A vector is a set of time series data sharing the same metric name and label set. Each time series in a vector represents a specific instance of the metric with different label values. Vectors are the primary data type used in PromQL queries.

*String: Strings are used for labeling, metadata, and other text-related operations. They are used to represent metric names and label values. For example, "http_requests_total" is a string representing a metric name.

*Instant Vector: An instant vector represents the set of time series data for a given timestamp. It contains the values of all time series at a specific point in time.

*Range Vector: A range vector represents the set of time series data over a range of time. Range vectors are often used in functions that require data over a specific time interval, such as calculating rate or sum over time.

*Matrix: A matrix is a two-dimensional data structure representing a range of data over time. It's used in range-based queries, where you specify a time window and get multiple time series for a given metric and set of labels.

## 5- How To calculate the average request duration over the last 5 minutes from a histogram ?
