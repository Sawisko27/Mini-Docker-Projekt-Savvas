# Anleitung Mini-Projekt Modul 168 (Aufgabe 2.3)
---  
  
## Beschreibung  
Dieses Projekt erstellt einen einfachen Webserver mit Nginx, verpackt in einem Docker-Container. Die Webseite wird als statische HTML-Datei ausgeliefert. Das gesamte Projekt wird auf einer Ubuntu Linux VM ausgeführt.  
  
## Voraussetzungen
- Docker muss installiert sein  
- Port 8080 muss frei sein
  
## Schritte zur Ausführung  
### 1. Verzeichnis erstellen  
```mkdir ~/mini-projekt-nginx``` - Erstellt das Verzeichnis  
```cd ~/mini-projekt-nginx``` - Wechselt zum neuen Verzeichnis  
  
### 2. HTML-Datei erstellen  
```mkdir html
echo '<!DOCTYPE html>
<html>
<head><title>Mein Docker Nginx-Server</title></head>
<body><h1>Hallo, Docker-Welt!</h1></body>
</html>' > html/index.html
```
Anmerkung: Der Text kann aber beliebig angepasst werden.  
  
### 3. Dockerfile erstellen  
Zuerst muss das File erstellt und bearbeitet werden:  
```nano Dockerfile```  
  
Das File soll folgenden Inhalt haben, das Label "maintainer" sollte allerdings noch angepasst werden:  
```# Basis-Image mit Ubuntu 20.04
FROM ubuntu:20.04

# Maintainer-Info
LABEL maintainer "savvas.ioannidis@edu.gbssg.ch"

# Nginx installieren und aufräumen
RUN apt-get update && \
    apt-get install -y nginx && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# HTML-Dateien in das Webserver-Verzeichnis kopieren
COPY html /var/www/html

# Port 80 für den Webserver freigeben
EXPOSE 80

# Standardbefehl: Nginx starten
CMD ["nginx", "-g", "daemon off;"]
```  
  
### 4. Docker-Image bauen  
Mit folgenden Befehl:  
```docker build -t mini-nginx . ```  
  
### 5. Docker-Container starten  
Der Container soll unter Port 8080 gestartet werden:  
```docker run -d -p 8080:80 --name my-nginx mini-nginx```  
  
### 6. Webseite im Browser öffnen  
Zum Schluss muss die Webseite im Browser mit der URL ```http://localhost:8080``` geöffnet werden  
  
## Endresultat  
Wenn das alles geklappt hat, sollte das Ganze am Schluss so aussehen:  
  
![image](https://github.com/user-attachments/assets/a83b24d1-4356-4d75-8a20-d127d38e93a0)
