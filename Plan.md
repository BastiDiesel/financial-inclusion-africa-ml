Der Plan — 4 Tage, nach Themen und Stunden
Dieser Plan ist gleichzeitig deine Projektdokumentation. Du kannst ihn direkt als README-Abschnitt oder als separates PLAN.md in dein Repo legen.

Tag 1 — Montag: Fundament und Datenverständnis
Ziel des Tages: Repo steht, Daten sind lokal, du weißt was in den Spalten steckt. Kein Modell, kein Plot, kein Preprocessing.
Schritt 1 — .gitignore prüfen

Bevor du irgendwas in data/ legst, öffne .gitignore und stelle sicher, dass data/*.csv oder data/ drin steht. Daten dürfen laut Zindi-Regeln nicht öffentlich auf GitHub. Das ist nicht optional.
Schritt 2 — Daten herunterladen

Melde dich bei Zindi an (falls noch nicht) und lade alle 5 Dateien herunter: Train.csv, Test.csv, VariableDefinitions.csv, SampleSubmission.csv, StarterNotebook.ipynb. Alle CSVs in den data/-Ordner legen. Das StarterNotebook separat ablegen oder kurz im Browser öffnen — nicht in dein Repo committen.
Schritt 3 — Virtuelle Umgebung

In PowerShell, im Projektordner:
powershellpython -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
Falls requirements.txt kein jupyter enthält: pip install jupyter pandas matplotlib seaborn scikit-learn zusätzlich installieren.
Schritt 4 — StarterNotebook lesen (nicht kopieren)

Öffne das Zindi-StarterNotebook einmal komplett durch. Fragen, die du dabei beantworten willst: Welche Spalten gibt es? Was ist der Datentyp jeder Spalte? Wie viele Missing Values? Wie sieht das Submission-Format aus — Wahrscheinlichkeiten oder 0/1?
Schritt 5 — Eigenes Notebook starten

Öffne EDA-and-modeling.ipynb. Erste Zelle: Imports. Zweite Zelle: pd.read_csv() für Train und Test. Dritte Zelle: df.shape, df.info(), df.head(), df.describe(). Vierte Zelle: Zielvariable bank_account — wie viele 1er, wie viele 0er? Das ist die Klassenverteilung. Fünfte Zelle: df.isnull().sum() — gibt es Missing Values?
Tagesende-Checkpoint: Du kannst beantworten: Wie viele Spalten hat der Datensatz? Was bedeutet jede Spalte laut VariableDefinitions.csv? Wie ungleich ist die Zielvariable verteilt?

Tag 2 — Dienstag: EDA und Hypothesen
Ziel des Tages: Du verstehst, welche Variablen wahrscheinlich wichtig sind. Du hast 6–8 Visualisierungen mit schriftlicher Interpretation im Notebook.
Schritt 1 — Kategorische Spalten untersuchen

Für jede kategorische Spalte (Land, Geschlecht, Bildung, Job-Typ, Wohnort Stadt/Land, Handy-Zugang): Wie verteilt sich bank_account = 1 innerhalb der Gruppe? Das machst du mit groupby und einem Balkendiagramm.
Schritt 2 — Numerische Spalten untersuchen

Alter und Haushaltsgröße sind wahrscheinlich numerisch. Boxplot oder Histogramm, aufgeteilt nach bank_account. Gibt es einen Alterseffekt?
Schritt 3 — Korrelationen

Für numerische Spalten: df.corr() und ein Heatmap. Für kategorische: Cramér's V oder einfach visuelle Inspektion.
Schritt 4 — Hypothesen aufschreiben

Nach jedem Plot schreibst du im Notebook einen Satz: Was siehst du? Was bedeutet das fachlich? Das ist kein netter Zusatz — das ist ein Pflichtbestandteil für Coaches und Präsentation. Beispiel: „Personen in städtischen Gebieten haben mit X% deutlich höhere Bankkonten-Penetration als ländliche Gebiete (Y%). Das deutet auf Infrastruktur als Schlüsselbarriere hin."
Schritt 5 — Klassenungleichgewicht dokumentieren

Notiere explizit: Wie viel Prozent haben ein Bankkonto, wie viele nicht? Welche Auswirkung hat das auf die Modellwahl? Welche Metrik bevorzugst du dadurch — und warum?
Tagesende-Checkpoint: Du kannst 5 Erkenntnisse aus den Daten benennen, die in der Präsentation verwendet werden können.

Tag 3 — Mittwoch: Preprocessing, Modelle, Evaluation
Ziel des Tages: Drei Modelle laufen, sind evaluiert, das beste ist identifiziert.
Schritt 1 — Preprocessing-Pipeline bauen

Mit sklearn.pipeline.Pipeline und ColumnTransformer:

Kategorische Spalten: OneHotEncoder oder OrdinalEncoder. Numerische Spalten: StandardScaler (für Logistic Regression nötig, für Baummodelle egal). Target-Spalte bank_account ist deine y. unique_id und ähnliche ID-Spalten raus aus den Features.
Schritt 2 — Train/Validation-Split

train_test_split mit stratify=y, weil die Klassen ungleich verteilt sind. 80/20 reicht.
Schritt 3 — Baseline

Dummy-Classifier mit strategy='most_frequent'. Was ist der MAE, wenn du immer die häufigste Klasse vorhersagst? Das ist deine Untergrenze — jedes echte Modell muss darunter kommen.
Schritt 4 — Drei Modelle

Modell 1: Logistic Regression. Modell 2: Decision Tree. Modell 3: Random Forest. Für jedes Modell: trainieren, auf dem Validation-Set evaluieren, MAE berechnen, zusätzlich Accuracy, Precision, Recall, F1, Confusion Matrix ausgeben.
Schritt 5 — Cross Validation

Für jedes Modell cross_val_score mit cv=5. Das zeigt, wie stabil das Modell über verschiedene Datensplits ist. Ergebnis: Mittelwert und Standardabweichung des Scores.
Schritt 6 — Hyperparameter Tuning für das beste Modell

GridSearchCV oder RandomizedSearchCV. Beim Random Forest zum Beispiel n_estimators, max_depth, min_samples_split. Nicht zu viele Parameter — 2–3 reichen für ein sauberes Ergebnis.
Tagesende-Checkpoint: Du weißt, welches Modell am besten ist und warum.

Tag 4 — Donnerstag: Submission, Notebook aufräumen, Slides
Ziel des Tages: Submission läuft auf Zindi. Notebook ist sauber. Erste Version der Slides steht.
Schritt 1 — Finale Vorhersage

Das beste Modell auf dem gesamten Trainingsdatensatz neu trainieren (nicht nur 80%). Auf Test.csv anwenden. Falls Zindi Wahrscheinlichkeiten erwartet: predict_proba()[:, 1] statt predict(). Submission-Datei bauen im Format aus SampleSubmission.csv.
Schritt 2 — Zindi-Submission

Datei hochladen. MAE-Score notieren. Ist er besser als der Baseline-Score? Wenn ja, gut. Wenn nicht — kurze Fehlersuche: Sind die IDs korrekt? Ist das Format stimmt?
Schritt 3 — Notebook aufräumen

Überflüssige Zellen löschen. Markdown-Zellen als Überschriften einbauen: # 1. Data Loading, # 2. EDA, # 3. Preprocessing, # 4. Modeling, # 5. Evaluation, # 6. Submission. Jeder Abschnitt hat eine kurze Erklärung, was und warum.
Schritt 4 — Slides bauen

Struktur (10 Folien, ca. 10 Minuten):

Titel + Team (= du) + Datum
Business Context: Was ist Financial Inclusion? Warum ist es wichtig?
Das Problem: Wer hat kein Bankkonto — und warum wollen wir das vorhersagen?
Datensatz: Woher, wie groß, welche Länder
Wichtigste EDA-Erkenntnisse (3–4 deiner besten Plots)
Modellansatz: Welche 3 Modelle, warum, welche Metriken
Modellvergleich-Tabelle: MAE, F1, Accuracy für alle 3
Bestes Modell + Feature Importance (welche Spalten sind am einflussreichsten?)
Data Product Idee: Wie könnte dieses Modell real genutzt werden? (z.B. Bank-App, NGO-Tool, Kreditvergabe-Vorhersage)
Limitations & Future Work

Tagesende-Checkpoint: Submission ist live auf Zindi. Notebook ist lesbar. Slide-Gerüst steht.

Tag 5 — Freitag: Finalisieren und Präsentation
Ziel des Tages: Alles ist auf GitHub, Präsentation ist geprobt.
Slides als PDF exportieren und ins Repo legen. README aktualisieren: Projektbeschreibung, wie man das Notebook ausführt, was die Ergebnisse sind. GitHub prüfen: Sind Daten in .gitignore? Ist das Notebook korrekt committed? Einmal die Präsentation laut durchsprechen — nicht vorlesen, sondern erzählen.