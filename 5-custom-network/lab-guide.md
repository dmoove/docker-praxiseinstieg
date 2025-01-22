# Benutzerdefiniertes Netzwerk

- **Ziel:** Ein benutzerdefiniertes Netzwerk erstellen, Container verbinden und den Nutzen von Netzwerken verstehen.

## Anleitung

1. Erstelle ein benutzerdefiniertes Netzwerk:

   ```shell
   docker network create my-network
   ```

2. Starte zwei Container in diesem Netzwerk:

   ```shell
   docker run -dit --name container1 --network my-network alpine sh
   docker run -dit --name container2 --network my-network alpine sh
   ```

3. Teste die Verbindung zwischen den Containern mit dem ping-Befehl:

   ```shell
   docker exec container1 ping container2
   ```

4. Was fällt dir auf?
   Die Container können sich direkt über ihren Namen erreichen, da Docker die DNS-Auflösung im lokalen Netzwerk übernimmt.
5. Erweitere die Übung:

   - Starte einen dritten Container und überprüfe, ob auch dieser mit den anderen kommunizieren kann:

     ```shell
     docker run -dit --name container3 --network my-network alpine sh
     docker exec container1 ping container3
     ```

   - Entferne einen Container aus dem Netzwerk und prüfe, ob die Verbindung unterbrochen wird:

     ```shell
     docker network disconnect my-network container2
     docker exec container1 ping container2
     ```

6. Stoppe alle Container:

   ```shell
   docker stop container1 container2 container3
   ```
