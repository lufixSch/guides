---
layout: lufix
title: Document
permalink: guides/latex/document
parent: Latex
grand_parent: Guides
nav_order: 3
---

# Latex Dokument
## Syntax

Alles, was in einer `.tex`-Datei geschrieben wird, interpretiert der Latex-Compiler als Text, welcher genau so im fertigen Dokument dargestellt wird. Des weiteren ermöglicht Latex das Nutzen von Formatierungsbefehlen und -umgebungen sowie Makros.

Der Standard-Befehlssatz von Latex kann durch das installieren und importieren von Paketen erweitert werden.

```tex
\usepackage[konfiguration]{packetname}
```

Kommentare beginnen in Latex mit einem `%`. Sollten innerhalb eines Textes Zeichen verwendet werden, welche auch Teil der Latex-Syntax sind können diese mit `\zeichen` dargestellt werden (Bsp.: `\%` => %). Das `\`-Zeichen kann mit `\backslash` dargestellt werden.

### Befehle und Makros

Formatierungsbefehle werden mit einem `\` eingeleitet. Damit kann der Text formatiert oder das Seitenlayout verändert werden. Ein Befehl kann aber auch ein Makro, also eine vorher definierte Konstante sein. Befehle sind wie folgt aufgebaut:

```tex
\befehl[konfiguration]{wert}
```

In den eckigen Klammern können Konfigurationen an den Befehl übergeben werden. In den geschweiften Klammern werden Parameter übergeben. Beides wird nicht von jedem Befehl verlangt oder ist optional.

**Bsp.:**
- `\textbf{Some Text}` => **Some Text**
- `\textcolor{blue}{Some Text}` => <span style="color:blue">**Some Text**</span>

### Umgebungen

Umgebungen (Environments) können Layout oder Formatierungen für ganze Textabschnitte konfigurieren. Sie sehen wie folgt aus:

```tex
\begin{Umgebung}[konfiguration]{wert}
  ... Some Text ...
\end{Umgebung}
```

Innerhalb einer Umgebung können beliebig viele weitere Latex-Befehle oder -Umgebungen verwendet werden solange diese mit der Umgebung kompatibel sind.

**Bsp.:**
```tex
\begin{math}
  5 = 3x + \frac{2}{3} + 10x^2
\end{math}
```

$$ 5 = 3x + \frac{2}{3} + 10x^2 $$

## Aufbau

Ein Latex Dokument beginnt in einer `.tex`-Datei bestehend aus der `\documentclass{}` einigen Konfigurationen und dem **document**-Environment.

### Documentclass

Dieser Befehl befindet sich immer zu beginn des Latex-Dokuments. Er gibt an auf welcher Vorlage das Dokument basieren soll. Diese Vorlagen liefern grundlegende Konfigurationen, wie das Seitenformat. Jede Vorlage bringt ein paar eigene Befehle mit sich. Für Laborprotokolle, Wissenschaftliche Abhandlungen und ähnliches ist die Klasse `article` zu empfehlen.

**Bsp.:**
```tex
\documentclass[a4paper, titlepage]{article}
```

### Konfigurationen

Hier werden allgemeine konfigurationen festgehalten und die benötigten Pakete importiert.

Ein Paket, das immer importiert werden sollte ist `babel`. Mit diesem Paket wird sichergestellt, dass alle Zeichen der verwendeten Sprache von Latex richtig interpretiert werden.

```tex
\usepackage[sprache]{babel}
```
**Für Deutsch:**
```tex
\usepackage[german]{babel}
```

### document-Environment

In diese Umgebung wird alles geschrieben, was tatsächlich im Dokument dargestellt werden soll. Erkennt Latex regulären Text außerhalb dieser Umgebung, wird ein Fehler ausgeworfen

```text
\begin{document}
  Dein Latex Dokument
\end{document}
```

## Wichtige Befehle

### Überschriften (`\documentclass{article}`-Spezifisch)
- `\section{Überschrift 1}`
- `\subsection{Überschrift 2}`
- `\subsubsection{Überschrift 3}`

### Text-Formatierungen
- `\textbf{Fett}`: **Fett**
- `\textit{Kursiv}`: *Kursiv*

### Seitenlayout
- `\\`: Zeilenumbruch
- `\p`: Zeilenumbruch mit Spacing (Eigener Befehl aus meiner Vorlage)
- `\newpage` oder `\pagebreak`: Seitenumbruch
- `\clearpage`: Seitenumbruch (Alle temporären Konfigurationen werden zurückgesetze - Gilt auch für *Floating* Objekte, wie Bilder)

### Formeln
Formeln in einer Zeile mit dem Text: `$formel$`, `\(formel\)`

Formelblock:

```tex
\begin{align*}
  x &= 2x + 3\\
  x &= -3
\end{align*}
```

Einzelne Zeilen werden anhand des `&`-Zeichens zentriert

Formelblock mit Zeilennummerierung:

```tex
\begin{align}
  x = 42
\end{align}
```

### Bilder

Diese Variante benötigt das Paket `\usepackage{graphicx}`

```tex
\begin{figure}[ht]
  \includegraphics[height=8cm]{/path/to/image}
  \caption{Bildunterschrift}\label{fig:bezeichnung}
\end{figure}
```

- `[ht]`: Bestimmt das verhalten des Bildes zum Text (Alternativen: `[]`, `[!ht]` ...)
- `[height=8cm]`: Angabe von Höhe und/oder Breite in *cm*, *pt*, *em* usw.
- `\label{fig:bezeichnung}`: Ermöglicht das Referenzieren des Bildes im Text mit `\ref{fig:bezeichnung}`

### Tabellen

Diese Variante benötigt das Paket `\usepackage{tabularx}`

```tex
\begin{table}[ht]
  \caption{Tabellenüberschrift}\label{tab:bezeichnung}
  \begin{tabular}{l|cc}
    a & b & c\\
    \hline
    d & e & f\\
  \end{tabular}
\end{table}
```

- `[ht]`: Bestimmt das verhalten des Bildes zum Text (Alternativen: `[]`, `[!ht]` ...)
- `{l|cc}`: Konfiguriert die Anzahl der Spalten und ihre Formatierung
  - `c`: Zentrierte Spalte
  - `l`: Linksbündig
  - `r`: Rechtsbündig
  - `|`: Trennlinie
- `&`: Aufteilen des Textes in die einzelnen Spalten
- `\\`: Neue Zeile
- `\label{tab:bezeichnung}`: Ermöglicht das Referenzieren des Bildes im Text mit `\ref{tab:bezeichnung}`}