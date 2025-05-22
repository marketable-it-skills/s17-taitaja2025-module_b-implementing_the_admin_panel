# Taitaja2025 - Moduuli B – Hallintapaneelin toteuttaminen

## Kilpailuaika
4 hours

## Johdanto

Tässä kilpailutehtävässä toteutetaan Hobbly Technologies Oy:n toimeksiantoon perustuva sovellus, joka auttaa käyttäjiä löytämään paikallisia harrastuksia ja tapahtumia. 

Kilpailijan tehtävänä on toteuttaa hallintapaneeli, jolla hallitaan Hobbly-sovelluksen aktiviteetti-ilmoituksia ja käyttäjiä.

## Yleinen kuvaus

Hallintapaneeli toteutetaan 1440 pikselin levyiselle työpöytänäkymälle, ja sen ulkoasun tulee noudattaa asiakkaan antamaa brändiohjeistusta. Käyttöliittymän tulee olla selkeä ja helppokäyttöinen, ja sen on mahdollistettava ilmoitusten ja käyttäjien hallinta eri rooleille määriteltyjen käyttöoikeuksien mukaisesti.

Tuomarointi keskittyy erityisesti toiminnallisuuteen, käytettävyyteen, tietoturvaan ja koodin laatuun. Kilpailijan toteutuksen on oltava teknisesti toimiva, selkeästi dokumentoitu ja jatkokehitykseen soveltuva.

## Vaatimukset

**Keskeiset toiminnallisuudet**
- Käyttäjien rekisteröityminen ja kirjautuminen (sähköpostilla ja salasanalla)
- Salasanan vaihtaminen käyttäjäasetuksissa
- Aktiviteettien lisääminen, muokkaaminen ja poistaminen (vain omat ilmoitukset)
- Ylläpitäjän oikeudet: kaikkien ilmoitusten ja käyttäjien hallinta
- Käyttäjien kaksivaiheinen poistaminen

### Käyttäjätilit ja kirjautuminen
Hallintapaneelin käyttäjät voivat luoda omia tilejään vaiheittaisen rekisteröitymislomakkeen kautta.

#### Rekisteröityminen (3 vaihetta, URL pysyy samana)

**Yhteystiedot:**
- Käyttäjän nimi
- Sähköpostiosoite
- Puhelinnumero
  
**Perustiedot:**
- Logon lataaminen (JPEG/PNG, max 2MB)
- Näkyvä nimi (display name)
- Kuvaus (min. 25 merkkiä, max. 200 merkkiä)
  
**Organisaation tiedot:**
- Virallinen nimi
- Osoite
- Kaupunki
- Postinumero
- Y-tunnus (valinnainen)
- Organisaation muoto:
 - Yhdistys
 - Yksityinen
 - Osakeyhtiö

#### Kirjautuminen ja tietoturva
- Sähköpostiosoite toimii käyttäjätunnuksena.
- Salasanassa on oltava vähintään 8 merkkiä ja yksi numero.
- Sama sähköposti ei voi rekisteröityä kahdesti → näytetään virheilmoitus.
- Salasanat tallennetaan turvallisesti (esim. bcrypt tai Argon2).
- Hallintapaneeliin ei voi päästä ilman kirjautumista.
  
#### Salasanan vaihtaminen
Ohjelma luo käyttäjälle salasanan, kun käyttäjätili perustetaan. Käyttäjällä pitää kuitenkin olla hallintapaneelissa mahdollisuus vaihtaa oma salasanansa. Ohjelman pitää salasanaa vaihdettaessa tarkistaa, että uusi salasana täyttää minimivaatimukset (vähintään 8 merkkiä ja yksi numero). Jos minimivaatimukset eivät täyty, ohjelma ilmoittaa asiasta eikä salasana vaihdu.

#### Ylläpitäjä (Admin)
- Ylläpitäjän oletuskäyttäjätunnus: taitaja@hobbly.app 
- Salasana: Taitaja123!
- Ylläpitäjä voi hallita kaikkia käyttäjiä ja ilmoituksia.
  
### Ilmoitusten hallinta
Hallintapaneelissa käyttäjä voi lisätä, muokata ja poistaa harrastus- ja aktiviteetti-ilmoituksia. Käyttäjä näkee vain omat ilmoituksensa. Ilmoituksia voi lisätä, muokata ja poistaa. Käyttäjä voi poistaa ilmoituksen lopullisesti tai siirtää sen roskakoriin (soft delete).

**Lisäyslomakkeessa on seuraavat kentät:**
- Otsikko (pakollinen)
- Kuvaus (pakollinen)
- URL-linkki (valinnainen, esim. lisätietoihin)
- Kuvan lataus (JPEG/PNG, max 2MB)
- Tapahtuman tyyppi (valitaan listasta)
- Kategoria (valitaan listasta)
- Tunnisteet (tags) (erotetaan pilkulla, uudet tagit lisätään automaattisesti)
- Sijaintitiedot:
 - Osoite (näytettävä tekstinä)
 - Leveysaste (Latitude)
 - Pituusaste (Longitude)

**Tapahtuman tyyppi – 5 vaihtoehtoa**
- Aktiviteetti
- Tapahtuma
- Harrastusmahdollisuus
- Kerho
- Kilpailu
  
**Kategoriat – 10 vaihtoehtoa**
- Urheilu ja liikunta
- Musiikki ja esittävä taide
- Käsityöt ja taide
- Tiede ja teknologia
- Pelit ja e-urheilu
- Ruoka ja kokkaus
- Luonto ja retkeily
- Kulttuuri ja historia
- Yhteisöllisyys ja vapaaehtoistyö
- Lapset ja perheet
  
**Tunnisteet (Tags) – 10 vaihtoehtoa**
(Jos tagia ei ole ennestään, se lisätään automaattisesti.)
- Ilmainen
- Avoin kaikille
- Helppo aloittelijoille
- Jatkuva tapahtuma
- Verkossa
- Sopii perheille
- Sopii senioreille
- Sopii erityisryhmille
- Välineet saa paikan päältä
- Vaatii ennakkoilmoittautumisen
  
#### Kaksivaiheinen poistaminen (roskakori)
1.	Siirtäminen roskakoriin (soft delete)
- Ilmoitus siirtyy roskakoriin, eikä se ole enää näkyvissä aktiivisena.
- Käyttäjä voi palauttaa ilmoituksen tai poistaa sen pysyvästi.
2.	Lopullinen poisto (permanent delete)
- Ilmoitus poistetaan pysyvästi tietokannasta, eikä sitä voi palauttaa.
- Käyttäjän täytyy vahvistaa poisto erikseen, jotta vältytään vahingoilta. "Haluatko varmasti poistaa tämän ilmoituksen pysyvästi? Tätä ei voi perua!"
  
### Käyttäjähallinta (vain ylläpitäjille)
Hallintapaneelin käyttäjillä on kaksi eri roolia:
1.	Toimijakäyttäjät (esim. urheiluseurat tai yritykset)
a.	Näkevät ja hallitsevat vain omia ilmoituksiaan.
2.	Ylläpitäjät (Hobblyn työntekijät)
a.	Pystyvät hallitsemaan kaikkien käyttäjien ilmoituksia.
b.	Voivat luoda, muokata ja poistaa käyttäjätilejä.
c.	Näkevät kaikki käyttäjätiedot ja heidän luomansa ilmoitukset.

## Arviointi

Projekti arvioidaan käyttämällä selaimia Google Chrome ja Firefox.axe-selainlaajennus on asennettu Chromeen ja sen avulla kilpailijat voivat tarkistaa sivuston saavutettavuuden WCAG-standardeihin perustuen.

## Pisteiden jakautuminen

| Kuvaus                | Pisteet |
| --------------------- | ------- |
| Rekisteröityminen     | 10      |
| Kirjautuminen         | 1       |
| Salasanan vaihtaminen | 2       |
| Ilmoitusten hallinta  | 8       |
| Käyttäjähallinta      | 4,5     |
| Koodin laatu          | 3       |
| Projektinhallinta     | 1,5     |
|                       |         |
| **Total**             | 30      |
