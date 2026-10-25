# Passordproblemet og løsningen

## Hva som skjedde

Den nye CRS304-switchen ble funnet i WinBox med fabrikkadressen 192.0.2.1 og RouterOS 7.15.3. PC-en var i 198.51.100.x-nettet. IP-forsøk ga timeout; MAC-tilkobling gjorde at innlogging kunne forsøkes uavhengig av IP-nettet.

Fabrikkpassordet på undersiden var vanskelig å lese. Flere bokstavtolkninger ble prøvd og avvist. Vi klarte ikke å fastslå korrekt passord. Prikkene i WinBox viser ikke passordets faktiske tegn.

Datamatrise-koden ble dekodet lokalt fra et bilde. Den inneholdt serienummeret, ikke passordet. Eskeetiketten hadde heller ikke noe passord. Ingen gjetninger skal behandles som et bekreftet fabrikkpassord.

Vanlig fabrikkreset legger tilbake fabrikkpassordet på nyere enheter og ville derfor ikke løst den uleselige etiketten. MikroTik opplyser at distributøren kan hente passordet fra serienummeret. Vi valgte Netinstall siden switchen var ny og uten oppsett som skulle bevares.

## Netinstall slik vi gjennomførte det

Netinstall reformaterer enhetens systemlagring og sletter oppsett og filer. Kontroller modell og mål; ikke installer på andre enheter eller lokale PC-disker.

1. Last ned Netinstall for Windows 64-bit og RouterOS for ARM64 fra offisiell produktside. Vi brukte versjon 7.25 av begge. Velg riktig arkitektur og kontroller gjeldende MikroTik-dokumentasjon ved senere bruk.
2. Ha internett via Wi-Fi på PC-en. Koble PC-ens Ethernet direkte til MGMT/BOOT på switchen. Koble switchen fra resten av lokalnettet mens Netinstall kjører.
3. Noter PC-kortets opprinnelige IPv4/DNS-oppsett. Vårt kort het Ethernet og brukte DHCP.
4. Sett bare kabelkortet midlertidig til 192.0.2.2, maske 255.255.255.0, uten gateway. Wi-Fi beholdes. Windows krevde at brukeren endret dette med administratorrettigheter.
5. Kjør Netinstall som administrator. I Net booting: Boot Server enabled på, Client IP address 192.0.2.3.
6. Trekk strømmen til switchen. Hold RESET, koble til strøm, hold videre mens USR blinker og deretter lyser fast. Slipp når USR slukker. La Ethernet-kabelen stå tilkoblet.
7. Vent til CRS vises som Ready og arm64. Velg CRS-enheten og RouterOS-pakken.
8. Keep old configuration AV. Apply default config AV. Configure script AV. Mode script AV. Vi ønsket tom konfigurasjon, slik at fabrikkoppsettet ikke la tilbake etikettpassordet.
9. Trykk Install. Ikke bryt strøm eller kabel under installasjon. Vi fikk Finished successfully.
10. Slå av Boot Server enabled. Reboot-knappen var utilgjengelig etter fullført installasjon, så vi tok strømmen av og på uten å holde RESET.
11. Åpne WinBox Neighbors og koble til MAC-adressen. Etter denne installasjonen fungerte admin med tomt passord. I passorddialogen lot brukeren Old password stå tomt og fylte inn nytt passord to ganger.

Den tomme konfigurasjonen er ikke en ferdig switchkonfigurasjon. Bridge og DHCP-klient måtte opprettes etterpå. Ikke forvent at ruterkabelen gir PC-en nett før dette er gjort.

## Kilder

- https://help.mikrotik.com/docs/spaces/UM/pages/271974525/CRS304-4XG-IN
- https://manual.mikrotik.com/docs/getting-started/configuration-management/default-configuration-passwords/
- https://manual.mikrotik.com/docs/getting-started/installation-and-upgrade/netinstall/netinstall-windows/
