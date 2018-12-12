Lohkot
================================

Lohkosijoitus on joukko sijoituksia. JavaScriptissä lohko rajataan aaltosulkeilla { } .
Lohko voi olla nimetty.::

   NimettyLohko: {
   //tee jotain
   }

Lohko näkyvyysalueena   
-------------------------------------------------------------------------------------

var- avainsannalla asetetut muuttujat EIVÄT tottele lohkoa näkyvyysalueena. 
let- ja const- avainsanoilla asetetut muuttujat sen sijaan saavat näkyvyysaluekseen sen lohkon missä ne sijaitsevat.
Tämän takia var:in käyttöä tulisi välttää. Sen sijaan tulisi käytää let- ja const- sijoituksia. Jos muuttujan uudestaan alustukselle ei ole mitään syytä niin on suositeltavaa käyttää const määrittelyä. Jos alustukselle on tarvetta niin let on hyvä vaihtoehto.

Muista käyttää aaltosulkeita
------------------------------------------------------------------------------------------------

JavaScript ymmärtää seuraavanlaisen if-lauseen::

   if (jotain)
      return false;

Mutta se on huono tapa. Muista käyttää aaltosulkeita kaikissa monirivisissä lohkoissa::

   if (jotain) {
      return false;
   }

Jos lohko mahtuu kuitenkin järkevästi yhdelle riville, aaltosulkeita ei tulisi käyttää koska se saattaa sekoittua uuden olion luonnin syntaksin kanssa::

   if (jotain) return false;

if & else- lohkot
------------------------------------------------------------------------------------------------

Laita else:t samalle riville if:fien sulkevan aaltosulkeen kanssa::

   //älä tee näin
   if (jotain) {
      juokse();
      write("moi");
   }
   else {
      hiivi();
   }

   //tee suinkin näin
   if (jotain) {
      juokse();
      write("moi");
   } else {
      hiivi();
   }


