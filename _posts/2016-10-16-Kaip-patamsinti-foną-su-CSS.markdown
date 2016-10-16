---
layout: post
comments: true
title:  Kaip patamsinti foną su CSS
excerpt_separator: <!--more-->
---
Fono tamsinimo gali prireikti tuo atveju, jei kontrastas tarp paveiksliuko ir teksto yra per mažas, todėl tekstas nepakankamai ryškus.
Tokia situacija iškilo ir man, todėl teko ieškoti sprendimo. Šiame straipsnyje aptarsiu galimus fono tamsinimo variantus su CSS.
<!--more-->
 
Šiuo metu kuriu puslapį pagal išsirinktą dizainą. Tai puiki proga įtvirtinti CSS žinias bei atrasti naujų dalykų. Be to, šis puslapis taps 
mano portfelio dalimi, kurį reikės rodyti būsimam darbdaviui. Taigi, jei to dar nedarai, tai labai rekomenduoju.
 
Nemokamų dizainų galima susirasti interneto platybėse. Gana populiarus yra <a href="https://dribbble.com/" target="_blank">Dribbble</a>. Aš savąjį radau 
<a href="https://themeforest.net/" target="_blank">Themeforest</a>. Žinoma, visus nemokamus dizaino pavyzdžius galima naudoti tik nekomerciniais
tikslais. 
  
Štai kaip atrodo viršutinė puslapio dalis, kuri, mano nuomone, nesuteikia pakankamai ryškumo tekstui. Galėčiau parinkti tamsesnę nuotrauką
ir tokiu būdu apeiti problemą, tačiau realiame gyvenime ne visada bus toks pasirinkimas.
  
![neryški dalis](/assets/neryski-dalis.png)  

### Sprendimas su pseudo elementu `:before`

`:before` yra pseudo elementas, kuris leidžia įterpti turinio dalį į puslapį iš CSS (todėl tos dalies nereikia nurodyti HTML) prieš rodant
likusią turinio dalį. Tikriausiai girdėjote apie pseudo elementą `:after`, kadangi jis dažnai naudojamas kaip *clearfix* metodas. Jis įterpia 
norimą turimo dalį jau po puslapio užkrovimo.

HTML:
  

{% highlight ruby %}

<div class="header-picture overlay">
    <div class="header-content">
        <div class="header-vertical-text">
            <p>Magic blog</p>
        </div>
        <div class="blog-title">
            <p>Travel</p>
        </div>
        <div id="publication-number">
            <p>83 Publications</p>
        </div>
    </div>
</div>


{% endhighlight %}

CSS:
```{r}
.header-content {
  position: relative;
}
.header-picture {
  height: 250px;
  position: relative;
  background: url(image.jpg) no-repeat 0 70%;
  background-size: cover;
}
.overlay:before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 250px;
  background: rgba(0, 0, 0, 0.4);
}
```
Jeigu tiesiog paprastai įterptume `.overlay` klasę, šis sluoksnis užgožtų tekstą, todėl ir jis būtų patamsintas. `:before` mums leidžia įterpti
patamsintą sluoksnį dar prieš parodant tekstą, todėl šis išlieka nepakitęs. 

Veikia, bet gana sudėtingas būdas pasiekti norimą rezultatą. Laimei, yra geresnis ir paprastesnis.

### Sprendimas su gradientu

Šiam sprendimui HTML *rinkmena* (matot, kaip stengiuosi naudoti [lietuviškus terminus]({% post_url 2016-10-12-Lietuvisku-programavimo-terminu-atradimai %}){:target="_blank"} :)) išlieka tokia pati, išskyrus tai, jog nereikalinga papildoma klasė (`overlay`). Gradientai paprastai naudojami spalvos
perėjimo efektui padaryti. Tačiau, kadangi mums reikia vientisos spalvos, mes abi spalvas nurodome tokias pačias. 

CSS: 
```{r}
.header-picture {
    height: 250px;
    background: linear-gradient(
        rgba(0, 0, 0, 0.4),
        rgba(0, 0, 0, 0.4)
        ),
        url(image.jpg) no-repeat 0 70%;
    background-size: cover;
}

``` 
Taip, tik tiek. Tiesa, IE9 ir senesnės IE naršyklės nepalaiko CSS gradientų, todėl jei reikalinga, jog svetainė veiktų ir su šiomis naršyklėmis,
reikia pridėti vadinamąjį *prefixą*. Beje, pasitikrinti, kurios naršyklės palaiko kurias funkcijas galima <a href="http://caniuse.com/" target="_blank">Can I Use</a>
 svetainėje. 

Štai abu sugretinti variantai:

![neryški dalis](/assets/neryski-dalis.png)
![paryškintas kontrastas](/assets/paryskintas-kontrastas.png) 

Mano nuomone, sprendimas su gradientu yra kur kas efektyvesnis. Be to, aš stengiuosi vengti absoliučiai pozicionuojamų elementų, nes mane
kankina galbūt ne visiškai racionali baimė, jog and skirtingo dydžio prietaisų ekranų tas paveiksliukas gali kaip nors išsikreipti. O su gradientu
tai visiškai negresia. 

O galbūt radai dar kokį variantą, ir gal jis dar geresnis? Pasidalink komentaruose!
 




 
 