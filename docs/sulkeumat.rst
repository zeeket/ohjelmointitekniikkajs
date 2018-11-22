Sulkeumat
================================

Sulkeumat ovat funktioita jotka säilyttävät tietoa. Sulkeumat mahdollistavat sellaisten muuttujien piilottamisen joita ei tarvita juuri tietyssä kohdassa ohjelman suoritusta.  
Yleensä kun missä tahansa ohjelmointikielessä luodaan funktio, funktiolle annetaan joko parametrejä tai funktioon määritellään jonkinlaisia sisäisiä arvoja. JavaScriptissä sulkeuman saa helpoiten käyttämällä funktiota funktion sisällä ja suljuttamalla halutut muuttujat ensimmäiseen funktioon. **Tärkeää:** JavaScriptissä sisäisillä funtioilla on näkyvyys funktion ulkoiseen viittausympäristöön. Toisinsanoen sisältä nähdään ulos, muttei päinvastoin. Lohkot eivät myöskään ole näkyvyysalueita JavaScriptissä, toisin kuin Javassa. 


Sulkeumaan suljetut vapaat muuttujat säilyvät sulkeuman suorituksen jälkeiseen aikaan
--------------------------------------------------------------------------------------

Vapaat muuttujat ovat muuttujia joita ei ole paikallisesti määritelty, eikä annettu funktiolle parametrinä. Seuraavassa esimerkissä nähdään myös miten globaali näkyvyysalue ei näe funks�llä olevaan paikalliseen näkyvyysalueeseen.::

   var lisaa = (function () {
      var laskuri= 0;
      return function () {laskuri+=1;return laskuri}
   })();

   var laskuri = 1;
   write(lisaa()); //tulostuu 1
   write(lisaa()); //tulostuu 2
   write(laskuri); //tulostuu 1
   write(lisaa()); //tulostuu 3


Sulkeumaan suljetuttujen vapaiden muuttujien määritellyt funktio päättyy, mutta sulkeuma säilyy
------------------------------------------------------------------------------------------------
Seuraavassa esimerkissä matalaHuutaja() ja kovaHuutaja() ovat kummatkin sulkeumia. teeHuutaja() luo funktioita jotka lisäävät halutun määrän huutomerkkejä huutoon- se tapahtuu ensin vaihtamalla kuinkaPaljon nimisen muuttuajan arvoa jonka jälkeen  oikea määrä huutomerkkejä tallentuu sulkeumaan ja jää sellaisenaan funktion assosiaatiolistaan vaikka lisää huutajia luodaan.::

    function teeHuutaja(){
        var huutomerkit = "!".repeat(kuinkaPaljon);
        return function(mitaHuutaa) {
              var huudettava=mitaHuutaa.toUpperCase();
              return huudettava+huutomerkit;
        }
    }

    var kuinkaPaljon = 1;
    var matalaHuutaja = teeHuutaja();
    var kuinkaPaljon = 5;
    var kovaHuutaja = teeHuutaja();

    write(kovaHuutaja("kova huuto")); //tulostuu KOVA HUUTO!!!!!
    write(matalaHuutaja("hiljaisempi huuto")); //tulostuu HILJAISEMPI HUUTO!
    write(kovaHuutaja("nyt")); //tulostuu NYT!!!!!



Sulkeumat käytännössä
-------------------------------------

Esimerkiksi jos halutaan suorittaa funktio jokaisella taulukon indeksillä, mutta ei haluta tärvellä alkuperäistä taulukkoa.:: 

   var taulukko = [{data:"voi"},{data:"ei"}];

   taulukko.forEach(function(indeksi){
      var juttu = indeksi.data;
      function a(){
         juttu += " toinen";
         alert(juttu);
      };
      a();
   });

   for(var i=0;i<taulukko.length;i++){
      alert(taulukko[i].data); //alkuperäiset voi ja ei
   }

