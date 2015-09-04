# lisptalk

Einarbeitung
============

1. Scheme
---------

In der Einarbeitungsphase befasste ich mich mit der Zielprogrammiersprache Scheme (Lisp-Dialekt). Hierbei war der Fokus auf den AST (Abstract Syntax Tree) von Bedeutung. Folgende AST-Elemente wurden bearbeitet:

- Top Level / Parent Environment
- Built-In      (feste Werte, z.B. Zahlen)
- Closure       (sichbare Variable im Environment)
- Rekursion     (Rücksprungadresse, nutzt Stack)
- Tail Call     (bei Rekursion = letzter Call in einer Funtkion; Darf kein Stack kosten -> loops obsolet)
- let*          (Evaluiert lokale Variablen -> Variable gleich im Environment)
- let           (lokale Variable; innere kann äußere Variable betrachten)
- lambda        (Args+Body+ Environment vom aktuellem Zeitpunkt)
- if            (bestimmt selbst die evalu. der Argumente)
- symbol        (nicht-mutierbare Zeichen)
- define        (Bindung von symbol an Wertinhalt)
- quote         (nicht evaluiertes Symbol)
- cons          (Datenstruktur)
- car/cdr       (Getter-Methoden)
- set!          (Setter-Methode)

Der Ablauf in einer Programmierprache beruht auf vier Phasen, die REPL genannt wird.
R steht für Read, d.h. die eingespeisten Codezeilen werden von einem Leser eingelesen. Hierbei wird der Code auf die Syntax geprüft
E steht für Evaluate, d.h. hier wird geprüft, ob die gewünschten Funtionen oder Variablen existieren. Zahlen evaluieren zu sich selbst. 
                             Variablen hingegen evaluieren zum Binding im Environment. Listen, die als Funktionsaufrufe dienen evaluieren die Funktion
P steht für Print, d.h. die Ausgabe der zuvor evaluierten Zeichen wird dem Benutzer auf einer Konsole oder GUI ausgegeben.
L steht für Loop, d.h. die Eingabe ist nach der Bearbeitung der vorhergegangenen noch möglich und wartet auf neuen Input. REPL wird wieder neu angestoßen.


1.2 Smalltalk und Squeak

Als weitere Einarbeitung war die Programmiersprache Smalltalk und der Entwicklungsumgebung (IDE) Squeak. Als IDE wurde Squeak mit dem Image 4.5 verwendet.
Hierbei hat YouTube zwei User mit dem Namen _jarober_ und _Lawson English_, die sehr prägnant die Funktionen von Squeak aufgezeichnet haben. In den Videos wurden stark auf das Erlernen von Smalltalk gsetzt. Ich habe insgesamt neun Stunden Videomaterial angesehen. Die versteckten Feature der IDE sind nach und nach aufgetaucht und gut benutzt. Als Beispiel ist der Erstellung von Setter/Getter-Methoden oder Methodenkopieren auf höherer Hierarchie zu erwähnen.


2. Ziel und Probleme

Ziel war es mit der Programmiersprache Smalltalk den Dialekt Scheme nachzuprogrammieren.
Durch die zahlreichen Eindrücke von Smalltalk und das selbige zu erlernen war die Umsetzung mit unterschiedlichen Lösungsansätze behaftet.

- Problem Symobl-Numeric
Die Lösung für die Unterscheidung von Symoblen und numerischen Zahlen stockte die Entwicklung sehr, da in Smalltalk die Umwandlungsroutinen von eingelesenen Werten, wie +123 oder 1-23 in Integer dieRetszeichen wegschnitt. Somit hatte ich Asserts mit 1 als Integer statt 1-23 als Symbol. Gelöst wurde es durch den regulären Ausdruck (+-)([0-9])+ .

- Problem Smalltalk's printOn
Diese Methode setzt in eingelesenen Werten mehrfache Quote hinzu. Demnach sah der String '(+ 1 2)' in etwa so aus '''(+''1''2)'''. Gelöst wurde das mit der Smalltalk-Methode storeOn.

- Problem Timeout-in-Testing
Bei Testdurchläufen ist die IDE in einen Timeout gefallen und konnte nicht mehr die Tests zu Ende führen. Es war eine Eval-Loop das Problem. Gelöst wurde es durch die Nutzung eines Leerzeichens zwischen den Symbolen + und a... (+a 2). Ouch!

- Problem Eval-Kategorieüberschreibung in IDE-Umgebung
Bei Namensgebung von Instanzvariablen muss beachtet werden, dass der Name _name_ von der IDE vordefiniert ist. Das führte oft dazu, dass die Kategorie SchemeEval einfach überschrieben wurde und nicht mehr genutzt werden konnte. Hierbei war die Lösung auf einen älteren Stand von Squeak zu gehen (Snapshot). Das kostete unmengen von Zeit dieses Problem zu lösen

3. Arbeitsumfang

Durch die neu erlernte Sprache Smalltalk und die anfänglichen Probleme in der Implementierung ist das Ergebnis der Arbeit auf ein Minimum reduziert worden.
- Integer als Numeric umgesetzt
- Floats als Numeric umgesetzt
- Eval von Closure (also _define_ klappt)
- Print in Squeak-Fenster Transcript
- Tests erstellt (auch Fac-Test)
- set! klappt
- Environment möglich
- if umgesetzt
- lambda umgesetzt
