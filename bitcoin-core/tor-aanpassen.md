{% hint style="info" %}
Tijd: 5 minuten
{% endhint %}

Tor moet een beetje aangepast worden. Hiervoor moeten wij een bestand wijzigen. Er staat veel troep in dus het is handig om het bestand eerst weg te gooien.

```bash
sudo rm /etc/tor/torrc
```

```bash
sudo nano /etc/tor/torrc
```

Eenmaal in dit bestand voeg je onderaan \(of bovenaan als je daar zin in hebt\) deze regels toe:

```text
ControlPort 9051
CookieAuthentication 1
CookieAuthFileGroupReadable 1

HiddenServiceDir /var/lib/tor/bitcoin/bitcoind
HiddenServiceVersion 3
HiddenServicePort 8332 127.0.0.1:8332
```

Sla het bestand op met de toestencombinatie `Control + X`. Geef `Y` als antwoord op de vraag of je op wil slaan.

Maak mappen aan met:

```bash
sudo mkdir /var/lib/tor/bitcoin
```

```bash
sudo mkdir /var/lib/tor/bitcoin/bitcoind
```

Geef de juiste rechten met:

```bash
sudo chown -R debian-tor:debian-tor /var/lib/tor/bitcoin/bitcoind
```

```bash
sudo chmod 700 /var/lib/tor/bitcoin/bitcoind
```

Tor moet nu opnieuw opgestart worden.

```bash
sudo systemctl restart tor
```

Om alles van kracht te laten zijn log je uit door "exit" te typen en op enter te drukken. **Vergeet dit niet!**

## Onion adres

Met onderstaand commando krijg je het Onion adres terug van je bitcoin node. Dit adres heb je later nodig als je wil communiceren met je node. In vervolg onderdelen van de guide \(zoals tijdens het opzetten van Lightning\) zul je een soortgelijk commando moeten invoeren.

```bash
sudo cat /var/lib/tor/bitcoin/bitcoind/hostname
```