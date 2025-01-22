# Verwalten der Compose-Anwendung

- **Ziel:** Die Multi-Container-Anwendung steuern und zusätzliche Verwaltungsbefehle kennenlernen.

## Anleitung

1. Liste die laufenden Dienste auf:

   ```shell
   docker-compose ps
   ```

2. Zeige die Logs der Dienste an:

   ```shell
   docker-compose logs
   ```

3. Skaliere einen Service:

   ```shell
   docker-compose up --scale web=3 -d
   ```

- **Hinweis:** Jede Instanz des Services versucht, denselben Host-Port zu belegen. Dies führt zu einem Konflikt, wenn keine dynamischen Ports oder ein Load-Balancer verwendet werden. Um Konflikte zu vermeiden, kannst du Traefik oder ein ähnliches Tool einbinden (siehe weiter unten).

4. Erweiterung mit Traefik:

- Öffne die `docker-compose.yml`, um diese mit Traefik zu erweitern.
- Hier ist ein einfaches Beispiel für die Integration:

```yaml
version: '3'
services:
  traefik:
    image: traefik:v2.7
    ports:
      - '80:80'
    command:
      - '--api.insecure=true'
      - '--providers.docker'
      - '--entrypoints.web.address=:80'
    volumes:
      - '/var/run/docker.sock:/var/run/docker.sock:ro'
  web:
    image: nginx
    labels:
      - 'traefik.http.routers.web.rule=Host(`localhost`)'
      - 'traefik.http.services.web.loadbalancer.server.port=80'
    environment:
      - DB_HOST=db
    depends_on:
      - db
  db:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: example
      MYSQL_DATABASE: workshop
```

5. Führe `docker-compose up -d` aus.
6. Teste die Erreichbarkeit mit `curl http://localhost`.
7. Skaliere einen Service:

   ```shell
   docker-compose up --scale web=3 -d
   ```

8. Überprüfe mit `docker-compose ps` ob nun drei Instanzen des Web-Servers laufen.
9. Teste die Erreichbarkeit mit `curl http://localhost`.
10. Stoppe und entferne die Anwendung:

- Entferne alle laufenden Container, Netzwerke und Volumes der Anwendung:

  ```shell
  docker-compose down
  ```

5. Bereinige ungenutzte Ressourcen:

- Falls du sicherstellen möchtest, dass keine ungenutzten Images, Volumes oder Netzwerke verbleiben, nutze:

  ```shell
  docker system prune -f
  ```

**Warnung:** Dieser Befehl entfernt alle nicht verwendeten Docker-Ressourcen.
