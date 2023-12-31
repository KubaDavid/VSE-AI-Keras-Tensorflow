<<<<<<< HEAD
# Abstrakt

Tato práce se věnuje studiu a vývoji neuronových sítí pro klasifikaci textových dat. Jejím cílem je zkoumat, jak efektivně a účinně tyto sítě dokážou zpracovat a rozdělit data do kategorií. Zaměřuje se zejména na analýzu sentimentu v textech, což znamená určení, jestli je obsah textu pozitivní či negativní. Výzkum využíval konkrétní soubor dat obsahující recenze zákazníků Amazonu. Proces psaní a úpravy kódu probíhal v prostředí Jupiter notebook za použití Google Colab a VSCode, s využitím dovedností získaných na cvičeních a rozšířením již existujícího kódu.

Zdrojové kódy a kompletní práce je k dispozici zde: 
 
# Obsah

[Abstrakt 2](#_Toc154915798)

[Úvod 4](#_Toc154915799)

[Metody 5](#_Toc154915800)

[Předzpracování 5](#_Toc154915801)

[Jednovrstvá síť 7](#_Toc154915802)

[Konvoluční síť 7](#_Toc154915803)

[Trénování a učení 8](#_Toc154915804)

[Vyhodnocení 8](#_Toc154915805)

[Výsledky 10](#_Toc154915806)

[Závěr 12](#_Toc154915807)

[Zdroje 13](#_Toc154915808)

# Úvod

V dnešní době narůstá potřeba analyzovat rozsáhlé množství textových dat, která jsou generována na internetu, v sociálních sítích, recenzích a dalších zdrojích. Proto se analýza sentimentu textů stává klíčovým úkolem pro mnohé odborníky. V této oblasti se neuronové sítě ukazují jako jeden z efektivních nástrojů pro zpracování a klasifikaci těchto dat. Tyto sítě představují soubor algoritmů, kde každý neuron funguje jako matematická funkce, která přijímá vstupy a podle daného algoritmu je rozděluje do kategorií. Neuronové sítě se skládají z několika vrstev a jsou schopné zpracovávat jak textová, tak obrazová data. V tomto případě se však zaměřujeme specificky na textová data, zejména recenze z Amazonu.

![](RackMultipart20231231-1-eic3jt_html_d75b10843b7652d3.png)

_Obrázek 1 - Ukázka dat_

# Metody

V této studii jsme použili dva typy neuronových sítí: jednovrstvou neuronovou síť a konvoluční neuronovou síť, abychom mohli porovnat jejich výkon. Konvoluční síť pracuje se dvěma vrstvami. Pro analýzu a vývoj byl vybrán programovací jazyk Python spolu s jeho knihovnami, zejména Keras a TensorFlow v prostředí Jupiter notebooku. Nejdříve došlo k předzpracování dat, včetně tokenizace, odstraňování stop slov, normalizace a vytvoření tzv. Bag of Words reprezentace. Poté byla data rozdělena na sady pro trénování, validaci a testování. Tento postup vycházel z předem připraveného kódu používaného na cvičeních.

## Předzpracování

Pro trénování a testování modelů byla využita datová sada od Kotzias et al. (2015), konkrétně "Sentiment Labelled Sentences Data Set – amazon\_cells\_labelled". Nejdříve byla tato data načtena pomocí knihovny pandas, přičemž byla rozdělena na jednotlivé věty a odpovídající štítky, které určují klasifikační kategorie. Poté jsem data rozdělil na trénovací, testovací a validační sady s využitím metody train\_test\_split z knihovny scikit-learn. Trénovací sada obsahuje 60 % všech dat, zatímco testovací a validační sady obsahují každá 20 % dat.

![](RackMultipart20231231-1-eic3jt_html_62f1ec3861d0281d.png)

_Obrázek 2 - Import a úprava dat_

![](RackMultipart20231231-1-eic3jt_html_329e2dd17cd7234b.png)

_Obrázek 3 - Dělení na trénovací a testovací data_

![](RackMultipart20231231-1-eic3jt_html_f28447c1778d5137.png)

_Obrázek 4 - Preprocessing_

## Jednovrstvá síť

První metodou použitou pro klasifikaci textu byla jednovrstvá neuronová síť. Tato síť se skládá pouze z jedné plně propojené vrstvy. Stejně jako u konvoluční sítě byla i zde provedena příprava vstupních dat pomocí techniky CountVectorizer. Poté byla vytvořena jednovrstvá síť s jednou plně propojenou vrstvou a byla v ní použita sigmoidní aktivační funkce. Stejná ztrátová funkce a optimalizační algoritmus, které byly použity u konvoluční sítě, byly aplikovány i zde. Metrikou použitou pro hodnocení výkonnosti sítě byla opět přesnost.

![](RackMultipart20231231-1-eic3jt_html_c18751594c70db74.png)

_Obrázek 5 - Nastavení jednovrstvé sítě_

## Konvoluční síť

V této práci byla pro klasifikaci textu využita konvoluční neuronová síť. Tento typ architektury obsahuje jednu nebo více konvolučních vrstev, které slouží k extrakci klíčových rysů ze vstupních dat. Použitá konvoluční síť obsahovala jednu konvoluční vrstvu a jednu vrstvu pro výstup. Vstupní data byla zpracována do formátu Bag of Words pomocí techniky CountVectorizer z knihovny scikit-learn, což převedlo textové vstupy na binární vektory.

Pro definici konvoluční sítě byla použita knihovna Keras. V konvoluční vrstvě byla implementována aktivační funkce "relu", zatímco pro výstupní vrstvu byla použita sigmoidní aktivační funkce. Zmínka: Při testování s aktivační funkcí "softmax" jsem dosahoval pouze nízké přesnosti okolo 0,0x, což naznačuje pravděpodobnou chybu v implementaci. Pro trénink sítě byla zvolena ztrátová funkce binary\_crossentropy a optimalizační algoritmus Adam. Jako metrika byla použita přesnost.

![](RackMultipart20231231-1-eic3jt_html_64af07930aabeb55.png)

_Obrázek 6 - Nastavení konvoluční sítě_

##

## Trénování a učení

Oba modely, konvoluční a jednovrstvá neuronová síť, byly trénovány na trénovací souboru dat s využitím metody fit z knihovny Keras. Pro každý z modelů byl stanoven specifický počet epoch a velikost dávek (batch size), což bylo určeno na základě provedených experimentů a validace na validační množině dat. Hlavním cílem tréninku bylo minimalizovat ztrátovou funkci a maximalizovat přesnost klasifikace. Nakonec byly pro oba modely zvoleny stejné parametry - počet epoch 10 a velikost dávek 10 - aby bylo možné lépe porovnat a ilustrovat rozdíly ve výsledcích obou metod.

## Vyhodnocení

Po dokončení učení byly oba modely, konvoluční i jednovrstvá neuronová síť, vyhodnoceny na testovací množině dat. K tomuto účelu byla použita metoda evaluate z knihovny Keras. Jako hlavní metriky pro hodnocení kvality obou modelů byly zvoleny přesnost (accuracy) a ztrátová funkce (loss). Tyto metriky poskytují důležitý přehled o výkonu modelů v praktických podmínkách.

![](RackMultipart20231231-1-eic3jt_html_b11dbc609fcbbbb.png)

_Obrázek 7 - Učení_

# Výsledky

Na základě provedených experimentů byly trénovány oba modely, jak konvoluční, tak jednovrstvý, na trénovací množině dat. Po tréninku byly modely následně vyhodnoceny na validačních a testovacích množinách dat. Výsledky tohoto vyhodnocení byly shrnuty v následující tabulce, která poskytuje přehled o výkonech obou modelů v různých scénářích testování.

| Model | Přesnost na TRD | Přesnost na VD | Přesnost na TD | Ztrátová funkce na VD | Ztrátová funkce na TD |
| --- | --- | --- | --- | --- | --- |
| Konvoluční | 0,997 | 0,847 | 0,808 | 0,420 | 0,462 |
| Jednovrstvá | 0,953 | 0,773 | 0,973 | 0,596 | 0,533 |

Na základě prezentovaných výsledků je patrné, že konvoluční síť dosáhla lepší přesnosti na validačních datech než jednovrstvý model, s přesností 84.7 % oproti 77.3 %. Na testovacích datech však jednovrstvý model překonal konvoluční síť, dosahující přesnosti 97.3 % proti 80.8 % u konvoluční sítě.

Co se týče ztrátové funkce, konvoluční síť dosáhla hodnoty 0.420 na validačních datech a 0.462 na testovacích datech. Nižší hodnota ztrátové funkce naznačuje lepší přizpůsobení modelu datům a vyšší přesnost předpovědí. Jednovrstvý model dosáhl hodnoty ztrátové funkce 0.596 na validačních datech a 0.533 na testovacích datech, což značí větší chybu v předpovědích a nižší přesnost v porovnání s konvoluční sítí.

Grafické zobrazení výsledků obou modelů ukazuje, že konvoluční síť má lepší výsledky na validačních datech, zatímco jednovrstvá síť exceluje na testovacích datech. Zajímavé je, že přes velký rozdíl v přesnosti na testovacích datech, oba modely dosahují podobného výkonu na validačních datech.

![](RackMultipart20231231-1-eic3jt_html_b2af6463ed94d2e.png)

_Obrázek 8 - Správnost obou modelů_

![](RackMultipart20231231-1-eic3jt_html_455c1b79bf8d272c.png)

_Obrázek 9 - Ztrátová funkce obou modelů_

Na základě dosažených výsledků lze konstatovat, že konvoluční síť obecně dosahuje nižších hodnot ztrátové funkce a vyšší přesnosti v porovnání s jednovrstvým modelem. Toto ukazuje, že konvoluční síť je efektivnějším modelem pro danou úlohu klasifikace dat. Díky své komplexnější struktuře a schopnosti efektivněji rozpoznávat vzory v datech, což byl i původní předpoklad, se konvoluční síť jeví jako vhodnější volba pro tuto specifickou úlohu.

# Závěr

V této studii jsme se věnovali analýze a implementaci dvou typů neuronových sítí - jednovrstvé a konvoluční - pro účely klasifikace sentimentu textu. Po implementaci byla provedena série experimentů, jejichž cílem bylo vyhodnotit přesnost obou modelů za použití specifických nastavení, která jsou popsána v předchozím textu. Získané výsledky naznačují, že konvoluční síť s dvěma vrstvami dosahuje lepších výsledků ve srovnání s jednovrstvým modelem, což ukazuje na její větší efektivitu v této konkrétní úloze klasifikace sentimentu.

# Zdroje

**1. Umělá inteligence a její aplikace.** _ **Materiály z hodin 4IZ232.** _ **[Online] [Citace: 28. 12 2023.]**

**2. Wikipedia.** _ **Umělá neuronová síť.** _ **[Online] [Citace: 28. 12 2023.] https://cs.wikipedia.org/wiki/Um%C4%9Bl%C3%A1\_neuronov%C3%A1\_s%C3%AD%C5%A5.**

**3. TensorFlow.** _**Convolutional Neural Network (CNN).**_ **[Online] [Citace: 28. 12 2023.] https://www.tensorflow.org/tutorials/images/cnn.**

**4. Datacamp.** _**Convolutional Neural Networks (CNN) with TensorFlow Tutorial.**_ **[Online] [Citace: 28. 12 2023.] https://www.datacamp.com/tutorial/cnn-tensorflow-python.**
=======
# Keras and Tensorflow
This repo contains the last seminar work from VŠE AI.

This work focuses on the study and development of neural networks for text data classification. It aims to investigate how efficiently and effectively these networks can process and categorize data. In particular, it focuses on sentiment analysis in texts, which means determining whether the content of a text is positive or negative. The research used a specific dataset containing Amazon customer reviews. The process of writing and editing code was done in a Jupiter notebook environment using Google Colab and VSCode, using skills learned in the exercises and extending existing code.
>>>>>>> 18ce873be0b1f15639e99b645dccff36802bcd7a
