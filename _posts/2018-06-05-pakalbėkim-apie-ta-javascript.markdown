---
layout: post
comments: true
title: Pakalbėkim apie "Tai"
excerpt_separator: <!--more-->
---

Tęsdama savo užrašų apie pagrindinius Javascript konceptus seriją, tiesiog negaliu praleisti `THIS` temos. Galiu garantuoti praktiškai 100 %,
kad bet kuriame techniniame interviu teks susidurti su `THIS` klausimu vienokiu ar kitokiu būdu. Gal tavęs bus paprašyta, į ką `THIS` referuos
vienu ar kitu atveju, arba bus paklausta, kuo skiriasi `bind`, `apply` ir `call`. Ši tema neabejotinai yra pati svarbiausia JavaScript pasaulyje,
todėl ją suprasti reikia kiekvienam JavaScript programuotojui.

<!--more-->

O turbūt sunkiausia atsakyti į klausimą - kas yra `this` JavaScript kalboje. Tad pabandykime panarstyti šį JavaScript kalbos aspektą.

Kalbant paprastai, raktažodis `this` referuoja į objektą, kuriame duotuoju metu yra vykdomas kodas. Pavyzdžiui, jei naršyklės konsolėje įrašysime
šią eilutę `console.log(this)`, mes gausime `window` objektą, nes naršyklėje globalus objektas yra `window`.

Tą patį mes gautume ir šioje funkcijoje, kadangi ji būtų vykdoma globaliame objekte:

```
function logThis() {
    console.log(this)
}

logThis() // window
```

Dėl šios priežasties mes galime padaryti tokį paprastą fokusą:

```
function createVariable () {
    this.newVariable = 'labas rytas'
}

createVariable()
console.log(newVariable) // labas rytas
```

o jeigu išlogintume patį globalų objektą (`console.log(window)`) ir išskleistume rezultatą, pamatytume savo sukurtą kintamąjį:
![window objektas](/assets/window.png)

Tad su globaliu objektu bei funkcijomis kaip ir viskas aišku - jei funkcija kviečiama globaliame kontekste, `this` referuos į globalų objektą.

O kaip visa tai atrodo neglobaliame objekte?

```
var obj = {
    name: 'Mr Object',
    log: function() {
        console.log(this);
    }
}

obj.log() // Object {name: 'Mr Object', log: f}
```
Kaip matyti, raktažodis `this` referuoja į objektą, mūsų atveju pavadintą `obj`, kadangi jo kontekste yra vykdomas kodas. Pažiūrėkime, kas bus tokiu atveju, jei objekto metodas viduje turi
dar vieną funkciją, kurioje naudojamas raktažodis `this`:

```
var obj = {
    name: 'Mr Object',
    log: function() {
        var updateName = function (newName) {
            this.name = newName;
        }

        updateName('Mrs Objectiss');
        console.log(this);
    }
}

```

Realiame gyvenime mes tokio kodo gal niekada ir nerašysime, bet tai gana aiškiai iliustruos mūsų problemą. Metode `log` mes atnaujiname mūsų objekto *property* `name`.
 Tuomet mes iškviečiame šią funkciją ir išloginame visą objektą. Tikimės, jog `name` dabar bus "Mrs Objectiss", ar ne?

`obj.log(); // Object {name: 'Mr Object', log: f}`

????????????????????????????????????????????????????????

Kas įvyko su mūsų atnaujintu vardu? `console.log(window.name) // "Mrs Objectiss`. Štai kaip. Vidinėje `log` metodo funkcijoje `this` referavo
į globalų objektą, todėl dabar jame turime `name` *property*.

![are you serious?](/assets/are-you-serious.jpg)

Čia yra galbūt viena iš tų keistų JavaScript vietų, apie kurią reikia žinoti. Pataisyti kodą galime keliais būdais. Anksčiau dažnai buvo galima
pamatyti tokį *fixą*:
```
var obj = {
    name: 'Mr Object',
    log: function() {
        var that = this;
        var updateName = function (newName) {
            that.name = newName;
        }

        updateName('Mrs Objectiss');
        console.log(this);
    }
}
```
Mes išsisaugojame `this` reikšmę prieš jai pasikeičiant `that` kintamajame (dažnai naudojamas ir `self`) ir šį kintamąjį naudojame vidinėje funkcijoje.

Taip pat yra ir specialios *built-in* JavaScript funkcijos, kurių pagalba galime teisingai susieti `this` reikšmę. Kalba eina apie `bind`,
`call` ir `apply`.

### `call` ir `apply`

Panagrinėkime labai paprastą pavyzdį, kaip mes galime teisingai susieti `this` kontekstą su `call` ir `apply` pagalba. Turime labai
paprastą objektą:

```
var obj = {
    num: 2
}
```
Ir funkciją:
```
var addToThis = function(a) {
    return this.num + a;
}
```
Šiuo metu funkcija nėra susijusi su objektu, jie gyvena atskirus gyvenimus. Kaip pamenate, `this` funkcijoje referuotų į globalų objektą,
todėl jei tiesiog iškviestume šią funkciją, gautume `NaN`, nes globaliame objekte neturime tokio dalyko kaip `num`.
Tam, kad funkciją galėtume iškviesti mūsų sukurtame objekte `obj`, mes turime juos susieti:

```
addToThis.call(obj, 3) // 5;
```
`call` pirmasis argumentas yra objektas, ant kurio mes norime iškviesti `addToThis` funkciją, o antrasis argumentas yra tai, ką mes norime
paduoti pačiai funkcijai.

Šiuo būdu mes galime teisingai susieti `this` reikšmę ir mūsų ankstesniame pavyzdyje:
```
var obj = {
    name: 'Mr Object',
    log: function() {
        var that = this;
        var updateName = function (newName) {
            that.name = newName;
        }

        updateName.call(this, 'Mrs Objectiss');
        console.log(this);
    }
}
obj.log() // Object {name: 'Mrs Objectiss', log: f}
```
Šįkart pirmasis argumentas yra pats objektas, todėl nurodome `this`.

`apply` veikia lygiai tokiu pačiu principu, vienintelis skirtumas yra tai, kad antrajam argumentui mes paduodame masyvą. Įsivaizduokime labai
panašią situaciją, kurią turėjome su `call`:

```
var obj = {
    num: 2
}

var addToThis = function(a, b, c) {
    return this.num + a + b + c;
}

var arr = [1, 2, 3];
addToThis.apply(obj, arr) // 8;
```
Tai štai ir visas skirtumas tarp `call` ir `apply`. Pastarasis dažniausiai naudojamas tokiais atvejais, kai nežinome tiksliai, kiek argumentų
turėsime.

### `bind`

Funkcija `bind` skiriasi nuo aukščiau aptartų funkcijų tuo, jog ji susieja raktažodį `this` ir mums grąžina teisingai susietą funkciją, kurią
mes galime patys iškviesti vėliau.

Imkime tą patį pavyzdį:

```
var obj = {
    num: 2
}

var addToThis = function(a) {
    return this.num + a;
}

var bound = addToThis.bind(obj) // šioje vietoje paduodame tik objektą, su kuriuo norime susieti funkciją

bound(3) // štai šioje vietoje paduodame addToThis funkcijai argumentus; 5
```

Labai dažnai `bind` yra naudojamas dirbant su vartotojo interakcijomis, pvz, *click events*, kadangi tuomet kodo vykdymo kontekstas pasikeičia.

Pabaigai dar apžvelgsime, kaip `this` veikimas keičiasi
su naująja JavaScript versija ES6, su kuria atsirado `arrow` funkcijos.

### `arrow` funkcijos ir 'Tai'

Išties, nauja anoniminių funkcijų sintaksė yra smagi ne vien dėl jos trumpumo, bet ir dėl skirtingo `this` reikšmės nustatymo.

Kaip matėme, `this` reikšmė priklauso nuo to, kaip ir kada funkcija yra kviečiama. Jei ji kviečiama globaliame objekte, `this` reikšmė bus `window`
objektas, jei funkcija kviečiama kaip objekto metodas, tai `this` reikšmė ir bus tas objektas (plius dar visi keistumai su *nested* funkcijomis ir metodais).

Tačiau su `arrow` funkcijomis `this` reikšmė nėra susiejama priklausomai nuo to, kur ir kada ji iškviečiama. `arrow` funkcijose `this` reikšmė
priklausys nuo to, kur ta funkcija parašyta. Tad jei ji parašyta objekte, `this` reikšmė visada ir bus tas objektas.

Paimkime jau mums matytą pavyzdį ir perrašykime jį naudojant `arrow` funkcijos sintaksę:
```
var obj = {
    name: 'Mr Object',
    log: function() {
        var updateName = (newName) => {
            this.name = newName;
        }

        updateName('Mrs Objectiss');
        console.log(this);
    }
}

obj.log() // Object {name: 'Mrs Objectiss', log: f}
```
Ech, tas `arrow` funkcijų grožis! Tiesą sakant, naudojant naująją sintaksę bent jau man praktiškai netenka "rankiniu būdu" (naudojant `bind`, `call` ar `apply`)
susieti `this` konteksto.

`arrow` funkcijos nusipelno atskiro straipsnio, nes tai išties labai laukiamas ir mėgstamas JavaScript kalbos funkcionalumas, tačiau
`this` kontekste pakanka žinoti, kad `arrow` funkcijose `this` reikšmė imama remiantis pagal tai, kur kodas yra parašytas, o ne kaip jis kviečiamas.

Labai norėčiau sužinoti, ar beskaitydami sužinojote ko nors naujo. Jei taip, rašykite komentaruose!

