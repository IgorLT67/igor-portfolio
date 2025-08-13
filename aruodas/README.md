# Aruodas.lt duomenų „scraping“ ir analizė

**Aruodas.lt** – populiariausias nekilnojamojo turto portalas Lietuvoje, siūlantis daug struktūruotos informacijos apie pardavimo situaciją.  
Tačiau portalo viešai prieinama informacija yra sunkiai apibendrinama dėl kelių priežasčių:
- Pateikiami tik riboti statistiniai įrankiai.
- Informacija pateikiama skirtingais suvedimo moduliais (pvz., mažmeniniams pardavėjams ir NT vystytojams).
- Naudojamas dinaminis duomenų generavimo bei atvaizdavimo būdas, apsunkinantis automatizuotą duomenų paėmimą.

Populiariausias duomenų gavimo būdas – **„scraping“** – Aruodas.lt atveju yra komplikuotas.

---

## Sprendimas
Sukurtas **Python kodas**, imituojantis realaus vartotojo elgesį – puslapiai peržiūrimi vienas po kito.  
Tokiu būdu galima gauti pradinius duomenis bei juos kaupti istorinei analizei.

---

## Tyrimo metodika
- **Duomenų struktūra:** iš anksto apibrėžta ir sudaryta taip, kad leistų atlikti nuoseklią kitimo stebėseną.
- **Atnaujinimai:** kiekvienas naujas „scraping“ pridės duomenis prie jau esančių, leisdamas atlikti istorines įžvalgas (pvz., kainos pokyčio stebėjimą).
- **Analizės prioritetas:** dėmesys sutelktas ne į kainų lygį, o į **pardavimo proceso dinamiką**.

**Analizuojami rodikliai:**
- Pardavimo laikas (sezoniškumas).
- Skelbimo redagavimo laikas.
- Kainos kitimas.
- Populiarumas (įsiminimų skaičius).
- Peržiūrų skaičius.

**Skaičiavimų vienetas:** Ploto kaina (EUR/m²), siekiant tikslesnio palyginimo.

---

## Duomenų grupavimas

**Pagal ploto kainą:**
- 1–1000 EUR/m²
- 1000–1700 EUR/m²
- 1700–2500 EUR/m²
- 2500–3500 EUR/m²
- 3500–5000 EUR/m² (dažniausiai naujos statybos)
- >5000 EUR/m²

**Pagal įsimintus skelbimus:**
- 1–5: *Nepopuliarus* (dažnai „širdeles“ deda patys talpintojai).
- 5–20: *Populiarus*.
- 20–40: *Karštas*.
- >40: *Top*.

**Pagal galiojimo trukmę:**
- <60 d.: *Naujas*.
- 60–180 d.: *Nenaujas*.
- 180–300 d.: *Senas*.
- >300 d.: *Nepopuliarus*.

---

## Pagrindinės įžvalgos

### 1. Skelbimo įkėlimo laikas
- Didžiausias įsiminimų skaičius fiksuojamas pirmadieniais, mažiausias – savaitgaliais.
- **Rekomendacija:** naujus skelbimus kelti pirmadienio rytą, kol jie nenustumti kitų į žemesnes pozicijas.

![Picture 1](link)

---

### 2. Populiarumo dinamika ir redagavimas
- Populiarumas mažėja bėgant laikui, tačiau susidaro trys aiškūs klasteriai:
  - *Iki 50 d.* – aktyviausi skelbimai.
  - *50–100 d.* – vidutinio populiarumo.
  - *>100 d.* – mažiausio populiarumo.
- Redagavimas sukelia trumpalaikį susidomėjimo šuolį (iki 3 kartų didesnį), tačiau:
  - efektas trunka iki 15 d.
  - po mėnesio susidomėjimas gali tapti net mažesnis nei be redagavimo.
- **Išvada:** redaguoti tik turint aiškią trumpalaikę pardavimo taktiką (akcija, nuolaida, svarbus pakeitimas).

![Picture 2](link)

---

### 3. Populiarumo stabilumas pagal klasterius
- Didžiausi svyravimai – „Populiarus“ grupėje (5–20 įsiminimų).
- Stabiliausias susidomėjimas – „Top“ grupėje (>40 įsiminimų).

![Picture 3](link)

---

### 4. Pasiūlos sezoniškumas (2025 m. tendencijos)
- Didžiausia pasiūla – liepos mėnesį, tačiau rugpjūtis žada viršyti šį rodiklį.
- Vartotojų susidomėjimas sparčiausiai auga segmente **2500–3500 EUR/m²**.
- Tai rodo, kad dauguma pirkėjų pasiekė savo įperkamumo ribą ir laukia palankių akcijų.

![Picture 4](link)

---

### 5. Segmentų palyginimas
- Brangesnių butų pasiūla (~≥3500 EUR/m²) sudaro beveik pusę rinkos.
- Segmento 2500–3500 EUR/m² skelbimų per pirmus 6 mėnesius sumažėja ~75 %.
- Brangesnių butų skelbimų sumažėjimas per tą patį laikotarpį – apie 66 %.
- Skelbimai, kurių trukmė viršija 300 dienų, yra reti bet kuriame segmente.

---

## Galimos plėtros kryptys
- Analizė pagal kitus turto tipus (namai, patalpos, sklypai).
- Miestų tarpusavio palyginimas.
- Išplėsta vartotojų veiksmų analizė, įtraukiant sezonines tendencijas.

---

**Pagrindiniai analizės įrankiai:** segmentavimas, laiko intervalų nustatymas, vartotojų veiksmų identifikavimas.
