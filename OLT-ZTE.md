# OLT-ZTE.md

## Required Library

Use exactly:

```text
Cepat-Kilat-Teknologi/snmp-olt-zte
Release v3.2.0
```

Reference:

```text
https://github.com/Cepat-Kilat-Teknologi/snmp-olt-zte/releases/tag/v3.2.0
```

## Intended capabilities

```text
Multi-OLT
Per-tenant keys
Uplink auto-detect
C300
C320
SNMP
```

## Modules

```text
OLT
PON
ONU
ONU Profiles
VLAN
Optical Power
Alarms
Monitoring
```

## Flow

```text
Go OLT Adapter
 ↓
snmp-olt-zte v3.2.0
 ↓
ZTE C300/C320
```

Do not invent unsupported commands.

Verify capabilities against the actual v3.2.0 implementation.

## Data

Track:

```text
OLT
PON
ONU
Serial
Customer
Status
RX
TX
Temperature
Uptime
Alarm
```
