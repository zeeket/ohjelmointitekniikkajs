Kommentit
================================

Kommentit ovat tärkeitä. Kommenttien avulla henkilöt, jotka eivät ole nähneet lähdekoodiasi aiemmin pääsevät nopeammin perille siitä, mitä ohjelmasi on tarkoitus tehdä. **Tärkeää:** kommentit lähdekoodissa eivät voi korvata kunnollista dokumentaatiota ohjelmistollesi. Kommentit ovat ainoastaan yksi työkalu auttamaan tulevia ohjelmistokehittäjiä ymmärtämään lähdekoodisi. Toinen tärkeä työkalu on tämän dokementaation mukainen, hyväksi todettujen rakenteiden ja tyylien käyttö. 

Yhden rivin kommentit   
-------------------------------------------------------------------------------------
Käytä // kirjoittaaksesi yhden rivin kommentin. Kommenttien tulee olla kohteen yläpuolella::

   //on lukenut dokumentaation
   const lukenut = true;

Eikä näin::

   const lukenut = true; //on lukenut dokumentaation
 
Kun yhden rivin kommentti on keskellä lohkoa, se tulee erottaa rivinvaihdoilla. Kommentit ovat kuitenkin edelleen aina kohteen yläpuolella::

   function muista() {
      write("painetaan mieleen");

      //aseta muistettavaksi asiaksi vakiona muisto
      const muistettava = this.muistettava || 'muisto';

      return muistettava;
   }

Monen rivin kommentit
-------------------------------------------------------------------------------------
Käytä::

/** ... */

kirjoittaaksesi monen rivin kommentin. Älä käytä montaa yhden rivin kommenttia peräkkäin monen rivin kommenttia kirjoittaessa. 
