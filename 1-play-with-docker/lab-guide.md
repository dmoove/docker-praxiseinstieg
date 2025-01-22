# Aufrufen von Play with Docker und Testen

- **Ziel:** Sicherstellen, dass Docker korrekt installiert ist und funktioniert.

## Anleitung

1. Öffne [Play with Docker](https://labs.play-with-docker.com/).
2. Wähle link "ADD NEW INSTANCE" aus.
3. Die neue Instand öffnet sich automatisch.
4. Es ist allerdings zu empfehlen, die über SSH zu öffnen (Unter Windows kannst du PuTTY verwenden); da ihr im Webbrowser nicht kopieren könnt.
5. Führe die folgenden Befehle aus, um die Installation zu testen:

   ```shell
   docker version
   docker info
   docker run hello-world
   ```

6. Schau dir die Ausgaben an, die generiert werden.
