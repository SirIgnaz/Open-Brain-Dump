# Herkunft

Der Name "Bogon" leitet sich von dem Wort "bogus" ab was "gefälscht, falsch, unsinnig" bedeutet.
Darauf entstand in den 90ern der Begriff Bogon was wiederrum "Falsche IP Adresse /Route" bedeutet.

Bogon = "bogus networks"

# Warum sind Bogons problematisch?

- Von außen: Wenn du von deinem WAN-Interface plötzlich Traffic mit Absender 192.168.x.x oder 10.x.x.x bekommst → Spoofing oder Angriffsversuch.
- Nach außen: Wenn Geräte aus deinem LAN versuchen, mit solchen Adressen ins Internet zu sprechen → meistens Fehlkonfig oder Malware.
  
Darum filtert man Bogons an der Firewall frühzeitig weg.

# IPv4-Bogons (nicht routbar im Internet)

| Netz                 | Zweck                               | Referenz                                                                                                         |
| -------------------- | ----------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `0.0.0.0/8`          | „This“ Network, ungültig als Quelle | [RFC 1122 §3.2.1.3](https://datatracker.ietf.org/doc/html/rfc1122)                                               |
| `10.0.0.0/8`         | Private-Use                         | [RFC 1918](https://datatracker.ietf.org/doc/html/rfc1918)                                                        |
| `100.64.0.0/10`      | Carrier-Grade NAT (CGNAT)           | [RFC 6598](https://datatracker.ietf.org/doc/html/rfc6598)                                                        |
| `127.0.0.0/8`        | Loopback                            | [RFC 1122 §3.2.1.3](https://datatracker.ietf.org/doc/html/rfc1122)                                               |
| `169.254.0.0/16`     | Link-Local (APIPA)                  | [RFC 3927](https://datatracker.ietf.org/doc/html/rfc3927)                                                        |
| `172.16.0.0/12`      | Private-Use                         | [RFC 1918](https://datatracker.ietf.org/doc/html/rfc1918)                                                        |
| `192.0.0.0/24`       | IETF Protocol Assignments           | [RFC 6890](https://datatracker.ietf.org/doc/html/rfc6890)                                                        |
| `192.0.2.0/24`       | TEST-NET-1 (Dokumentation)          | [RFC 5737](https://datatracker.ietf.org/doc/html/rfc5737)                                                        |
| `192.88.99.0/24`     | 6to4 Relay (deprecated)             | [RFC 7526](https://datatracker.ietf.org/doc/html/rfc7526)                                                        |
| `192.168.0.0/16`     | Private-Use                         | [RFC 1918](https://datatracker.ietf.org/doc/html/rfc1918)                                                        |
| `198.18.0.0/15`      | Benchmarking/Test                   | [RFC 2544](https://datatracker.ietf.org/doc/html/rfc2544)                                                        |
| `198.51.100.0/24`    | TEST-NET-2 (Dokumentation)          | [RFC 5737](https://datatracker.ietf.org/doc/html/rfc5737)                                                        |
| `203.0.113.0/24`     | TEST-NET-3 (Dokumentation)          | [RFC 5737](https://datatracker.ietf.org/doc/html/rfc5737)                                                        |
| `224.0.0.0/4`        | Multicast                           | [RFC 5771](https://datatracker.ietf.org/doc/html/rfc5771)                                                        |
| `240.0.0.0/4`        | Reserved for Future Use             | [RFC 1112 §4](https://datatracker.ietf.org/doc/html/rfc1112)                                                     |
| `255.255.255.255/32` | Broadcast                           | [RFC 919](https://datatracker.ietf.org/doc/html/rfc919), [RFC 922](https://datatracker.ietf.org/doc/html/rfc922) |

# IPv6-Bogons

| Netz            | Zweck                      | Referenz                                                  |
| --------------- | -------------------------- | --------------------------------------------------------- |
| `::/128`        | Unspecified Address        | [RFC 4291](https://datatracker.ietf.org/doc/html/rfc4291) |
| `::1/128`       | Loopback                   | [RFC 4291](https://datatracker.ietf.org/doc/html/rfc4291) |
| `::ffff:0:0/96` | IPv4-Mapped IPv6           | [RFC 4291](https://datatracker.ietf.org/doc/html/rfc4291) |
| `64:ff9b::/96`  | IPv4/IPv6 Translation      | [RFC 6052](https://datatracker.ietf.org/doc/html/rfc6052) |
| `100::/64`      | Discard-Only               | [RFC 6666](https://datatracker.ietf.org/doc/html/rfc6666) |
| `2001:db8::/32` | Documentation (TEST-NET)   | [RFC 3849](https://datatracker.ietf.org/doc/html/rfc3849) |
| `fc00::/7`      | Unique Local Address (ULA) | [RFC 4193](https://datatracker.ietf.org/doc/html/rfc4193) |
| `fe80::/10`     | Link-Local                 | [RFC 4291](https://datatracker.ietf.org/doc/html/rfc4291) |
| `ff00::/8`      | Multicast                  | [RFC 4291](https://datatracker.ietf.org/doc/html/rfc4291) |

