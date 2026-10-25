# Oppsett som vanlig switch

Bruk WinBox etter innlogging. Dette gjelder en tom konfigurasjon; ikke legg til duplikater på en allerede konfigurert enhet.

1. Bridge → New. Behold navn bridge1 og RSTP. Lagre.
2. Bridge → Ports → New. Velg bridge1 og legg til Ethernet-portene. I den dokumenterte økten valgte vi Interface all, som ga dynamiske porter for ether1 til ether5. Hardware Offload var avkrysset. Alternativt kan de fem portene legges inn enkeltvis for avgrenset medlemskap.
3. Tilkoblingen kan falle ut når den tilkoblede porten blir bridgeport. Vi logget inn igjen gjennom Neighbors og MAC.
4. IP → DHCP Client → New. Interface bridge1. Enabled på. Vi beholdt Use Peer DNS, Use Peer NTP og Add Default Route yes.
5. Koble én kabel fra lokalnettet/ruteren til en ledig port. DHCP-klienten skal gå fra searching til bound. Les full adresse i Status-fanen.
6. Sett PC-ens Ethernet tilbake til tidligere IPv4/DNS-oppsett, normalt automatisk DHCP. Behold Wi-Fi til dette er kontrollert.
7. Flytt PC og NAS til 10G-portene. MGMT/BOOT er 1G og kan stå tom. Administrasjon fungerer også fra bridgeportene.

På første switch fikk vi 198.51.100.218. Ikke kopier denne adressen statisk til flere switcher. La DHCP gi hver enhet en unik adresse. DHCP-reservasjon kan settes i ruteren som et eget senere steg.

## Kontroller

- DHCP Client viser bound og adresse i ønsket lokalnett.
- Bridge Ports viser de forventede portene og forwarding på aktive tilkoblinger etter RSTP-oppstart.
- H-flagg viser maskinvareavlasting på støttede porter. MGMT-porten kan oppføre seg annerledes enn de fire 10G-portene.
- Windows viser forventet linkhastighet. Dette er ikke det samme som målt filhastighet.
- En stor fil kan kopieres uten stopp. Disker, NAS, protokoll og klient påvirker faktisk hastighet.
- Oppsettet bevares når PC-en slås av. Switchen trenger egen strøm for å fungere.
