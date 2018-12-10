Oliot
======

Luominen
---------
Olion luominen voi javaScriptissä tapahtua monella eri tavalla. Yksinkertaisin tapa on tietenkin käyttää koodissa olioliteraalia::

  let olio = {kenttä: "123"};

Olioliteraalin luominen on helppoa, mutta se ei välttämättä sovi tilanteeseen jossa olioille halutaan enemmän rakennetta. Tällaisiin tilanteisiin sopiva ja muutenkin hyvä periaate olion luontiin on käyttää konstruktori funktiota. Konstruktori antaa raamit olioiden rakentamiseen ja mikä parasta, konstruktorin avulla voidaan luoda toiminnallisuutta joka on jokaisen sen ilmentymän käytössä::

  function Apina(a,b) {
    this.nimi = a,
    this.laji = b
  }

  Apina.prototype.terve = function() {write("Moi!")}

  const apina = new Apina("aatu", "makaki");
  apina.väri = "harmaa";
  oK(apina)
  write(apina.nimi + " " + apina.laji + " " + apina.väri);
  apina.terve();

  nimi: aatu
  laji: makaki
  väri: harmaa
  
  aatu makaki harmaa
  Moi!

Esimerkkikoodissa on muuttujaan "apina" käytetty tarkoituksella const määrettä. Kyseisen määreen käyttö estää koodissa muuttujan "apina" uudelleen alustamisen. JS:n on tarkoitus olla joustavaa ja dynaamista, mutta mikäli muuttujaa ei tulla alustamaan uudestaan on const-määreen käyttö hyvä varotoimi. Vaikka se estää muuttujan alustuksen, on sen kenttiä vielä mahdollista poistaa, lisätä ja muokata. Näin ollen se ei riko JS:n perus ajatusta ja saattaa samalla säästää muutamalta virhetoiminnolta.
 
Kieli tarjoaa myös muita tapoja olioiden luomiseen. Olioiden luonti voi tapahtua myös class määrettä käyttämällä (käytännössä sama kuin konstruktorifunnktion käyttö) ja tyhjän olion täytöllä. Konstruktori funktion käyttö on kuitenkin mielestämme selkein ja suositeltavin tapa luoda olioita javaScriptissä.


Käyttö
------

Kielen luonteesta johtuen luotuja olioita voi vääntää, kääntää ja muokata juuri niin paljon kun ikinä haluat. Tämä on hieno ominaisuus ja se mahdollistaa sellaisia toiminnallisuutta, mitä monilla jäykemmillä kielillä olisi hyvin vaikeaa tai jopa mahdotonta toteuttaa. Vapauden kanssa tulee kuitenkin olla varovainen ja javaScriptissä onkin järkevää käyttää jonkinlaista turvaverkkoa.
Ensinnäkin ihan koodin yleisen siisteyden ja yhdenmukaisuuden nimissä olisi hyvä päättää vakio tapa sille miten olion kenttiin viitataan. Pistenotaatio on tietenkin helpoin ja siistein ratkaisu. Kuulosta hyvältä, mutta valitettavasti pistenotaatio ei aina toimi. kenttien/attribuuttien nimeämisessä voi harrastaa melkoista luovuutta ja hyväksyttäviä nimiä omvat mm. "", "peruna", 222 ja 1.2. Edellä mainituista pistenotaatiolla voi viitata ainoastaan "peruna" nimiseen kenttään. Tällaisissa tilanteissa olisi suositeltavaa käyttää aina toimivaa hakasulku ratkaisua::

  let olio = {
    1: 2,
    4.5: "peruna",
    kenttä: "toimii"
  }

  write(olio.kenttä) // toimii
  write(olio.1) // virhe
  write(olio.4.5) // virhe
  write(olio[1]) tai write(olio["1"]) //2
  write(olio[4.5]) tai write(olio["4.5"]) //peruna 

Dynaaminen kenttien muuttelu, poisto ja lisäys eivät aina ole välttämättä joillekkin olion kentille haluttua toiminnallisuutta ja jos jokin kenttä vaatii erityistä suojelua niin on se fiksua muuttaa ominaisuuksiltaan ei muokattavaksi. Mikään (lähes) ei ole lopullista javaScriptissä, joten jos myöhemmin tulee tarvetta sittenkin muuttaa kyseisen kentän arvoja tai poistaa kenttä kokonaan, voidaan muuttujan ominaisuuksia taas muuttaa::

  Object.defineProperty(olio, "kenttä", {writable: false});
  olio.kenttä = "vaihdu";
  write(olio.kenttä) //toimii

  Object.defineProperty(olio, "kenttä", {writable: true});
  olio.kenttä = "vaihdu";
  write(olio.kenttä) //vaihdu

Class VS Perinteinen
---------------------

Olioiden luontia käsittelevässä osassa tuli jo mainittua että JS:stä löytyy periaatteessa java tyylinen class toiminnallisuus. Class ei oikeastaan tuo mukanaan mitään uutta, vaan käyttää javaScriptissä jo olemassa olevia työkaluja class toiminnallisuuden simuloimiseen. Tästä syystä on suositeltavaa, niin ikävältä kun se aluksi tuntuukin, opetella käyttämään JS:n perinteisiä työkaluja olioiden luonnissa. Tämä pakottaa ohjelmoijan perehtymään kielen rakenteisiin, jotka ovat javaScriptin osaamisen kannalta on erittäin oleellista. Vaikka class:in käyttö ei sinänsä ole huonompi ratkaisu, javaScript menettää hieman merkityksensä jos kieltä lähdetään pakottamaan takaisin kankeampaan muotoon.
