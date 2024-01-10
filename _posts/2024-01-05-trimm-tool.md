---
layout: post
title: "Enzo Trim Tool"
description: "Der Gleitschirmtrim unter der Lupe"
categories: Future-Project
---

Im Wettkampf fliegen alle den gleichen Schirm und wenn einer besser geht, muss es am Trim liegen!
Stephan hat deshalb ein mega geilen bluetooth basierten Laser gebastelt um die Leinen vermessen zu können.

## Das Problem
Im Moment werden die (Leinen) Messungen in einer Exceltabelle irgendwie gespeichert und verrechnet. Man kann ein paar Dinge visualisieren und realtives Trim Tuning betreiben, aber ob das irgendwie Sinnvoll ist, steht auf einem anderen Blatt.

Blickt man ins Detail merkt man, dass sich Leinen auch verzweigen oder entlasten. Leinen können nicht verlängert werden und das Tuning selbst ist ein spannendes Integer Problem.
Relatives Trim Tuning ist auch nur so gut wie der Herstellertrim.

## Die Vision
Wir wollen eine Datenbank von Messungen anlegen. Dabei sieht man, wie sich über die Zeit die Leinen von einem Schirm ändern. Aber auch, welche Abweichungen die besten Schirme vom Herstellertrim haben.

In einem zweiten Schritt, kann man das tuning assistieren, indem man nach gewissen Kriterien ein Optimum findet. Oder Auswirkungend der geplanten änderungen visualisiert.

## Die Umsetzung
Wichtig ist es, die Daten von dem Code zu trennen. Damit kann man in der Datenbank (Sammlung von CSV Files) die Schirmmodelle pflegen und im Code verschiedene Module zur Visualisierung oder Optimierung implementieren. Verschiedene Schirmmodelle könnten Unterstützt werden.

