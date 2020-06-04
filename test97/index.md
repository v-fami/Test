Az Azure Static Web Apps olyan statikus alkalmazásokat üzemeltet, mint a Gatsby-vel készíthetők. Ehhez először lefordítja az alkalmazás statikus összetevőit, majd üzembe helyezi azokat a felhőben.

Itt helyben fordíthatja le az alkalmazás statikus összetevőit, hogy megvizsgálhassa azokat, és helyileg üzemeltetve próbálja ki őket. Csak ez után küldi le a kódot a GitHubba, és hoz létre Azure Static Web Apps-példányt az alkalmazás webes üzemeltetésére.

## <a name="build-your-site"></a>A webhely buildelése

A webhely buildelésével és az üzembe helyezésre való előkészítésével járó munka nagyját a Gatsby elvégzi Ön helyett.

Adja ki a következő parancsot a projektkönyvtárban:

```bash
gatsby build
```

Ez a parancs egy *éles buildet* állít elő. Az összes fájl egy `build/` nevű alkönyvtárba kerül.

A buildelési folyamat befejeződése után beléphet a `build/` könyvtárba, és megnyithatja a fájlokat egy böngészőben. A `http-server` használatával ugyanúgy böngészheti a buildet, mintha az a weben volna üzemeltetve. Ez a parancssori eszköz HTTP-n keresztül szolgáltatja a helyi fájlokat, így megjeleníthetők a böngészőben.  

Most a teljes webalkalmazást fogja egy helyi webkiszolgálóról szolgáltatni. A terminálban a `cd` paranccsal lépjen a `build/` könyvtárba, majd adja ki a következő parancsot:

```bash
npx http-server -p 5000
```

A böngészőben nyissa meg a `http://localhost:5000` címet.

A következő renderelt tartalomnak kell megjelennie:

:::image type="content" source="../media/built-site.png" alt-text="A buildelt alkalmazás":::

Buildelte a webhelyet, így az már nem Gatsby-alkalmazás, hanem statikus oldalak halmaza, amelyek csak HTML-ből, CSS-ből és JavaScript-ből állnak.

A `build/` könyvtárba belépve keresse meg a renderelt `about` összetevőt a `build/about/index.html` címen. Egy optimalizálási eljárás minden térközt eltávolított, és az oldal egyetlen hosszú sorként jelenik meg. Ennek ellenére meg lehet találni a renderelt címet és leírást, amely az alábbihoz hasonló:

```html
// excerpt from about/index.html

<h2>Gatsby Default Starter</h2><div>Kick off your next, great Gatsby project with this default starter. This barebones starter ships with the main Gatsby configuration files you might need.</div>
```

## <a name="push-your-code-to-github"></a>A kód leküldése a GitHubba

Az alkalmazás a következő lépésekben készíthető elő az üzembe helyezésre:

1. Git-adattár inicializálása
2. GitHub-adattár léterhozása és a helyi Git-adattár leküldése

### <a name="create-a-git-repository"></a>Git-adattár létrehozása

Navigáljon a projekt gyökeréhez a konzolon, majd a következő paranccsal inicializálja a Git-adattárat, és véglegesítse abban az összes fájlt:

```bash
git init
```

Ez után hozzon létre egy `.gitignore` nevű fájlt a projekt gyökerében, és helyezze el benn az alábbi tartalmat:

```bash
node_modules
build
```

A fenti konfiguráció megakadályozza, hogy a `build/` és a `node_modules` könyvtár hozzá legyen adva az adattárhoz. A `build/` könyvtár minden buildeléskor módosul, a `node_modules/` könyvtárra pedig csak a buildelés során van szükség, és meglehetősen nagy lehet a benne lévő sok kódtár miatt.

Végül vegye fel a kódot az adattár-indexbe, és véglegesítse azt.

```bash
git add .
git commit -m "adding Gatsby project"
```

### <a name="create-a-github-repo-and-push-the-code"></a>GitHub-adattár létrehozása és a kód leküldése

1. Lépjen a GitHubra és jelentkezzen be. Az aktuális URL-cím a következőhöz hasonló: `https://github.com/<your username>?tab=repositories`

2. Kattintson az `new` gombra, ahogyan az alábbi ábrán látható: :::image type="content" source="../media/create-github-repo.png" alt-text=\"Új GitHub-adattár létrehozása\":::

3. Adja meg az adattárhoz a `gatsby-app` nevet, és kattintson az `Create repository` gombra az ábra szerint: :::image type="content" source="../media/github-naming.png" alt-text="GitHub-adattár elnevezése":::

4. Végül vegye fel távoliként a GitHub-adattárat, és végezze el a leküldést. Ezt az alábbi parancsokkal hajthatja végre (a `<user>` rész helyére írja be a saját GitHub-felhasználónevét):

   ```bash
   git remote add origin https://github.com/<user>/gatsby-app.git
   git push -u origin master
   ```

Most már minden készen áll az Azure Static Web Apps-beli üzembe helyezéshez!

## <a name="create-a-static-web-app"></a>Statikus webalkalmazás létrehozása

Most, hogy létrehozta a GitHub-adattárat, létrehozhat egy Static Web Apps-példányt az Azure Portalon.

Ez az oktatóanyag az Azure-tesztkörnyezet használatával biztosít Önnek egy ingyenes, ideiglenes Azure-előfizetést, amellyel elvégezheti a gyakorlatot. Mielőtt továbblépne, győződjön meg arról, hogy aktiválta a tesztkörnyezetet a lap tetején.

1. Jelentkezzen be az [Azure Portalon](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true), és győződjön meg arról, hogy ugyanazt a fiókot használja a bejelentkezéshez, mint amellyel a tesztkörnyezetet aktiválta.
1. A felső sávon keressen rá a **Static Web Apps** kifejezésre.
1. Válassza a **Static Web Apps** elemet.
1. Válassza az **Új** lehetőséget.

### <a name="basics"></a>Alapbeállítások

Ezután konfigurálja az új alkalmazást, és kapcsolja össze a GitHub-adattárral.

1. Adja meg a **Projekt részleteit**

   | Beállítás          | Érték                                    |
   | ---------------- | ---------------------------------------- |
   | _Előfizetés_   | **Concierge-előfizetés**               |
   | _Erőforráscsoport_ | <rgn>[Tesztkörnyezeti erőforráscsoport neve]</rgn> |

1. Adja meg a **Static Web Apps részleteit**

   | Beállítás  | Érték                                                                         |
   | -------- | ----------------------------------------------------------------------------- |
   | _Név_   | Nevezze el az alkalmazást. Az érvényes karakterek az `a-z` (kis- és nagybetűk megkülönböztetése nélkül) `0-9`és az `_`. |
   | _Régió_ | Válassza ki az Önhöz legközelebb eső régiót                                                  |
   | _Termékváltozat_    | **Ingyenes**                                                                      |

1. Kattintson a **Bejelentkezés GitHub-fiókkal** gombra, majd végezzen hitelesítést a GitHub-fiókkal
1. Adja meg a **Verziókövetés részleteit**

   | Beállítás        | Érték                                                    |
   | -------------- | -------------------------------------------------------- |
   | _Szervezet_ | Válassza ki a szervezetet, amelynél létrehozta az adattárat |
   | _Adattár_   | **gatsby-app**                              |
   | _Ág_       | **fő**                                               |

1. Kattintson a **Tovább: Létrehozás >** gombra a létrehozási konfiguráció szerkesztéséhez

   :::image type="content" source="../media/next-build-button.png" alt-text="Ugrás a buildelési menüre":::

### <a name="build"></a>Buildelés

Ezután adja meg az Ön által választott előtér-keretrendszerhez tartozó konfigurációs adatokat.

| Beállítás                 | Érték                |
| ----------------------- | -------------------- |
| _Alkalmazás helye_          |  *Hagyja meg az alapértelmezett értéket*     |
| _API helye_          |  *Hagyja meg az alapértelmezett értéket*     |
| _Alkalmazás-összetevő helye_ | **public**           |

Kattintson az **Ellenőrzés és létrehozás** gombra

:::image type="content" source="../media/review-create-button.png" alt-text="Ellenőrzés és létrehozás gomb":::

### <a name="review--create"></a>Ellenőrzés és létrehozás

Lépjen tovább az alkalmazás létrehozásához.

1. Kattintson a **Létrehozás** gombra :::image type="content" source="../media/create-button.png" alt-text="Létrehozás gomb":::

1. Az üzembe helyezés végeztével kattintson az **Erőforrás megnyitása**, majd az :::image type="content" source="../media/go-to-resource-button.png" alt-text="Ugrás az erőforráshoz"::: gombra

### <a name="review-the-github-action"></a>A GitHub-művelet ellenőrzése

Ebben a szakaszban már létrejött a Static Web Apps-példány az Azure-ban, de az alkalmazás még nincs üzembe helyezve. Az Azure által az adattárban létrehozott GitHub Actions-művelet automatikusan lefut, hogy elvégezze az alkalmazás első létrehozását és üzembe helyezését, de igénybe vesz néhány percet, amíg befejeződik.

Az alábbi hivatkozásra kattintva tekintheti meg a buildelés és üzembe helyezési művelet állapotát:

:::image type="content" source="../media/static-app-portal.png" alt-text="A GitHub-művelet előrehaladásának megtekintése a böngészőben":::

### <a name="view-website"></a>Webhely megtekintése

Miután a GitHub Actions-művelet befejezte a webalkalmazás létrehozását és közzétételét, a futó alkalmazás megtekintéséhez megnyithatja azt a böngészőben.

Kattintson az Azure Portalon található _URL-cím_ hivatkozásra az alkalmazás böngészőben való megnyitásához.

:::image type="content" source="../media/static-app-portal-finished.png" alt-text="Az Azure Static Web Apps Áttekintés lapja":::

:::image type="content" source="../media/published.png" alt-text="Az Azure Static Web Apps Áttekintés lapja":::

Gratulálunk! Üzembe helyezte az első alkalmazást az Azure Static Web Apps-ben!

> [!NOTE]
> Ne aggódjon, ha egy olyan weblap jelenik meg, amely szerint az alkalmazás még nincs létrehozva és üzembe helyezve. Próbálja meg egy perc múlva frissíteni a böngészőt. Az Azure Static Web Apps-példány létrehozásakor a GitHub Actions-művelet automatikusan lefut. Szóval ha a kezdőlap jelenik meg, az alkalmazás üzembe helyezése még folyamatban van.

Megcsinálta! Üzembe helyezte a Gatsby-alkalmazást a felhőben.
