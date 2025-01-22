# Erster Container

- **Ziel:** Einen einfachen Container starten und grundlegende Befehle anwenden.

## Anleitung

1. Starte in Play with Docker einen neuen Container mit:

   ```shell
   docker run hello-world
   ```

2. Zeige alle laufenden Container an:

   ```shell
   docker ps
   ```

3. Wieso wird dir kein laufender Container angezeigt?
4. Starte einen Container im Hintergrund (detached mode):

   ```shell
   docker run -d --name webserver -p 80:80 nginx
   ```

5. Fällt dir etwas auf, während der Container startet? Der Container besteht aus mehr als einem Layer; daher werden mehrere Layer runtergeladen. Dazu gleich mehr im Kurs.
6. Lass dir nochmal alle laufenden Container auflisten. Bekommst du nun einen angezeigt?
7. In dem Container läuft ein Webserver. Du kannst diesen mit einem curl aufrufen.

   ```shell
   curl http://localhost
   ```

8. Da der Container nun im Hintergrund läuft, können wir ihn auch stoppen.
   Verwende eines der beiden Kommandos

   ```shell
   docker stop webserver
   docker stop <container-id>
   ```

9. Wenn du den Container über die Container-Id stoppen möchtest, wie findest du diese raus?
