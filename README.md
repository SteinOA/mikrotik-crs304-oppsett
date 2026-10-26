# MikroTik CRS304 oppsett

Norsk oppskrift for flere CRS304-4XG-IN som vanlige Ethernet-switcher. Basert på gjenoppretting og oppsett 25. oktober 2026.

## Resultatet

- RouterOS ble reinstallert med Netinstall, uten gammel konfigurasjon eller standardkonfigurasjon.
- Brukeren logget inn som admin med tomt passord og opprettet selv et nytt passord.
- Bridge `bridge1` ble opprettet med RSTP. Alle fem Ethernet-porter ble lagt inn med Hardware Offload aktivert.
- I denne økten ble grensesnittlisten `all` valgt. Det opprettet dynamiske bridgeporter for ether1–ether5. Listen omfatter også fremtidige grensesnitt; ved mer avansert oppsett bør medlemskap vurderes eksplisitt.
- DHCP-klient ble opprettet på bridge1. Ingen DHCP-server eller NAT ble opprettet.
- Ruteren tildelte administrasjonsadressen 198.51.100.218/24 med gateway 198.51.100.1. Adressen er ikke reservert og kan endre seg.
- PC-kortet ble satt tilbake til DHCP og fikk 198.51.100.108.
- PC-en ble flyttet fra MGMT/BOOT til en 10G-port. Windows rapporterte 10 Gbit/s. NAS ble koblet til switchen, og brukeren bekreftet rask filkopiering. Ingen tallfestet gjennomstrømmingstest ble fullført.

## For neste switch

1. Prøv normal innlogging via WinBox Neighbors og MAC-adressen. Bruk etikettpassordet dersom enheten har et. Netinstall er en gjenopprettingsmetode, ikke nødvendig ved fungerende innlogging.
2. Hvis passordet ikke kan brukes, følg [passord og Netinstall](docs/PASSORD-OG-NETINSTALL.md).
3. Følg [switchoppsettet](docs/SWITCHOPPSETT.md).
4. Kontroller adresse, portstatus og filkopiering. Se [feilsøking](docs/FEILSOKING.md).

## Programvare

Se [programvareoversikten](software/README.md). Installeringsfilene hentes direkte fra MikroTiks offisielle nedlastingssider. De inngår ikke i denne offentlige dokumentasjonen. Ingen passord, private nøkler, enhetsbackup eller etikettbilder ligger her.

Dette er en dokumentasjon av oppsettet, ikke en komplett sikkerhetsrevisjon av RouterOS eller hjemmenettverket.

Fabrikk-IP-en er **192.168.88.1**, ifølge [MikroTiks CRS304-manual](https://help.mikrotik.com/docs/spaces/UM/pages/271974525/CRS304-4XG-IN). Dette er en offentlig standardverdi, ikke en hemmelig adresse. Adressene i 198.51.100.0/24 og 192.0.2.0/24 ellers i veiledningen er dokumentasjonseksempler. Bruk eget lokalnett og et isolert subnett ved Netinstall; ikke kopier eksemplene ukritisk inn i et eksisterende nett.

## Sikkerhet

Se [sikkerhetspolicyen](SECURITY.md). Veiledningen åpner ingen porter mot internett. Hold administrasjon på et betrodd lokalnett, sett et unikt passord selv, og oppbevar enhetsbackup privat. Bruk gjeldende leverandørdokumentasjon ved senere oppsett.
