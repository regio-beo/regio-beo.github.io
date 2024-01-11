---
layout: post
title: "Numeric Solver for optimal Task"
description: "Ein gradient basierter Solver für die optimale Task Linie"
categories: Project Task
permalink: /igc2kmz-on-docker
---

Alle fliegen der blauen Linie entlang. Aber wie korrekt ist diese Linie? XCTrack kann es uns nicht verraten, da die Entwickler
die Vorteile von Open Source entwicklung noch nicht entdeckt haben.

Deshalb haben wir einen Solver für dieses Problem geschrieben. Die Basis ist ein quadratischer Loss, kombiniert mit Graident Descent.
Der Solver funktioniert. Aber XCTrack ist aktuell noch etwas besser (Im Schnitt ca. 500m auf 50km). Grosse Radien und flache Winkel sorgen für ein numerisch interessantes Problem.

Die Frage ist ob eine Normalisiering des Tasks oder ein Netwon Solver zu der gewünschten Verbesserung führt. Mehr Informationen [https://github.com/fankib/shortest-path](https://github.com/fankib/shortest-path).
