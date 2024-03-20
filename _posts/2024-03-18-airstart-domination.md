---
layout: post
title: "Dominieren beim Airstart"
description: "Wer dominiert wer beim Airstart?"
categories: Project Task
---

Dominieren bedeutet im Wettbewerb, dass man die Position vom vorderen (und tieferen) Piloten durch Vollgasfliegen erreichen kann, in der nächsten Thermik höher ankommt und sich über den dominierten Piloten setzen kann. Dies ist normalerweise der Fall, wenn ein Pilot in einem 45 Grad Winkel hinter einem anderen fliegt. Der Gleitwinkel zwischen diesen beiden Piloten ist 1:1.

Der Dominanz-Gleitwinkel ist der Gleitwinkel, mit diesem der hintere obere Pilot noch am dominieren ist. Je nach Tag, also Task, Soaringkanten, Thermikstärke und Gegenwind, ändert sich dieser Dominanz-Gleitwinkel. Er liegt üblicherweise zwischen 1:1 und 1:3, an thermikschwachen Tagen auch mal bei 1:4.

Der dominierende Pilot kann entweder angreifen, indem er selbst voraus fliegt, oder verwalten, indem er bewusst etwas langsamer fliegt aber dafür die Informationen von den unteren Piloten ausnutzen kann. Z.B. über die Steigwerte oder Zyklen der Thermik. Ziel des verwaltenden Piloten ist es, die dominierende Position bis zum Endanflug zu halten. Ziel des angreifenden Piloten ist es, sich so viel schneller zu bewegen, dass man aus dem Dominanz-Gleitwinkel des oberen entkommt und somit den Vorsprung bis zur ESS halten kann.

Dieser Dominanz-Gleitwinkel entspricht nicht dem Gleitwinkel des Schirms. Das hat mehrere Gründe. Z.B. muss der obere Pilot schneller fliegen, um den unteren aufzuholen. In der Zeit bis der obere Pilot an der Position des tieferen ist, ist der tiefere bereits etwas weiter geflogen. Ein weiterer Grund ist der Hangaufwind: nah am Gelände haben die tieferen Piloten das bessere Gleiten. Dieser Dominanz-Gleitwinkel kann mit der Erfahrung bestimmt werden. 1:1, also 45 Grad hinter oben einem Piloten zu fliegen ist sehr dominant. In einem 1:3 (18 Grad) hinter einem Piloten zu fliegen, reicht in der Regel um ihn in der nächsten Thermik einhohlen zu können. Fliegt man noch flacher hinter einem Piloten wird es irgendwann unmöglich ihn einhohlen zu können, obwohl man höher ist.

Der Airstart ist der Ort, wo diese Dominanz am meisten zum Tragen kommt: gut positionierte Starter können den Pulk verfolgen und sind nicht gezwungen anzugreifen. Erst falls tiefere Piloten versuchen sich abzusetzen, müssen diese verfolgt werden. In dieser verwaltenden Position tragen die guten Starter nur ein kleines Risiko und verlieren nur wenig Leadingpoints, da sie Teil vom Spitzenpulk sind.

Die tiefen Starter müssen sich entscheiden, ob sie Leadingpoints wollen und tief vorausfliegen, oder ob sie aufdrehen. Der erste Fall hat ein hohes Risiko und sendet viele Informationen an die Konkurrenz. Beim zweiten Fall, werden sie in einen Verfolgerpulk zurück fallen und verlieren viele Leadingpoints.

Aus diesem Grund wollen wir herausfinden, wer beim Airstart wie viele Piloten dominiert. 
Wir berechnen die Richtung der SSS zum WP1 (nach optimiertem Weg) und legen eine Ebene in den Raum. Wir bestimmen diese durch die Normale $ \vec{n} $, welche entsprechend dem Dominanz-Gleitwinkel in Richtung des Rennens geneigt ist. Danach schieben wir diese Ebene zum Piloten und berechnen mit dem Skalarprodukt ob ein anderer Pilot überhalb oder unterhalb der Ebene fliegt. $ A~\text{dom}~B := (\vec{B}-\vec{A}) \cdot \vec{n} < 0 $:

![airstart_theory](../../../../../img/airstart/theory.jpg)

Wir können dies beim Airstart auf den gesamten Pulk anwenden. Dazu ermitteln wir die Position von jedem Piloten und berechnen für jeden Piloten wie viele andere er dominiert. Der best platzierte Pilot dominiert die meisten anderen Piloten.

### Airstart Regio Verbier

Beim Airstart von Regio in Verbier erhalten wir folgenden Rangliste:

```
Maret Luca               33
Aeschbacher Roger        32
Fankhauser Benjamin      30
Montavon Morane          29
Cox Steve                28
Périsset Lucien          28
Liard Bruno              27
Descombes Henri          25
Blum Pascal              25
Schwery Michael          23
Strahm Hans              21
Frochaux Gaël            21
Mabillard Jonas          20
Clénin Reto Ivan         20
Maurer Christian         19
Kitagawa Sebastian       19
Textor Florian           17
Bise Lucas               16
Flügel Oliver            15
Kiener Noah              15
Buob Simon               14
Court Noé                12
Zimmermann Sarah         11
Celada Andres            11
Dietrich Olivier         10
Thiébaud Fabrice         9
Wüthrich Silvan          8
Morisetti Jean           7
Fromm Christopher        7
Monnet Frédéric          6
Heldstab Corina          5
Meyer Jonathan           4
Morgenthaler Patrick     4
Wagner François          4
Sommerfeld Marco         3
Brodbeck Georg           2
Steiner Simon            2
Eyer Sebastian           1
Montavon Morane          0
```

Ebenfalls können wir das ganze in 3D visualisieren. Dazu bestimmen wir einen Piloten aus dessen Sicht wir das Feld analysieren (Per Zufall mich selbst) und zeichnen die dominierten Piloten als rote Punkte.

![regio_verbier_race_start](../../../../../img/airstart/regio_verbier_race_start.jpg)

Ein roter Haufen bedeutet ein guter Start. Es wurde ein Dominanz-Gleitwinkel von 1:3 verwendet. Würde man versuchen unten davon zu fliegen, wäre der Haufen ziemlich blau.

### Code
Den Code und die Grafiken sind öffentlich verfügbar:

[https://github.com/fankib/shortest-path/blob/main/regio_verbier.py](https://github.com/fankib/shortest-path/blob/main/regio_verbier.py).

### Zukunft

Die Darstellung eignet sich auch angewandt auf das gesamte Race. Damit kann visuell sichtbar gemacht werden, zu welchem Zeitpunkt man die verwaltende Position verloren hat, oder ein Angriff erfolgreich war.
Interessant ist auch die Frage, ob man diesen Dominanz-Gleitwinkel im Nachhinein bestimmen kann, also in welcher Phase welcher Gleitwinkel noch erfolgreich war.

