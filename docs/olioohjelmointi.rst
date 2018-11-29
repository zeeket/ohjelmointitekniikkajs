Olio-ohjelmointi JavaScriptillä
===============================

Olio-ohjelmointi on ohjelmointiparadigma, joka on ollut yleisesti käytössä ja hyvin pitkään. Puhuttaessa tästä paradigmasta, tulee ihmisillä yleensä mieleen tunnetuimmat kielet kuten Java, C++, C# ja Python. JavaScriptikin on oliopohjainen kieli, sillä käytännössä kaikki sen komponentit ovat olioita (funktiot, stringit, numerot) ja niitä luodaan yleensä olioliteraaleilla ja konstruktorifunktioilla. Tärkeimmät ohjelmointitekniikat JavaScriptiä koodatessa ovat kapselointi ja periytyminen. Jos näitä kahta käyttää hyvin ja oikein, tulee ohjelmasta skaalautuvainen, helpommin ymmärrettävä ja koodista uudelleen käytettävä.

Kapselointi
-----------

Usein haluttaessa luoda vain yksi olio ja nopeasti tallennettua siihen jotakin tietoa, käytetään vain olioliteraalia ja homma on sillä selvä. Kuitenkin kun halutaan luoda useita olioita samalla toiminnallisuudella tai kentillä, kapseloidaan toiminnallisuudet funktioon, jonka konstruktoria käytetään olioiden luomiseen.

Seuraavassa esimerkissä näkyy, kuinka funktiolla saadaan kapseloitua olion luominen.::
  
  function Kayttaja (annettuNimi, annettuSahkoposti) {
    this.nimi = annettuNimi;
    this.sahkoposti = annettuSahkoposti;
  }

  Kayttaja.prototype = {
    constructor: Kayttaja,
    vaihdaSahkoposti:function (uusiSahkoposti)  {
        this.sahkoposti = uusiSahkoposti;
    }
  }
  
Ja tätä Kayttaja-funktiota voidaan käyttää::

  ekaKayttaja = new Kayttaja("Uolevi", "Uolevi@example.com"); 
  ekaKayttaja.vaihdaSahkoposti("Kalevi@example.com"); 
  
  // Toinen Kayttaja
  tokaKayttaja = new Kayttaja("Ilmari", "Ilmari@example.com");
  
Kuten esimerkeistä näkee, nyt Kayttaja-funktiota käyttäen voidaan luoda uusia käyttäjiä, joilla kaikilla on käytössään sama funktionaalisuus ilman, että se vaikuttaisi aiempiin olioihin.

Periytyminen
------------

Periytymisellä haetaan ohjelmaan funktionaalisuutta, jolla oliot perivät "ylemmiltä" funktioilta toiminnallisuutta, joita oliot voivat käyttää niiden omien toiminnallisuuksien lisäksi. Kyseessä on siis aivan perinteinen olio-ohjelmoinnin ohjelmointiparadigma. Kurssin esimerkissä on hyvin havainnollistettu periytyminen ja funktioiden prototyyppiolioihin liitetyt aksessorimetodit.::

  function Elain() {
  this.paino = 0
  }
  Elain.prototype.asetaPaino =
     function (maara) {this.paino=maara}
  Elain.prototype.syo =
     function (maara) {this.paino+=maara}
  Elain.prototype.kuluta =
     function (maara) {this.paino-=maara}
  
  function Tuotantoelain() {
    this.tuotto = 0
  }
  Tuotantoelain.prototype = new Elain()
  Tuotantoelain.prototype.asetaTuotto =
     function (maara) {this.tuotto=maara}
  Tuotantoelain.prototype.tuota =
     function () {return this.tuotto}
  
  function Lehma(nimi) {
    this.nimi = nimi || "";   // kelvoton nimi => tyhjäksi
  }                               //  (tämä on JavaScript-idiomi!)
  Lehma.prototype = new Tuotantoelain()
  Lehma.prototype.toString =
     function () { return this.nimi+
                   ": "+this.paino+" Kg, "+
                    this.tuotto+" litraa"
                 }
  var m = new Lehma("Mansikki")

  oK(m)                       // nimi: Mansikki  (vain yksi oma kenttä!)
  
  write(m)                    // Mansikki: 0 Kg, 0 litraa
  
  m.asetaPaino(500)
  oK(m)                       // nimi: Mansikki (kaksi omaa kenttää)
                              // paino: 500     
  
  write(m)                    // Mansikki: 500 Kg, 0 litraa
  
  m.asetaTuotto(20)
  m.syo(15)
  oK(m)                       // nimi: Mansikki (kolme omaa kenttää)
                              // paino: 515
                              // tuotto: 20
  
  write(m)                    // Mansikki: 515 Kg, 20 litraa
  
  m.kuluta(100)
  write(m)                    // Mansikki: 415 Kg, 20 litraa
  write("Tuotetaan "+m.tuota()) // Tuotetaan 20
                 
Esimerkistä näkee selvästi, kuinka periytyminen etenee Elain-funktiosta aina Lehma-funktion prototyyppiolioon saakka.