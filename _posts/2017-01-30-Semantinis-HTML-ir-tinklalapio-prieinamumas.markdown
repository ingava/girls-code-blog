---
layout: post
comments: true
title: Semantinis HTML ir tinklalapio prieinamumas
excerpt_separator: <!--more-->
---

Dažnai apie HTML programuotojai galvoja kaip apie mažiausiai svarbų dalyką. Kai kurių iš jų manymu, HTML nėra tikra programavimo kalba,
todėl neverta skirti daug dėmesio išmokti rašyti gerą HTML. Tačiau geras HTML reiškia semantinis HTML, o tai ypač aktualu didinant tinklalapio
prieinamumą.

<!--more-->

Šiame straipsnyje ir aptarsime, kodėl semantinis HTML yra svarbu, ir kaip parašyti tokį kodą, kuris būtų draugiškas įvairias negalias
turintiems tinklalapio lankytojams.

Semantinis HTML yra skirtas perteikti tinklalapio turinio reikšmę, o ne jo išdėstymą ir reprezentaciją. Šią funkciją atlieka CSS. Semantinis
kodas suteikia naršyklėms daugiau informacijos apie elementų paskirtį ir jų sąsajas su likusiu turiniu.

Ekranų skaitymo programos paverčia tekstą į kalbą bei naudoja įvairius HTML elementus navigacijai. Pavyzdžiui, teksto skaitymo programa, atpažinusi
skirtingas `h1` - `h6` žymes, gali pritaikyti skirtingą intonaciją, o tai atitinkamai leidžia suprasti klausytojui elementų hierarchiją. Tinkamai
naudojant šias žymes taip pat palengvinama tinklalapio navigacija, kadangi įvairios pagalbinės programos gali jomis vaikščioti ir leisti
vartotojui praleisti ar pasirinkti dominančią turinio dalį.

Tinkamai parašytos duomenų lentelės taip pat gali suteikti papildomos navigacijos. Panašiai ir su sąrašais - ekranų skaitymo prgramos gali
nuskaityti, kiek sąraše yra elementų.

Yra keletas svarbių bet nesudėtingų principų, užtikrinančių semantinį HTML kodą.

Pirmiausia, konteinerių elementai turi būti naudojami tik išdėstymui, o ne perteikti turiniui. divai ir spanai neturi jokios semantinės reikšmės.
Todėl kai divai ir spanai yra naudojami vietoje antraščių ar mygtukų, naršyklė negali jų paversti į alternatyvius formatus, kuriuos galėtų panaudoti
įvairūs prieinamumą suteikiančios technologijos.

Antra, semantinės HTML žymės turi būti naudojamos pagal paskirtis. Antraštės kuriamos `h1` - `h6` žymėmis, duomenys suguldomi į lenteles,
nuorodos (`a`) naudojamos navigacijai, o mygtukai (`button`) - tam tikriems veiksmams atlikti. `input` žymės visuomet turi būti formos elemento
viduje, prie jų turi būti `label` aprašas. Sąrašo elementai turi visada būti žymių `ol` arba `ul` viduje.

Žymė `h1` turėtų būti naudojama tik vieną kartą puslapyje, paprastai pavadinimui. Apskritai, jei visos antraštės būtų išimtos iš konteksto,
jos turėtų logiškai perteikti tinklalapio turinį.

Trečia, puslapiui turi būti suteikta aiški struktūra naudojant `header`, `nav`, `main`, `article`, `aside`, `footer` žymes.

Gal atrodo ir nemažai dalykų, kuriuos reikia turėti omenyje, bet tai yra įpročio reikalas. Porą kartų apie juos pagalvojus, toliau viskas
vyksta jau automatiškai.

Be to, semantinis HTML kodas taip pat pasitarnauja SEO. Kuo geriau struktūrizuotas tinklalapis, tuo aukštesnis reitingas jam suteikiamas
tarp paieškos rezultatų (žinoma, tai tik vienas iš daugybės kitų faktorių).

Nagi, parodykim truputį daugiau meilės senam geram HTML!

![HTML tatuiruotė ant kaklo](/assets/html.jpg)

Gal irgi turi patarimų, kaip rašyti geresnį HTML? Dalinkis jais komentaruose!

