# Latex Distro

Es gibt viele verschiedene Latex Distributionen.
Die einfachste Bedienung (über ein graphisches Interface) bietet [MikTex](https://miktex.org). Ein alternatives Command Line Tool ist [TexLive](http://www.tug.org/texlive/).
[Perl](https://www.perl.org) wird nur benötigt, wenn der Compiler `latexmk` verwendet wird.

## MikTex

MikTex kann einfach von der [Herstellerwebseite](https://miktex.org) heruntergeladen und installiert werden.
Fehlende Bibliotheken werden automatisch installiert, wenn sie in dem verwendeten Latexprojekt benötigt werden.

## TexLive

Für die Installation von TexLive kannst du der Anleitung auf der [Herstellerwebseite](http://www.tug.org/texlive/) für dein Betriebssystem folgen.

## Perl

Perl ist auf Unix Betriebssystemen (Linux, MacOS) in der Regel schon installiert. Für Windows kann Strawberry Perl von der [Herstellerwebsite](https://strawberryperl.com) runtergeladen werden.
Nach der Installation sollte sichergestellt werden, dass der Pfad zu Perl in der `PATH` Variable hinterlegt wurde. Normalerweise liegt Perl hier: `C:\Strawberry\perl\bin`
Damit Perl in Visual Studio Code erkannt wird muss der Computer möglicherweise neu gestartet werden.
