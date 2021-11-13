
- nmap APIs?
- Extra tools & Resources
- nse quick ref.
---

A quick nmap reference guide

## SUDO vs. REGULAR-USER SCANNING

Scan unprivileged: TCP Connect ( -sT default)
Scan Privileged: Stealth Scan ( -sS default)

https://nmap.org/book/man-port-scanning-techniques.html

## RANDOM SCANNING
The default scan method is random and only the 1000 "most popular" ports will be scanned.
-r for scanning ports "in consecutive order"

** Checar, "most common 1000 ports", cuáles son? Checa el archivo "/usr/share/scripts/nmap-services"; esta es una lista de puertos comunes que se actualiza constantemente (
https://nmap.org/book/man-port-specification.html
https://nmap.org/book/nmap-services.html

-sn != -sN (Ping scan, no port. -> TCP Null scan)
    Null scan: Does not set any bits (TCP flag header is 0). (El packet enviado queda como TCP none, sin información) https://nmap.org/book/man-port-scanning-techniques.html
    
-Pn     {No ping;   
  
> nmap -sL {host}           { Resolución de nombre; Host discovery. Rápido }
> nmap -A {host}            { OS + Version + script scan + traceroute }
> nmap -v -sV {host}        { Verbose + Versión }
> 
HOST DISCOVERY: 

> nmap -h                    { ayuda está seccionada por default (discovery / scan / scripts)

SERVICE/OS DETECTION:

> nmap -p http -sV {host}
> nmap -O -Pn --osscan-limit {host}     { OS detection only when 1 open & 1 closed TCP port detected (Bueno para sweeps, discovery en redes) }
> nmap -O --fuzzy -max-os-tries 1 {host}    { Aggressive OS detection }



  891  sudo nmap -sV -p 5357 192.168.1.8
  892  sudo nmap -sV -v -p 5357 192.168.1.8
  893  sudo nmap -sV -v -p 5040 192.168.1.8
  894  sudo nmap network/CIDR -sL
  895  nslookup 104.17.244.235
  896  ping -c 1 104.17.244.235
  897  host 104.17.244.235
  898  nslookup 104.17.244.235
  899  sudo nmap -sN 192.168.1.8
  900  sudo nmap -sn 192.168.1.8
  901  sudo nmap -Pn 192.168.1.8
  905  sudo nmap -p U:1-80 T:1-80 -sU -sS 192.168.1.8
  
    890  nmap -PA502 -PS502 10.10.133.243 -sV
  891  sudo nmap -sU -p 53 192.168.1.8
  892  sudo nmap -p http 192.168.1.8
  
  sudo nmap -PO[1,2,3,8] 192.168.1.8
  
>> Dudas:

P (Protocol numbers? 8 para SNMP, 0 para respuestas ICMP, etc.)

Root/not-sudo nmap type of scan?

NSE SCRIPTING NSE

> nmap -sC [host] -v                        { equivalent to --script=default }

HOST DISCOVERY:

https://nmap.org/book/man-host-discovery.html (PO, PE, PS, PA, Pn, sL, etc.)

NMAP PERFORMANCE:

-T (Timing) 0-paranoid -> 5-Insane  https://nmap.org/book/performance-timing-templates.html

IDS EVASION / SPOOFING:

-f; --mtu {val}: fragment packets (optionally w/given MTU)

-D {decoy-IP}{decoy-IP#2}{Real-IP} {dest} // Sólo los primeros packets salen con los decoy IP, la carga que genera la respuesta sale con la IP real

-S www.microsoft.com www.facebook.com
-g -> Spoof port (e.g. -g 53)

--data-string "Hello, this is the payload's string" (Parece que sólo funciona en TCP - SYN packets)

--packet-trace ** Muestra los packets, la comunicación antes de mostrar los resultados; como si estuviera corriendo tcpdump exactamente cuando se hace el escaneo

# OUTPUT FILES

-oG [Greppable format] - En 1 sola fila, en lugar de hacer el output "prettified"; host + status + info. Greppable -> Sed/Awk friendly
-oN [normal], -oA [All] - Saca 3 archivos con el nombre [file] file.gnmap (Greppable), file.nmap (Normal) y XML.
-oS Sk1dd13 - L337 l4ngu4g3. (Útil?)

* Tip: -oG - genera un output greppable sin generar un archivo. 

--append-output

### HTML OUTPUT:

**XML - HTML**

nmap -opciones- -oX nmap.xml
apt install xsltproc
xsltproc nmap.xml -o nmap.html

---

Aaron Jones - Reconnaissance
https://retro64xyz.gitlab.io/presentations/2017/01/22/introduction-to-reconnaissance/

Online tools, API, etc.
https://pentest-tools.com/features/api
http://nmap.online-domain-tools.com/
https://nmap.org/book/nse-api.html

Proxy -> VPS:
- Bullet-proof Hosting Services (BPHS)
- Offshore Hosting

Tunneling OVER DNS? C2
DNS cat2 ¿? - Registro de Dominio (C2), y DNS tunneling - C2 is the authoritative domain server. [DNS Cat2](https://github.com/iagox86/dnscat2)


