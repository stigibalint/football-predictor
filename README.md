<div align="center">
  <h1>⚽ StigiTips — AI Fociprediktor Platform</h1>
  
  <p>
    <strong>Teljes stack focielemző webalkalmazás, amely Poisson-eloszlást, Dixon-Coles korrekciót, ELO-ratinget és Monte Carlo szimulációt kombinál.</strong>
  </p>

  <p>
    <a href="#-áttekintés">Áttekintés</a> •
    <a href="#-képernyőképek--videók">Demó</a> •
    <a href="#-funkciók">Funkciók</a> •
    <a href="#-technológiai-stack">Tech Stack</a> •
    <a href="#-architektúra">Architektúra</a>
  </p>

  <div>
    <img src="https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react" alt="React" />
    <img src="https://img.shields.io/badge/TypeScript-5.9-3178C6?style=for-the-badge&logo=typescript" alt="TypeScript" />
    <img src="https://img.shields.io/badge/Vite-7-646CFF?style=for-the-badge&logo=vite" alt="Vite" />
    <img src="https://img.shields.io/badge/Tailwind_CSS-4-06B6D4?style=for-the-badge&logo=tailwindcss" alt="TailwindCSS" />
    <img src="https://img.shields.io/badge/Node.js-Express-339933?style=for-the-badge&logo=nodedotjs" alt="Node.js" />
    <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql" alt="PostgreSQL" />
  </div>
</div>

<br/>

## 🎯 Áttekintés

A **StigiTips** egy előfizetéses fociprediktor platform, amely AI-alapú mérkőzéselemzést, valószínűségi eloszlásokat és fogadási betekintőket kínál a top európai bajnokságokból (Premier League, La Liga, Bundesliga, Serie A, Ligue 1 stb.).

A platform három fő rétegre épül:

- 💻 **Frontend:** React / TypeScript *(Ez a repository)*
- ⚙️ **Backend:** Node.js / Express / PostgreSQL *(REST API, auth, adattárolás)*
- 🧠 **AI Motor:** Python *(Statisztikai számítások — privát repository)*

---

## 📸 Képernyőképek

<img width="2555" height="1349" alt="landing-page" src="https://github.com/user-attachments/assets/4eaea241-7656-44c9-874b-71005c1ad632" />
<img width="2544" height="1348" alt="reg-page" src="https://github.com/user-attachments/assets/223f1970-e16e-453a-b611-630c51332dcf" />
<img width="2487" height="1295" alt="dashboard" src="https://github.com/user-attachments/assets/8b9a8fe9-a866-414d-ad80-82e6fe2c8936" />

### 🎥 Videós bemutatók

**Főoldal & Áttekintés**

https://github.com/user-attachments/assets/387da8ac-67d9-4de8-9622-d159bad5ce2e

**Meccs predikciós folyamat**

https://github.com/user-attachments/assets/2b17d472-2719-4356-a057-f7b21c55ca48

**Poisson Kalkulátor**

https://github.com/user-attachments/assets/02df4bb2-1d41-420c-af74-965bee6e2406

**Gyakori kérdések**

https://github.com/user-attachments/assets/4d26fdf6-980a-41fe-ae8a-cd69ff60e870

---

## ✨ Funkciók

### 📊 Dashboard & Elemzés
* **AI Mérkőzéselemzés** — 1X2 valószínűségi eloszlás, várható gólok (xG), pontos eredmény valószínűségek, Over 2.5 / BTTS, valamint interaktív radar chart csapatösszehasonlítással.
* **HC Napi Kiemelt Tippek** — Prémium szekció a legmagasabb konfidenciájú tippekkel (`SUPER` / `STRONG` / `CONFIDENT` besorolás a modell gap score-ja alapján).
* **Közösségi szavazás** — H/D/V szavazatok optimista UI élő százaléksávokkal.
* **Élő adatok** — Ligatáblák és góllövőlisták bajnokságonkénti widgetekkel.

### 🛠️ Elemző Eszközök
* **Poisson Kalkulátor** — Eredményvalószínűségi mátrix generálása támadó/védekezési erőértékekből.
* **Szurebet & Margin Kalkulátor** — Arbitrázs kereső és bukmékeri margin számítás fair odds megállapításához.
* **Modell Építő & Backtester** — Egyedi motor-súlyozás és historikus adatokon alapuló stratégia-visszatesztelés.

### 🌐 Platform
* **Stigi Akadémia & AI Chatbot** — Videós oktatókönyvtár és beépített asszisztens a maximális hatékonyságért.
* **Pro / Ingyenes szint** — Zökkenőmentes paywall rendszer és upgrade folyamat.

---

## 🛠 Technológiai Stack

| Frontend | Backend | AI Motor *(Privát)* |
| :--- | :--- | :--- |
| **React 19** | **Node.js & Express** | Python |
| **TypeScript 5.9** | **PostgreSQL** | Poisson / Dixon-Coles |
| **Vite 7** | REST API | ELO rating rendszer |
| **Tailwind CSS v4** | JWT (Cookie + Memória) | Monte Carlo szimuláció |
| **React Router v7** | | Külső API integrációk |
| **Recharts** | | |

---

## 🏛 Architektúra Megjegyzések

> **💡 Biztonságos Hitelesítés (Token Stratégia)** > Az Access Token **kizárólag JS modulmemóriában** él (soha nem kerül a localStorage-ba az XSS sebezhetőség elkerülése végett). A Refresh Token egy `httpOnly` süti. A háttérben érkező `401 Unauthorized` válaszokat az Axios interceptorok elkapják, és csendes újrahitelesítést indítanak.

> **⚡ Hibatűrő Predikciós Folyamat** > Az elemzés két párhuzamos API kérést indít (`/predict-ai` és `/match-details`) `Promise.allSettled` használatával. Ez biztosítja, hogy egy esetleges külső H2H vagy felállás-API hiba ne akassza meg a legfontosabbat: a valószínűségi kimenet megjelenítését.

---

## 🚀 Helyi Futtatás (Csak Frontend)

A frontend egy `/api` címen futó Node.js backendet és a Python AI motort várja. Ezek hiányában a felület és a design böngészhető, de az élő adatok és a predikciók nem töltődnek be.

```bash
# 1. Repository klónozása
git clone [https://github.com/stigibalint/football-predictor](https://github.com/stigibalint/football-predictor)

# 2. Mappa megnyitása
cd football-predcitor

# 3. Függőségek telepítése
npm install

# 4. Fejlesztői szerver indítása
npm run dev
