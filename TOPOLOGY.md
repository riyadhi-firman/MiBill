# TOPOLOGY.md

## Mandatory Dependency Chain

```text
OLT
 ↓
PON
 ↓
ODC
 ↓
ODP
 ↓
ONU
 ↓
Customer
```

## Node Types

```text
OLT
PON
ODC
ODP
ONU
CUSTOMER
```

## Relationship

```text
OLT contains PON
PON connects ODC
ODC contains/feeds ODP
ODP connects ONU
ONU serves Customer
```

## UI

Interactive graph:

```text
zoom
pan
search
filter
select
dependency highlight
status
alarm
customer lookup
```

When selecting an ONU, highlight:

```text
OLT
PON
ODC
ODP
ONU
Customer
```

## Realtime

Update node status from monitoring events.
