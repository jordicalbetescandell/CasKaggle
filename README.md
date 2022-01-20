# Cas-Kaggle
Anàlisi de dades exhaustiu, amb el dataset :https://www.kaggle.com/gloseto/traffic-driving-style-road-surface-condition	

# Pràctica Kaggle APC UAB 2021-22
### Nom: Jordi Calbet Escandell
### DATASET: Traffic, Driving Style and Road Surface Condition
### URL: [kaggle](https://www.kaggle.com/gloseto/traffic-driving-style-road-surface-condition)
## Resum
El dataset conté paàmetres adquirits de l'automòbil Opel Corsa 1.3 HDi (95 CV) com ara el fluxe de massa d'aire, la vaariació d'altitud o la carga del motor, a través de les quals calculam la superfície de la carretera,  el trànsit i l'estil de conducció.
Tenim 7392 dades amb 17 atributs.
### Objectius del dataset
Volem crear un classificador bo per determinar la superficie de la carretera donades unes certes característiques.
## Experiments
Primer vàrem aplicar un preprocessat bàsic i vam generar els models i després, vam aplicar hyperparameter tunning pels millors models per veure si érem capaços de millorar el accuracy. Després vam tornar al preprocessament per trobar quina configuració era l'òptima per la nostra base de dades i vam tornar a crear els models.
### Preprocessat
Per preparar el dataset, hem codificat la superfície de la carretera, eliminat el trànsit i l'estil de conducció, omplert els NA amb -1 i estandarditzant les dades. Amb aquest preprocessament és amb el que hem aconseguit els millors resultats.
### Model
| Model | Hiperparametres | Mètrica | Temps |
| -- | -- | -- | -- |
| OneVsOneClassifier | LogisticRegression() | 98.9% | 0.037s |
| OneVsRestClassifier | LogisticRegression() | 98.9% | 0.039s |
| OutputCodeClassifier | LogisticRegression() | 98.9% | 0.072s |
| KNeighborsClassifier | n_neighbors=45 | 99.4% | 0.0388s |
| KNeighborsClassifier | n_neighbors=45, weights="distance" | 99.4% | 0.058s |
| DecisionTreeClassifier | criterion= 'entropy', max_depth= None, max_features= 14, min_samples_leaf= 61, splitter= 'best' | 99.8% | 29.039s |
| RandomForestClassifier | criterion= 'entropy', max_depth= 10, max_features= 'sqrt', n_estimators= 1000 | 100% | 344.610s |
| Stacked | Model creat a partir del DecisionTreeClassifier, RandomForestClassifier i RandomForestClassifier amb Grid Serch| 99.9% | 30.695s |
## Conclusions
El millor model basant-nos amb l'accuracy és el RandomForestClassifier però té un temps molt elevat, en canvi, els altres models també tenen un accuracy molt elevat, tot per dalt del 98%, i la gran majoria amb un temps inferior a 0.1s.
