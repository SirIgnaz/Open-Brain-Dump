# 1. FastTrack

- Beschleunigt Verbindungen massiv (CPU-Entlastung).
- Aber: Alles, was durch FastTrack geht, überspringt Queues, Mangle, manche Firewall-Regeln.

⇒ Lösung: FastTrack nur nutzen, wenn du kein komplexes QoS brauchst, oder gezielt Ausnahmen setzen.

# 2. Firewall-Chains

- Input = Traffic zum Router selbst (z. B. Ping auf Router-IP, Winbox, SSH).
- Forward = Traffic durch den Router hindurch (LAN → WAN, VLAN → VLAN).
- Output = Traffic, den der Router selbst erzeugt (z. B. DNS-Query, NTP).
  
👉 Viele verwechseln input und forward, dadurch „verschwinden“ Pakete.

# 3. RAW-Tabelle

- Sitzt vor Conntrack (Connection Tracking).
- Gut, um Spam/Scans/Bogons sehr früh zu droppen.
- Aber: RAW-Regeln wie „drop rest“ können leicht legitimen Traffic killen, wenn man nicht aufpasst.

# 4. Bridge VLAN Filtering

- CPU (=Bridge) muss als tagged in jedem VLAN eingetragen sein, sonst sieht der Router den Traffic nicht.
- Ports immer sauber als Access (pvid=x) oder Trunk (tagged) definieren.
- Häufiger Fehler: VLAN-Interfaces (vlan10) in die Bridge packen – gehört da nicht rein.

# 5. Address-Lists

- Sehr mächtig: Kannst damit ganze Gruppen von IPs/Subnetzen definieren und in Firewall/NAT/Mangle nutzen.
- Auch dynamisch (per Scripte, per Timeout).
- Beispiel: „ssh_bruteforce“ Liste, die sich automatisch füllt und 24h geblockt wird.

# 6. NAT vs. Routing

- NAT ist nur für Traffic Richtung WAN nötig.
- Interne VLANs brauchen kein NAT, nur Routing + Firewall.

# 7. Default Config Stolpersteine

- Manche Boards kommen mit „defconf“, die schon VLANs oder Firewall hat.
- Oft besser: von Null starten und gezielt eigene Regeln aufbauen.
- Sonst mischen sich alte defconf-Einträge rein (z. B. in RAW).

# 8. IP Services

- Standardmäßig läuft fast alles (www, ftp, telnet, api, ssh, winbox).
- Best Practice: nur die Dienste aktivieren, die du brauchst, und Zugriff auf eine Address-List einschränken.

# 9. Routing Besonderheiten

- Router kennt nur Netze, die als IP-Adresse auf einem Interface konfiguriert sind oder die in /ip route stehen.
- Kein Auto-Magic wie bei vielen Consumer-Routern.

⇒ Wer VLANs anlegt, braucht auch immer IP-Adressen darauf (für L3).

# 10. Terminologie

- „Bridge“ bei MikroTik = Switch.
- „Switch“ bei MikroTik = der Hardware-Switch-Chip (Low-Level).

Das sorgt bei Einsteigern oft für Verwirrung.
