---
last_modified_on: "2020-04-24"
title: Metric Event
description: A detailed guide on Vector's internal metric data model.
---

import Fields from '@site/src/components/Fields';
import Field from '@site/src/components/Field';
import Jump from '@site/src/components/Jump';
import SVG from 'react-inlinesvg';

<SVG src="/img/data-model-metric.svg" />

<!--
     THIS FILE IS AUTOGENERATED!

     To make changes please edit the template located at:

     website/docs/about/data-model/metric.md.erb
-->

## Description

A `metric` event represents a numerical operation to a time series. Operations
offered are heavily inspired by the StatsD and Prometheus models, and determine
the schema of the metric structure within Vector.

When a metric event is sent to a sink the schema will be translated into the
closest equivalent format of the sink protocol.

## Examples

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

<Tabs
  defaultValue="counter"
  select={true}
  values={[
    { label: 'Counter', value: 'counter', },
    { label: 'Gauge', value: 'gauge', },
    { label: 'Set', value: 'set', },
    { label: 'Distribution', value: 'distribution', },
    { label: 'Aggregated Histogram', value: 'aggregated_histogram', },
    { label: 'Aggregated Summary', value: 'aggregated_summary', },
  ]
}>
<TabItem value="counter">

```json
{
  "name": "login.count",
  "timestamp": "2019-11-01T21:15:47+00:00",
  "kind": "absolute",
  "tags": {
    "host": "my.host.com"
  },
  "counter": {
    "value": 24.2
  }
}
```

</TabItem>
<TabItem value="gauge">

```json
{
  "name": "memory_rss",
  "timestamp": "2019-11-01T21:15:47+00:00",
  "kind": "absolute",
  "tags": {
    "host": "my.host.com"
  },
  "gauge": {
    "value": 51200000000.0
  }
}
```

</TabItem>
<TabItem value="set">

```json
{
  "name": "user_names",
  "timestamp": "2019-11-01T21:15:47+00:00",
  "kind": "absolute",
  "tags": {
    "host": "my.host.com"
  },
  "set": {
    "values": ["bob", "sam", "ben"]
  }
}
```

</TabItem>
<TabItem value="distribution">

```json
{
  "name": "response_time_ms",
  "timestamp": "2019-11-01T21:15:47+00:00",
  "kind": "absolute",
  "tags": {
    "host": "my.host.com"
  },
  "distribution": {
    "values": [2.21, 5.46, 10.22],
    "sample_rates": [5, 2, 5]
  }
}
```

</TabItem>
<TabItem value="aggregated_histogram">

```json
{
  "name": "response_time_ms",
  "timestamp": "2019-11-01T21:15:47+00:00",
  "kind": "absolute",
  "tags": {
    "host": "my.host.com"
  },
  "aggregated_histogram": {
    "buckets": [1.0, 2.0, 4.0, 8.0, 16.0, 32.0],
    "counts": [20, 10, 45, 12, 18, 92],
    "count": 197,
    "sum": 975.2
  }
}
```

</TabItem>
<TabItem value="aggregated_summary">

```json
{
  "name": "response_time_ms",
  "timestamp": "2019-11-01T21:15:47+00:00",
  "kind": "absolute",
  "tags": {
    "host": "my.host.com"
  },
  "aggregated_summary": {
    "quantiles": [0.1, 0.25, 0.5, 0.9, 0.99, 1.0],
    "values": [2, 3, 5, 8, 9, 10],
    "count": 197,
    "sum": 975.2
  }
}
```

</TabItem>
</Tabs>

## Schema

The metric data model is comprised of 6 types: [`aggregated_histogram`](#aggregated_histogram),  [`aggregated_summary`](#aggregated_summary), [`counter`](#counter), [`distribution`](#distribution), [`gauge`](#gauge), [`set`](#set). A metric event contains a map named after one of these types at the top level. This map contains corresponding numeric values.

In addition, all kinds of metric events have the following top level fields: [`name`](#name), [`timestamp`](#timestamp), [`kind`](#kind), [`tags`](#tags).

<Fields filters={true}>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[]}
  groups={[]}
  name={"aggregated_histogram"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"struct"}
  unit={null}
  warnings={[]}
  >

### aggregated_histogram

Also called a "timer". A [`aggregated_histogram`](#aggregated_histogram) samples observations (usually
things like request durations or response sizes) and counts them in
configurable buckets. It also provides a sum of all observed values.



<Fields filters={false}>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[[1,2,5,10,25]]}
  groups={[]}
  name={"buckets"}
  path={"aggregated_histogram"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"[double]"}
  unit={null}
  warnings={[]}
  >

#### buckets

The buckets contained within this histogram.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[54]}
  groups={[]}
  name={"count"}
  path={"aggregated_histogram"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"int"}
  unit={null}
  warnings={[]}
  >

#### count

The total number of values contained within the histogram.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[[1,5,25,2,5]]}
  groups={[]}
  name={"counts"}
  path={"aggregated_histogram"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"[int]"}
  unit={null}
  warnings={[]}
  >

#### counts

The number of values contained within each bucket.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[524.0]}
  groups={[]}
  name={"sum"}
  path={"aggregated_histogram"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"double"}
  unit={null}
  warnings={[]}
  >

#### sum

The sum of all values contained within the histogram.




</Field>
</Fields>

</Field>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[]}
  groups={[]}
  name={"aggregated_summary"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"struct"}
  unit={null}
  warnings={[]}
  >

### aggregated_summary

Similar to a histogram, a summary samples observations (usually things like
request durations and response sizes). While it also provides a total count of
observations and a sum of all observed values, it calculates configurable
quantiles over a sliding time window.



<Fields filters={false}>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[54]}
  groups={[]}
  name={"count"}
  path={"aggregated_summary"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"int"}
  unit={null}
  warnings={[]}
  >

#### count

The total number of values contained within the summary.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[[0.1,0.5,0.75,1.0]]}
  groups={[]}
  name={"quantiles"}
  path={"aggregated_summary"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"[double]"}
  unit={null}
  warnings={[]}
  >

#### quantiles

The quantiles contained within the summary, where 0 ≤ quantile ≤ 1.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[524.0]}
  groups={[]}
  name={"sum"}
  path={"aggregated_summary"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"double"}
  unit={null}
  warnings={[]}
  >

#### sum

The sum of all values contained within the summary.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[[2.1,4.68,23.02,120.1]]}
  groups={[]}
  name={"values"}
  path={"aggregated_summary"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"[double]"}
  unit={null}
  warnings={[]}
  >

#### values

The values contained within the summary that align with the [`quantiles`](#quantiles).




</Field>
</Fields>

</Field>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[]}
  groups={[]}
  name={"counter"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"struct"}
  unit={null}
  warnings={[]}
  >

### counter

A single value that can _only_ be incremented or reset to zero value, it cannot
be decremented.



<Fields filters={false}>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[2.6,5.0]}
  groups={[]}
  name={"value"}
  path={"counter"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"double"}
  unit={null}
  warnings={[]}
  >

#### value

The value to increment the counter by. Can only be positive.




</Field>
</Fields>

</Field>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[]}
  groups={[]}
  name={"distribution"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"struct"}
  unit={null}
  warnings={[]}
  >

### distribution

A distribution represents a distribution of sampled values.



<Fields filters={false}>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[[12,43,25]]}
  groups={[]}
  name={"sample_rates"}
  path={"distribution"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"[int]"}
  unit={null}
  warnings={[]}
  >

#### sample_rates

The rate at which each individual value was sampled.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[[12.0,43.3,25.2]]}
  groups={[]}
  name={"values"}
  path={"distribution"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"[double]"}
  unit={null}
  warnings={[]}
  >

#### values

The list of values contained within the distribution.




</Field>
</Fields>

</Field>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[]}
  groups={[]}
  name={"gauge"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"struct"}
  unit={null}
  warnings={[]}
  >

### gauge

A gauge represents a point-in-time value that can increase and decrease.
Vector's internal gauge type represents changes to that value. Gauges should be
used to track fluctuations in values, like current memory or CPU usage.



<Fields filters={false}>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[554222.0]}
  groups={[]}
  name={"value"}
  path={"gauge"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"double"}
  unit={null}
  warnings={[]}
  >

#### value

A specific point-in-time value for the gauge.




</Field>
</Fields>

</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={{"absolute":"The value is an absolute, stand-alone value. It can be used individually.","incremental":"The value is incremental and is used to form a holistic value by merging with other incremental values. Individually it does not tell the whole story."}}
  examples={["absolute","incremental"]}
  groups={[]}
  name={"kind"}
  path={null}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### kind

The metric value kind. This determines how the value is merged downstream if
metrics are aggregated.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["login.count","response_time"]}
  groups={[]}
  name={"name"}
  path={null}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### name

The metric name.




</Field>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[]}
  groups={[]}
  name={"set"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"struct"}
  unit={null}
  warnings={[]}
  >

### set

A set represents a count of unique values, AKA the cardinality.



<Fields filters={false}>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[["unique item 1","unique item 2"]]}
  groups={[]}
  name={"values"}
  path={"set"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"[string]"}
  unit={null}
  warnings={[]}
  >

#### values

The list of unique values.




</Field>
</Fields>

</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[{"host":"my.host.com"}]}
  groups={[]}
  name={"tags"}
  path={null}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"map"}
  unit={null}
  warnings={[]}
  >

### tags

Tags that add additional metadata or context to the metric. These are simple
key/value pairs in `string` format and cannot be nested.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["2019-11-01T21:15:47+00:00"]}
  groups={[]}
  name={"timestamp"}
  path={null}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"timestamp"}
  unit={null}
  warnings={[]}
  >

### timestamp

The metric timestamp, representing when the metric was created/ingested within
Vector.




</Field>
</Fields>

## Components

<Jump to="/components/?event-types[]=metric">View all metric compatible components</Jump>



