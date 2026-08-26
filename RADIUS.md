# RADIUS.md

## Version

FreeRADIUS 3.2.x.

Recommended target:

```text
3.2.10
```

## Ports

```text
1812/udp authentication
1813/udp accounting
3799/udp CoA/Disconnect where required
```

## Architecture

```text
Go
 ↓
RadiusService
 ↓
FreeRADIUS
 ↓
MikroTik
```

## Authentication

Support applicable:

```text
PAP
CHAP
MS-CHAP
MS-CHAPv2
```

## Accounting

```text
Start
Interim
Stop
```

Default interim:

```text
5 minutes
```

## Policy

Account states:

```text
PENDING
ACTIVE
SUSPENDED
DISABLED
EXPIRED
TERMINATED
```

## Attributes

Support where applicable:

```text
Mikrotik-Rate-Limit
Mikrotik-Group
Mikrotik-Address-List
Framed-IP-Address
Framed-IP-Netmask
Framed-Pool
Session-Timeout
Idle-Timeout
Simultaneous-Use
```

## CoA

Use for:

```text
speed changes
package changes
suspension
reactivation
policy changes
```

## Security

Never log:

```text
password
shared secret
database password
API token
```

Use encrypted secret storage in the application.
