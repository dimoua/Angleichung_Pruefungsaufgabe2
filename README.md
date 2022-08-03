# Prüfungsaufgabe2: Logging und Input-Output Unit Test Ansatz auf Machine Learning basierter Software Systeme:die Funktionen werden auf das Decision-Tree Projekt implementiert.



[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/dimoua/Angleichung_Pruefungsaufgabe2.git/HEAD)

Quellen: Unit Testing & Logging: https://towardsdatascience.com/unit-testing-and-logging-for-data-science-d7fb8fd5d217 Decision-Tree: Udemy Kurs - Python für Data Science, Machine Learning & Visualization

## Funktionsausführung
Nach der Aufruf der Binder badge, bitte auf der Notebook 3-Aufgabe2_Decision_Trees_und_Random_Forests_Projekt-Loesung_Fix - Version2.ipynb klicken. Restart der Kernel und Run das gesamte Notebook, damit alle Bibliotheken aufgeladen werden und somit die Funktion head() ausgeführt wird.

Analog zu der ausgeführte Programm in der Artikel, werden die Funktionen my_logger und my_timer hinzugefügt: from functools import wraps def my_logger(orig_func): import logging logging.basicConfig(filename='{}.log'.format(orig_func.name), level=logging.INFO)

<img width="351" alt="2022-08-03 23_45_53-3-Aufgabe2_D… (auto-d) - JupyterLab" src="https://user-images.githubusercontent.com/62958158/182718616-1369bc6d-33a7-4db9-bf3b-0ad719c7acf5.png">


Anwendung von my_logger und my_timer auf ausgewählte Funktionen.

*** Die erste Funktion ist die Fit-Funktion aus der Decision-Tree Projekt

@my_logger
@my_timer
def modelruntime(): 
    return dtree.fit(X_train,y_train)
modelruntime()

**Nach Ausführung wird folgenden Ergebnis angezeigt: ***modelruntime ran in: 0.09817290306091309 sec


***Zweite Funktion auf die Prediction-Funktion @my_logger @my_timer

def lm_predict(): return logmodel.predict(X_test) predict = lm_predict()

**Nach Ausführung wird folgenden Ergebnis angezeigt: ***lm_predict ran in: 0.002523660659790039 sec

**Für die my_logger Funktion wird eine Log-Datei "logmodelFit.log" erzeugt, welcher im Ordner gespeichert wird

#Testfälle 1 und 2

**Für den Testfall 1 steht zum einen der testdatenfile_1.txt sowie der testdatenfile_2.txt zur Verfügung. **Die textfiles werden an folgender Stelle eingelesem with open("testdatenfile_1.txt", 'r') as f: Inhalt = f.read() **Bei Verwendung des ersten Textfiles (testdaten_score=0.85) ist der Test erfolgreich (Anzeige von "OK"). Zur Verwendung des zweiten Testfiles (testdaten_score=0.90) muss in der obigen Funktion der "testdatenfile_1.txt" durch "testdatenfile_2.txt" ersetzt werden. Als Ergebnis werden wir erhalten, dass der Test durchgefallen (Anzeige von "FAILED") ist.

Für Testfall 2 wird überprüft, ob die Laufzeit der Trainingsfunktion, die 120%-Grenze der repräsentativen Laufzeit überschreitet. time_1=time.time() logmodel_test.fit(X_train,y_train) self.time_2 = time.time() - time_1 Durch Ausführen der oben gezeigten Zeilen, wird im Notebook die Laufzeit für die Trainingsfunktion ermittelt, in dem die aktuelle Zeit (time_1) erfasst wird, das Model gefittet wird und im Anschluss erneut die Zeit ermittelt wird und time_1 subtrahiert wird. Das ergenis entspricht dann time_2. Die 120%ige repräsentative Laufzeit wird ermittelt, indem der erhaltene Wert bei: @my_logger @my_timer def logmodelFit(): return logmodel.fit(X_train,y_train) logmodelFit() **Mit dem Ergebnis: logmodelFit ran in: 0.031914472579956055 sec mit dem Faktor 1,2 multipliziert wird. Im vorliegenden Ergebnis liegt die Laufzeit der Trainingsfunktion 0.03780817985534668 *unter der Grenzwert der repräsentativen Lautzeit bei 0.0637061119079589

**Das folgende Bild zeigt, was auf dem Notebook zusehen ist, wenn testdatenfile_1.txt verwendet wird:
