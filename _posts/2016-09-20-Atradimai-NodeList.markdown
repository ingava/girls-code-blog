---
layout: post
comments: true
title:  Atradimai žaidžiant su getElementsByClassName
excerpt_separator: <!--more-->
---
Šiandien besimokydama jau, atrodo, žinomų dalykų apie JavaScript sąveiką su DOM, atradau visiškai naują ir negirdėtą - `NodeList`. Tai panašus
dalykas į `array`, bet yra labai svarbių skirtumų, kuriuos reikia turėti omenyje manipuliuojant DOM. 
<!--more-->

Su `NodeList` susidursi norėdama pasirinkti daugiau nei vieną DOM elementą, pavyzdžiui:

{% highlight ruby %}
# įsivaizduokime, jog html turime keletą h3 elementų su klase "bolded"
var tags = document.getElemenentsByClassName("bolded");

# maždaug taip atrodys rezultatas konsolėje:
tags 
[ <h3 class="bolded">Heading</h3>, <h3 class="bolded">Heading</h3>, <h3 class="bolded">Heading</h3>]
{% endhighlight %}

Panašu į `array`, bet ne `array`. Didžiausias skirtumas yra tai, jog `NodeList` negali taikyti metodų, kuriuos taikytum `array`. 
Pavyzdžiui, norėdama pereiti per visus `NodeList` elementus negali taikyti `forEach` ar `map` metodų. Tai gali padaryti su `for` ciklu.
Tačiau gali naudoti `length` metodą:

{% highlight ruby %}
tags.length # rezultatas: 3
{% endhighlight %}

Gera žinia yra tai, jog jeigu tau reiktų visgi taikyti įvairius metodus, tu gali paversti `NodeList` į `array`.
Štai du būdai, bet jų yra ir daugiau:

{% highlight ruby %}
var tags = document.getElemenentsByClassName("bolded");
var myArray = Array.prototype.slice.call(tags); 
# arba
var myArray = Array.from(tags);
{% endhighlight %}

Turi klausimų ar pastebėjimų? Rašyk komentaruose!