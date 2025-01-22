# Volumes verwenden

- **Ziel:** Persistente Daten speichern und sicherstellen, dass Daten unabhängig vom Container-Status verfügbar bleiben.

## Anleitung

1. Starte einen Container mit einem Volume:
   Der folgende Befehl erstellt ein neues Volume (my-volume) und bindet es an das Verzeichnis /data im Container:

   ```shell
   docker run -d --name volume-test -v my-volume:/data alpine sleep 1000
   ```

   Wir verwenden `sleep 1000` damit sich der Container nicht direkt wieder beendet.

2. Öffne eine Shell im Container:

   ```shell
   docker exec -it volume-test sh
   ```

3. Erstelle eine Datei im Volume:

   ```shell
   echo "Hello, Volume!" > /data/testfile.txt
   ```

4. Schließe die Shell wieder mit `exit`.
5. Stoppe den Container.

   ```shell
   docker stop volume-test
   ```

6. Starte ihn wieder.

   ```shell
   docker start volume-test
   ```

7. Öffne erneut eine Shell in den Container.
8. Überprüfe, ob die Datei noch vorhanden ist:

   ```shell
   cat /data/testfile.txt
   ```

9. Nun stoppe und lösche deinen Container.

   ```shell
   docker rm -f volume-test
   ```

10. Erstelle einen neuen Container, der dasselbe Volume verwendet:

```shell
docker run -it --rm -v my-volume:/data alpine cat /data/testfile.txt
```

Die Daten im Volume sind weiterhin verfügbar, auch nach dem Löschen des ursprünglichen Containers.
