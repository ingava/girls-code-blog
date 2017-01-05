---
layout: post
comments: true
title: Kodėl CSS "outline" pašalinimas yra pavojinga praktika?
excerpt_separator: <!--more-->
---
Galbūt jums teko koduoti dizainą, kuriame, pavyzdžiui, *input* laukelis yra apvaliais kampais? Kaip tuomet negražiai atrodo, kai šis laukelis yra
kvadratiniame fokuso kontūre. Anksčiau net nesusimąsčiusi, kam tas kontūras fokuso metu reikalingas, jį tiesiog pašalindavau su `outline: none` (gerai,
kad tai nebuvo tikri projektai). Tačiau naršyklių *default* elgesys nėra be priežasties, ir šiuo atveju tą priežastį yra svarbu suprasti.
<!--more-->

CSS `outline` apibrėžia liniją aplink elementą, kuris yra fokuse. Tai ypač reikalinga ypatybė ekrano skaitymo įrenginiams, kuriuos naudoja
regos sutrikimus turintys asmenys. Be šio naršyklės elgesio tokiems asmenims internetiniai puslapiai tampa sunkiai prieinami, jais neįmanoma
naviguoti naudojant TAB mygtuką.

Dažnu atveju programuotojai yra kone priversti pašalinti šį numatytą elgesį, kadangi reikia įgyvendinti kokį nors įmantrų dizainą. Be to,
kai kurie "CSS reset" paruoštukai nuima `outline` (pavyzdžiui, gana žinomas Eric Mayers CSS Reset šablonas), todėl būtina nepamiršti vėl jį pridėti koduojant dizainą.

Kaip apeiti šią situaciją, kad dizainas išliktų patrauklus, o puslapis prieinamas visiems? Nors iš pažiūros `outline` ypatybė yra panaši į rėmelį,
tačiau jai negalima nuimti sienų ar uždėti spindulį. Visgi, formuojant stilių turime truputį pasirinkimo: galima pakeisti fono spalvą,
pakeisti teksto spalvą arba patį kontūrą. Padariau paprastą codepen pavyzdėlį, atsidarę pavaikščiokit su TAB mygtuku:

<p data-height="265" data-theme-id="0" data-slug-hash="egmVLL" data-default-tab="html,result" data-user="inga_va" data-embed-version="2" data-pen-title="Outline styling example" class="codepen">See the Pen <a href="http://codepen.io/inga_va/pen/egmVLL/">Outline styling example</a> by Inga (<a href="http://codepen.io/inga_va">@inga_va</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

Apskritai, mano nuomone, programuotojai skiria per mažai dėmesio jų kuriamų produktų prieinamumui. Ir negali jų kaltinti, nes mes ir be to
turime apgalvoti daugiau nei 1293453 dalykų (skaičius čia atsitiktinis, bet juk tikrai daug ką turime apgalvoti). Prieinamumo tema labiau domėtis
mane įkvėpė <a href="https://medium.freecodecamp.com/looking-back-to-what-started-it-all-731ef5424aec#.jumbslgec" target="_blank">Medium platformoje matytas straipsnis</a> apie tai, kaip aklas žmogus mokosi programavimo ir su kokiomis problemomis jis susiduria.

`outline` yra tik viena iš dalių, kurios padaro puslapį labiau prieinamą regos ar kitokius sutrikimus turintiems asmenims (beje, Indijoje mačiau
kūrybišką neįgaliųjų įvardijimą - "differently abled" :) ). Prieinamumo tema nusipelno straipsnių serijos - galbūt jai pribręsiu ir dar jums
parašysiu.

Beje, su Naujaisiais jus visus! Tebūnie jie laukiamų pokyčių metai. O gal ir rezoliucijų prisirašėte? Dalinkitės komentaruose. Sako, jei jau
prisižadi viešai, tai kur kas sunkiau savo pažadų nevykdyti.

![Naujųjų metų rezoliucija](/assets/new-year-resolution.jpg)



