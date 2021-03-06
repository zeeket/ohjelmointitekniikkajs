Sulkeumat
================================

Sulkeumat ovat funktioita jotka säilyttävät tietoa. Sulkeumat mahdollistavat sellaisten muuttujien piilottamisen joita ei tarvita juuri tietyssä kohdassa ohjelman suoritusta.  
Yleensä kun missä tahansa ohjelmointikielessä luodaan funktio, funktiolle annetaan joko parametrejä tai funktioon määritellään jonkinlaisia sisäisiä arvoja. JavaScriptissä sulkeuman saa helpoiten käyttämällä funktiota funktion sisällä ja suljuttamalla halutut muuttujat ensimmäiseen funktioon. **Tärkeää:** JavaScriptissä sisäisillä funtioilla on näkyvyys funktion ulkoiseen viittausympäristöön. Toisinsanoen sisältä nähdään ulos, muttei päinvastoin. `Lohkot <lohkot.html>`_ eivät myöskään ole näkyvyysalueita JavaScriptissä, toisin kuin Javassa. 

Sulkeuman muuttujat suorituksen jälkeiseen aikaan
--------------------------------------------------------------------------------------

Vapaat muuttujat ovat muuttujia joita ei ole paikallisesti määritelty, eikä annettu funktiolle parametrinä. Seuraavassa esimerkissä nähdään miten sulkeumaan suljetut vapaat muuttujat säilyvät sulkeuman suorituksen jälkeiseen aikaan, sekä miten globaali näkyvyysalue ei näe funktion sillä olevaan paikalliseen näkyvyysalueeseen::

   let lisaa = (function () {
      let laskuri= 0;
      return function () {laskuri+=1;return laskuri}
   })();

   let laskuri = 1;
   write(lisaa()); //tulostuu 1
   write(lisaa()); //tulostuu 2
   write(laskuri); //tulostuu 1
   write(lisaa()); //tulostuu 3

Määritellyt funktio päättyy, sulkeuma säilyy 
------------------------------------------------------------------------------------------------
Sulkeumaan suljetuttujen vapaiden muuttujien määritellyt funktio voi päättyä, mutta sulkeuma säilyy. Seuraavassa esimerkissä matalaHuutaja() ja kovaHuutaja() ovat kummatkin sulkeumia. teeHuutaja() luo funktioita jotka lisäävät halutun määrän huutomerkkejä huutoon- se tapahtuu ensin vaihtamalla kuinkaPaljon nimisen muuttuajan arvoa jonka jälkeen oikea määrä huutomerkkejä tallentuu sulkeumaan ja jää sellaisenaan funktion assosiaatiolistaan vaikka lisää huutajia luodaan::

    function teeHuutaja(){
    let huutomerkit = "!".repeat(kuinkaPaljon);
    return function(mitaHuutaa) {
      let huudettava=mitaHuutaa.toUpperCase();
      return huudettava+huutomerkit;
      }
    }

    let kuinkaPaljon = 1;
    let matalaHuutaja = teeHuutaja();
    let kuinkaPaljon = 5;
    let kovaHuutaja = teeHuutaja();

    write(kovaHuutaja("kova huuto")); //tulostuu KOVA HUUTO!!!!!
    write(matalaHuutaja("hiljaisempi huuto")); //tulostuu HILJAISEMPI HUUTO!
    write(kovaHuutaja("nyt")); //tulostuu NYT!!!!!



Sulkeumat käytännössä
-------------------------------------

Esimerkiksi jos halutaan tehdä jotain jokaisella taulukon indeksillä, mutta ei haluta muuttaa alkuperäistä taulukkoa::

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
      write(taulukko[i].data);
   }

On myös tärkeää ymmärtää, että sulkeumien avulla toteutetaan yleisesti "kapselointi" rakenne/ kuvio. Kapselointi on tuttu olio-ohjelmoinnista "yksityisten" tai "piilotettujen" kenttien kautta, joita sitten muutetaan aksessorien kautta. Laskuri- esimerkissä laskurin sen hetkinen luku on kapseloitu sen sisälle.
