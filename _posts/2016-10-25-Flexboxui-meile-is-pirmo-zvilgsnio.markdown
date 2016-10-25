---
layout: post
comments: true
title:  Flexboxui - meilė iš pirmo žvilgsnio
excerpt_separator: <!--more-->
---
Jeigu dar nenaudoji *flexboxo* puslapio kūrime, nežinai, ką prarandi. Tai nuostabi CSS išdėstymo ypatybė, kuri supaprastina CSS ir puikiai
tinka prisitaikančiam dizainui. Neabejoju, tu irgi jį pamilsi. 
<!--more-->

Kad įrodyčiau, koks iš tikrųjų nuostabus yra tas *flexbox*, parodysiu jo naudojimą viename pavyzdyje. Galime panaudoti projektuką, prie kurio šiuo
metu dirbu, ir kuris man padėjo atrasti šią meilę.

![pavyzdys](/assets/pavyzdys-meniu.png)
 
[Šį pavyzdį jau naudojau]({% post_url 2016-10-16-Kaip-patamsinti-fona-su-CSS %}){:target="_blank"}, norėdama parodyti, kaip patamsinti paveiksliuką,
jei reikia suteikti daugiau kontrasto tekstui. 

Štai taip atrodo meniu HTML:

{% highlight ruby %}

<nav class="menu-items">
    <svg width="45px" height="45px">
    <a href="#">news</a>
    <a href="#">features</a>
    <a href="#">prices</a>
    <a href="#">blog</a>
    <a href="#">about</a>
    <div class="search-field">
        <i class="fa fa-search"></i>
    </div>
</nav>

{% endhighlight %}

Visą meniu turime "įvilkti" į atskirą `<div>`, o jį paversti `flex` konteineriu. Reikia turėti omenyje tai, jog tik tiesioginiai konteinerio 
vaikai paveldi `flex` ypatybę. 

Štai mūsų CSS, susijęs su elementų išdėstymu (stilizavimo neįtraukiu paprastumo dėlei): 
 
{% highlight ruby %}
 
.menu-items {
    display: flex;
    flex-flow: row wrap;
    justify-content: flex-end;
}

svg {
 margin-right: auto;
}
 
{% endhighlight %} 

Ir tai viskas, ko mums reikia, kad elementai būtų išdėstyti horizontaliai, o logotipas atsidurtų puslapio kairėje.
Jį "pastumia" `margin-right: auto` nustatymas. `flex-flow: row wrap` užtikrina, jog kai ekranas sumažės, meniu elementai susidėlios eilėmis.
Tai atitinka prisitaikančio dizaino principus.
 
Dabar pagalvokime, kaip visa tai atliktume be *good old* `flexboxo`. Pirmiausia, meniu elementus reikėtų sudėti į `<ul>` ir `<li>`, šiuos 
išdėlioti horizontaliai su `display: inline-block` nustatymu. Logotipas ir paieškos laukelis turėtų turėti savo *divus*. Logotipui nustatytume
`float: left`, o kitiems - `float: right`. Be to, reikėtų nustatyti visų šių elementų maksimalų plotį, kad visi gražiai sutilptų į vieną eilę.

O dabar eikit ir išbandykit pačios. Garantuoju, jog patiks! Beje, daugiau pasimokyti apie *flexboxą* galite
 <a href="https://www.youtube.com/playlist?list=PL4cUxeGkcC9i3FXJSUfmsNOx8E7u6UuhG" target="_blank">The Net Ninja</a> įrašuose.
 
![Titanikas](/assets/titanic.png) 