Tyyppiturvallisuuden Tavoittelua
================================

JavaScript tarjoaa ohjelmoijalle monipuolisen ja tehokkaan työkalun, joka tarvittaessa venyy projektin kuin projektin tarpeisiin. Kyseinen vapaus johtuu suurilta osin muuttujien tyypittömyydestä ja saattaa kieleen tutustuvasta tuntua yhtäaikaa niin uskomattoman mahdollisuuksia pursuavalta kuin pelottavan huteralta. Onkin mahdollista että javascript tekee ohjelmoijasta oman pahimman vihollisensa, kun muuttujat karkaavat globaaleiksi ja käyttäjä suorittaa numerokentässä merkkijonojen yhteenlaskua.

Toisaalta kyseiset ominaisuudet ovat myös kielen vahvuuksia, ja niiden käyttämättä jättö ottaa idean javaScriptin käytöstä. Välttämisen sijaan ohjelmoijan tulisi valita itselleen luonteva tapa kirjoittaa javaScriptiä ja pysyä kyseisessä tyylissä. Tällöin virheiden mahdollisuus vähenee ja koodi saadaan ihmisystävällisempään muotoon. Tarvittaessa on myös hyvä käyttää kielen tarjoamia apufunktioita tai luoda itse kokonaan uusia. 

Tarkistusfunktiot kokonaisluvuille
-----------------------------------

Kuten alla esimerkeissä näkyy, javaScript mahdollistaa muuttujien monipuolisen käytön. Aina tällainen toiminta ei kuitenkaan ole haluttua, ja jos haluamme tarkastella onko syöte kokonaisluku, tulee meidän tarkastella sitä hieman lähemmin. Numero on kokonaisluku jos sen jakojäännös yhdellä on nolla. Tämä on helppo selvittää laskutoimituksella. JavaScript tarjoaa paljon työkaluja tyypin tunnistamiseen, mutta kuten huomataan, ne eivät ole aina riittäviä. Alla määritelty muuttuja a on Number olio ja se käyttäytyy oikein laskutoimituksissa, mutta sen tyyppi ei ole numero. Jotta tämä saadaan oikaistua, täytyy viitata hierarkiassa ylöspäin Object function prototyyppi olion toString:iin. Nyt niin Number-olio kuin numero yksikin tunnistetaan numeroiksi, kun taas merkkijono "1" saa tyypikseen String:: 

  var a = new Number(3)
  write(typeof a == 'number')						// false
  write(typeof 1 == 'number')						// true
  write(typeof "1" == 'number')						// false
  write(a + 1)								// 4
  write(a % 1)								// 0
  write(1 + "1")							// 11
  write(Object.prototype.toString.call(a) == '[object Number]')		// true
  write(Object.prototype.toString.call(1) == '[object Number]')		// true
  write(Object.prototype.toString.call("1") == '[object Number]') 	// false

Nyt voidaan siis muodostaa funktio, jonka avulla saadaan tarkastettua onko syöte kokonaisluku. Palautusarvona toimii tuttu ja turvallinen boolean::

  function kLuku(a) {
    return ((Object.prototype.toString.call(a) == '[object Number]') && (a % 1 == 0))
  }

Tarkistusfunktiot yleisesti luvuille
-------------------------------------

Tarkastus sille onko syöte luku voidaan johtaa kokonaislukujen tarkastuksesta. Hyväksyttävissä parametreissa on nyt mukana myös desimaaliluvut, joten jakojäännöksen tarkastamisen voi jättää pois::

  function luku(a) {
    return (Object.prototype.toString.call(a) == '[object Number]')
  } 

Tarkistusfunktiot merkkijonoille
---------------------------------

Merkkijonoille voidaan jälleen kerran soveltaa kokonaisluku tarkastuksen ratkaisua. Muutetaan toStringin vertailu muotoon '[object String]', jolloin funktiomme palauttaa true jos parametri täyttää merkkijonon kriteerit ja muuten false::

  var a = "abc"
  var b = 1
  var c = undefined
  write(Object.prototype.toString.call(a) == '[object String]')		// true
  write(Object.prototype.toString.call(b) == '[object String]')		// false
  write(Object.prototype.toString.call(c) == '[object String]')		// false

  function mjono(a) {
    return (Object.prototype.toString.call(a) == '[object String]')
  } 


Tarkistusfunktiot kokonaisluku taulukoille
-------------------------------------------

Taulukoiden tarkastamisessa voimme käyttää kokonaisluvun tunnistamisfunktiota ja valmista Array.every(func) apufunktiota. Every palauttaa toden mikäli taulukon kaikki alkiot läpäisevät function parametrina saaman testin. Kokonaisluku taulukon tarkastava funktio::

  function klTaulukko(array) {
    return array.every(kLuku)
  }

Tarkistusfunktiot lukuja sisältäville taulukoille
--------------------------------------------------

Yleisesti lukuja sisältävän taulukon tarkastus tapahtuu hyvin samalla tavalla kuin kokonaisluku taulukon tarkastus. Tällä kertaa every() funktiolle annetaan vain parametrina aikaisemmin määritelty luku() funktio, joka tarkastaa onko taulukon alkio jonkinlainen luku::

  function lukuTaulukko(array) {
    return array.every(luku)
  }

Käyttöesimerkki
---------------

Oikein käytettynä edellä esitellyt apufunktiot estävät suuren osan syötteistä johtuvista virhetilanteista. Tässä yksinkertainen esimerkki kokonaisluvun tarkastavan funktion käytöstä::

  function kLuku(a) {
     // peruna = false
     // 3,5 = false
     // 2 = true
     return ((Object.prototype.toString.call(a) == '[object Number]') && (a % 1 == 0))
  }

  var a = prompt("Anna kokonaisluku:");
  a = new Number(a);
  if (kLuku(a)) {
     write("Lukusi on kokonaisluku!")
  } else {
     write("Anna kokonaisluku!")
  }
