# Latex Editor

Grundsätzlich kann jeder Texteditor benutzt werden um Latex zu schreiben. Ich empfehle jedoch den Editor [Visual Studio Code](https://code.visualstudio.com). Eine Alternative wäre der auf Latex angepasste Editor [TexMaker](https://www.xm1math.net/texmaker/).

## TexMaker

TexMaker kann einfach von der [Herstellerseite](https://www.xm1math.net/texmaker/) heruntergeladen werden.

Wie du den Editor für dich einrichtest findest du in den [Dokumentationen](https://www.xm1math.net/texmaker/doc.html)

## VSCode

Visual Studio Code ist ein Texteditor, welcher durch sogenannten Extensions für verschiedene Usecases optimiert werden kann.

### Extensions

Extensions können installiert werden, indem du Links in der Sidebar auf "Extensions"-Reiter gehst. Dort kannst du die gewünschte Erweiterung in der Suchleiste eingeben.

Folgende Erweiterungen werden für die Verwendung von Latex benötigt:

- [Latex Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)
- [Latex Utilities](https://marketplace.visualstudio.com/items?itemName=tecosaur.latex-utilities)

Folgende weitere Extensions werden empfohlen:

- [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
- [German - Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker-german)
- [Bracket Pair Colorizer 2](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer-2)

### Latex Packages

Die verwendung des Latex Workshops benötigt folgende Latex Packages:

- Synctex
- ChkTex
- Latexindent

Wenn `latexmk` als Compiler verwendet werden soll:

- latexmk

Installiere diese Pakete über deine Latex Distribution.

### Einstellungen

Nun sollte Latex mit VSCode schon funktionieren. Für das optimale Erlebnis sind jedoch einige Änderungen in den Einstellungen notwendig.
Öffne die `settings.json` indem du `cmd - shift - p` (Mac) bzw. `strg - shift - p` (Windows, Linux) drückst und "settings" in das erscheinende Textfeld eingibst. Wähle "Preferences: Open Settings (JSON)". Es öffnet sich ein Dokument, in welchem du folgende Einstellung hinzufügen kannst:

Mit `xelatex` als Compiler

```json
"latex-workshop.latex.recipes": [
  {
    "name": "standard",
    "tools": ["xelatex"]
  },
],
"latex-workshop.latex.tools": [
  {
    "name": "xelatex",
    "command": "xelatex",
    "args": [
      "-synctex=1",
      "-interaction=nonstopmode",
      "-file-line-error",
      "-output-directory=%OUTDIR%",
      "%DOC%"
    ],
    "env": {}
  },
],
"latex-workshop.intellisense.package.enabled": true,
"latex-workshop.intellisense.unimathsymbols.enabled": true,
"latex-workshop.intellisense.update.delay": 600,
"latex-workshop.latex.autoClean.run": "never",
"latex-utilities.liveReformat.enabled": true,
"latex-workshop.view.pdf.viewer": "browser",
"[latex]": {
  "editor.defaultFormatter": "James-Yu.latex-workshop"
},
"latex-workshop.latex.outDir": "%DIR%/build",
"latex-utilities.message.update.show": false,
"latex-workshop.message.update.show": false,
```

Mit `latexmk` als Compiler

```json
"latex-workshop.latex.recipes": [
  {
    "name": "standard",
    "tools": ["latexmk"]
  },
  {
    "name": "xelatex",
    "tools": ["xelatex"]
  },
],
"latex-workshop.latex.tools": [
  {
    "name": "latexmk",
    "command": "latexmk",
    "args": [
      "-synctex=1",
      "-interaction=nonstopmode",
      "-file-line-error",
      "-pdf",
      "-outdir=%OUTDIR%",
      "%DOC%",
      "-f"
    ],
    "env": {}
  },
  {
    "name": "xelatex",
    "command": "xelatex",
    "args": [
      "-synctex=1",
      "-interaction=nonstopmode",
      "-file-line-error",
      "-output-directory=%OUTDIR%",
      "%DOC%"
    ],
    "env": {}
  },
],
"latex-workshop.intellisense.package.enabled": true,
"latex-workshop.intellisense.unimathsymbols.enabled": true,
"latex-workshop.intellisense.update.delay": 600,
"latex-workshop.latex.autoClean.run": "never",
"latex-utilities.liveReformat.enabled": true,
"latex-workshop.view.pdf.viewer": "browser",
"[latex]": {
  "editor.defaultFormatter": "James-Yu.latex-workshop"
},
"latex-workshop.latex.outDir": "%DIR%/build",
"latex-utilities.message.update.show": false,
"latex-workshop.message.update.show": false,
```
