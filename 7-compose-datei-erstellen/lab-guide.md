# Compose-Datei erstellen

- **Ziel:** Eine Multi-Container-Anwendung definieren und sicherstellen, dass Services miteinander kommunizieren können.

## Anleitung

1. Erstelle einen neuen Ordner `compose-example`.
2. Wechsle in diesen Ordner.
3. Erstelle eine neue Datei `docker-compose.yml` mit folgendem Inhalte:

   ```yaml
   version: '3'
   services:
   web:
     image: nginx
     ports:
       - '80:80'
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

4. Erklärung der Konfiguration:
   - `web`-Service:
     - Lädt ein `nginx`-Image.
     - Exponiert den Port `80` auf dem Host.
     - Enthält eine Umgebungsvariable `DB_HOST`, die den Hostnamen des Datenbankcontainers (`db`) angibt.
     - Hat eine Abhängigkeit (`depends_on`) von `db`, was bedeutet, dass der Datenbank-Service zuerst gestartet wird.
   - `db`-Service:
     - Lädt ein `mysql`-Image.
     - Setzt die Datenbank-Umgebung mit einem Root-Passwort (`MYSQL_ROOT_PASSWORD`) und einem standardmäßigen Datenbanknamen (`MYSQL_DATABASE`).
5. Starte die Anwendung, während du noch im Ordner bist, den wir eben grade erstellt haben:

   ```shell
   docker-compose up -d
   ```

6. Überprüfe, ob beide Services laufen:

   ```shell
   docker-compose ps
   ```

7. Zeige die Logs der Container an:

   ```shell
   docker-compose logs
   ```

8. Der web-Container kann die db-Container-Adresse über den Namen db auflösen, da Docker Compose automatisch ein internes Netzwerk erstellt, in dem alle Services erreichbar sind.
