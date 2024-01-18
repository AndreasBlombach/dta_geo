# Geo-Daten für Texte des Deutschen Textarchivs (DTA)
Die [vorliegende Excel-Tabelle](dta_geo.xlsx) wurde von Bettina Lindner-Bornemann und mir erstellt; sie enthält Geoinformationen und weitere Metadaten zu den im DTA (samt DTA-Erweiterungen) gesammelten Werken. Ursprünglich angelegt wurde sie für unser [Projekt zum possessiven Dativ](https://github.com/AndreasBlombach/Possessiver_Dativ), kann jedoch für beliebige diatopische Untersuchungen auf DTA-Basis verwendet werden.

## Datenquellen
Die Basisdaten stammen aus einer [DTA-Abfrage über die Kaskade-Oberfläche](https://kaskade.dwds.de/dstar/dta/dstar.perl?q=count%28*+%23sep%29+%23by%5Bbasename%2C+dtaid%2C+textClass%2C+collection%2C+flags%2C+firstDate%2C+author%2C+title%5D&fmt=kwic&start=1&limit=20&ctx=8&debug=&export=):

```count(* #sep) #by[basename, dtaid, textClass, collection, flags, firstDate, author, title]```

Weitere Spalten wurden von uns hinzugefügt. Nach der Extraktion der IDs der Gemeinsamen Normdatei (GND) konnten wir über die [Culturegraph-API](https://hub.culturegraph.org/search) weitere Autorenmetadaten sammeln, insbesondere Geburtsorte und deren Längen- und Breitengrade. Fehlende Informationen wurden in einem langwierigen Prozess manuell ergänzt (mit Informationen aus Wikipedia, Pfarrbüchern, Adelsstammbüchern, Universitätsmatrikeln usw.). Einige Informationen, die automatisch gewonnen wurden, haben wir zudem korrigiert.

## Spalten-Übersicht
### Aus dem DTA übernommene Daten
- **tokens**: Anzahl der Tokens im Dokument
- **basename**: Name des Dokuments (eindeutiger Identifikator) im DTA (wird auch in URLs der DTA-Website verwendet -- so ist bei `https://www.deutschestextarchiv.de/book/show/bohse_helicon01_1703` der Dokumentname `bohse_helicon01_1703`)
- **dtaid**: alternative eindeutige ID im DTA
- **textClass**: Textklassifikation; Unterklassen folgen auf doppelte Doppelpunkte, z.B. `Gebrauchsliteratur::Leichenpredigt`
- **collection**: Angabe, ob das Dokument im DTA-Kernkorpus (`dtak`) oder im Erweiterungskorpus (`dtae`) enthalten ist
- **subcorpus**: Angabe zum Subkorpus, aus dem das Dokument stammt, z.B. `ready::blumenbach` für "Johann Friedrich Blumenbach – online"; vgl. [Übersicht beim DTA](https://www.deutschestextarchiv.de/doku/textquellen)
- **year**: Jahr des ersten Erscheinens
- **author**: Autorenangabe im DTA
- **title**: Titel des Werks

### Weitere Spalten
- **author_id**: GND-ID laut DTA (für Korrekturen unsererseits siehe Spalte **dnb_id**)
- **name**: vollständiger Name
- **surname**: Nachname
- **forename**: Vorname
- **gender**: Geschlecht
- **place_of_birth**: Geburtsort (primär); in einigen Fällen ist hier auch bloß ein Wirkungsort angegeben, was dann aber in einem Kommentar vermerkt ist; im Falle von Zeitungen u.ä. der Erscheinungsort
- **translation**: nur im Falle alter Übersetzungen: Erscheinungsort der Übersetzung (nur wenn keine Informationen zum Übersetzer vorliegen)
- **longitude**: Längengrad unserer Ortszuordnung (WGS 84)
- **latitude**: Breitengrad (WGS 84)
- **dnb_id**: korrekte GND-ID (nur wenn **author_id** nicht stimmt oder obsolet geworden ist)
- **comment**: Kommentar zu unserer Recherche
- **coords_birth**: Wahrheitswert: beziehen sich die eingetragenen Koordinaten auf einen tatsächlichen Geburtsort des angegebenen Autors oder nicht (im Falle von Wirkungsorten, Erscheinungsorten, Übersetzungen oder Geburtsorten von Übersetzern) -- als Filtermöglichkeit intendiert
