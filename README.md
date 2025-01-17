<h2><b><a href="https://1coderookie.github.io/BSB-LPB-LAN_EN">English language version of this manual now available!</a></b></h2>  
   
# Handbuch zum BSB-LPB-LAN-Adapter    

Hier findet sich eine druckerfreundliche Version dieses Handbuchs zum Projekt "BSB-LPB-LAN" als [PDF-Dokument zum Herunterladen](https://github.com/1coderookie/BSB-LPB-LAN/raw/master/Handbuch_BSB-LPB-LAN-Adapter.pdf) und Ausdrucken. Da es sich jedoch um eine auf dem Inhalt der GitHub-Pages basierende und automatisch erstellte PDF-Datei handelt, funktionieren leider nicht alle Links und Querverweise innerhalb des Dokuments.  

***Die GitHub Pages dieses Handbuchs sind [hier](https://1coderookie.github.io/BSB-LPB-LAN) verfügbar.***  
   
---  
  
Das Copyright des Handbuchs liegt bei dem Autor Ulf Dieckmann.  
  
---  
   
## BSB-LPB-LAN - Ein kurzer Überblick   

"BSB-LPB-LAN" ist ein gemeinschaftliches Hard- und Softwareprojekt, welches ursprünglich zum Ziel hatte, mittels PC/Laptop/Tablet/Smartphone Zugriff auf die Steuerungen bzw. Regler von verschiedenen Wärmeerzeugern (Öl- und Gasheizungen, Wärmepumpen, Solarthermie etc.) bestimmter Hersteller (bspw. Brötje und Elco) zu erlangen.  
Im weiteren Verlauf wäre es dann wünschenswert, Daten auszulesen, sie weiter zu verarbeiten (z.B. loggen und grafisch darstellen) oder gar Einfluss auf die Steuerung/Regelung nehmen zu können und das System in bestehende SmartHome-Systeme einzubinden.  
  
All dies ist mittlerweile umgesetzt worden:  
Mittels eines eigenbaufähigen Adapters, eines Arduino Due und eines LAN-Shields oder eines ESP32 kann nun ein entsprechender Wärmeerzeuger mit einem ["Boiler-System-Bus" (BSB)](https://1coderookie.github.io/BSB-LPB-LAN/kap02.html#21-bsb-und-lpb), einem ["Local-Process-Bus (LPB)](https://1coderookie.github.io/BSB-LPB-LAN/kap02.html#21-bsb-und-lpb) oder einer ["Punkt-zu-Punkt-Schnittstelle" (PPS)](https://1coderookie.github.io/BSB-LPB-LAN/kap02.html#22-pps-schnittstelle) kostengünstig ins heimische Netzwerk eingebunden werden. Dies sind in diesem Fall i.d.R. Systeme, bei denen ein (gebrandeter) SIEMENS-Regler zum Einsatz kommt.

Mit Hilfe des Adapters und der BSB-LAN-Software können nun unkompliziert verschiedene Funktionen, Werte und Parameter beobachtet, geloggt und bei Bedarf web-basiert gesteuert und geändert werden.
Eine optionale Einbindung in bestehende Smart-Home-Systeme wie bspw. [FHEM](https://1coderookie.github.io/BSB-LPB-LAN/kap11.html#111-fhem), [openHAB](https://1coderookie.github.io/BSB-LPB-LAN/kap11.html#112-openhab), [HomeMatic](https://1coderookie.github.io/BSB-LPB-LAN/kap11.html#113-homematic-eq3), [IoBroker](https://1coderookie.github.io/BSB-LPB-LAN/kap11.html#114-iobroker), [Loxone](https://1coderookie.github.io/BSB-LPB-LAN/kap11.html#115-loxone), [IP-Symcon](https://1coderookie.github.io/BSB-LPB-LAN/kap11.html#116-ip-symcon), [EDOMI](https://1coderookie.github.io/BSB-LPB-LAN/kap11.html#1110-edomi) oder [Home Assistant](https://1coderookie.github.io/BSB-LPB-LAN/kap11.html#1111-home-assistant) kann mittels [HTTPMOD](https://1coderookie.github.io/BSB-LPB-LAN/kap11.html#1112-einbindung-mittels-httpmod-modul), [MQTT](https://1coderookie.github.io/BSB-LPB-LAN/kap11.html#117-mqtt-influxdb-telegraf-und-grafana) oder [JSON](https://1coderookie.github.io/BSB-LPB-LAN/kap08.html#824-abrufen-und-steuern-mittels-json) erfolgen. 
Darüber hinaus ist der Einsatz des Adapters als [Standalone-Logger](https://1coderookie.github.io/BSB-LPB-LAN/kap09.html#91-verwendung-des-adapters-als-standalone-logger-mittels-bsb-lan) ohne LAN- oder Internetanbindung bei Verwendung einer microSD-Karte ebenfalls möglich.  
Zusätzlich können [Temperatur- und Feuchtigkeitssensoren](https://1coderookie.github.io/BSB-LPB-LAN/kap12.html#123-verwendung-optionaler-sensoren-dht22-und-ds18b20) angeschlossen und deren Daten ebenso geloggt und ausgewertet werden. Durch die Verwendung eines Arduino und die Möglichkeit, eigenen Code in die BSB-LAN-Software zu integrieren, bietet sich darüber hinaus ein weites Spektrum an Erweiterungsmöglichkeiten. 
    
Als erste grobe Orientierung, ob das eigene Heizungssystem komaptibel ist oder nicht, kann in der Bedienungsanleitung der Heizung nach einer Anschlussmöglichkeit für optionale Raumgeräte gesucht werden. Sind dort Raumgeräte des Typs QAA55/QAA75 als kompatibel aufgeführt (bei Brötje werden diese u.a. auch als "RGB Basic" und "RGT B Top" bezeichnet), so ist erfahrungsgemäß der Anschluss des Adapters via BSB möglich und der volle Funktionsumfang von BSB-LAN gegeben. Dies ist bei den meisten Öl-, Gas- und Wärmepumpensystemen der letzten Jahre der Fall.  
Sollten andere Raumgeräte aufgeführt sein, so kann im Kapitel "[Raumgeräte](docs/kap03.md#36-konventionelle-raumgeräte-für-die-aufgeführten-reglertypen)" im BSB-LPB-LAN-Handbuch nachgesehen werden.  
Genauen Aufschluss bietet letztlich aber immer nur die eigentliche Reglerbezeichnung.  
   
Die folgende Auflistung gibt eine grobe Übersicht über die Reglertypen, die je nach Typ des Wärmeerzeugers (Öl, Gas, WP etc.) normalerweise verbaut sind (bzw. waren) und die mittels BSB-LAN bedient werden können. Gewisse Einzel- und Spezialfälle (wie bspw. ein RVS-Regler bei einem Gasgerät) sind hier nicht berücksichtigt. Für genauere Informationen bzgl der [Reglertypen](https://1coderookie.github.io/BSB-LPB-LAN/kap03.html#32-detailliertere-auflistung-und-beschreibung-der-unterstützten-regler) und der zu verwendenden [Anschlüsse](https://1coderookie.github.io/BSB-LPB-LAN/kap02.html#23-anschluss-des-adapters) lies bitte im [BSB-LPB-LAN-Handbuch](https://1coderookie.github.io/BSB-LPB-LAN) nach.

**Gasregler:**  
- [LMU74/LMU75](https://1coderookie.github.io/BSB-LPB-LAN/kap03.html#3211-lmu-regler) und (aktuelle Generation) [LMS14/LMS15](https://1coderookie.github.io/BSB-LPB-LAN/kap03.html#3212-lms-regler), Anschluss via BSB  
- [LMU54/LMU64](https://1coderookie.github.io/BSB-LPB-LAN/kap03.html#3211-lmu-regler), Anschluss via PPS   
   
**Öl-/Solar-/Zonenregler:**  
- [RVS43/RVS63/RVS46](https://1coderookie.github.io/BSB-LPB-LAN/kap03.html#3222-rvs-regler), Anschluss via BSB / LPB  
- [RVA/RVP](https://1coderookie.github.io/BSB-LPB-LAN/kap03.html#3221-rva--und-rvp-regler), Anschluss via PPS (modellspezifisch vereinzelt auch LPB)  
   
**Wärmepumpenregler:**  
- [RVS21/RVS61](https://1coderookie.github.io/BSB-LPB-LAN/kap03.html#3222-rvs-regler), Anschluss via BSB  
   
**Weishaupt (Modell WTU):**  
- [RVS23](https://1coderookie.github.io/BSB-LPB-LAN/kap03.html#3222-rvs-regler), Anschluss via LPB    
   
   
**Um eine detailliertere Übersicht der gemeldeten Systeme einzusehen, die bisher erfolgreich mit BSB-LAN genutzt werden, folge bitte dem entsprechenden Link:**  
- **[Brötje](https://1coderookie.github.io/BSB-LPB-LAN/kap03.html#311-brötje)**
- **[Elco](https://1coderookie.github.io/BSB-LPB-LAN/kap03.html#312-elco)**
- **[weitere Hersteller (z.B. Fujitsu, Atlantic, Weishaupt)](https://1coderookie.github.io/BSB-LPB-LAN/kap03.html#313-weitere-hersteller)**      
   
  
### Die Software ist [hier](https://github.com/fredlcore/bsb_lan) verfügbar.  
