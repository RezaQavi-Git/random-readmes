# What is Prometheus

Prometheus is an open source monitoring solution written in Go that collects metrics data and stores that data in a time series database.
Prometheus scrapes metrics data from HTTP endpoints and then pushes that data into a database that uses a multidimensional model.

## How Prometheus work

1. Data collection and retrieval: Prometheus follows a pull-based model, where it periodically scrapes data from the targets (applications, services or infrastructure components) that are instrumented with its client libraries. The targets expose metrics and endpoints, allowing Prometheus to gather relevant information.
2. Data storage: The collected metrics are stored in a time-series database, providing a historical record of system performance over time.
3. Service discovery: Prometheus utilizes discovery mechanisms to ensure that new instances are automatically detected and monitored without manual intervention.

# PromQL

PromQL, which is short for Prometheus Query Language, is a functional tool which features allows you to select and aggregate time series data. It’s a flexible, powerful language that allows you to slice and dice your data however you need.

# Metrics

### Metric names and labels

`Metric names`:
Specify the general feature of a system that is measured

`Metric labels`:
Enable Prometheus's dimensional data model to identify any given combination of labels for the same metric name. It identifies a particular dimensional instantiation of that metric

### Best Practice

For detail [link](https://prometheus.io/docs/practices/naming/)

- As a rule of thumb, either the sum() or the avg() over all dimensions of a given metric should be meaningful.
- Do not put the label names in the metric name, as this introduces redundancy and will cause confusion if the respective labels are aggregated away.

**CAUTION**: _Remember that every unique combination of key-value label pairs represents a new time series, which can dramatically increase the amount of data stored. Do not use labels to store dimensions with high cardinality (many different label values), such as user IDs, email addresses, or other unbounded sets of values_

### Types

The Prometheus client libraries offer four core metric types.

#### Counter

A counter is a cumulative metric that represents a single monotonically increasing counter whose value can only increase or be reset to zero on restart. For example, you can use a counter to represent the number of requests served, tasks completed, or errors.

#### Gauge

A gauge is a metric that represents a single numerical value that can arbitrarily go up and down.

- Gauges are typically used for measured values like temperatures or current memory usage, but also "counts" that can go up and down, like the number of concurrent requests.

#### Histogram

A histogram samples observations (usually things like request durations or response sizes) and counts them in configurable buckets. It also provides a sum of all observed values.
A histogram with a base metric name of **_basename_** exposes multiple time series during a scrape:

- cumulative counters for the observation buckets, exposed as _basename_bucket{le="upper inclusive bound"}_
- the total sum of all observed values, exposed as **basename_sum**
- the count of events that have been observed, exposed as **basename_count** (identical to **basename_bucket{le="+Inf"}** above)

#### Apdex score

Random maybe useful document [Apdex](https://en.wikipedia.org/wiki/Apdex)
A straight-forward use of histograms (but not summaries) is to count observations falling into particular buckets of observation values.

- You might have an SLO to serve 95% of requests within 300ms. In that case, configure a histogram to have a bucket with an upper limit of 0.3 seconds.

  example:

  ```
  sum(rate(http_request_duration_seconds_bucket{le="0.3"}[5m])) by (job)
  /
  sum(rate(http_request_duration_seconds_count[5m])) by (job)
  ```

#### Quantiles

The φ-quantile is the observation value that ranks at number φ\*N among the N observations. Examples for φ-quantiles: The 0.5-quantile is known as the median. The 0.95-quantile is the 95th percentile.

- Let us return to the SLO of serving 95% of requests within 300ms. This time, you do not want to display the percentage of requests served within 300ms, but instead the 95th percentile, i.e. the request duration within which you have served 95% of requests. To do that, you can either configure a summary with a 0.95-quantile and (for example) a 5-minute decay time, or you configure a histogram with a few buckets around the 300ms mark, e.g. {le="0.1"}, {le="0.2"}, {le="0.3"}, and {le="0.45"}. If your service runs replicated with a number of instances, you will collect request durations from every single one of them, and then you want to aggregate everything into an overall 95th percentile.

  example:

  `histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (le))`

# Functions

For detailed documentation use [link](https://prometheus.io/docs/prometheus/latest/querying/functions/).

# References

- [newrelic.com](https://newrelic.com/blog/best-practices/what-is-prometheus)
- [prometheus.io](https://prometheus.io/)
