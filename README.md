# snmpwalk.exe

SNMPv3 CLI walk tool for Windows.

**Version:** 1.1.0

## Features

- SNMPv3 USM authentication: SHA, SHA224, SHA256, **SHA384**, **SHA512**
- AES/AES128/AES192/AES256 privacy encryption
- Multi-host scanning support
- GET, SET, BULK operations

## Usage

```
snmpwalk.exe -H <host> [options]
```

### Examples

```bash
# Basic walk
snmpwalk.exe -H 192.168.1.254 -u admin -a SHA256 -A password -x AES256 -X password

# Single OID GET
snmpwalk.exe -H 192.168.1.254 -u admin -a SHA256 -A password -x AES256 -X password -o 1.3.6.1.2.1.1.1.0

# Debug mode
snmpwalk.exe -H 192.168.1.254 -u admin -a SHA256 -A password -x AES256 -X password -d
```

### Options

| Flag | Description |
|------|-------------|
| `-H` | SNMP device address (required) |
| `-p` | UDP port (default 161) |
| `-u` | Username (SNMPv3) |
| `-o` | Starting OID (default 1.3.6.1) |
| `-t` | Timeout in seconds (default 5) |
| `-r` | Retry count (default 3) |
| `-d` | Enable debug output |
| `-a` | Auth protocol: SHA, SHA224, SHA256, SHA384, or SHA512 |
| `-A` | Auth password |
| `-x` | Privacy protocol: AES, AES128, AES192, or AES256 |
| `-X` | Privacy password |
| `-v` | Show version |

## Tested Devices

| Device | Auth | Privacy | Status |
|--------|------|---------|--------|
| Linux net-snmp (Ubuntu) | SHA512 | AES256 | ✅ Working |
| Linux net-snmp (Ubuntu) | SHA256 | AES256 | ✅ Working |
| Palo Alto Network Device | SHA256 | AES256 | ✅ Working |
| Palo Alto Network Device | SHA512 | AES256 | ❌ Use SHA256 instead |

## Known Issues

- **Palo Alto Network Device** with SHA512/AES256: Use **SHA256** with AES256 for PA devices (works correctly).

### Palo Alto Configuration Recommendation

```bash
# Recommended for Palo Alto devices
snmpwalk.exe -H 192.168.1.254 -u admin -a SHA256 -A P@ssw0rd -x AES256 -X P@ssw0rd
```

## License

Built by Billy Lam with AI assistance (2026).
