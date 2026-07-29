# Ghid: de la fișiere la fișierul .aab pentru Google Play

Ai nevoie de 2 conturi gratuite: **GitHub** (îl ai deja) și **Codemagic**.
Urmează pașii în ordine. La orice pas te blochezi, trimite-mi un screenshot.

---

## Partea 1 — Urcă proiectul pe GitHub

1. Intră pe github.com și apasă butonul verde **New** (sau **+ → New repository**).
2. Repository name: `neon-drop`
3. Lasă-l **Public** (sau Private, merge oricum). NU bifa "Add a README".
4. Apasă **Create repository**.
5. Pe pagina goală care apare, apasă linkul **"uploading an existing file"**.
6. Dezarhivează `neon-drop-play.zip` pe calculator, apoi trage TOATE fișierele și folderul `www` în zona de upload:
   - `www` (folderul cu index.html)
   - `capacitor.config.json`
   - `package.json`
   - `codemagic.yaml`
   - `.gitignore`
7. Apasă **Commit changes**.

Gata Partea 1 — proiectul e pe GitHub.

---

## Partea 2 — Conectează Codemagic și fă build

1. Intră pe **codemagic.io** → **Sign up** → alege **Sign in with GitHub** (autorizezi accesul la repository-uri).
2. În Codemagic apasă **Add application** → alege **GitHub** → selectează repo-ul `neon-drop`.
3. La întrebarea despre tipul proiectului alege **Other / Capacitor** (sau "I have a codemagic.yaml"). Codemagic va citi singur fișierul `codemagic.yaml`.
4. **Înainte de primul build** trebuie să adaugi 3 parole (le alegi tu, ține-le minte):
   - Mergi la **Teams / Settings → Environment variables** (sau tab-ul "Environment variables" al aplicației).
   - Creează un grup numit exact: `keystore`
   - Adaugă 3 variabile în grupul `keystore` (bifează **Secure** la fiecare):
     - `KEYSTORE_PASSWORD` = o parolă (ex: `NeonDrop2026!`)
     - `KEY_ALIAS` = `neondrop`
     - `KEY_PASSWORD` = aceeași parolă ca la KEYSTORE_PASSWORD
5. Apasă **Start new build** → alege workflow-ul **Neon Drop Android** → **Start build**.
6. Așteaptă ~10-15 min. Când termină cu bifă verde, la secțiunea **Artifacts** descarci:
   - fișierul **`.aab`** (ăsta se urcă pe Google Play)
   - fișierul **`keystore.jks`** → SALVEAZĂ-L bine, îți trebuie ca să poți face update-uri în viitor.

---

## Partea 3 — Urcă pe Google Play

1. În Play Console → **Test and release → Production → Create new release**.
2. Urcă fișierul **`.aab`**.
3. La "Release name" scrie `1.0`, la "Release notes" scrie ceva scurt (ex: "Prima versiune").
4. **Next → Save → Review release → Start rollout to Production**.
5. Aplicația intră în review la Google (poate dura de la câteva ore la câteva zile). După aprobare, e live!

---

Dacă build-ul din Codemagic dă eroare (bifă roșie), deschide build-ul, copiază ultimele linii roșii din log și trimite-mi-le — le rezolvăm.
