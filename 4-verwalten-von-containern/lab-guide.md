# Verwaltung eines Containers

- **Ziel:** Einen Container starten und grundlegende Verwaltungsbefehle verwenden.

## Anleitung

1. Starte einen Container im Hintergrund (detached mode):

   ```shell
   docker run -d --name webserver -p 80:80 nginx
   ```

2. Du solltest eine Fehlermeldung bekommen? Wieso?
3. Den Container gibt es unter dem Namen `webserver` schon. Versuche es einmal mit:

   ```shell
   docker start webserver
   ```

4. Zeige mit `docker ps` alle Container an.
5. Öffne die Shell im Container:

   ```shell
   docker exec -it webserver bash
   ```

   Das kann nützlich sein, um Applikationen im Container zu troubleshooten und so bspw. Labs aufzurufen.

6. Führe ein paar Befehle innerhalb vom Container aus.
7. Wie kommst du wieder aus dem Container raus?
8. Versuche es mit `exit`.
9. Stoppe und entferne den Container

   ```shell
   docker stop webserver
   docker rm webserver
   ```
