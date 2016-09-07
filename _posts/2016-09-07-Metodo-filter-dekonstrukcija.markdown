---
layout: post
comments: true
title:  Metodo .filter() dekonstrukcija
excerpt_separator: <!--more-->
---
Metodai Javascript programavimo kalboje sukurti tam, jog dažnai rašomą kodą būtų galima sutrumpinti. Vienas iš tokių metodų yra `.filter`, ir
šiame straipsnyje mes pamėginsime išsiaiškinti, kaip jis sukonstruotas.
<!--more-->

Tokie pratimai padeda įgauti gilesnį supratimą apie programavimo kalbą. Šis metodas yra taikomas masyvams (array), ir paprastai tariant, jis ima kiekvieną masyvo elementą ir 
vykdo nurodytą funckiją, o rezultatą grąžina į naują masyvą. Tai padeda išvengti FOR ciklo (loop) bei IF sąlygos sakinio. Pirmiausia, pradėkime nuo 
šių ir išfiltruokime masyvą išplėstiniu būdu.

{% highlight ruby %}

# 1. sukuriame masyvą, kuriuo norime manipuliuoti
# 2. konstatuojame tuščią masyvą, į kurį sudėsime išfiltruotus elementus

var myArray = [0, 0, 1, 0, 1, 0]; 
var newArray = []; 

# 1. užvedame FOR ciklą, kuris nustatytas kartoti tiek kartų, kiek yra masyve elementų
# 2. su IF sąlygos sakiniu atsirenkame, kurių elementų mums reikia. Šiuo atveju, mes norime vienetų. 
# 3. su .push metodu sudedame vienetus į tuščią masyvą
 
function filterArray(element) {
	for (var i = 0; i < myArray.length; i++) { 
		if (element[i] === 1) { 
			newArray.push(element[i]); 
		}
	} return newArray;
}
filterArray(myArray); # mūsų gautas rezultatas - [1, 1]
{% endhighlight %}

Kodo ilgis - 8 eilutės. Dabar pažiūrėkime, kaip `.filter()` metodas sutrumpina šį kodą.

{% highlight ruby %}

# nustatome funkciją, kuri tikrina, ar elementas atitinka kriterijų, t.y. ar dėti į naują masyvą.

function myFilter(element) {
	return element === 1;
}
# nurodome, kokiam masyvui pritaikyti mūsų filterWithFilter funkciją
myArray.filter(myFilter) // rezultatas - [1, 1]
{% endhighlight %}

Matote, kodas viso labo trijų eilučių ilgio (eilučių skaičius priklauso ir nuo rašymo stilius. Man patinka labiau išplėstas, nes jį lengviau skaityti).
Dėl jo trumpumo sumažėja kodo įvedimo klaidų tikimybė.
`filter()` metodą galima rašyti ir su anonimine funkcija. Tuomet viskas atrodytų taip: 

{% highlight ruby %}
myArray.filter(function(element) {
	return element === 1;
});
{% endhighlight %}

Tai štaip veikia `.filter()` metodas. 

Turi klausimų ar idėjų? Rašyk komentaruose!
