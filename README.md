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

Se [programvareoversikten](software/README.md). Offisielle installasjonsfiler følger som vedlegg til GitHub-utgivelsen; de legges ikke i Git-historikken. WinBox hentes fra MikroTik. Ingen passord, private nøkler, enhetsbackup eller etikettbilder ligger her.

Dette er en dokumentasjon av oppsettet, ikke en komplett sikkerhetsrevisjon av RouterOS eller hjemmenettverket.

Alle IP-adresser i dette repoet er dokumentasjonseksempler, ikke adresser fra det faktiske nettverket. Bytt dem til et egnet, isolert subnett og ditt eget lokalnett. Fabrikkadressen er erstattet med en eksempeladresse; se leverandørens manual for faktisk standardadresse.
