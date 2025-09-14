# Die Grundidee bei Mikrotik
Wer zum ersten Mal mit MikroTik-Geräten arbeitet, ist oft verwirrt, selbst mit Vorerfahrung in Netzwerken. MikroTik geht bei der Konfiguration von VLANs und Ports etwas anders vor als viele andere Hersteller.

Grundsätzlich besteht jedes Gerät aus einem RouterBoard (Hardware mit CPU und Switch-Chip), das mehrere physische Ports bereitstellt.
Die Hardware (Switch-Chip) kann Frames direkt weiterleiten (Hardware-Switching).
Routing, Firewall, NAT und Mangle greifen aber nur, wenn der Traffic über die CPU läuft.

Damit man Ports flexibel bündeln und VLANs einheitlich managen kann, legt man heute fast immer eine Bridge an.

# Die Bridge

- Eine Bridge ist wie ein virtueller Switch im Router.
- Alle Ports, die Mitglied der Bridge sind, verhalten sich wie Ports in einem Switch.
- Vorteil:
  - Zentrale Stelle für VLAN-Filtering und Port-Regeln.
  - Klare Abbildung von Access- und Trunk-Ports.
  - Die Bridge selbst CPU kann als tagged Teilnehmer in jedem VLAN eingetragen werden. So kann der Router für diese VLANs IP-Adressen haben und Traffic routen.

# Access-Port

- Access-Port = Port, an dem ein Gerät hängt, das keine VLAN-Tags versteht.
- Frames sind hier untagged.
- Mit der Einstellung pvid=<VLAN-ID> weiß die Bridge, in welches VLAN untagged Frames einsortiert werden.

# Trunk-Port

- Trunk-Port = Port, über den mehrere VLANs gleichzeitig transportiert werden.
- Typische Einsätze:
  - Uplink zu einem Switch
  - Verbindung zu einem Access Point mit mehreren SSIDs/VLANs
- Auf einem Trunk laufen alle VLANs als [802.1Q](Open-Brain-Dump/Netzwerk/Protokolle/802.1Q)-getaggte Frames.

# Warum ist die Bridge so wichtig?

1. Zentrale Schaltstelle
Alle Ports hängen an der Bridge. VLAN-Filtering entscheidet, welche Frames durchkommen.

2. CPU-Teilnahme
Damit der Router selbst (Routing, Firewall, NAT) in einem VLAN sichtbar ist, muss die Bridge in diesem VLAN als tagged eingetragen sein.

3. Firewall & Routing
IP-Adressen bindet man auf VLAN-Interfaces (/interface vlan mit interface=bridgeLocal). Ohne, dass die Bridge im VLAN mitläuft, sieht die CPU den Traffic nicht.

4. Flexibilität
Du kannst Ports beliebig als Access oder Trunk definieren – zentral über die Bridge, ohne direkt den Switch-Chip konfigurieren zu müssen.
