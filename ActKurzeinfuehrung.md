# Kurzeinführung in Act! für die lokale Orga des Deutschen Perl-Workshops

Seit 2009 wird für die Organisation des Deutschen Perl-Workshops die Software [Act!](http://act.mongueurs.net/).
Die Instanz wird von den französischen Perlmongers verwaltet, die lokale Orga füllt die Seite "nur" mit Inhalten.

Das Anfordern der Instanz übernimmt Frankfurt.pm, in der Regel macht das Renée (wenn nicht, einfach anstubsen).
Die Workshop-Daten liegen dann in einem Github-Repository. Die Berechtigungen für das Repository und auch im Act! 
werden von initial von Frankfurt.pm vergeben. Wenn irgendwo Rechte fehlen, bitte Bescheid geben.

Im Repository (z.B. das Repository von [2018](https://github.com/Act-Conferences/gpw2018)) gibt es zwei Ordner:

* actdocs
* wwwdocs

Fangen wir mit dem Einfachen an. Das sind die Dateien in wwwdocs. Darin werden die statischen Dateien abgelegt.
Wir benutzen seit Jahren das selbe Layout. Wenn ihr das ebenfalls verwenden wollt, ist nur der Unterordner images
interessant um dort bspw. die Logos der Sponsoren abzulegen.

Wenn ihr ein eigenes Layout machen wollt, dann werden hier auch JavaScript-Dateien und CSS abgelegt.

Zum eigenen Layout später mehr.

## actdocs

Das Verzeichnis `actdocs` ist wesentlich interessanter...

Die wichtigste Datei zuerst: [conf/act.ini](./conf/act.ini). 

### act.ini

Viele Sachen können über die act.ini konfiguriert werden.

 * Registration
 * Call for Papers
 * Preise
 * Räume

### static

## eigenes Layout

Für Act! wird die Template-Engine [Template::Toolkit](https://metacpan.org/pod/Template::Toolkit) verwendet.

```txt
Das ist noch ein TODO
```
