---
layout: post
comments: true
title: Viskas apie closures
excerpt_separator: <!--more-->
---

Pats efektyviausias būdas besimokant yra užrašų darymas. Tad pamaniau, kodėl man nepasidalinus savo užrašais ir su kitais? Taigi, šiame straipsnyje
nagrinėsiu vieną svarbiausių temų JavaScript kalboje - *closures*. Prašymas paaiškinti *closure* dažnai iškeliamas techninių pokalbių metu,
todėl labai svarbu šią temą suprasti iš esmės ir sugebėti duoti praktinį pavyzdį.

<!--more-->

Pirmiausia, pradėkime nuo paprasto *closure* apibrėžimo. Jeigu naudotume vieno žinomiausių JavaScript guru Kyle Sympson apibūdinimą, *closure*
yra toks atvejas, kai funkcija gali "prisiminti" ir "prieiti" prie savo leksiškos apimties (lexical scope), net jei ta funkcija yra vykdoma už
tos leksiškos apimties ribų.

*Lexical scope* yra dar kita, nors ir susijusi JavaScript tema, tad labai nesigilinant į šį terminą, apie *closures*
galime pasakyti šitaip: tai toks atvejas, kai vidinė funkcija turi prieigą prie ją apgaubiančios funkcijos kintamųjų, nors jei ta vidinė funkcija
yra vykdoma visai kitame konktekste.

Be kodo šią savoką sunku suprasti, tad pažiūrėkime į keletą pavyzdžių.

```
function logName() {
  var name = 'Vingių Jonas';

  function show() {
    console.log(name);
  }
  return show;
}

var person = logName();

person(); // Vingių Jonas
```
Funkcijoje `logName` mes deklaruojame kintamąjį `name`, kuris naudojamas vidinėje funkcijoje `show`, kurią mes vėliau grąžiname.
Tuomet į `person` kintamąjį mes įsidedame grąžintą funkciją (`show`), kurią galiausiai iškviečiame paskutinėje eilutėje.

Gal tai ir neatrodo kažkoks stebuklas, bet ar nekeista, kad mes galime vidinę funkciją iškviesti kada ir kur norime, bet ji vis tiek turi
prieigą prie jos išorinės funkcijos kintamojo (`name`)!

Na gerai, pakeiskime šiek tiek šį kodą, ir tas 'stebuklas' galbūt pasidarys dar įspūdingesnis:

```
 function logName(name) {

   function show() {
     console.log(name);
   }
   return show;
 }

 var person = logName('Vingių Jonas');

 person(); // Vingių Jonas
```

Kas skiriasi šiame variante yra tai, jog nedeklaruojame `name` išorinėje funkcijoje, bet jį paduodame kaip parametrą. Tuomet, kaip ir pirmame
pavyzdyje, mes grąžiname vidinę funkciją, kuri mums išlogina `name`, paduotą ne jai, bet jos išorinei funkcijai.

Galime sakyti, jog vidinė funkcija "uždaro" (closes in) išorinės funkcijos kintamuosius, kuriuos ji gali vėliau panaudoti. Matyt, iš čia ir bus
tas žodis *closure*.

Pažiūrėkime į dar vieną pavyzdį:

```
function greet(greetingWord) {
    return function (name) {
        console.log(greetingWord + ' ' + name);
    }
}
```

Tai štai kodas, kuriame vidinė funkcija naudoja savo ir išorinės funkcijos parametrus. Galiausiai, iškviečiame abi funkcijas su jų parametrais:

```
var greeting = greet('Labas');
greeting('Vingių Jonai'); // Labas Vingių Jonai
```

Labai įdomūs pavyzdžiai būna su skaičių sudėjimu. Tiesiog *magic*:

```
function makeAdder(outer) {
    return function(inner) {
        return outer + inner;
    }
}
```
Šiame pavyzdyje mes grąžiname anoniminę funkciją, kuri grąžina sudėtus išorinės funkcijos ir jos pačios, vidinės, argumentus.

Tuomet:
```
var add3 = makeAdder(3);
var add4 = makeAdder(4);

console.log(add3(3)); // 6 - jėga, matot, kaip ši funkcija 'prisiminė', kad išorinės funkcijos parametras buvo trys??

console.log(add4(4)); // 8 - tas pats ir čia ^
```

Argi ne puikus tas JavaScript pasaulis?

O jeigu *closures* pasirodė gana lengva tema, panagrinėkime pavyzdį su ciklu (*loop*). Turime tokią funkciją:
```
function buildFunctions() {
    var arr = [];

    for (var i = 0; i < 3; i++) {
        arr.push(
            function() {
                console.log(i);
            }
        )
    }
    return arr;
}
```
Jos viduje kuriame masyvą, į kurį kiekvieno ciklo metu įdedame po anoniminę funkciją, kuri tiesiog logina `i` reikšmę. Pastebėkite, jog mes
tiesiog įsidedame į masyvą tas funkcijas, jų neiškviečiame.

Taigi, susikurkime masyvą ir iškvieskime jame esančias funkcijas:
```
var fs = buildFunctions();

// sintaksė gal ir keista, bet mes tiesiog imame masyvo funkcijas ir jas kviečiame:
fs[0]();
fs[1]();
fs[2]();
```

Kaip manote, ką išlogins konsolėje šios funkcijos? `0, 1, 2`? Deja, ne. Rezultatas bus triskart `3`! Whaaaaat???

![ką??](/assets/what.gif)

Iš kur išvis čia trejetas??

Reikalas tame, jog *closure* 'uždaryto' `i` kintamojo reikšmė yra paskutinė, kuri buvo nustatyta cikle. Taigi, sukant pirmą ciklą, `i = 0`, antrą ciklą -
`i = 1`, trečią ciklą `i = 2`. Nepamirškime, jog kiekvieno ciklo pabaigoje `i` yra padidinamas vienu vienetu (`i++`), todėl sukant ketvirtą ciklą
`i` reikšmė jau tapo `3`, tačiau `3 < 3 === false`, todėl iš ciklo buvo išeita. O `var i` reikšmė atmintyje išliko 3.

Štai į tą paskutinę - 3 - reikšmę referuoja mūsų grąžintos funkcijos `fs[0], fs[1], fs[2]`.

Taigi toks tas kabliukas su *closures* cikluose. Naujoji ES6 sintaksė situaciją mums leidžia lengvai pataisyti:
```
function buildFunctions() {
    var arr = [];

    for (let i = 0; i < 3; i++) {
        arr.push(
            function() {
                console.log(i);
            }
        )
    }
    return arr;
}
```

Skirtumai tarp `var` ir `let` reikalauja atskiro straipsnio, bet iš esmės, kalbant labai paprastai,
 `let` kiekvieno ciklo metu sukuria naują kintamąjį, tuo tarpu `var`
jį perrašo iš naujo.

Štai ir aptarėme, kas yra tas mistiškasis *closure*. Gal jūs jau rašote funkcijas, kurių veikimas remiasi *closure*, tačiau to iki šiol nesupratote?

Vienas gana žinomas *closure* panaudojimo būdas yra vadinamajame *Revealing Module Pattern*. Tai vėlgi atskira tema, bet šis *design pattern* yra
tikriausiai vienas žinomiausių JavaScript pasaulyje, kadangi jis leidžia kurti privačius ir viešus metodus bei apsaugo mus nuo globalių kintamųjų
kūrimo ir naudojimo.

Šiais karkasų laikais *Revealing module pattern* nebėra toks aktualus, bet jei norite daugiau programuoti su vanilla JS, galbūt verta į jį
pasigilinti. O pagrindinį jo veikimo principą - *closures* - jau suprantame.

Tikiuosi, kad mano mokymosi užrašai yra aiškūs ir naudingi. O jei radai netikslumą arba turi klausimų, rašyk komentaruose!


