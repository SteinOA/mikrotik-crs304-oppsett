# Feilsøking fra første oppsett

## Timeout eller feil passord

Connection timed out betyr manglende forbindelse og bekrefter ikke at passordet er galt. Wrong username or password betyr at enheten svarte og avviste opplysningene. MAC-tilkobling i WinBox unngår problemer med ulike IP-nett ved førstegangsoppsett.

## Ingen link

PC-ens Ethernet-kort viste Media disconnected under klargjøringen. Nettverkskortet måtte aktiveres, switchen måtte ha strøm og kabelen sitte riktig. Etterpå ble 192.0.2.2 synlig på kabelkortet.

## Filkopiering stopper

En første melding var Fil i bruk i Windows Utforsker. Lukk avspilling og forhåndsvisning før nytt forsøk.

Senere viste undersøkelser at navnet NAS-SERVER ble slått opp til en Tailscale-adresse, og aktiv SMB brukte denne. Lokal NAS-adresse var 198.51.100.30. Vi ba derfor om ny åpning av \\198.51.100.30\home i Utforsker og ny kopiering derfra. Ikke anta at en eksisterende tilordnet disk automatisk velger lokal 10G-vei.

Kontrollene viste Wi-Fi avslått, Ethernet 10 Gbps, ingen rapporterte pakke-/discard-feil og ping uten pakketap til lokal NAS, også med 1472 byte og DF. Dette er begrensede kontroller, ikke bevis på maksimal gjennomstrømming.

Brukeren opplyste at Jumbo Frames allerede var slått av, og bekreftet senere at kopieringen gikk svært raskt. Vi målte ikke endelig hastighet og kan ikke isolere én sikker årsak til forbedringen. La det fungerende standard-MTU-oppsettet stå før ytterligere optimalisering.

## Lokal speedtest

http://198.51.100.30:3000/ avviste TCP-forbindelse da vi prøvde. Porten svarte ikke; ingen lokal speedtest ble gjennomført. Tjenestestatus og portmapping gjenstår å undersøke. Dette beviser ikke feil på switchen.
