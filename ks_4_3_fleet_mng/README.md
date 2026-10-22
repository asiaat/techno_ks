# KS 4.3 – Ansible Fleet Management & Multi-OS Docker Lab

See repositoorium sisaldab valmis konfiguratsioonifaile ja Ansible'i *Playbook*'e suuremahulise kaughalduse (*Fleet Management*) harjutamiseks 5 erineva Dockeri konteineri (Ubuntu, Debian/Raspberry Pi OS analoog, Alpine Linux) ja füüsiliste Raspberry Pi seadmete peal.

## 📁 Failide ülevaade

* **`docker-compose.yml`** – Käivitab 5 konteinerit kolme erineva Linuxi distributsiooniga (pordid `2201`–`2205` SSH jaoks ja `8081`–`8085` veebiserveri jaoks).
* **`ansible.cfg`** – Ansible'i lokaalne seadistus (määrab inventarifaili ja keelab testkeskkonnas SSH *host key* kontrolli).
* **`hosts.ini`** – Struktureeritud inventarifail, kus sõlmed on jagatud rollide järgi gruppidesse (`ubuntu_servers`, `rpi_and_debian`, `iot_alpine` ja koondgrupp `fleet`).
* **`fleet_deploy.yml`** – Universaalne *Playbook*, mis seadistab kõik 5 masinat, paigaldab vajalikud paketid sõltumata OS-ist, seadistab Debiani/RPi masinatele Kioski poliitika (KS 4.0) ja loob igale masinale dünaamilise riistvara-armatuurlaua (KS 4.2).
* **`rpi_setup.yml`** ja **`rpi_webserver.yml`** – Mooduli KS 4.2 *Playbook*'id üksiku Raspberry Pi või Debiani grupi haldamiseks.

## 🚀 Kiire alustamine

1. **Klooni repositoorium ja liigu kausta:**
   ```bash
   git clone <sinu-githubi-repo-url>
   cd ansible-fleet-lab
   ```

2. **Käivita Dockeri 5-masinaline testklaster:**
   ```bash
   docker compose up -d
   ```

3. **Kontrolli ühendust kõigi 5 masinaga:**
   ```bash
   ansible fleet -m ping
   ```

4. **Käivita peamine Playbook:**
   ```bash
   ansible-playbook fleet_deploy.yml
   ```

5. **Vaata tulemust brauseris:**
   * Masin 1 (Ubuntu): [http://localhost:8081](http://localhost:8081)
   * Masin 2 (Ubuntu): [http://localhost:8082](http://localhost:8082)
   * Masin 3 (Debian): [http://localhost:8083](http://localhost:8083)
   * Masin 4 (Raspberry Pi Simulaator): [http://localhost:8084](http://localhost:8084)
   * Masin 5 (Alpine Linux IoT): [http://localhost:8085](http://localhost:8085)
