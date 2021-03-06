---
delivery_guarantee: "best_effort"
component_title: "Socket"
description: "The Vector `socket` sink streams `log` events to a socket, such as a TCP or Unix domain socket."
event_types: ["log"]
function_category: "transmit"
issues_url: https://github.com/timberio/vector/issues?q=is%3Aopen+is%3Aissue+label%3A%22sink%3A+socket%22
min_version: null
operating_systems: ["Linux","MacOS","Windows"]
service_name: "Socket"
sidebar_label: "socket|[\"log\"]"
source_url: https://github.com/timberio/vector/tree/master/src/sinks/socket.rs
status: "prod-ready"
title: "Socket Sink"
unsupported_operating_systems: []
---

The Vector `socket` sink [streams](#streaming) [`log`][docs.data-model.log] events to a socket, such as a TCP or Unix domain socket.

<!--
     THIS FILE IS AUTOGENERATED!

     To make changes please edit the template located at:

     website/docs/reference/sinks/socket.md.erb
-->

## Configuration

import Tabs from '@theme/Tabs';

<Tabs
  block={true}
  defaultValue="unix"
  values={[{"label":"unix","value":"unix"},{"label":"tcp","value":"tcp"},{"label":"unix (adv)","value":"unix-adv"},{"label":"tcp (adv)","value":"tcp-adv"}]}>

import TabItem from '@theme/TabItem';

<TabItem value="unix">

import CodeHeader from '@site/src/components/CodeHeader';

<CodeHeader fileName="vector.toml" learnMoreUrl="/docs/setup/configuration/"/ >

```toml
[sinks.my_sink_id]
  mode = "tcp" # required
  path = "/path/to/socket" # required, required when mode = "unix"
```

</TabItem>
<TabItem value="tcp">

<CodeHeader fileName="vector.toml" learnMoreUrl="/docs/setup/configuration/"/ >

```toml
[sinks.my_sink_id]
  address = "92.12.333.224:5000" # required, required when mode = "tcp"
  mode = "tcp" # required
```

</TabItem>
<TabItem value="unix-adv">

<CodeHeader fileName="vector.toml" learnMoreUrl="/docs/setup/configuration/"/ >

```toml
[sinks.my_sink_id]
  # General
  mode = "tcp" # required
  path = "/path/to/socket" # required, required when mode = "unix"

  # Buffer
  buffer.max_size = 104900000 # required, bytes, required when type = "disk"
  buffer.type = "memory" # optional, default
  buffer.max_events = 500 # optional, default, events, relevant when type = "memory"
  buffer.when_full = "block" # optional, default
```

</TabItem>
<TabItem value="tcp-adv">

<CodeHeader fileName="vector.toml" learnMoreUrl="/docs/setup/configuration/"/ >

```toml
[sinks.my_sink_id]
  # General
  address = "92.12.333.224:5000" # required, required when mode = "tcp"
  mode = "tcp" # required

  # Buffer
  buffer.max_size = 104900000 # required, bytes, required when type = "disk"
  buffer.type = "memory" # optional, default
  buffer.max_events = 500 # optional, default, events, relevant when type = "memory"
  buffer.when_full = "block" # optional, default

  # TLS
  tls.ca_path = "/path/to/certificate_authority.crt" # optional, no default
  tls.crt_path = "/path/to/host_certificate.crt" # optional, no default
  tls.enabled = false # optional, default
  tls.key_pass = "${KEY_PASS_ENV_VAR}" # optional, no default
  tls.key_path = "/path/to/host_certificate.key" # optional, no default
  tls.verify_certificate = true # optional, default
  tls.verify_hostname = true # optional, default
```

</TabItem>
</Tabs>

## Options

import Fields from '@site/src/components/Fields';

import Field from '@site/src/components/Field';

<Fields filters={true}>


<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["92.12.333.224:5000"]}
  groups={["tcp"]}
  name={"address"}
  path={null}
  relevantWhen={{"mode":"tcp"}}
  required={true}
  templateable={false}
  type={"string"}
  unit={null}
  >

### address

The address to connect to. The address _must_ include a port.


</Field>


<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[]}
  groups={["tcp","unix"]}
  name={"buffer"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"table"}
  unit={null}
  >

### buffer

Configures the sink specific buffer behavior.

<Fields filters={false}>


<Field
  common={true}
  defaultValue={500}
  enumValues={null}
  examples={[500]}
  groups={["tcp","unix"]}
  name={"max_events"}
  path={"buffer"}
  relevantWhen={{"type":"memory"}}
  required={false}
  templateable={false}
  type={"int"}
  unit={"events"}
  >

#### max_events

The maximum number of [events][docs.data-model] allowed in the buffer.


</Field>


<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[104900000]}
  groups={["tcp","unix"]}
  name={"max_size"}
  path={"buffer"}
  relevantWhen={{"type":"disk"}}
  required={true}
  templateable={false}
  type={"int"}
  unit={"bytes"}
  >

#### max_size

The maximum size of the buffer on the disk.


</Field>


<Field
  common={true}
  defaultValue={"memory"}
  enumValues={{"memory":"Stores the sink's buffer in memory. This is more performant, but less durable. Data will be lost if Vector is restarted forcefully.","disk":"Stores the sink's buffer on disk. This is less performant, but durable. Data will not be lost between restarts."}}
  examples={["memory","disk"]}
  groups={["tcp","unix"]}
  name={"type"}
  path={"buffer"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  >

#### type

The buffer's type and storage mechanism.


</Field>


<Field
  common={false}
  defaultValue={"block"}
  enumValues={{"block":"Applies back pressure when the buffer is full. This prevents data loss, but will cause data to pile up on the edge.","drop_newest":"Drops new data as it's received. This data is lost. This should be used when performance is the highest priority."}}
  examples={["block","drop_newest"]}
  groups={["tcp","unix"]}
  name={"when_full"}
  path={"buffer"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  >

#### when_full

The behavior when the buffer becomes full.


</Field>


</Fields>

</Field>


<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={[]}
  groups={[]}
  name={"encoding"}
  path={null}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"table"}
  unit={null}
  >

### encoding

Configures the encoding specific sink behavior.

<Fields filters={false}>


<Field
  common={true}
  defaultValue={null}
  enumValues={{"json":"Each event is encoded into JSON and the payload is represented as a JSON array.","text":"Each event is encoded into text via the `message` key and the payload is new line delimited."}}
  examples={["json","text"]}
  groups={[]}
  name={"codec"}
  path={"encoding"}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"string"}
  unit={null}
  >

#### codec

The encoding codec used to serialize the events before outputting.


</Field>


<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[["timestamp","message","host"]]}
  groups={[]}
  name={"except_fields"}
  path={"encoding"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"[string]"}
  unit={null}
  >

#### except_fields

Prevent the sink from encoding the specified labels.


</Field>


<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[["timestamp","message","host"]]}
  groups={[]}
  name={"only_fields"}
  path={"encoding"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"[string]"}
  unit={null}
  >

#### only_fields

Limit the sink to only encoding the specified labels.


</Field>


<Field
  common={false}
  defaultValue={"rfc3339"}
  enumValues={{"rfc3339":"Format as an RFC3339 string","unix":"Format as a unix timestamp, can be parsed as a Clickhouse DateTime"}}
  examples={["rfc3339","unix"]}
  groups={[]}
  name={"timestamp_format"}
  path={"encoding"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  >

#### timestamp_format

How to format event timestamps.


</Field>


</Fields>

</Field>


<Field
  common={true}
  defaultValue={true}
  enumValues={null}
  examples={[true,false]}
  groups={[]}
  name={"healthcheck"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"bool"}
  unit={null}
  >

### healthcheck

Enables/disables the sink healthcheck upon start. See [Health Checks](#health-checks) for more info.


</Field>


<Field
  common={true}
  defaultValue={null}
  enumValues={{"tcp":"TCP Socket.","unix":"Unix Domain Socket."}}
  examples={["tcp","unix"]}
  groups={["tcp","unix"]}
  name={"mode"}
  path={null}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"string"}
  unit={null}
  >

### mode

The type of socket to use.


</Field>


<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["/path/to/socket"]}
  groups={["unix"]}
  name={"path"}
  path={null}
  relevantWhen={{"mode":"unix"}}
  required={true}
  templateable={false}
  type={"string"}
  unit={null}
  >

### path

The unix socket path. This should be the absolute path.


</Field>


<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[]}
  groups={["tcp"]}
  name={"tls"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"table"}
  unit={null}
  >

### tls

Configures the TLS options for connections from this sink.

<Fields filters={false}>


<Field
  common={true}
  defaultValue={false}
  enumValues={null}
  examples={[false,true]}
  groups={["tcp"]}
  name={"enabled"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"bool"}
  unit={null}
  >

#### enabled

Enable TLS during connections to the remote.


</Field>


<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={["/path/to/certificate_authority.crt"]}
  groups={["tcp"]}
  name={"ca_path"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  >

#### ca_path

Absolute path to an additional CA certificate file, in DER or PEM format (X.509).


</Field>


<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["/path/to/host_certificate.crt"]}
  groups={["tcp"]}
  name={"crt_path"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  >

#### crt_path

Absolute path to a certificate file used to identify this connection, in DER or PEM format (X.509) or PKCS#12. If this is set and is not a PKCS#12 archive, [`key_path`](#key_path) must also be set.


</Field>


<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={["${KEY_PASS_ENV_VAR}","PassWord1"]}
  groups={["tcp"]}
  name={"key_pass"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  >

#### key_pass

Pass phrase used to unlock the encrypted key file. This has no effect unless [`key_path`](#key_path) is set.


</Field>


<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["/path/to/host_certificate.key"]}
  groups={["tcp"]}
  name={"key_path"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  >

#### key_path

Absolute path to a certificate key file used to identify this connection, in DER or PEM format (PKCS#8). If this is set, [`crt_path`](#crt_path) must also be set.


</Field>


<Field
  common={false}
  defaultValue={true}
  enumValues={null}
  examples={[true,false]}
  groups={["tcp"]}
  name={"verify_certificate"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"bool"}
  unit={null}
  >

#### verify_certificate

If `true` (the default), Vector will validate the TLS certificate of the remote host. Do NOT set this to `false` unless you understand the risks of not verifying the remote certificate.


</Field>


<Field
  common={false}
  defaultValue={true}
  enumValues={null}
  examples={[true,false]}
  groups={["tcp"]}
  name={"verify_hostname"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"bool"}
  unit={null}
  >

#### verify_hostname

If `true` (the default), Vector will validate the configured remote host name against the remote host's TLS certificate. Do NOT set this to `false` unless you understand the risks of not verifying the remote hostname.


</Field>


</Fields>

</Field>


</Fields>

## How It Works

### Buffers

import SVG from 'react-inlinesvg';

<SVG src="/img/buffers.svg" />

The `socket` sink buffers events as shown in
the diagram above. This helps to smooth out data processing if the downstream
service applies backpressure. Buffers are controlled via the
[`buffer.*`](#buffer) options.

### Environment Variables

Environment variables are supported through all of Vector's configuration.
Simply add `${MY_ENV_VAR}` in your Vector configuration file and the variable
will be replaced before being evaluated.

You can learn more in the [Environment Variables][docs.configuration#environment-variables]
section.

### Health Checks

Health checks ensure that the downstream service is accessible and ready to
accept data. This check is performed upon sink initialization.
If the health check fails an error will be logged and Vector will proceed to
start.

#### Require Health Checks

If you'd like to exit immediately upon a health check failure, you can
pass the `--require-healthy` flag:

```bash
vector --config /etc/vector/vector.toml --require-healthy
```

#### Disable Health Checks

If you'd like to disable health checks for this sink you can set the
`healthcheck` option to `false`.

### Streaming

The `socket` sink streams data on a real-time
event-by-event basis. It does not batch data.


[docs.configuration#environment-variables]: /docs/setup/configuration/#environment-variables
[docs.data-model.log]: /docs/about/data-model/log/
[docs.data-model]: /docs/about/data-model/
