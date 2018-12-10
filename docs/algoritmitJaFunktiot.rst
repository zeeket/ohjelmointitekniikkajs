Algoritmejä ja funktioita
=========================

Kaikessa ohjelmoinnissa, mukaanlukien JavaScriptissä, on keskeisessä osassa hyvien ratkaisujen löytäminen loogisiin ongelmiin. JavaScript ei kuitenkaan yleisesti ottaen ole niin performanssikriittinen kieli kuten esimerkiksi C, ja sen eri iteraatiot, sillä JavaScript pyörii selainympäristössä. Huolimatta ympäristön rajoittavista tekijöistä, voi JavaScriptillä toteuttaa erittäinkin viisaita ja ohjelmallisesti nopeita ratkaisuja, algoritmejä. Tästä hyvänä esimerkkinä on Oleksii Trekhlebin aloittama kirjasto "javascript-algorithms", jossa on toteutettu Javasta yleisimmät ja tunnetuimmat tietorakenteet sekä algoritmit. Loppujen lopuksi ajallisesti eivät kyseiset implementaatiot yllä performanssikriittisimpien kielien toteutuksiin. 

Alla olevassa esimerkissä laskimme tutun for-silmukan sisällä tapahtuvaa lisäysoperaation performanssia verraten sitä kielen omaan reduce-funktioon.
Testit on suoritettu `Pienessä testiympäristössä <https://www.cs.helsinki.fi/u/wikla/OTjs/materiaalia/suoritus/Testiymparisto.html>`_::

    const posts = [ 
    {upVotes: 2},
    {upVotes: 18}, 
    {upVotes: 1}, 
    {upVotes: 30}, 
    {upVotes: 50} 
    ];
    let sum = 0;
    console.time('reduce');
    sum = posts.reduce((s, p)=> s+=p.upVotes,0);
    console.timeEnd('reduce')

    sum = 0;
    console.time('for loop');
    for(let i=0; i<posts.length; i++) {
        sum += posts[i].upVotes;
    }
    console.timeEnd('for loop');

    sum = 0;
    console.time('for each');
    posts.forEach(element => {
        sum += element.upVotes;
    });

    console.timeEnd('for each');

    //reduce: 3ms
    //for loop: 1ms
    //for each: 0ms

Tässä testissä huomataan, että hyvin pienellä testidatalla (5 alkiota) kielen oma funktio reduce on hitain, mutta kun testidataan lisätään lisää alkioita::

    let i = 0;
    for(i = 0; i < 10000000; ++i){
    upVotes = i;
    posts.push(upVotes);
    }

    //reduce: 1306ms
    //for loop: 2137ms
    //for each: 607ms

10 miljoonalla alkiolla saadaan luotettavampaa dataa, jolloin for each on edelleen nopein silmukka, mutta reduce funktio on nyt nopeampi kuin for-silmukka.
Tämä todennäköisesti natiivin reduce-funktion raskaudesta, joka tulee ilmi pienellä testidatalla. Toisaalta natiivissa reduce-funktiossa on toteutettu jotain
optimointeja, joka nopeuttaa taulukon läpikäyntiä suurella testidatalla.

Testeistä huomataan, että silmukan läpikäynti on huomattvasti hitaampaa, kuin muissa laajasti käytetyissä ohjelmointikielissä. Tämä onkin erittäin hyvä syy käyttää muuttujien, parametrien ja funktioiden tyypittömyyttä hyväksi. JavaScriptin tyypittömyys luo erittäin hyvät työkalut toteuttaa yleispäteviä algoritmejä ja funktioita, joita voidaan koodissa uudelleenkäyttää helposti. Esimerkiksi voidaan luoda funktio, joka järjestää erityyppisten alkioiden taulukon järjestykseen vaikka niin, että ensin tulee numerot pienimmästä suurimpaan ja sitten merkkijonot aakkosjärjestyksessä. Tämän tyylisten apufunktioiden luominen on yleistä JavaScriptissä, ja sitä pitäisi käyttää hyödykseen yhä enemmän.

Imperatiivinen- vs. funktionaalinen ohjelmointi
-----------------------------------------------

JavaScriptiä suurimmaksi osaksi tehdään imperatiivisesti, todennäköisesti johtuen kaikkien tutoriaalien ja aloittelevien ohjelmoijien tavasta aloittaa ohjelmointi. Kuitenkin lopulta imperatiivisella tavalla ohjelmointi tuottaa "huojuvan tornin" ja liikuteltaessa alimpia palikoita, koko torni romahtaa ja sen joutuu rakentamaan uudestaan. Tätä yritetään tietysti välttää viimeiseen asti, jolloin funktionaalinen ohjelmointi tulee kuvioihin mukaan. Funktionaalisella ohjelmoinnilla on hyvin paljon hyötyjä imperatiiviseen ohjelmointiin nähden. Sillä mm. vähennetään koodin mutaatiota, koodin testaaminen helpottuu, rakenne pysyy mielekkäänä sekä koodiin on helpompaa tehdä muutoksia. Hyvin usein JavaScriptiä käytetään ohjelmoinnissa julkisivun tekemiseen, tästä hyviä esimerkkejä ovat esimerkiksi React, Redux ja Vue, jolloin funktionaalinen ohjelmointi ja "puhtaat funktiot" ovat käytännön asioita ja tapoja joita on käytettävä. Lähtökohtana on se, ettei mitään alkuperäistä oliota/muuttujaa muuteta suoraan, vaan luodaan siitä ensin kopio jota käytetään jatkossa. Täysin funktionaalisesti ei voida JavaScriptiä kuitenkaan ohjelmoida, jolloin funktionaalisen ja imperatiivisen ohjelmoinnin tasapainoittelu koodin kirjoittamisessa on paras lähestymistapa ohjelmistokehitykseen JavaScriptillä.
