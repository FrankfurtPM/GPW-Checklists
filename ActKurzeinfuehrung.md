# Kurzeinführung in Act! für die lokale Orga des Deutschen Perl-Workshops

## Initialisierung

Seit 2009 wird für die Organisation des Deutschen Perl-Workshops die Software [Act!](http://act.mongueurs.net/) genutzt.
Die Instanz wird von den französischen Perlmongers verwaltet, die lokale Orga füllt die Seite "nur" mit Inhalten.

Das Anfordern der Instanz übernimmt Frankfurt.pm, in der Regel macht das Renée (wenn nicht, einfach anstubsen).
Die Workshop-Daten liegen dann in einem Github-Repository. Die Berechtigungen für das Repository und auch im Act! 
werden von initial von Frankfurt.pm vergeben. Wenn irgendwo Rechte fehlen, bitte Bescheid geben.

## Vom Repository ins Internet

Im Repository (z.B. das Repository von
[2019](https://github.com/Act-Conferences/gpw2019)) gibt es zwei
Branches. Was auch immer dorthin gepusht wird, erscheint in wenigen
Minuten auf der entsprechenden Webseite:

   * `master` - wird veröffentlicht auf dem Testserver [http://test.mongueurs.net/gpw2019/]
   * `production` - wird veröffentlicht auf dem offiziellen Server [http://act.yapc.eu/gpw2019/index.html]

Der Prozess läuft also wie folgt:

   1. Inhalte im Branch `master` lokal bearbeiten
   2. `git commit` + `git push`
   3. Kaffee kochen
   4. Prüfen auf dem [Testserver](http://test.mongueurs.net/gpw2019/)
   5. Falls nicht ok: goto 1, wenn alles in Ordnung: `git rebase master` im Branch `production`
   6. `git push origin production`
   7. Kaffee trinken
   8. Letzter Check auf der [offiziellen Webseite](http://act.yapc.eu/gpw2019/index.html)


## Inhalt des Repository

-> [Act-Manual](http://act.mongueurs.net/doc/Manual/Organizer/Layout.html)

Im Repository gibt es zwei Ordner:

* actdocs
* wwwdocs

## wwwdocs

Fangen wir mit dem Einfachen an. Das sind die Dateien in wwwdocs. Darin werden die statischen Dateien abgelegt, die vom Webserver unverändert durchgereicht werden:
Bilder (`images`), JavaScript-Bibliotheken (`scripts`) und Stylesheets (`styles`).
Wir benutzen seit Jahren das selbe Layout. Wenn ihr das ebenfalls verwenden wollt, ist nur der Unterordner images
interessant um dort bspw. die Logos der Sponsoren abzulegen.

Wenn ihr ein eigenes Layout machen wollt, dann werden hier auch JavaScript-Dateien und CSS abgelegt.

Zum eigenen Layout später mehr.

*FIXME:* Die Datei `wwwdocs/styles/bronx-in-style.css` wird nicht verwendet und referenziert ein nicht (mehr) existierendes Bild `images/caravan-2048x400.jpeg`.

## actdocs

Das Verzeichnis `actdocs` ist wesentlich interessanter...

Die wichtigste Datei zuerst: [conf/act.ini](./conf/act.ini). 

### act.ini

Viele Sachen können über die act.ini konfiguriert werden.

 * Registration: Abschnitt '[registration]', Wert 'open' 
 * Call for Papers: Wert 'submissions_open'
 * Preise
 * Räume: Abschnitt '[rooms]', von der lokalen Orga zu befüllen

### Änderungen in der act.ini

  * Nach erstellen des Repositories: Überall sollte die Jahreszahl angepasst werden
  * Wenn Datum feststeht: unter `[talks]` sollte das `start_date` und `end_date` angepasst werden
  * Bei Livestellung der Webseite: Die Möglichkeit, Vortragsvorschläge einzureichen sollte gleich aktiviert werden (`submission_open` auf 1 setzen)
  * Wenn Veranstaltungsort feststeht: Räume und Raumbezeichnungen eintragen, ggf. Preise anpassen

### static

In diesem Verzeichnis liegen die Texte, die auf den Webseiten sichtbar
werden, als Dateien mit der Endung `.html`.  Diese Texte sind
HTML-Blöcke, die Act mit dem
[Template::Toolkit](https://metacpan.org/pod/Template::Toolkit) (TT) weiter
verarbeitet.  Die erste und letzte Zeile müssen also erhalten bleiben!

Die Zweisprachigkeit der Texte wird über Fake-HTML-Elemente `t` in den
Seiten organisiert, die überall stehen können, wo in HTML Texte
erlaubt sind, aber auch in Attributen von HTML-Elementen:

```txt
<t>
  <de>Deutscher Text</de>
  <en>English text</en>
</t>
```

Wenn das Repository existiert, müssen alle statischen Dateien durchgegangen werden und Einträge von alten Perl-Workshops entfernt bzw. ausgeblendet werden.

## eigenes Layout

Für Act! wird die Template-Engine [Template::Toolkit](https://metacpan.org/pod/Template::Toolkit) verwendet.

```txt
Das ist noch ein TODO
```

### CSS-Klassen für Styling

Act! verwendet [Bootstrap](https://github.com/twbs/bootstrap) für CSS-Klassen, ergänzt um eigene Styles.
Eine alphabetische Übersicht der Bootstrap-Klassen findet man bei [W3Schools](https://www.w3schools.com/bootstrap/bootstrap_ref_all_classes.asp).
Selbst definierte Klassen (in `wwwdocs/styles/base.css`) sind
 * `conferencedata` - für zentrierten Block
 * `span.conference` - für Block-Display
 * `icon.envelope` - Briefumschlag-Emoji
 * `clearfixafter` - Float-Elemente beenden (angelehnt an `clearfix` aus Bootstrap)
 * `homelink` - optische Gimmicks

Bislang in CSS nicht definierte Klassen zur Strukturierung: `dateaddon`, `what`, `where`, `when`, `email`, `newsblock`

Das "Responsive Design" in `wwwdocs/styles/base.css` unterscheidet
wie Bootstrap nach folgenden Bildschirmbreiten:
 * **xs** <=767px (@screen-xs-max)
 * **sm** 768px(@screen-sm-min) - 991px(@screen-sm-max)
 * **md** 992px(@screen-md-min) - 1199px(@screen-md-max)
 * **lg** >1200px(@screen-lg-min)

Das ist allerdings in der Datei eingermaßen unübersichtlich angeordnet.

...in `wwwdocs/styles/base.css` stehen am Ende noch einige Fragen, die
vielleicht seit 2017 unbeantwortet sind... wohl weil sie niemand dort
erwartet hätte.


### templates

-> [Act Manual](http://act.mongueurs.net/doc/Manual/Organizer/Templates.html)

Hier liegen die Templates für TT.  Das "Master-Template" ist die Datei
`ui`.  Sowohl die statischen als auch die dynamisch von Act
generierten Seiten verwenden dies als Rahmen um den eigentlichen
Inhalt, der anstelle der TT-Variablen `[% content %]` eingefügt wird.

#### Anzupassende Templates

* Sobald das Repository existiert

In `/actdocs/templates/ui` muss für das vorangegangene Jahr ein Eintrag im Dropdown (select mit id="archiv") gemacht werden, so dass man auch zu früheren Deutschen Perl-Workshops springen kann.

In `/actdocs/templates/payment/invoice` muss das Jahr angepasst werden

* Sobald der Veranstaltungsort feststeht

In `/actdocs/templates/event/show` müssen die Geodaten des Veranstaltungsortes eingetragen werden


## Die "dynamischen" Seiten: Wiki, News, Events, ...

Neben dem statischen Inhalt, der aus dem Repository bedient wird, gibt
es auch Inhalte, die "live" in die Datenbank eingepflegt und aus
dieser auch geliefert werden: Neben den Vorträgen sind das das Wiki,
die News und die Events.

### Die Vorträge

Registrierte Nutzer können Vorträge einreichen, und das Orga-Team
(genauer: Nutzer mit `talks_admin`-Berechtigung) kann diese annehmen
und bearbeiten.  Über die "edit"-Funktion werden auch der Raum und der
Termin für den Vortrag festgelegt und sind danach im Programm
sichtbar.

### Das Wiki

Im Wiki (URL z.B. https://act.yapc.eu/gpw2019/wiki) können alle
angemeldeten Teilnehmer Inhalte nach Lust und Laune pflegen.

Es gibt leider keinen News-Feed für das Wiki.  Eine redaktionelle
Prüfung kann aber über die "Recent changes"
(https://act.yapc.eu/gpw2019/wiki?action=recent) durchgeführt werden.

### Die News

Die News sind kurze, zweisprachig angelegte Artikel, die das Orga-Team
(genauer: Nutzer mit `news_admin`-Berechtigung) erzeugen kann.  Für
publizierte News wird ein Feed über die URLs
https://act.yapc.eu/gpw2019/atom/de.xml und
https://act.yapc.eu/gpw2019/atom/en.xml bereitgestellt.

### Die Events

Events sind "Ereignisse" mit Datum, Uhrzeit und Ort, und sie werden
zusammen mit den Vorträgen im Programm angezeigt.  Auf diesem Weg
sollten auch Termin und Ort für Registrierung, Vorabend-Meeting und
Social Event eingetragen werden, sonst sind sie im Programm nicht
sichtbar!
