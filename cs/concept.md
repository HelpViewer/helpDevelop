# 🗺️ Základní přehled

Aplikace je postavená na **pluginech (zásuvných modulech) a přenosu událostí (zpráv) mezi nimi**.

V pluginech lze definovat:

- události (zprávy),
- jejich obsluhy,
- odesílání událostí,
- UI prvky,
- obsluhy javascript událostí,
- členství v komunikační cestě (skupina příjemců)

Díky tomu jsou přístupy pro UI i programovou logiku jednotné napříč celou aplikací.  
Systém pluginů i distribuce zpráv je vyvinut od základů, bez použití cizích frameworků.  

**Technické řešení:**

- komprimovaný balíček aplikačních dat (s možností běhu s rozzipovaným obsahem),
- běh na klientovi, bez nutnosti serveru či backendu,
- minimum pro nasazení: prohlížeč s podporou **ES2021** + místní disk (Internet není nutný) (doporučeno vypnutí CORS, byť aplikace obsahuje podporu pro upload dat ručně uživatelem)

**Hlavní součásti aplikace:**

- zavaděč (**hvdata/appmain.js + jszip.min.js**),
- aplikační data (**hvdata/data.zip**; **STO_DATA**), kde je uložena převážná část aplikace (asi 86 % velikosti balíčku)
  - nízkoúrovňový kód (v **js.lst**),
  - pluginový kód (v **plugins.lst**).
- knihovny třetích stran (oddělené, načítané jako samostatné moduly)
- soubor implementačních dat - samostatný archiv v aplikaci logicky pojmenovaný jako **STO_HELP**
