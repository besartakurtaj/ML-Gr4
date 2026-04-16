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
      <p><strong>Profesoreshë:</strong> Prof.Dr. Lule Ahmedi</p>
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

## Authors
- *Besarta Kurtaj*
- *Fjolla Gjikolli*
- *Melos Ymeri*
