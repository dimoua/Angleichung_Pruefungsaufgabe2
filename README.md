# Prüfungsaufgabe2: Logging und Input-Output Unit Test Ansatz auf Machine Learning basierter Software Systeme:die Funktionen werden auf das Decision-Tree Projekt implementiert.



[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/dimoua/Angleichung_Pruefungsaufgabe2.git/HEAD)

Quellen: Unit Testing & Logging: https://towardsdatascience.com/unit-testing-and-logging-for-data-science-d7fb8fd5d217 Decision-Tree: Udemy Kurs - Python für Data Science, Machine Learning & Visualization

## Funktionsausführung
Nach der Aufruf der Binder badge, bitte auf der Notebook Prüfungsaufgabe2_Decision_Tree.ipynb klicken. Restart der Kernel und Run das gesamte Notebook, damit alle Bibliotheken aufgeladen werden und das gesamte Programm ausgeführt wird.

Analog zu der ausgeführte Programm in der Artikel, werden die Funktionen my_logger und my_timer hinzugefügt: from functools import wraps def my_logger(orig_func): import logging logging.basicConfig(filename='{}.log'.format(orig_func.name), level=logging.INFO)

<img width="351" alt="2022-08-03 23_45_53-3-Aufgabe2_D… (auto-d) - JupyterLab" src="https://user-images.githubusercontent.com/62958158/182718616-1369bc6d-33a7-4db9-bf3b-0ad719c7acf5.png">


Anwendung von my_logger und my_timer auf ausgewählte Funktionen.

### Die erste Funktion ist die Fit-Funktion aus der Decision-Tree Projekt

 @my_logger
  @my_timer
   def modelruntime(): 
     return dtree.fit(X_train,y_train)
        modelruntime()

<img width="261" alt="Training Funktion" src="https://user-images.githubusercontent.com/62958158/184456441-60f3f29a-aa52-4245-9574-c35e4dc896ad.png">

**Nach Ausführung wird folgenden Ergebnis angezeigt: 

### modelruntime ran in: 0.10902047157287598 sec


### Die Zweite Funktion wird auf die Predict Funktion angewendet

@my_logger
@my_timer
def dt_predict():
    return dtree.predict(X_test)
predict = dt_predict()


<img width="276" alt="Predict Funktion" src="https://user-images.githubusercontent.com/62958158/184456468-9e7276cd-0df0-41f7-a234-de03da349d5d.png">


**Nach Ausführung wird folgenden Ergebnis angezeigt: 

### dt_predict ran in: 0.0033729076385498047 sec

**Zum Zweck Protokollierung wird ein modelruntime.log automatisch für die Funktion mylogger erzeugt. Der Log-Datei steht auch in dem Ordner zur Verfügung.


#Testfälle 1 und 2

**Für den Test Fall 1 wird einen CSV Test Datei dummy_data.csv erzeugt. Während der Testfall wird diese Datei mit den Daten aus der bereinigten CSV-Datei der Übung ausgefüllt und mithilfe der Funktion read_csv () auf das Pandas Bibliothek angewendet bzw. ausgelesen. Bei der Verwendung von dieser Datei wird der Unittest Funktion über die Behauptung, dass self.actual_score == testdata_score richtig dargestellt. Das ist eine Bestätigung, dass die Vorhersage Funktion erfolgreich funktioniert wie auf das unten stehende Bild.

<img width="341" alt="Testfall1" src="https://user-images.githubusercontent.com/62958158/184445974-68ea9eb1-8a8e-4155-a247-9aa41dcf7176.png">

Mit dem Testfall 2 geht es darum zu überprüfen, ob die Trainingsfunktion die 120%-Grenze der repräsentativen Laufzeit überschreitet. Es wird erst mal die Laufzeit der Trainingsfunktion übermittelt.<img width="282" alt="Decision Tree Classifier Laufzeit" src="https://user-images.githubusercontent.com/62958158/184459914-c80083ca-5c10-4905-ab87-f29b446b67de.png">

<img width="282" alt="Decision Tree Classifier Laufzeit" src="https://user-images.githubusercontent.com/62958158/184459914-c80083ca-5c10-4905-ab87-f29b446b67de.png">

 **Mit dem Ergebnis: logmodelFit ran in: 0.031914472579956055 sec mit dem Faktor 1,2 multipliziert wird. Im vorliegenden Ergebnis liegt die Laufzeit der Trainingsfunktion 0.03780817985534668 *unter der Grenzwert der repräsentativen Lautzeit bei 0.0637061119079589


Für Testfall 2 wird überprüft, ob die Laufzeit der Trainingsfunktion, die 120%-Grenze der repräsentativen Laufzeit überschreitet. time_1=time.time() logmodel_test.fit(X_train,y_train) self.time_2 = time.time() - time_1 Durch Ausführen der oben gezeigten Zeilen, wird im Notebook die Laufzeit für die Trainingsfunktion ermittelt, in dem die aktuelle Zeit (time_1) erfasst wird, das Model gefittet wird und im Anschluss erneut die Zeit ermittelt wird und time_1 subtrahiert wird. Das ergenis entspricht dann time_2. Die 120%ige repräsentative Laufzeit wird ermittelt, indem der erhaltene Wert bei: @my_logger @my_timer def logmodelFit(): return logmodel.fit(X_train,y_train) logmodelFit() **Mit dem Ergebnis: logmodelFit ran in: 0.031914472579956055 sec mit dem Faktor 1,2 multipliziert wird. Im vorliegenden Ergebnis liegt die Laufzeit der Trainingsfunktion 0.03780817985534668 *unter der Grenzwert der repräsentativen Lautzeit bei 0.0637061119079589

**Das folgende Bild zeigt, was auf dem Notebook zusehen ist:

<img width="396" alt="Testfall2" src="https://user-images.githubusercontent.com/62958158/184446193-7d9f25b8-8aa2-4db9-8a0b-c4673d3351df.png">
