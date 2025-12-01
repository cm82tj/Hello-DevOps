Hello DevOps – egyszerű Node.js alkalmazás

Orosz László - CM82Tj

Ez egy egyszerű „Hello world” jellegű webalkalmazás.
HTTP-n keresztül elérhető, és egy szöveget ad vissza a böngészőnek.

Az alkalmazás alapértelmezett címe: http://localhost:8080

A projekt célja az alap DevOps lépések bemutatása:

kódkészítés

verziókövetés

buildelés

Docker image készítése és futtatása

Dev Container használata

1. Előfeltételek

A projekt futtatásához az alábbi programokra van szükség:

Node.js és npm

Git

Docker

Dev Containers bővítmény

2. Projekt klónozása

GitHub-ról:

git clone https://github.com/cm82tj/Hello-DevOps.git

cd Hello-DevOps

3. Alkalmazás buildelése és futtatása lokálisan

Az alkalmazás Node.js + Express szerver, amely egyetlen végpontot (/) szolgál ki.

3.1. Függőségek telepítése

npm install

Ez letölti és telepíti a szükséges Node modulokat.

3.2. Build

npm run build

Ez a parancs lefordítja a forráskódot a dist/ mappába a tsconfig.json beállításai alapján.

3.3. Futtatás

npm start

Sikeres indítás után a konzolban ehhez hasonló üzenetnek kell megjelennie:

Server is running on http://localhost:8080

Ezután az alkalmazás elérhető:

böngészőből: http://localhost:8080
parancssorból: curl http://localhost:8080

Válaszként egy egyszerű „Hello DevOps” jellegű szöveg érkezik.

4. Docker használata

A projekt gyökérkönyvtárában található egy Dockerfile, amelyből Docker image építhető.

4.1. Docker image buildelése

A projekt mappájában futtasd:

docker build -t hello-devops:v1 .

-t hello-devops:v1 – az image neve és tage

Siker esetén létrejön a hello-devops:v1 nevű Docker image.

4.2. Konténer futtatása

docker run --rm -p 8080:8080 hello-devops:v1

-p 8080:8080 – a host 8080-as portja a konténer 8080-as portjára irányítódik

--rm – a konténer leállítás után automatikusan törlődik

Ezután az alkalmazás ugyanúgy elérhető:

http://localhost:8080

A futó konténer leállítása ebben a módban:
Ctrl + C a terminálban.

4.3. Konténer futtatása háttérben

Ha nem szeretnéd, hogy a docker run elfoglalja a terminált, futtathatod háttérben is:

docker run -d --name hello-devops-app -p 8080:8080 hello-devops:v1

-d – háttérben fut

--name hello-devops-app – név a konténernek

Futó konténerek listázása:

docker ps

Konténer leállítása:

docker stop hello-devops-app vagy konténer id

5. Dev Container használata

A repó tartalmaz egy .devcontainer mappát, benne:

.devcontainer/devcontainer.json

.devcontainer/Dockerfile

Ez lehetővé teszi, hogy a projektet GitHub Codespaces segítségével egy előre beállított fejlesztői környezetben futtasd.

5.1. Használat VS Code-ban

Nyisd meg a repót VS Code-ban.

Telepítsd a „Dev Containers” kiegészítőt.

Nyomd meg: Ctrl+Shift+P → keresd: „Dev Containers: Reopen in Container”.

A konténer felépítése után a VS Code automatikusan a konténeren belül dolgozik.

A konténeren belül:

Függőségek telepítése:
npm install

Build:
npm run build

Futtatás:
npm start

Az alkalmazás ezután a host gépről továbbra is a http://localhost:8080 címen érhető el.

6. Git és trunk-based development

A projekt verziókövetése Git-tel történik.
A használt modell: trunk-based development.

fő ág: main,

új módosítások: rövid életű feature branchek,

a feature branchek merge-ölve vannak a main ágba.

6.1. Alap Git lépések

Első commitok a main ágon:

git add .
git commit -m "Alap Hello DevOps alkalmazás hozzáadása"
git branch -M main
git push -u origin main

6.2. Példa feature branch folyamatra

Új feature branch létrehozása:

git checkout -b feature/change-greeting

Változtatások commitolása:

git add src/server.ts
git commit -m "Hello üzenet módosítása egy új feature keretében"

Feature branch feltöltése a távoli repóba:

git push -u origin feature/change-greeting

A Git szolgáltatón Pull Request / Merge Request készítése a main ág felé.

A commit üzenetek célja, hogy egyértelműen leírják a változtatást.
Most készíttettem először ilyet.

