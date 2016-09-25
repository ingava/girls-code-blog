---
layout: post
comments: true
title:  Apie JavaScript "hoisting" ir kitus įdomius dalykus
excerpt_separator: <!--more-->
---
Atradau dar vieną įdomų kursą, kuriame, kaip sako dėstytojas, "lendame po JavaScript gaubtu" ir mokomės, kaip iš tikrųjų veikia ši programavimo
kalba. Man ypač įstrigo "hoisting" terminas, kurio nesuprantant gali kilti įvairių keistų klaidų.
<!--more-->

Vienoje iš programavimo naujokų facebook grupių buvo įkelta nuoroda į 3.5 val. ilgio <a href="https://www.youtube.com/watch?v=Bv_5Zv5c-Ts" target="_blank">youtube paskaitą</a>. 
Kaip tik jau buvau baigusi [paskaitų ciklą]({% post_url 2016-09-13-Geriau-pazinkim-kompiuteri-ir-interneta %}){:target="_blank"} apie kompiuterius 
ir internetą, todėl ieškojau kažko, ką galiu žiūrėti valgydama ar šiaip kažką veikdama. 

Šiame kurse detaliai analizuojama, kaip veikia JavaScript programavimo kalba, ir aiškinami iš pirmos pažiūros keistesni šios kalbos aspektai
(man keistų aspektų nėra, nes neturiu su kuo šios kalbos palyginti).
 
Pasirodo, kodo vykdymas susideda iš kelių fazių. Pirmiausia, JavaScript variklis nuskaito kodą ir išsaugo jį atmintyje. Todėl funkcijas
JavaScript kalboje galima rašyti ir tokiu būdu:

{% highlight ruby %}
b();

function b() {
  console.log("Hello World!);
}
{% endhighlight %}
Tai nemes jokių klaidų, kadangi JavaScript variklis jau buvo nuskaitęs šį kodą anksčiau ir išsisaugojo `b` funckiją. Tačiau istorija su kintamaisiais
yra kiek kitokia, todėl tokie triukai čia neišdegs. Pavyzdžiui, jei savo programą parašysite tokia tvarka:

{% highlight ruby %}
console.log(a);

var a = "Hello World!"
{% endhighlight %}

konsolėje matysite `undefined`. Taip yra todėl, jog JavaScript variklis, skaitydamas kodą pirmą kartą, atmintyje išsaugo kintamuosius, o jų
reikšmę priskiria `undefined`, kadangi šioje fazėje nėra aišku, kokia gi bus kintamojo reikšmė. O jau tik kodo vykdymo fazėje kintamojo reikšmė yra priskiriama tokia, kokia yra nurodyta programoje.

Ši dalis, kai nuskaitomas kodas ir išsaugomas atmintyje, klaidingai vadinamas "hoisting" - kodo dalių kėlimas viršun. Klaidinga todėl, jog
pats kodas niekur nėra kilnojamas, tiesiog jis išsaugojamas atmintyje.
 
Šios istorijos moralas tikriausiai toks, kad globalūs kintamieji turėtų būti apibrėžiami programos pradžioje, o tik po to naudojami funkcijose. 
Antraip, gausite keistas klaidas - kintamųjų reikšmės bus `undefined`. 

O kol neišsiaiškinau daugiau pamatinių JavaScript veikimo aspektų, programuoju daugiau ar mažiau šitaip:
![JavaScript](/assets/Javascript-please-work.png) 
 
 