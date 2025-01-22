# Erstellen eines Dockerfiles

- **Ziel:** Ein eigenes Dockerfile erstellen und ein Image bauen.

## Anleitung

1. Erstelle einen neuen Ordner für unseren Container.
   Nenne den Ordner `first-container`.
2. Wechsle in diesen Ordner.
3. Erstelle eine neue Datei namens `Dockerfile`.
4. Öffne diese Datei mit `vi` oder einem ähnlichen Editor.
5. Füge folgenden Inhalt ein:

   ```Dockerfile
   FROM nginx:alpine
   LABEL maintainer="workshop@example.com"
   LABEL purpose="Docker Praxiseinstieg"
   COPY index.html /usr/share/nginx/html/index.html
   ```

6. Erstelle eine Datei index.html im selben Verzeichnis mit folgendem Inhalt:

   ```html
   <!DOCTYPE html>
   <html lang="de">
     <head>
       <meta charset="UTF-8" />
       <title>Willkommen</title>
     </head>
     <body>
       <h1>Hallo Welt</h1>
     </body>
   </html>
   ```

7. Baue das Docker-Image:

   ```shell
   docker build -t first-container .
   ```

8. Starte einen Container basierend auf deinem Image und mappe den Port 80:

   ```shell
   docker run -d --name first-container -p 80:80 first-container
   ```

9. Fällt dir etwas auf, während der Container startet? Der Container muss nicht runtergeladen werden, da er lokal gespeichert ist.
10. Teste den laufenden Container mit `curl`. Rufe den Webserver auf:

    ```shell
    curl http://localhost
    ```

11. Liste die laufenden Images auf, um dein neues Image zu sehen:

    ```shell
    docker ps
    ```

12. Liste die vorhandenen Images auf, um dein neues Image zu sehen:

    ```shell
    docker images
    ```

13. Stoppe dein Container mit `docker stop`..
14. Lösche den Container mit `docker rm`.
15. Lösche dein Container Image mit `docker rmi`.
