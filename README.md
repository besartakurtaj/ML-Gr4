<table border="0">
 <tr>
    <td style="width:300px; vertical-align:middle; text-align:center;">
      <img src="https://upload.wikimedia.org/wikipedia/commons/e/e1/University_of_Prishtina_logo.svg" 
           alt="University Logo" 
           style="width:250px; height:auto;" />
    </td>
    <td style="vertical-align:middle; padding-left:20px;">
      <h2><strong>Universiteti i Prishtinës</strong></h2>
      <h3>Fakulteti i Inxhinierisë Elektrike dhe Kompjuterike</h3>
      <p>Inxhinieri Kompjuterike dhe Softuerike - Programi Master</p>
      <p><strong>Profesoreshë:</strong> Prof.Dr. Lule AHMEDI</p>
      <p><strong>Profesor:</strong> Dr.Sc. Mërgim H. HOTI</p>
    </td>
 </tr>
</table>

# Zhvillimi i modelit për parashikimin e performancës së bankave në Kosovë

## Faza I: Përgatitja e modelit

### Përshkrimi i detyrave
Gjatë Fazës I, detyrat kryesore kanë përfshirë:  
- Mbledhjen e të dhënave nga burime të ndryshme online për bankat që operojnë në Kosovë.  
- Përpunimin dhe normalizimin e të dhënave në një format të përbashkët për analizë dhe modelim.  

### Burimet e të dhënave
Të dhënat janë mbledhur përmes **web scraping** nga raportet financiare të bankave:  

- **Raiffeisen Bank:** [Link](https://www.raiffeisen-kosovo.com/sq/rreth-nesh/raporte-dhe-njoftime/pasqyrat-financiare.html)  
- **Teb Kosova:** [Link](https://teb-kos.com/raportet-financiare/)  
- **NLB:** [Link](https://www.nlb-kos.com/sq/per-banken/raportet-vjetore?page=1)  
- **Pro Credit Bank:** [Link](https://www.procreditbank-kos.com/shq/per-ne/publikimet-financiare/raportet-tremujore/)  
- **Banka Ekonomike:** [Link](https://bekonomike.com/sq/Bilanci-i-Gjendjes)  
- **Credins Bank:** [Link](https://bankacredins-ks.com/kush-jemi/raporte-dhe-njoftime/raporte-vjetore/#)  
- **Pri Bank:** [Link](https://pribank-ks.com/individual/about-us?form=6)  
- **Ziraat Bank:** [Link](https://www.ziraatbank-kosova.com/sq/pasqyrat-financiare)  

### Përshkrimi i datasetit
Dataset-i përmban të dhëna të strukturuara për çdo bankë, duke përfshirë të ardhurat, shpenzimet, dhe të dhëna të tjera financiare.  

- **Numri i rreshtave:** 9527  
- **Numri i kolonave:** 15  
- **Kolonat kryesore:** `DATA_SOURCE`, `FILE_NAME`, `BANK_ID`, `DT_REPORT`, `CURRENT_VALUE`, `PREVIOUS_VALUE`, `YEAR`, `QUARTER`  
- **Datatype-et e kolonave:**

| Kolona               | Tipi i të dhënave       |
|---------------------|------------------------|
| DATA_SOURCE          | object                 |
| FILE_NAME            | object                 |
| BANK_ID              | int64                  |
| DT_REPORT            | datetime64[ns]         |
| EXTRACTION_DATE      | datetime64[ns]         |
| STATEMENT_TYPE       | object                 |
| CATEGORY_TYPE        | object                 |
| ORIGINAL_CATEGORY    | object                 |
| CATEGORY_CODE        | Int64                  |
| CURRENT_VALUE        | float64                |
| PREVIOUS_VALUE       | float64                |
| CATEGORY_TYPE_NUM    | int64                  |
| REPORT_DATE          | datetime64[ns]         |
| YEAR                 | Int64                  |
| QUARTER              | Int64                  |

### Rezultatet e Fazës I
- Të dhënat janë të organizuara sipas bankave dhe periudhave vjetore/trimestrale.  
- Janë identifikuar kategoritë kryesore financiare për modelin e parashikimit të performancës së bankave.

![image alt](https://github.com/besartakurtaj/ML-Gr4/blob/d0d5a5d8c11930d9a42756d3a1a625b8d58bb805/Screenshot%202026-03-21%20at%2023.02.45.png)

## Mapping i kategorive financiare

Këto janë kodet që përdoren për kategorizimin e të dhënave të nxjerra nga raportet e bankave:

**Të ardhurat dhe fitimet:**
- 'Të hyrat nga interesi': 1  
- 'Shpenzimet e interesit': 2  
- 'Neto të hyrat nga interesi': 3  
- 'Të hyrat nga tarifat dhe komisionet': 4  
- 'Shpenzimet e tarifave dhe komisioneve': 5  
- 'Neto të hyrat nga tarifat dhe komisionet': 6  
- 'Neto të hyrat nga tregtimi me valuta të huaja': 7  
- 'Neto të hyrat nga tregtimi': 7  
- 'Neto të hyrat nga instrumentet tjera financiare': 8  
- 'Neto të hyrat (shpenzimet) tjera operative': 9  
- 'Gjithsej të hyrat': 10  
- 'Provizionet për humbjet nga kreditë': 11  
- 'Provizione të tjera': 13  
- 'Fitimi (humbja) para tatimit': 14  
- 'Shpenzimet e tatimit në fitim': 15  
- 'Fitimi (humbja) neto': 16  
- 'Të ardhurat tjera gjithëpërfshirëse': 17  
- 'Gjithsej të ardhurat gjithëpërfshirëse': 19  

**Pasuritë dhe detyrimet:**
- "Paraja e gatshme dhe gjendja me BQK-në": 20  
- "Kërkesat ndaj bankave": 21  
- "Bonot e thesarit": 22  
- "Investimet në letra me vlerë": 23  
- "Mjetet jo qarkulluese të mbajtura për shitje": 24  
- "Kapitali aksionar": 38  
- "Rezervat e kapitalit": 40  
- "Fitimi i mbajtur/(humbja) nga vitet paraprake": 41  
- "Fitimi/(humbja) e vitit aktual": 42  
- "Përbërësit tjerë të ekuitetit": 43  
- "Gjithsej ekuiteti i aksionarëve": 44  
- "Gjithsej detyrimet dhe ekuiteti i aksionarëve": 45  

**Borxhet dhe detyrimet tjera (33-37):**
- "Detyrimet ndaj bankave", "Borgjet afatgjata", "Borxhet afatgjata", "Borxhet afatshkurtera", etj.: 33  
- "Fondet tjera të huazuara": 34  
- "Detyrimet tatimore të shtyra": 35  
- "Detyrimet tjera": 36  
- "Gjithsej detyrimet": 37  

Ky mapping e bën datasetin të qartë për analizat dhe përgatitjen e modelit të parashikimit.  


## Faza II: Ndërtimi dhe trajnimi i modelit

### Përshkrimi i detyrave
Gjatë Fazës II, detyrat kryesore kanë përfshirë:
- Përpunimin e të dhënave në formatin e duhur për modelim (pivot).
- Feature engineering për të krijuar variabla të reja.
- Trajnimin e tre algoritmeve të ndryshme të Machine Learning (supervised learning algorithms).
- Vlerësimin e performancës së modeleve dhe parashikimin e fitimit neto për tremujorin e ardhshëm.

### Përgatitja e të dhënave (Pivot)
Të dhënat janë transformuar nga formati i gjatë (long format) në formatin e gjerë (wide format), ku çdo rresht përfaqëson një bankë dhe periudhë të vetme, dhe çdo kolonë përfaqëson një metrikë financiare.

- **Dimensionet pas pivot:** 267 rreshta × 65 kolona

### Inxhinieria e veçorive (Feature Engineering)
Janë krijuar variablat e mëposhtëm për të përmirësuar fuqinë parashikuese të modelit:

| Veçoria | Përshkrimi |
|---|---|
| `16_lag1`, `16_lag2`, `16_lag4` | Fitimi neto i 1, 2 dhe 4 tremujorëve të mëparshëm |
| `16_roll4_mean` | Mesatarja lëvizëse e 4 tremujorëve të fundit |
| `1_lag1`, `3_lag1`, `6_lag1`, `10_lag1`, `14_lag1` | Lag-1 i metrikave kryesore të ardhurash |
| `16_qoq_growth` | Rritja tremujore e fitimit neto (%) |
| `profit_margin_lag1` | Marzhi i fitimit të tremujorëve të mëparshëm |
| `provision_burden_lag1` | Raporti i provizioneve ndaj të ardhurave totale |
| `quarter_sin`, `quarter_cos` | Kodimi ciklik i tremujorit |
| `year_feature` | Viti si veçori numerike |
| `bank_quarters` | Numri kumulativ i tremujorëve raportues për çdo bankë |

**Variabla target:** Fitimi neto i tremujorëve të ardhshëm (`next_net_profit` = kolona 16 e zhvendosur me -1).

### Algoritmet e përdorura
Janë trajnuar tre algoritme të ndryshme të mësimit të mbikëqyrur (supervised learning):

**1. XGBoost (Extreme Gradient Boosting)**
- `n_estimators=300`, `max_depth=3`, `learning_rate=0.05`
- Shumë i përshtatshëm për të dhëna financiare me marrëdhënie jo-lineare

**2. Random Forest**
- `n_estimators=300`, `max_depth=5`, `min_samples_leaf=3`
- Stabil dhe rezistent ndaj overfitting-ut në dataset të vogla

**3. LightGBM**
- `n_estimators=300`, `max_depth=3`, `learning_rate=0.05`
- I ngjashëm me XGBoost por më i shpejtë dhe shpesh më i saktë


### Rezultatet e modeleve

| Modeli | MAE | RMSE | R² (Fold 5) |
|---|---|---|---|
| XGBoost | ~3,569 | ~5,304 | 0.804 |
| Random Forest | ~3,387 | ~5,607 | 0.780 |
| LightGBM | ~3,249 | ~5,072 | 0.820 |

> **Fold 5 është më i rëndësishmi** pasi modeli trajnohet në 100% të të dhënave historike — saktësisht si në skenarin real të parashikimit.

### Parashikimet për tremujorin e ardhshëm
Për çdo bankë, rreshti i fundit i disponueshëm (tremujori aktual) është përdorur si input për të parashikuar fitimin neto të tremujorëve të ardhshëm.

### Vizualizimi
Është krijuar grafiku krahasues i fitimit neto aktual (Q4 2025) me parashikimin e modelit (Q1 2026) për secilën bankë.

![image alt](https://github.com/besartakurtaj/ML-Gr4/blob/main/Screenshot%202026-04-19%20at%2019.59.35.png)

Grafiku i fitimit neto (Q4 2024) me vlerat (Q1 2025) për krahasim.

![image alt](https://github.com/besartakurtaj/ML-Gr4/blob/main/Screenshot%202026-04-19%20at%2020.08.57.png)

### Grupimi i bankave (K-Means Clustering + PCA)

Përveç modeleve të parashikimit, është aplikuar edhe **K-Means Clustering** — 
një algoritëm i mësimit të pambikëqyrur (unsupervised learning) — për të 
grupuar bankat bazuar në profilet e tyre financiare.

**Metodologjia:**
- Janë përdorur 43 metrika financiare nga tremujori i fundit i disponueshëm për çdo bankë.
- Të dhënat janë normalizuar me StandardScaler.
- Dimensionet janë reduktuar në 2D me **PCA** për vizualizim.
- Algoritmi ka identifikuar **3 klasterë** natyrorë.

**Rezultatet:**

| Klasteri | Bankat | Karakteristika |
|---|---|---|
| Cluster 1 | Raiffeisen Kosovo | Bankë e madhe, profil financiar krejtësisht i ndryshëm nga të tjerat |
| Cluster 2 | TEB Kosovo, NLB Bank, ProCredit Bank, Banka Ekonomike | Banka të mesme me profile të ngjashme financiare |
| Cluster 3 | PriBank, Ziraat Bank | Banka të vogla me volume të ulëta të ardhurash dhe fitimi |

**Çfarë tregon ky analizë:**  
Algoritmi, pa asnjë informacion paraprak për madhësinë apo pozicionin e 
bankave në treg, zbuloi në mënyrë të pavarur grupime që përputhen saktësisht 
me realitetin e tregut bankar në Kosovë.

![image alt](https://github.com/besartakurtaj/ML-Gr4/blob/main/Screenshot%202026-04-19%20at%2020.18.55.png)

## Faza III: Analiza dhe Evaluimi (Ritrajnimi)

### Përshkrimi i detyrave
Gjatë Fazës III, detyrat kryesore kanë përfshirë:
- Optimizimi i parametrave të modeleve për të përmirësuar performancën.
- Ritrajnimi i modeleve me parametra të optimizuar.
- Krahasimi i rezultateve para dhe pas optimizimit.
- Analiza e përmirësimeve të arritura në metrikat e evaluimit.

### Optimizimi i modeleve
Pas analizës fillestare, janë bërë rregullime në parametrat e secilit model për të reduktuar gabimin dhe për të rritur saktësinë e parashikimeve.

#### Ndryshimet kryesore:
- **XGBoost:** Shtimi i early_stopping_rounds për të parandaluar overfitting-un dhe rregullimi i parametrave të regularizimit.
- **Random Forest:** Rritja e numrit të pemëve (n_estimators=500) dhe thellësia maksimale (max_depth=7).
- **LightGBM:** Optimizimi i parametrave të regularizimit dhe strukturës së pemëve.

### Krahasimi i rezultateve

#### Rezultatet para optimizimit (Fold 5)

| Modeli | MAE | RMSE | R² |
|---|---|---|---|
| XGBoost | ~3,569 | ~5,304 | 0.804 |
| Random Forest | ~3,387 | ~5,607 | 0.780 |
| LightGBM | ~3,249 | ~5,072 | 0.820 |

#### Rezultatet pas optimizimit (Fold 5)

| Modeli | MAE | RMSE | R² |
|---|---|---|---|
| XGBoost | 1,953 | 2,723 | 0.872 |
| Random Forest | 2,470 | 3,279 | 0.814 |
| LightGBM | 2,282 | 3,011 | 0.843 |

### Përmirësimet e arritura

| Modeli | R² para optimizimit | R² pas optimizimit | Përmirësimi |
|---|---|---|---|
| XGBoost | 0.804 | 0.872 | ↑ 0.068 |
| Random Forest | 0.780 | 0.814 | ↑ 0.034 |
| LightGBM | 0.820 | 0.843 | ↑ 0.023 |

### Diskutime rreth rezultateve

#### Performanca e modeleve
Optimizimi i parametrave ka sjellë përpjekje të thelbësishme në performancën e të tre modeleve:

- **XGBoost** tregoi përmirësimin më të madh me rritje të R² nga 0.804 në 0.872 (↑ 8.5%), dhe zvogëlim të MAE-it nga 3,569 në 1,953 (↓ 45.3%). Ky model është përfaqësuesi më i mirë për këtë detyrë.
  
- **LightGBM** ruajti pozicionin e dytë me R² 0.843, pasi ishte tashmë në performancë të lartë, por prapasëpari u optimizua më tej.

- **Random Forest**, megjithëse tregoi përmirësim (R² 0.814), mbeti më pas në krahasim me dy algoritmet e bazuara në boosting. Kjo mund të jetë për shkak të natyres të ndryshme të më-këqyrjes dhe të pamundësisë për të kapur marrëdhëniet jo-lineare aq mirë sa gradient boosting.

#### Stabilitet dhe generalizim
Ndryshimet në parametra kanë reduktuar overfitting-un duke përmirësuar aftësinë e modeleve për të përgjithësuar në të dhëna të ardhshme. Early stopping në XGBoost dhe optimizimi i regularizimit në LightGBM ishin çelësat në këtë përmirësim.

#### Vërejtje mbi K-Means Clustering
Grupimi i bankave nxjerr në pah struktura natyrale të tregut bankar Kosovar, duke ndarë bankat në tre kategori të qarta bazuar në profilimet e tyre financiare. Kjo klasifikim është i vlefshëm për strategjitë e segmentimit të tregut.

### Kontributi i projektit në krahasim me punën paraprake

Ky projekt ofron disa inovacione të rëndësishme:

1. **Automatizimi i mbledhjes së të dhënave**: Përmes web scraping-ut, mbledhja e të dhënave financiare është bërë më i shpejtë dhe më i besueshëm sesa mbledhja manuale.

2. **Modelim i saktë i parashikimit**: Tre algoritme të ndryshme janë testuar dhe optimizuar për të dhënat financiare të Kosovës, duke ofruar një nivel të lartë saktësie.

3. **Segmentimi i tregut bankar**: Aplikimi i K-Means Clustering ka zbuluar strukturën natyrore të tregut pa nevojë për klasifikim paraprak.

4. **Feature engineering i drejtuar financiarisht**: Veçoritë e krijuara (lag variables, moving averages, profit margins) janë të orientuara nga domeni financiar dhe ndihmojnë modelimet.

5. **Evaluimi rigoroz i modeleve**: Përdorimi i k-fold cross-validation siguron që rezultatet nuk janë të përmbysura nga të dhënat specifike të trajnimit.

### Rezultatet përfundimtare të tre fazave: Krahasim global

| Aspekti | Faza I | Faza II | Faza III |
|---|---|---|---|
| **Të dhëna të disponueshme** | 9,527 rreshta | 267 rreshta (pivotuar) | E njëjtë + optimizuar |
| **Algoritmet** | - | 3 (XGBoost, RF, LightGBM) | 3 (optimizuar) |
| **R² mesatar (Fold 5)** | - | 0.801 | 0.843 |
| **MAE mesatar** | - | ~3,402 | ~2,235 |
| **Përmirësim përfundimtar** | - | Baseline | ↑ 5.25% (R²), ↓ 34.3% (MAE) |

## Interpretim i rezultateve: Si të lexohen ato?

### Për investitorët dhe menaxherët e bankave:

1. **Parashikimet tremujore të fitimit neto** ofrojnë një ide të qartë mbi performancën e pritshme financiare për periudhën e ardhshme. Kjo ndihmon në planifikimin buxhetor dhe alokimin e resurseve.

2. **Vlerat R² 0.87+ tregojnë se modeli mund të shpjegojë 87% të ndryshueshmërisë në fitim neto**, që është shumë i lartë për të dhëna të botës reale. Mbetja e 13% është për shkak të faktorëve të paardhshëm (ndryshime në politikë, kushtet e tregut global, etj).

3. **MAE i ulët (≈2,000)** në krahasim me vlerat e fitimit neto (të cilat variojnë nga 100,000 në dhjetëra miliarda) tregon saktësi të lartë relative.

### Për analistët financiarë:

1. **Segmentimi i tre klasterëve** ndihmon në identifikimin e bankave të ngjashme dhe në krahasimin e benchmarks brenda secilës kategori.

2. **Variablat lag** të fitimit neto tregojnë se performanca e kaluar është shumë përplot për performancën e ardhshme — kjo validohet nga korelacionet e larta në modelim.

3. **Marginalet e fitimit dhe buxheti i provizioneve** janë variabla krejtësisht të rëndësishme në parashikimin e fitimit neto.

### Për vendimmarrësit në institucionet rregullatore:

1. **Modeli mund të përdoret për monitorimin e shëndetit financiar të bankave** dhe identifikimin e bankave me rrezik më të lartë (duke parë parashikimet negative).

2. **K-Means clustering-u** ofron një mje për grupimin e bankave sipas profilit të rrezikut dhe përvojës.

## Kush përfiton dhe si?

### 1. **Bankat** → Menaxhim më i mirë finansiar
- Parashikimet e saktë të fitimit neto ndihmojnë në vendimmarrje strategjike
- Identifikimi i faktorëve kritikë të performancës
- Planifikimi më i mirë i kapitalit dhe likuiditetit

### 2. **Investitorët dhe aksionarët** → Investime më të informuara
- Parashikimet mund të përdoren për të vlerësuar vlerën e aksioneve
- Identifikimi i bankave me perspektiva të mira rritjeje
- Minimizimi i rrezikut përmes parashikimit të dështimit potencial

### 3. **Rregullatorët (BQK-ja)** → Monitorim më i mirë i tregut
- Detektimi i bankave me probleme para kohe
- Vlerësimi i stabilitetit makroekonomik të sektorit
- Informim i politikave rregullatore

### 4. **Konkurrentët** → Zgjim i tregut
- Krahasimi i pozicionit të tyre me konkurentët bazuar në të dhëna objektive
- Identifikimi i dobësive dhe forcave relative

### 5. **Academic Research** → Bazë për kërkime të mëtejshme
- Dataset i përsosur për qëllime kërkimore
- Metodologi e validuar për modelim financiar
- Bazë për studime më komplekse të sektorit bankar

## Konkluzione

### Përfundimet kryesore:

1. **Modelimi i grumbullimit të të dhënave financiare është i mundshëm dhe i përdorshëm** për parashikimin e performancës së bankave. Saktësia e arritur (R² ≈ 0.87) validohet këtë qasje.

2. **XGBoost është algoritmi më i mirë për këtë detyrë**, duke ofruar balancën më të mirë midis saktësisë dhe shpejtësisë.

3. **Të dhënat financiare të kalimeve kanë fuqi parashikuese të mjaftueshme** — nuk nevojiten faktorë të jashtëm (makroekonomikë, tregje globale) për të arritur R² të lartë, megjithëse këta faktorë do të përmirësonin modelin më tej.

4. **Segmentimi natyral i tregut bankar në tre klasterë** pasqyron realitetin e përqasur dhe mund të përdoret për analizat e mëtejshme strategjike.

5. **Optimizimi i parametrave u bë i domosdoshëm dhe u mundësoi përmirësim të konsiderueshëm** — algoritmet me parametra standard kanë gjasa të përmbysjen ose të nënvlerësojnë të dhënat.

## Perspektiva të ardhshme dhe rekomandime

### Përmirësimet e mundshme:

1. **Përfshirja e faktorëve makroekonomikë**
   - Norma të interesit të ECB-s dhe BQK-s
   - Indeksa të bursave të Ballkanit
   - Të dhëna rreth GDP-s dhe inflacionit të Kosovës
   - Këto faktorë do të rrisin R² dhe do të përmirësojnë parashikimet në periudha me ndryshime të mëdha ekonomike

2. **Modelim sezonar më i avancuar**
   - Përdorimi i ARIMA ose SARIMA për të kapur sezonalitetin më mirë
   - Kombinimi i modeleve të serive kohore me machine learning

3. **Deep Learning (LSTM, GRU)**
   - Rrjete neurale të recurruese mund të kapin marrëdhëniet komplekse të serive kohore
   - Këto modele janë më të përshtatshme për të dhëna me varësi kohore të gjata

4. **Modelim i veçantë për çdo bankë**
   - Në vend të modelit global, trajnimit i modeleve të veçanta për çdo bankë ose klasteri
   - Kjo mund të përmirësojë saktësinë për banka specifike

5. **Integrimi i të dhënave të mëtejshme**
   - Burimet alernative të të dhënave (rreporte të mediave, sentiment analysis)
   - Të dhëna mbi ndryshimet në menaxhim ose strategjitë e biznesit

6. **Modeli i kërkesës për kredi**
   - Modelimi i paralajmërimit të kërkesës për kredi mund të ndihmohet bankat në planifikimin e likuiditetit
   - Kombinimi i parashikimit të fitimit neto me kërkesën për kredi ofron një pamje më të plotë

7. **Analiza e rrezikut dhe stres-testi**
   - Përdorimi i modeleve për skenarioanaliza dhe stres-teste
   - Vlerësimi se si bankat do të performonin nën skenario të ndryshme ekonomike (p.sh., rënie ekonomike, kriza likuiditeti)

### Rekomandime për implementim:

1. **Shpërndarje në një platformë web** për qasje të lehtë të modeleve dhe parashikimeve
2. **Automatizim i plotë i mbledhjes dhe përpunimit të të dhënave** në bazë tremujore
3. **Dashboard-e interaktive** për vizualizimin e parashikimeve dhe trendeve
4. **Monitorim i modeleve** dhe ri-trajnim periodik kur merren të dhëna të reja

## Authors
- *Besarta Kurtaj*
- *Fjolla Gjikolli*
- *Melos Ymeri*
