# 🏙️ Šalies miestų butų kainų analizė su Power BI & Python

## 📈 Apie projektą

Ober-Haus reguliariai skelbia mėnesio butų 1 m2 kainas ir sukaupė didelį duomenų kiekį. Toks kiekis leidžia daryti tikslesnę duomenų analizę įvairiais pjūviais.
Žinau nekilnojamo turto rinka ir ypatumus, todėl nusprendžiau panaudoti duomenų apdorojimo metodus ir pažiūrėti ar tie metodai aptiks neatskleistas sąsajas.
Nors pati duomenų struktūra nėra gyli, nėra duomenų apie realius pardavimus, kiekius, pirkėjus, pardavėjus ir panašiai, pamaniau kad dideliame duomenų kiekyje galimai slypi neištirti dėsningumai.

Faktiškai, duomenyse yra tik vienas rodmuo, tai 1 m2 kaina, išreikšta kaina NUO ir kaina IKI. 
Galima padaryti prielaidą, kad kaina atspindi pirkėjo ir pardavėjo konsensusą, o kainos kitimas  - to konsensuso paieškos kryptį.
Todėl į šį rodiklį ir buvo nukreiptas pagrindinis dėmėsis.
Taigi, pagrindinis tyrimo objektas – **kainų dinamikos vertinimas laike**, kainų sąsaja su ekonominiais rodikliais ir dėsningumų paieška.

**Tikslas:**  
Identifikuoti veiksmingus butų rinkos analizės indikatorius, įžvelgti jų tarpusavio koreliacijas ir įvertinti, kaip makroekonominiai veiksniai gali paveikti gyventojų nuomonę apie teisingą būsto kainą.
---
## 🛠️ Naudoti įrankiai

- **Power BI** – vizualizacijos, indikatoriai, skaičiavimai, koreliacijų grafikai
- **Python** – duomenų transformavimas, įkėlimas, skaičiavimai, apdorojimas
---

## 📊 Naudoti duomenų šaltiniai

- [Ober-Haus mėnesinės butų kainų ataskaitos](https://www.ober-haus.lt/rinkos_apzvalgos/kainu-lenteles/)
  ![Dashboard Preview](ooh_1.png)
  
- Lietuvos statistikos departamentas
- Lietuvos Bankas
- EURIBOR duomenys
- 
## Naudoti mėtodai

🧹 1. Duomenų paruošimas
-	PDF lentelių ištraukimas su pdfplumber
-	Stulpelių konvertavimas 
-	Data normalizavimas į datetime 
________________________________________
🔁 2. Laiko eilutės transformacijos
-	Grupavimas 
-	Lag skaičiavimai: delta_lag1, MoM_lag1 – vėluojantys rodikliai (nuo praeito mėnesio)
________________________________________
📊 3. Regresinė analizė
-	Multiple Linear Regression su sklearn.linear_model.LinearRegression
o	Naudota:
	kainų rėžių dydis
	delta_MoM_%
	Infliacija, Euribor 3 mėn., darbo užmokėsčio kitimas
	Sintetinis rodiklis: Santykinis_skirtumas = vidutinė kaina / darbo užmokėsčio kitimas
•	StandardScaler – nepriklausomų kintamųjų standartizavimas 
________________________________________
📈 4. Statistinė analizė su statsmodels (OLS)
-	statsmodels.OLS (Ordinary Least Squares) modeliai:
-	Atskiras modelis su makro rodikliais
-	Atskiras modelis su delta + MoM
-	Pateikti rodikliai:
-	coef – koeficientai
-	R², Adj. R²
-	t, p-value – reikšmingumo testai
-	AIC, BIC – modelio kokybės kriterijai
________________________________________
📉 5. Modelio kokybės vertinimas
Naudotos šios metrikos:
-	R² – determinacijos koeficientas
-	MAE – vidutinė absoliuti paklaida
-	RMSE – šakninis vidutinis kvadratinis nuokrypis
-	MSE – vidutinis kvadratinis nuokrypis
________________________________________
🎨 6. Vizualizacijos
-	Scatter grafikai su:
-	Taškų dydžiu pagal kainų rėžių dydį
-	Spalvine temperatūra pagal MoM_lag1
-	Laiko eilučių grafikų interpretacijos:
-	Reali vs prognozuota kaina


## 📊 1 m2 buto kainų ir makroekonominių indikatorių sąsajos analizė

Naudoti indikatoriai:
•	3 mėn. EURIBOR
•	Infliacija
•	Šalies vidutinio darbo užmokėsčio prieaugis, %

## 🖼️ Vizualizacijos pavyzdžiai. 
      Galimi pjuviai pagal visus požymius: miestas, rajonas, buto tipas, kambarių skaičius.

### 📊 1. Koreliacija buto kainos ir Kainų režių dydžio indikatorio

![Dashboard Preview](ooh_2.png)
![Dashboard Preview](ooh_3.png)

---

### 📊 2. Infliacijos įtaka

![Dashboard Preview](ooh_4.png)

---

### 📊 3. Makroekonominiai rodikliai ir kainos kitimas


![Dashboard Preview](ooh_5.png)

---

## 🔍 Naudoti rodikliai

| Rodiklis                               | Aprašymas                                                              |
|----------------------------------------|------------------------------------------------------------------------|
| **Kainos vidurkis**                    | 1 m² buto vidutinė kaina, eurais                                       |
| **Kainos rėžių dydis (KR)**            | Skirtumas tarp mažiausios ir didžiausios butų kainos pagal kategoriją  |
| **MoM**                                | Mėnesinis vidutinės kainos pokytis (%)                                 |
| **Vidutinio darbo užmokesčio kitimas** | Skelbiamo darbo užmokėsčio kumuliatyvus pokytis (%)                    |

---

## 📌 Pagrindinės įžvalgos

- **Infliacija**: Sąlyginai nedidelė infliacijos įtaka kainai.

- **Kambarių skaičius**: Įtaka 1 m2 kainai nedidelė, bet šis rodiklis reikšmingai įtakoja **MoM indikatorių**. t.y. butai skirtingų kambarių skaičiaus "aktivuojasi" pardavimuose skirtingai.
    
- **Kainos rėžių dydžio indikatorius**: Parodė stiprią koreliaciją su kainos kitimu, gali indikuoti apie ateities kainų tendencijas.
  
- **MoM indikatorius**: Buto vidutinės kainos mėnesio kitimas procentais, gali indikuoti apie ateities kainų tendencijas.

---

## 🎯 Pagrindinis tikslas

Suprasti, **kaip rinkos dalyviai vertina teisingą buto kainą** ir kaip tai keičiasi laike.  
Kitaip tariant — **identifikuoti lūkesčius ir nuotaikas** per objektyvius ekonominius rodiklius.



📉 5. Modelio kokybės vertinimas
Naudotos šios metrikos:
•	R² – determinacijos koeficientas
•	MAE – vidutinė absoliuti paklaida
•	RMSE – šakninis vidutinis kvadratinis nuokrypis
•	MSE – vidutinis kvadratinis nuokrypis
________________________________________
🎨 6. Vizualizacijos
•	Scatter grafikai su:
o	Taškų dydžiu pagal kainų rėžių dydį
o	Spalvine temperatūra pagal MoM_lag1
•	Laiko eilučių grafikų interpretacijos:
o	Reali vs prognozuota kaina


## 📊 1 m2 buto kainų ir makroekonominių indikatorių sąsajos analizė

Naudoti indikatoriai:
•	3 mėn. EURIBOR
•	Infliacija
•	Šalies vidutinio darbo užmokėsčio prieaugis, %

📊 OLS regresijos rezultatas ir bendras modelio vertinimas:

|Rodiklis           	|Reikšmė	       |Paaiškinimas
|-----------------------|------------------|----------------------------------------------------------------------------------------------------|
|R-squared	            |   0.771     	 |Modelis paaiškina 77,1% kainos vidurkio kitimą.                                                     |
|Adj. R-squared	      |   0.771	       |Pataisytas R², atsižvelgiant į kintamųjų skaičių. Mažai skiriasi nuo R², visi kintamieji reikšmingi.|
|F-statistic / Prob(F)	|   5501, 0.000	 |Modelis statistiškai reikšmingas (p < 0.001).                                                       |
-------------------------------------------------------------------------------------------------------------------------------------------------

📉 Kintamųjų įtaka (coef + p-vertės) 


|Kintamasis	           |Koeficientas	|P reikšmė	 |Interpretacija                                                                                                                   |
|----------------------|------------------|------------|---------------------------------------------------------------------------------------------------------------------------------|
|Intercept (const)     | 1017.19      	|< 0.001	 |Kai visi prediktoriai = 0, vidutinė buto kaina būtų ~1017 € (be kitų faktorių).                                                  |
|price_delta	     |   +1.145	      |< 0.001 ✅  |Labai stipri įtaka: kainų rėžiams padidėjus 1 EUR, vidutinė kaina didėja apie 1.15 EUR. Tai pagrindinis prognozuojantis veiksnys.|
|Infliacija	           |   +0.59	      |  0.675 ❌  |Statistiškai nereikšminga, šioje regresijoje. Įtakos neturi (nėra koreliacijos su kaina).                                        |
|Kitimas (DU)          |  +10.01      	|< 0.001 ✅  |Darbo užmokesčio augimas 1% = kainos augimas apie 10 EUR – statistiškai reikšminga.                                              |
|Euribor3	           |  −14.55	      |  0.008 ✅  |Euribor didėjimas 1 p.p. = kainos mažėjimas apie 14.5 EUR.                                                                       |
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
________________________________________

![Dashboard Preview](Reali_vs_prognozuota.png)

## 📊 Nekilnojamo turto išvestinių indikatorių **Kainų rėžių dydis** + **Kainos vidurkio kitimas %** (delta + MoM) ir buto 1 m2 kainos vidurkio sąsajos analizė


|Rodiklis           	|Reikšmė	       |Paaiškinimas
|-----------------------|------------------|----------------------------------------------------------------------------------------------------|
|R-squared	            |   0.765     	 |Modelis paaiškina 76,5% kainos vidurkio kitimą.                                                     |
|Adj. R-squared	      |   0.765	       |Patvirtina R², atsižvelgiant į kintamųjų skaičių.                                                   |
|F-statistic / Prob(F)	|   10390, 0.000	 |Modelis statistiškai reikšmingas (p < 0.001).                                                       |
-------------------------------------------------------------------------------------------------------------------------------------------------
Observations: 6396, labai stiprus imties dydis = rezultatai patikimi.
________________________________________

🔍 Koeficientai


|Kintamasis	           |Koeficientas	|P > t reikšmė | Interpretacija                                                                                                                    |
|----------------------|------------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------|
|Intercept (const)     | 1143.01      	|< 0.001	   |Kai visi prediktoriai = 0, vidutinė buto kaina būtų ~1143 € / m2 (be kitų faktorių).                                               |
|price_delta	     |   +1.1503	      |< 0.001 ✅    |Stipri įtaka: kainų rėžiams padidėjus 1 EUR, vidutinė kaina didėja apie 1.15 EUR. Tai pagrindinis prognozuojantis veiksnys.        |
|delta_MoM-pct         |   -2.3291	      |  0.00  ✅    |Neigiamas poveikis:kai delta greitai keičiasi, trumpalaikiai spaudžia kainą žemin.                                                 |
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 ![Dashboard Preview](Delta_MoM.png)

 MoM dydis atvaizduotas spalvotai. Spalva kinta nuo žemo rodmens (mėlina) iki aušto (raudona). Taškų dydid rodo delta reikšmė: didesnis taškas reiškia delta (Kainos rėžių dydis) padidėjimą.
 Grafikas rodo, kaip dideli taškai signalizuoja apie kainos kilimą ir kaip sumažėję taškai signalizuoja apie kainos kilimo pabaigą. Gerai matosi delta ir MoM koreliacija.
________________________________________
🟠 Išvados:
--------------------------------------------------------------------------------------------------------------------------------------
- 	price_delta yra stiprus prognozės kintamasis ✅                                                                               
- 	delta_MoM_pct yra statistiškai reikšmingas, atskiro rodiklio poveikis ne toks stiprus, kartu su delta sustiprina kainos trendą.
- 	Durbin-Watson: 0.848 → likučiai priklauso nuo laiko, rekomenduojamas time series modelis arba lag kintamųjų modelis.           
- 	Condition Number: 1660 → nėra didelis, bet signalizuoja, kad kai kurie kintamieji galbūt koreliuoja.                           
--------------------------------------------------------------------------------------------------------------------------------------
________________________________________

✅ Apibendrinimas:
Modelis:
-	Tinkamas, interpretuojamas.
-	Aiškiai rodo, kad kainų rėžiai (price_delta) yra geras trumpalaikis kainos kitimo rodiklis.
-	MoM pokytis taip pat turi įtaką.
-	Modelio tikrinimui reikia papildomo testo su lag (delta_lag1, MoM_lag1 – vėluojantys rodikliai (nuo praeito mėnesio)).

Lag delta+ MoM
🔍 1. Prognozė parodo kad prieš pakilimą reikšmė yra aukštesnė už tikrą kainą. Paaiškinimas:delta ir MoM indikatoriai reaguoja greičiau nei pati kaina. Kitaip tariant — jie turi prognostinę galią.


