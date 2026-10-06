Telco Customer Churn Prediction

Acest proiect analizeaza datele clientilor unei companii de telecomunicatii si construieste modele de machine learning pentru a estima daca un client va renunta la servicii.

## Project objective

Am comparat **Logistic Regression** si **Random Forest** cu un model de referinta `DummyClassifier`. Deoarece este mai costisitor sa nu identificam un client care urmeaza sa plece, am folosit **recall-ul clasei Churn** drept criteriu principal pentru alegerea modelului final.

## Dataset

Setul de date Telco Customer Churn contine **7.043 de clienti si 21 de coloane**. Aproximativ **26,54%** dintre clienti au renuntat la servicii.

Datele sunt incarcate direct dintr-o sursa publica IBM, astfel incat notebook-ul poate fi rulat fara incarcarea manuala a unui fisier CSV.

## Workflow

- explorarea si vizualizarea datelor;
- identificarea valorilor lipsa si curatarea coloanei `TotalCharges`;
- transformarea coloanelor categorice si standardizarea celor numerice;
- crearea caracteristicilor `tenure_group` si `number_of_services`;
- impartirea datelor in seturi de antrenare si testare;
- compararea cu un baseline;
- antrenarea modelelor Logistic Regression si Random Forest;
- evaluarea prin confusion matrix, accuracy, precision, recall, F1 si ROC-AUC;
- compararea variantelor cu si fara echilibrarea claselor si feature engineering;
- segmentarea clientilor cu K-Means si compararea ratei de churn dintre clustere.

## Results

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Dummy Classifier | 0.7342 | 0.0000 | 0.0000 | 0.0000 | 0.5000 |
| Logistic Regression | 0.7271 | 0.4917 | **0.7941** | 0.6074 | 0.8337 |
| Random Forest | 0.7491 | 0.5186 | 0.7834 | **0.6241** | **0.8369** |

Logistic Regression a identificat aproximativ **79% dintre clientii care au plecat** si a obtinut cel mai bun recall. Random Forest a produs mai putine alarme false si rezultate generale usor mai echilibrate.

Am ales **Logistic Regression** ca model final deoarece rezultatul sau este cel mai bine aliniat cu obiectivul proiectului: identificarea unui numar cat mai mare de clienti care risca sa plece.

## Additional experiments

Echilibrarea claselor a crescut recall-ul Logistic Regression de la **53,18%** la **79,93%** in cross-validation. Caracteristicile create prin feature engineering au produs imbunatatiri mici, dar constante pentru toate metricile Random Forest.

## Customer segmentation with K-Means

Am folosit K-Means pentru a grupa clientii dupa vechime, costuri si numarul de servicii utilizate. Variabila `Churn` nu a fost folosita pentru formarea clusterelor, ci doar pentru analiza ulterioara a grupurilor obtinute.

| Cluster | Number of customers | Average tenure | Average monthly charges | Average services | Churn rate |
|---|---:|---:|---:|---:|---:|
| 0 | 2.500 | 54,49 luni | 90,27 | 5,52 | 17,72% |
| 1 | 4.532 | 20,25 luni | 50,75 | 2,17 | 31,47% |

Clusterul 1, format din clienti mai noi si cu mai putine servicii, are o rata de churn cu aproximativ **14 puncte procentuale mai mare**. Clasificarea identifica individual clientii care risca sa plece, iar clustering-ul ajuta la descrierea profilului grupurilor care necesita mai multa atentie.

## Limitations

Datele provin de la o singura companie de telecomunicatii. Performanta modelului poate fi diferita pentru alti clienti, alte companii sau alte perioade, iar importanta caracteristicilor nu demonstreaza cauzalitatea.

## Notebook

[Open the complete project notebook](project01_ML_training_comparison.ipynb)

Notebook-ul contine codul, graficele, rezultatele si interpretarile complete.

## Technologies

Python, pandas, NumPy, Matplotlib, Seaborn si scikit-learn.
