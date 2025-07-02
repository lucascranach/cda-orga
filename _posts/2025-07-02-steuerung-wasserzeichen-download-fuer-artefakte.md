---
layout: simple
title:  "Steuerung von Wasserzeichen- und Download-Option für Artefakte"
date: 02.07.2025
---

## Konzept
Für die Bereitstellung von Artefakten im **CDA**  mit optionalem Wasserzeichen und  optionaler Download-Möglichkeit wird folgendes technische Konzept definiert.

Die relevanten Informationen zur Wasserzeichen- und Download-Verfügbarkeit eines Artefakts werden **in den IPTC-Daten** der jeweiligen **Bild-Datei** hinterlegt. Dafür wird das **Feld** `SpecialInstructions` verwendet.

## Kennzeichnung
Folgende Keywords und Kombinationen werden zur Kennzeichnung verwendet:

| Zustand                                               | IPTC-Eintrag (`SpecialInstructions`) |
| ----------------------------------------------------- | ------------------------------------ |
| Artefakt hat Wasserzeichen                            | `watermark`                          |
| Artefakt ist downloadbar                              | `download`                           |
| Artefakt hat Wasserzeichen **und** ist downloadbar    | `watermark, download`                |
| Artefakt ohne Wasserzeichen und **nicht** downloadbar | *(Feld leer lassen)*                 |


Die Keywords werden als **kommagetrennte Liste** im Feld `SpecialInstructions` abgelegt.

## Vorteile

- Das IPTC-Feld `SpecialInstructions` ist **standardisiert** und **maschinell auslesbar**.
- Die Daten können **redaktionell gepflegt** werden.
- Eine **Stapelverarbeitung** z. B. in **Adobe Photoshop** ist problemlos möglich.


Volker, 07.2025