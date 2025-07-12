# 🏙️ Šalies miestų butų kainų analizė su Power BI & Python

**Tikslas:**  
Identifikuoti veiksmingus butų rinkos analizės indikatorius, įžvelgti jų tarpusavio koreliacijas ir įvertinti, kaip makroekonominiai veiksniai gali paveikti gyventojų nuomonę apie teisingą būsto kainą.

---

## 📈 Apie projektą

Šiame darbe buvo analizuojamos **gyvenamųjų butų skelbiamos 1 m² kainos** skirtinguose Lietuvos miestuose.  
Pagrindinis tyrimo objektas – **kainų dinamikos vertinimas laike** ir kainų sąsaja su ekonominiais rodikliais.

> ❗ Šiame darbe **nėra vertinami**: pardavimų kiekiai, nuolaidos, finansavimo šaltiniai ir t.t.

---

## 🖼️ Vizualizacijos pavyzdžiai. 
      Galimi pjuviai pagal visus požymius: miestas, rajonas, buto tipas, kambarių skaičius.

### 📊 1. Koreliacija buto kainos ir Kainų režių dydžio indikatorio

![Dashboard Preview](ooh_2.jpg)
![Dashboard Preview](ooh_3.jpg)

---

### 📊 2. Infliacijos įtaka

![Dashboard Preview](ooh_4.jpg)

---

### 📊 3. Makroekonominiai rodikliai ir kainos kitimas


![Dashboard Preview](ooh_5.jpg)

---

## 🛠️ Naudoti įrankiai

- **Power BI** – vizualizacijos, indikatoriai, skaičiavimai, koreliacijų grafikai
- **Python** – duomenų transformavimas, įkėlimas, skaičiavimai, apdorojimas

---

## 📊 Naudoti duomenų šaltiniai

- [Ober-Haus mėnesinės butų kainų ataskaitos](https://www.ober-haus.lt/rinkos_apzvalgos/kainu-lenteles/)
  ![Dashboard Preview](ooh_1.jpg)
  
- Lietuvos statistikos departamentas
- Lietuvos Bankas
- EURIBOR duomenys

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

---

## Rezultatų tikrinimas

Naudoti metodai:
🧹 1. Duomenų paruošimas
•	PDF lentelių ištraukimas su pdfplumber
•	Stulpelių konvertavimas 
•	Data normalizavimas į datetime 
________________________________________
🔁 2. Laiko eilutės transformacijos
•	Grupavimas 
•	Lag skaičiavimai: delta_lag1, MoM_lag1 – vėluojantys rodikliai (nuo praeito mėnesio)
________________________________________
📊 3. Regresinė analizė
•	Multiple Linear Regression su sklearn.linear_model.LinearRegression
o	Naudota:
	kainų rėžių dydis
	delta_MoM_%
	Infliacija, Euribor 3 mėn., darbo užmokėsčio kitimas
	Sintetinis rodiklis: Santykinis_skirtumas = vidutinė kaina / darbo užmokėsčio kitimas
•	StandardScaler – nepriklausomų kintamųjų standartizavimas 
________________________________________
📈 4. Statistinė analizė su statsmodels (OLS)
•	statsmodels.OLS (Ordinary Least Squares) modeliai:
o	Atskiras modelis su makro rodikliais
o	Atskiras modelis su delta + MoM
•	Pateikti rodikliai:
o	coef – koeficientai
o	R², Adj. R²
o	t, p-value – reikšmingumo testai
o	AIC, BIC – modelio kokybės kriterijai
________________________________________
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

