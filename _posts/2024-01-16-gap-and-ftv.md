---
layout: post
title: "GAP und Fixed Total Validity"
description: "Wie versteht man die magischen Formeln"
categories: Knowledge
---

Verschieden sind die Versuche die Fromeln zu erklären. Hier ist die einzige Anleitung die du jemals benötigst:

  * Mit rechnen gewinnt man keinen Task
  * Nur die Formeln sind die Wahrheit. Programmiere sie selbst, wenn du sie verstehen willst.

# Wettkampf Punktesystem

Ein komplexes Problem braucht auch eine komplexe Lösung. Das Problem für ein Gleitschirm Punktesystem scheitert bereits nach der Frage, was denn nun der beste Pilot ausmacht. Wir schiessen keine Tore und die nur die benötigte Zeit von A bis B zu messen, findet zwar den schnellsten, aber definitiv nicht den besten Piloten.

GAP versucht 3 Gewinner zu definieren: der Erste der die Thermik verlässt und ins Goal kommt, der Erste der im Goal ist und der schnellste Pilot.

## Anfänger vs Profis
Anfänger zeichnen aus, dass sie unterschiedliches Material fliegen und unterschiedliche Fähigkeiten haben. In den einen Bedingungen ist Pilot A besser, in den anderen Pilot B. Hier genügt ein einfach zu verstehendes Punktesystem, da es lediglich darum geht, die Tage irgendwie vergleichbar zu machen. Spass steht über der sportlichen Fairness. Z.B. TBS ist dazu ideal.

Profis unterscheiden sich kaum im Material und kaum in den fliegerischen Fähigkeiten. Alle Bedingungen und Routen sind fliegbar und es geht darum, die besseren Entscheidungen zu treffen. Ein komplexeres, dafür fairerers System wird von den Teilnehmer bevorzugt. GAP hat sich hier etabliert.

## Flachland vs Alpen
Während in den Alpen die Thermik Hotspots mehr oder weniger offensichtlich sind, sind Informationen von Vorflieger im Flachland zentral. Ebenfalls kann in den Alpen im Talwind hoch gesoart werden und entsprechend aggressiv kann angegriffen werden. Es ergeben sich komplett unterschiedliche Taktiken, die im Punktesystem berücksichtigt werden sollten.

## Der Widerspruch
Aktuell sind die Punkte Anfänger - Profis, Flachland - Alpen diametrisch und (wenigstens) orthogonal. Das bedeutet, das ein System in zwei Punkten gut sein kann, aber entsprechende Abstriche in den anderen macht. Liegt ein System in der Hälfte von zwei Punkten ist es ein Kompromiss und wird überall ein paar Schwächen haben.


# GAP und FTV
Mit GAP ist ein bunter Flickenteppich entstanden, der, aus mathematischer Sicht, überhaupt keinen Sinn mehr macht. Mehrere nicht-lineare Funktionen treffen aufeinander. Solch ein System kann nicht in Worten zusammengefasst oder korrekt vereinfacht werden.

Gut gemeinte Ideen wurden diskutiert und irgendwelche Kompromisse wurden getroffen. Da sich das Material und Tasksetting über die Jahre verändert, aber auch die Piloten sich den GAP Regeln anpassen, muss immer wieder eine andere Lücke geschlossen werden. Das ist prinzipiell eine gute Weiterentwicklung. Mit im Paket sind aber auch eine ganze Reihe von Formeln und Regeln, die auf Sonderfällen aufbauen. Weil 1980 Michi Muster der einzige war, der nach dem Airstart gestartet ist und noch eine Thermik erwischt hat, haben wir die Minimal Distance um beim Wettkampf ohne Thermik Niemandem einen Vorteil zu bieten. Stellt die Thermik aber 10km im Rennen komplett ab (z.B. totale Abschattung beim Airstart), war das natürlich ein ganz faires Rennen und jeder muss versuchen, mit seiner verbliebenen Höhe und Gleitleistung noch ein Maisfeld weiter anzupeilen. Konkret: statt im Nachhinen in einem Komitee zu besprechen ob der Wettkampf faire Bedingungen hatte, wird im Vorhinein geraten und jeder Spezialfall wird versucht in die Regeln zu pressen. Aber Spezialfälle fallen durch die Definition aus der Norm und es ist nicht möglich, vor dem Start eine faire Regel zu erstellen.

Aktuell werden einfach die bunten Formeln gefüllt und weil Niemand genau versteht was die einzelnen Parameter ausmachen, wird auf die Rangliste gewartet und dieser heilige Auszug, zeigt dann welcher der Beste war.

Eigentlich ist es sogar unwichtig, da es auch nicht so präzise sein muss: fliegen zwei Piloten ähnlich gut, ist jede ähnliche Punkteverteilung gut. Also unabhängig davon, ob Pilot A oder B vorne ist.

Da die Formeln mathematisch schlecht sind, werden sie falsch oder nicht komplett verstanden. Das führt dazu, dass gewisse Parameter nicht perfekt gesetzt werden. Aber das ist auch gar nicht möglich, denn dazu müsste erstens jeder der Wettkampfleitung jeder Teil der Formel komplett verstehen und zweitens: jeder Pilot will ja mitreden, also muss auch jeder Pilot die Folgen der Parameter komplett kennen.

Aktuell wird meistens einfach etwas gesetzt und gut ist. Nach dem Motto gleiche Regeln für alle. Das Ergebnis von solchen falschen Parameter sind aber unfair verteilte Punkte. Vor dem Start kann ich nicht in die Zukunft blicken, aber ich kann extreme Situationen erkennen und versuchen mich besser zu positionieren, falls das Scenario XY eintrifft.

## FTV-WTF
Um etwas Licht ins dunkle zu bringen habe ich die Formeln für mich programmiert. Damit kann man simulieren, was für änderungen durch welche Einflüsse verursacht werden. Mehr Infos unter Project.








