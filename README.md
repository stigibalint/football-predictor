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

<img width="2555" height="1349" alt="landing-page" src="https://github.com/user-attachments/assets/4e4ddd24-acb4-43a1-affe-e4c8653b1a30" />
<img width="2544" height="1348" alt="reg-page" src="https://github.com/user-attachments/assets/306202e3-d506-4c6b-9380-86f30bb6cdde" />
<img width="2487" height="1295" alt="dashboard" src="https://github.com/user-attachments/assets/ae2f0525-1332-45b5-a88e-241442e9faf1" />

### 🎥 Videós bemutatók

**Főoldal & Áttekintés**

https://github.com/user-attachments/assets/b75b39eb-4f4d-4cbd-8915-ae7df80c3bc0

**Meccs predikciós folyamat**

https://github.com/user-attachments/assets/cb4ab6a1-197c-4131-b30a-0f0aa1cee7b3

**Poisson Kalkulátor**

https://github.com/user-attachments/assets/37cc7cf8-055a-41ed-9bfa-6c2f48cbf8c7


**Gyakori kérdések**

https://github.com/user-attachments/assets/506efb43-4474-40ee-bdb2-eb85aabd994d



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
