---
layout: post
title: "How To: Ranglisten und FTV"
description: "Endlich wurde der Code geknackt: nicht GAP/FTV ist das Problem, sondern die Darstellung könnte besser sein"
categories: Project
---

Im Jahr 2023 hatten wir am OGO an der Sportklasse eine spannende Situation am Tag 3. Der Wettbewerb dauerte 4 Tage. Jakob hat jeden Task dominant gewonnen, aber einen 0er wegen den Wildschutzzonen kassiert. Aktuell ist er auf Rang 4. Auf Rang 3 steht Marco, der zwar konstant, aber ohne Task Sieg geflogen ist. FTV belohnt aber tendenziell Siege. Ich bin auf Rang 2, mit einem Task Sieg (0er von Jakob). Auf dem ersten Rang ist Georg. Ebenfalls ohne Task Sieg, mit zwei guten Läufen an Tag 1 und 3, aber einem Streicher an Tag 2. Es wird mit 25% FTV geflogen und folgende Task Validity wurden erreicht: 98%, 54%, 99%. Jakob wird also einen Teil von seinem 0er vom Tag 1 nicht streichen können. Insgesamt eine sehr spannende Ausgangslage für den vierten Tag. Werfen wir einen Blick auf die Rangliste:

![rangliste_fs](../../../../img/ftv-analyzer/rangliste_fs.png)

Absolute Punkte. Was will ich mit absoluten Punkten?! Ich will wissen, welche Piloten um den Sieg fliegen Ich will wissen, wie viel Vorsprung ich brauche um Georg zu überhohlen, und ob ich es mir leisten kann hinter Jakob ins Ziel zu kommen. Als erstes mache ich mir dazu eine Rangliste, welche die Differenzen zum Erstplatzierten anzeigt. Dazu sortiere ich die Tasks auch nach FTV Performance, statt nach dem Datum. Die FTV Performance ist die erreichte Punktzahl geteilt durch die maximale Punktzahl. Pro Pilot mache ich zwei Zeilen. In der oberen Zeile stehen Task, Erreichte Punkte, Maximale Punkte (nach Validity), und die FTV Performance (von links nach rechts). In der unteren Zeile steht die Differenz zum Erstplatzierten. Dies zeigt, wieviele Punkte man an diesem Tag verloren hat. In der Klammer steht der Anteil nach FTV, also zu wieviel Prozent dieser Verlust zum Gesamtergebnis zählt. 100% bedeutet zählt voll, 0% bedeutet der Task wurde gestrichen.

![rangliste_difference](../../../../img/ftv-analyzer/difference_score_current.png)

Mit dieser Darstellung, sieht man bereits besser, wer an welcher Stelle seinen Punkte verloren hat.


Da wir bereits am rechnen sind, können wir einen 4. Task hinzurechnen. Dazu fügen wir einen Task ein, wo alle abstehen und 0 Punkte machen. Wir nennen ihn "TV". Danach wiederhohlen wir das ganze mit einem zweiten Task, wo jeder 1000 Punkte macht. Also alle eng beisammen ins Goal kommen. Gibt es in diesen Extremfällen einen Sieger? Wegen der Einfachheit lassen wir die Task Validity auf 1.0.

![rangliste_difference](../../../../img/ftv-analyzer/difference_score_min.png)

Die Minimalen Scores, falls alle Piloten 0 Punkte an Tag 4 machen.

![rangliste_difference](../../../../img/ftv-analyzer/difference_score_max.png)

Die Maximalen Scores, falls alle Piloten 1000 Punkte an Tag 4 machen.

Hier finden wir die ersten echten Erkenntnisse: Falls alle 0 Punkte machen, bin ich zuoberst, da ich noch einen Streicher übrig habe, Jakob und Georg aber nicht. Marco war immer hinter mir und kommt deshalb mit einem 0er nicht vor mich. Ebenfalls interessant ist der Fall, wo alle mit 1000 Punkte ins Goal kommen: in diesem Fall kann Georg mit einem Vorsprung davon ziehen. Ich und Jakob liegen 4 Punkte auseinander, das wäre ein knappes Rennen. Marco würde in diesem Fall seinen 3. Rang verlieren. Schauen wir genau auf den 5. platzierten Artem. Vergleichen wir seine maximalen Punkte mit unseren minimalen, hat er noch eine Chance auf den 1. Rang. Das Bedingt aber auch ein enstsprechend schlechtes Resultat von Mir, Jakob, Georg und Marco. In der nächsten Rangliste fasse ich das aktuelle, das minimale (Falls jeder ein 0er macht) und das maximale (Falls jeder 1000 Punkte macht) Ergebnis zusammen. In den Klammern steht jeweils, welche Position im schlechtesten Fall erreicht wird und welchen Rang im besten Fall noch erreicht werden könnte, falls alle andern 0 Punkte machen.

![rangliste_difference](../../../../img/ftv-analyzer/simulate_min_max.png)

Dass Georg das Ding noch nicht im Trokenen hat, dass Jakob am aufhohlen ist und dass ich wahrscheinlich über Marco stehen werde, kann jeder geübte Pilot aus der originalen Rangliste lesen. Jedoch kann keiner genau erklären warum genau das so ist. Jeder erfahrene Pilot hat eine Intuition, wie die Rangliste in Kombination von den Tagessiegen und FTV zu interpretieren ist. Ich möchte aber das Warum genauer untersuchen. Ebenfalls kann Jakob mit 3500 Total Validity den ersten Tag nicht komplett streichen lassen. Wie wirkt sich dies auf die Gesamtrangliste aus?

Aktuell fliegen Ich, Jakob, Georg, Marco und (theoretisch) Artem um den ersten Rang. Möchte man jetzt fixe Regeln ablesen, wird es kompliziert. Wer gewinnen wird hängt nicht nur von der eigenen Leistung, sondern auch der Leistung der Konkurrenz ab. Die Rangliste wird dynamsich. Klar, die Extremfälle haben wir bereits Untersucht: mit 1000 Punkten kann Georg das Ding nach Hause bringen. Im nächsten Schritt untersuchen wir die Fälle die zwischen den Extrema liegen und werden diesen Fällen eine Eintrittswahrscheinlichkeit zuordnen.

Dazu verwenden wir die Monte Carlo Methode. Dazu simulieren wir das Ergebnis von Task 4 komplett Zufällig: jeder Pilot zieht eine zufällige Zahl zwischen 0 und 1000. Diese Zahl steht für sein Ergebnis am Tag 4. Danach berechnen wir die Gesamtrangliste unter Berücksichtigung von FTV und zählen, wer wie oft gewinnt, zweiter wird, dritter wird und so weiter. Zum Schluss teilen wir diese Zähler durch die Anzahl Simulationen und erhalten pro Piloten eine Wahrscheinlichkeit für jeden Rang. Das ist unter der Annahme, dass jeder Pilot zufällig fliegt. Also nach dem Motto alles ist Möglich, alles kann passieren. Der Skill vom Piloten wird bewusst nicht berücksichtigt.

![monte_carlo_uniform](../../../../img/ftv-analyzer/monte_carlo_uniform_small.png)

Die Monte Carlo Simulation von Tag 4. Obwohl jeder Pilot zufällige Punkte erfliegt, zeichnen sich Tendenzen in der Rangliste ab. Pro Zeile ist das Maximum gelb eingefärbt. In den Zellen steht die Wahrscheinlichkeit, dass der Pilot diesen Rang erreicht.

Jetzt wird es Spannend. Beginnen wir bei Jakob. Bei ihm ist alles Möglich. In 15% der Fällen erreicht er Rang 1. Er kann aber auch noch auf Rang 10 abrutschen (Ausserhalb der Grafik). Er fliegt definitiv um den Sieg. Georg hat gute Chancen auf ein Sieg: in 33% der Endranglisten stand er zuoberst. Da er aber bereits am Tag 2 ein Streicher benutzt hat, sieht man in der Simulation, dass er auch noch auf Platz 4 oder 5 abrutschen kann. Meine Zeile zeigt super Chancen für ein Podestplatz: ich habe noch keinen Streicher und falls ich einen 0er fliegen werde, müsste Marco entsprechend gut fliegen um mich vom Podest zu kicken. Interessant ist auch die Zeile von Marco. Obwohl er aktuell auf Rang 3 ist, sieht die Simulation ihn eher auf Rang 4. Eine Chance auf den Sieg ist zwar vorhanden aber sie ist mit 5% eher klein.

Fassen wir zusammen. Die Simulation bestätigt unsere Intuition: es fliegen primär Ich, Georg und Jakob um den Sieg. Jakob kann mit einem schlechten Flug weit nach hinten rutschen. Georg kann, je nach Ergebnis, vom Podest fallen. Ich bin mit hoher Wahrscheinlichkeit auf dem Podest und kann deshalb mit viel Risiko angreifen. Falls aber alle gleich gut fliegen (nahe an 1000 Punkten) wird Georg seinen Vorsprung nach Hause bringen. Aber wie sieht es aus, wenn Georg nicht 1000 Punkte macht? Könne wir herausfinden, wo die Grenzen liegen? Also welcher Vorsprung brauche ich um auf Rang 1 zu kommen? Interessant ist auch, dass dieser Vorsprung abhängig von der Punktzahl sein kann.

Dazu lassen wir unsere Simulation wieder laufen. Dieses mal schaue ich nur die Endranglisten an, wo ich auf Rang 1 stehe und untersuche, wieviele Punkte Jakob und Georg geflogen sind. Meine Punkte trage ich auf der Y-Achse ein, die Punkte der anderen beiden auf der X Achse. Für jede solche Konfiguration, wo ich als Sieger hervorgehe, mache ich einen Punkt auf der nächsten Grafik. Die X-Achse ist etwas schwer zu lesen, aber es ist die gleiche Skala wie auf der Y-Achse:

![beni_first_raw](../../../../img/ftv-analyzer/beni_first_raw.png)

Oben Links ist der Fall, in welchen ich 1000 Punkte mache und die andern jeweils 0. Offensichtlich gewinne ich da. Unten rechts mache ich 0 Punkte und die anderen 1000, damit gewinne ich nicht und deshalb ist dort kein Punkt von mir. Oben rechts ist der Bereich, wo alle um die 1000 Punkte fliegen. Das ist eher der spannende Bereich. Ich entferne unwichtige Punkte und trage eine Winkelhalbierende ein. Auf dieser Linie habe ich und meine Konkurrenz gleich viele Punkte (wir fliegen also Gleichzeitig ins Goal), oberhalb dieser Linie benötige ich mehr Punkte (ich muss führen), unterhalb dieser Linie benötige ich weniger Punkte (ich darf verfolgen). Damit sieht man, ob man vor oder hinter einem Piloten im Ziel sein muss um dennoch den ersten Rang zu erreichen.

![beni_first](../../../../img/ftv-analyzer/beni_first.png)
 ![beni_first_zoom](../../../../img/ftv-analyzer/beni_first_zoom.png)

Machen wir zuerst der Vergleich nur mit Georg in Orange: Macht er ca. 940 Punkte oder mehr, kann ich nicht mehr gewinnen. Es ist kein Punkt rechts von x=940 vorhanden (Punkt = Sieg von mir). Aber es gibt auch einen zweiten Bereich: Macht Georg weniger als 600 Punkte werde ich Siegen, falls wir Gleichzeitig ins Goal kommen. Macht Georg weniger als 500 Punkte werde ich sogar mit 0 Punkten gegen ihn siegen.
Als zweites machen wir den Vergleich mit Jakob in Blau. Man sieht das Kopf an Kopfrennen im Bereich oben rechts. Falls er 1000 Punkte macht, kann ich mit 998 noch gewinnen! Sobald er 800 Punkte oder weniger macht, wird es für mich deutlich einfacher ihn in der Gesamtrangliste zu bezwingen.

Uff. Jetzt wissen wir endlich, was die aktuelle Rangliste eigentlich bedeutet. Warum stellen wir die Rangliste nicht gleich in dieser Form dar? Nicht jeder kann diese Informationen direkt aus der originalen Tabelle lesen.

Wie ging es weiter? Natürlich wird das Rennen in der Luft und nicht am Computer geflogen! Aktuell haben wir mit Wahrscheinlichkeiten jongliert und angenommen, jeder Pilot kann jedes Ergebnis erfliegen. Machen wir an dieser Stelle einen Exkurs in die Prognose. Dabei möchten wir jedem Pilot, basierend auf den vorherigen Ergebnissen, einen Skill zuordnen. Danach simulieren wir den Tag 4 basierend auf diesem Skill. Dazu mitteln wir die FTV Performance und berechnen ihre Standardabweichung von den geflogenen nicht 0er Tagen. Von dieser pilotenbasierten Verteilung ziehen wir eine zufällige Performance für den 4. Task und begrezen die Punkte bei 0 und 1000. Dadurch werden sich die Punkte vom 4. Tag an die Performance von den ersten Tagen anpassen.

![monte_carlo_pilot_performance](../../../../img/ftv-analyzer/monte_carlo_pilot_performance.png)

Die Prognose nimmt an, dass die Piloten am 4. Tag ähnliche Leistung zeigen, wie an den Tagen zuvor. Dabei spricht die Simulation eine deutliche Sprache: 1. Jakob, 2. Beni, 3. Georg, 4. Marco.

Wer hat Schlussendlich gewonnen? Sieh dir selbst das [Ogoy Replay](https://ogoy.app/player/?scene=org8oilewmfd1xktu48vjev) an und gib deinen Tipp ab. Du hast jetzt alle Informationen um ein Auswerter zu sein.

Analyse Task 4. Jakob hat bereits 3 Rennen mehr oder weniger dominiert und hat den 4. Task mit Abstand gewonnen. Sein Gesamtsieg war mehr als verdient. Ich bin auf Rang 2 geflogen. Marco hat sich an meine Fersen gehängt und mit einer super aggressiven Linie viel Zeit aufgehohlt. Damit hat er sich sein Podestplatz gesichert! Georg hatte vom Start an Baustellen und die Bedingungen wurden immer wie schwieriger (undankbar zum Aufhohlen). Leider ist er mit 450 Punkten unter seine Schmerzgrenze gefallen und hat damit den Podestplatz um 30 Punkte gegen Marco verpasst.

Happy Landings.




