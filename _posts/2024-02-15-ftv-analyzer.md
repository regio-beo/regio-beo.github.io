---
layout: post
title: "Ranglisten analysieren"
description: "Wie man Ranglisten mit FTV analysiert"
categories: Project
---

Im Jahr 2023 hatten wir am OGO an der Sportklasse eine spannende Situation am Tag 3 von 4. Jakob hat jeden Task dominant gewonnen, aber einen 0er wegen den Wildschutzzonen kassiert. Aktuell ist er auf Rang 4. Auf Rang 3 steht Marco, der zwar konstant, aber ohne Task Sieg geflogen ist. FTV belohnt tendenziell Siege. Ich bin auf Rang 2, mit einem Task Sieg (0er von Jakob). Auf dem ersten Rang ist Georg. Ebenfalls ohne Task Sieg, mit zwei guten Läufen an Tag 1 und 3, aber einen Streicher am Tag 2. Es wird mit 25% FTV geflogen und folgende Task Validity: 98%, 54%, 99%. Jakob wird also einen Teil von seinem 0er vom Tag 1 nicht streichen können. Insgesamt eine sehr spannende Ausgangslage für den vierten Tag.

![rangliste_fs](../../../../img/ftv-analyzer/rangliste_fs.png)

Absolute Punkte. Was will ich mit absoluten Punkten? Ich will wissen, welche Piloten um den Sieg fliegen! Ich will wissen, wie viel Vorspurng ich brauche um Georg zu überhohlen, und ob ich es mir leisten kann hinter Jakob ins Ziel zu kommen. Als erstes mache ich mir dazu eine Rangliste, welche die Differenzen zum Erstplatzierten anzeigt. Dazu sortiere ich die Tasks auch nach FTV Performance, statt nach dem Datum. In der oberen Zeile steht Task, Erreichte Punkte, Maximale Punkte (nach Validity), und die FTV Performance. Die FTV Performance ist die erreichte Punktzahl geteilt durch die maximale Punktzahl. In der zweiten Zeile steht die Differenz zum Erstplatzierten, das zeigt, wieviele Punkte an diesem Tag verloren wurden. In der Klammer steht der Anteil nach FTV, also zu wieveil Prozent dieser Verlust zum Gesamtergebnis zählt.

![rangliste_difference](../../../../img/ftv-analyzer/difference_score_current.png)

Mit dieser Darstellung, sieht man bereits besser, wer an welcher Stelle seinen Punkte verloren hat.


Da wir bereits am rechnen sind, können wir auch einen 4. Task hinzurechnen. Dazu fügen wir einen Task ein, wo alle abstehen und 0 Punkte machen. Und einen zweiten, wo jeder 1000 Punkte macht. Also alle eng beisammen ins Goal kommen. Gibt es in diesen Extremfällen einen Sieger? Natürlich können wir auch verschiedene Task Validity setzen, aber wir lassen die Task Validity zur Einfachheit auf 1.0.

![rangliste_difference](../../../../img/ftv-analyzer/difference_score_min.png)

Die Minimalen Scores, falls alle Piloten 0 Punkte an Tag 4 machen.

![rangliste_difference](../../../../img/ftv-analyzer/difference_score_max.png)

Die Maximalen Scores, falls alle Piloten 1000 Punkte an Tag 4 machen.

Hier finden wir die ersten echten Erkenntnisse: Falls alle 0 Punkte machen, bin ich zuoberst, da ich noch einen Streicher übrig habe, Jakob und Georg aber nicht. Marco war immer hinter mir und kommt deshalb mit einem 0er nicht vor mich. Ebenfalls interessant ist der Fall, wo alle mit 1000 Punkte ins Goal kommen: in diesem Fall kann Georg mit einem Vorsprung davon ziehen. Ich und Jakob liegen 4 Punkte auseinander, das wäre ein heisses Rennen. Marco würde seinen 3. Rang verlieren. Schauen wir genau auf den 5. platzierten Artem, sehen wir, dass er Chancen auf den 1. Rang hätte. Das Bedingt aber auch ein 0er von Mir, Jakob, Georg und Marco. In der nächsten Rangliste fasse ich das aktuelle, das minimale (Falls jeder ein 0er macht) und das maximale (Falls jeder 1000 Punkte macht) Ergebnis zusammen. In den Klammern steht jeweils, welche Position im schlechtesten Fall erreicht wird und welchen Rang im besten Fall noch erreicht werden könnte, falls alle andern 0 Punkte machen.

![rangliste_difference](../../../../img/ftv-analyzer/simulate_min_max.png)

Dass Georg das Ding noch nicht im Trokenen hat, dass Jakob am aufhohlen ist und dass ich wahrscheinlich über Marco stehen werde, kann jeder geübte Pilot aus dieser Rangliste lesen. Jedoch kann keiner genau erklären warum genau das so ist. Jeder erfahrene Pilot hat eine Intuition, wie die Rangliste in Kombination von den Tagessiegen und FTV zu interpretieren sind. Ich möchte jetzt aber das Warum genauer untersuchen. Ebenfalls kann Jakob mit 3500 Total Validity den ersten Tag nicht komplett streichen lassen. Wie wirkt sich dies auf die Gesamtrangliste aus?

Aktuell fliegen Ich, Jakob, Georg, Marco und (theoretisch) Artem um den ersten Rang. Die Dynamik der Rangliste ist aber auch von der Platzierung der anderen Piloten abhängig und hat jetzt eine komplexität angenommen, die sich nicht mehr mit einfachen Regeln erklären lässt. Klar, die Extremfälle haben wir bereits Untersucht: mit 1000 Punkten kann Georg das Ding nach Hause bringen. Im nächsten Schritt möchten wir aber den Fällen die dazwischen liegen untersuchen und ihnen Wahrscheinlichkeiten zuordnen.

Dazu machen wir eine Monte Carlo Simulation. Dazu simulieren wir das Ergebnis von Task 4 komplett Zufällig: jeder Pilot zieht eine zufällige Zahl zwischen 0 und 1000. Danach berechnen wir die Gesamtrangliste unter Berücksichtigung von FTV und zählen, wer wie oft gewinnt, zweiter wird, dritter wird und so weiter. Zum Schluss teilen wir diese Zähler durch die Anzahl Simulationen und erhalten pro Piloten eine Wahrscheinlichkeit für jeden Rang. Das ist unter der Annahme, dass jeder Pilot zufällig fliegt. Also nach dem Motto alles ist Möglich, alles kann passieren.

![monte_carlo_uniform](../../../../img/ftv-analyzer/monte_carlo_uniform_small.png)

Die Monte Carlo Simulation vom 4. Task. Obwohl jeder Pilot zufällige Punkte erfliegt, zeichnen sich klare Tendenzen in der Rangliste ab. Pro Zeile ist das Maximum gelb eingefärbt. In den Zellen steht die Wahrscheinlichkeit, dass der Pilot diesen Rang erreicht. Der Skill vom Piloten wird bewusst nicht berücksichtigt.

Jetzt wird es Spannend. Beginnen wir bei Jakob. Bei ihm ist alles Möglich. In 15% der Fällen erreicht er Rang 1. Er kann aber auch noch auf Rang 10 abrutschen (Ausserhalb der Grafik). Er fliegt definitiv um den Sieg. Georg hat gute Chancen auf ein Sieg: 33%. Da er aber bereits am Tag 2 ein Streicher benutzt hat, sieht man in der Simulation, dass er auch noch auf Platz 4 oder 5 abrutschen kann. Meine Zeile zeigt super Chancen für ein Podestplatz: ich habe noch keinen Streicher und falls ich einen 0er fliegen werde, müsste Marco entsprechend gut fliegen um mich vom Podest zu kicken. Interessant ist auch die Zeile von Marco. Obwohl er aktuell auf Rang 3 ist, sieht die Simulation ihn eher auf Rang 4. Eine Chance auf den Sieg ist vorhanden aber sie ist klein.

Fassen wir zusammen. Die Simulation bestätigt unsere Intuition: es fliegen Primär Ich, Georg und Jakob um den Sieg. Jakob kann mit einem schlechten Flug richtig weit abrutschen, Georg kann noch vom Podest fallen. Ich bin ziemlich Sicher auf dem Podest und kann mit viel Risiko angreifen. Falls aber alle gleich gut fliegen (nahe an 1000 Punkten) wird Georg seinen Vorsprung nach Hause bringen. Aber wie sieht es aus, wenn Georg nicht 1000 Punkte macht? Könne wir herausfinden, wo die Grenzen liegen? Also welcher Vorsprung brauche ich um auf Rang 1 zu kommen? Interessant ist auch, dass dieser Vorsprung abhängig von der Punktzahl sein kann.

Dazu lassen wir unsere Simulation wieder laufen. Dieses mal schaue ich nur die Ranglisten an, wo ich gewinne und untersuche, wieviele Punkte Jakob und Georg geflogen sind. Meine Punkte trage ich auf der Y-Achse ein, die Punkte der anderen auf der X Achse. Für jede solche Konfiguration, wo ich als Sieger hervorgehe, mache ich einen Punkt auf der nächsten Grafik.

![beni_first_raw](../../../../img/ftv-analyzer/beni_first_raw.png)

Oben Links ist der Fall, in welchen ich 1000 Punkte mache und die andern jeweils 0. Offensichtlich gewinne ich da. Deshalb entferne ich unwichtige Punkte und trage eine Winkelhalbierende ein. Auf dieser Linie habe ich und meine Konkurrenz gleich viel Punkte (wir fliegen also Gleichzeitig ins Goal), oberhalb dieser Linie habe ich mehr (ich muss führen), unterhalb habe ich weniger (ich darf verfolgen). Damit sieht man, ob man vor oder hinter einem Piloten im Ziel sein muss um dennoch den ersten Rang zu erreichen.

![beni_first](../../../../img/ftv-analyzer/beni_first.png)
 ![beni_first_zoom](../../../../img/ftv-analyzer/beni_first_zoom.png)

Machen wir zuerst der Vergleich mit Georg in Orange: Macht er ca. 940 Punkte oder mehr, kann ich nicht mehr gewinnen. Es ist kein Punkt von rechts von x=940 vorhanden (Punkt = Sieg von mir). Aber es gibt auch einen zweiten Bereich: Macht Georg weniger als 600 Punkte werde ich Siegen, falls wir Gleichzeitig ins Goal kommen. Macht Georg weniger als 500 Punkte werde ich sogar mit 0 Punkten gegen ihn siegen.
Als zweites kommt der Vergleich mit Jakob in Blau. Man sieht das Kopf an Kopfrennen im Bereich oben rechts. Falls er 1000 Punkte macht, kann ich mit 998 noch gewinnen! Sobald er 800 Punkte oder weniger macht, wird es für mich deutlich einfacher ihn in der Gesamtrangliste zu bezwingen.

Uff. Jetzt wissen wir endlich was die aktuelle Rangliste eigentlich bedeutet. Jörg, warum zeigt die Rangliste das nicht gleich so an? Nicht jeder kann diese Informationen direkt aus der Tabelle lesen.

Wie ging es weiter? Natürlich wird das Rennen in der Luft und nicht am Computer geflogen! Aktuell haben wir mit Wahrscheinlichkeiten jongliert und angenommen, jeder Pilot kann jedes Ergebnis erfliegen. Machen wir an dieser Stelle einen Exkurs in die Prognose. Dabei möchten wir jedem Pilot, basierend auf den vorherigen Ergebnissen, einen Skill zuordnen und den 4. Task mit entsprechendem Pilotenskill simulieren. Dazu mitteln wir die FTV Performance und berechnen ihre Standardabweichung von den geflogenen nicht 0er Tagen. Von dieser Verteilung ziehen wir eine zufällige Performance für den 4. Task und begrezen die Punkte bei 0 und 1000. Dadurch wird sich die Punkte vom 4. Tag an die Performance von den ersten Tagen anpassen.

![monte_carlo_pilot_performance](../../../../img/ftv-analyzer/monte_carlo_pilot_performance.png)

Die Prognose nimmt an, dass die Piloten am 4. Tag ähnliche Leistung zeigen, wie an den Tagen zuvor. Dabei spricht die Simulation eine deutliche Sprache: 1. Jakob, 2. Beni, 3. Georg, 4. Marco.

Wer hat Schlussendlich gewonnen? Sieh dir selbst das Ogoy Replay an und gib deinen Tipp. Du hast jetzt alle Informationen um ein Auswerter zu sein.

Task Analyse. Jakob hat bereits 3 Rennen mehr oder weniger dominiert und hat den 4. Task mit Abstand gewonnen. Sein Gesamtsieg war mehr als verdient. Ich bin auf Rang 2 geflogen. Marco hat sich an meine Fersen gehängt und mit einer super aggressiven Linie viel Zeit aufgehohlt. Damit hat er sich sein Podestplatz gesichert! Georg hatte vom Start an Baustellen und die Bedingungen wurden immer wie schwieriger (undankbar zum Aufhohlen). Leider ist er mit 450 Punkten unter seine Schmerzgrenze gefallen und hat damit den Podestplatz um 30 Punkte gegen Marco verpasst.

Happy Landings.




