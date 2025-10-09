---
layout: simple
title:  "Steuerung von Wasserzeichen- und Download-Option für Artefakte"
date: 02.07.2025
---

## Konzept
Zur Steuerung der Anzeige von Wasserzeichen in Artefakten und der Download-Möglichkeit von Artefakten im **CDA** werden entsprechende Kennzeichnungen in den **IPTC-Daten** der jeweiligen **Bilddatei** hinterlegt.  

Hierfür wird das IPTC-Feld **`SpecialInstructions`** verwendet.  

## Kennzeichnung
Folgende Keywords und Kombinationen werden zur Kennzeichnung verwendet:

| Zustand                                                    | IPTC-Eintrag (`SpecialInstructions`) |
| ---------------------------------------------------------- | ------------------------------------ |
| Artefakt hat kein Wasserzeichen                            | `no-watermark`                       |
| Artefakt ist downloadbar                                   | `download`                           |
| Artefakt hat kein Wasserzeichen **und** ist downloadbar    | `no-watermark, download`             |
| Artefakt ohne Wasserzeichen und **nicht** downloadbar      | *(Feld leer lassen)*                 |


Die Keywords werden als **kommagetrennte Liste** im Feld `SpecialInstructions` abgelegt.

## Vorteile

- Das IPTC-Feld `SpecialInstructions` ist **standardisiert** und **maschinell auslesbar**.
- Die Daten können **redaktionell gepflegt** werden.
- Eine **Stapelverarbeitung** z. B. in **Adobe Photoshop** ist problemlos möglich.


Volker, 07.2025