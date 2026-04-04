# anre-simulator-installer

Repository public pentru distribuirea installer-ului **Simulator Examen ANRE**.

Aplicatia verifica automat acest repository la fiecare pornire si notifica utilizatorul daca exista o versiune noua.

---

## Fisiere

| Fisier | Rol |
|--------|-----|
| `app_version.txt` | Versiunea curenta a aplicatiei (format `X.Y.Z`). Aplicatia o compara cu versiunea instalata. |
| `SimulatorExamenANRE_Setup.exe` | Installer Windows (atasat ca Release Asset — NU stocat direct in repo). |

---

## Workflow publicare versiune noua

1. **Build aplicatie + installer:**
   ```bat
   build.bat
   ```
   Genereaza `dist\installer\SimulatorExamenANRE_Setup.exe`.

2. **Actualizeaza `app_version.txt`** cu noua versiune (ex: `1.1.0`).

3. **Creeaza un Release nou pe GitHub:**
   - Tag: `v1.1.0`
   - Titlu: `Simulator Examen ANRE v1.1.0`
   - Ataseaza `SimulatorExamenANRE_Setup.exe` ca Release Asset.

4. **Push `app_version.txt`** pe branch `main`.

Aplicatiile deja instalate vor detecta versiunea noua la urmatoarea pornire si vor oferi descarcarea automata.

---

## Structura URL-uri folosite de aplicatie

```
Verificare versiune:
  https://raw.githubusercontent.com/CristianCasapu/anre-simulator-installer/main/app_version.txt

Descarcare installer:
  https://github.com/CristianCasapu/anre-simulator-installer/releases/latest/download/SimulatorExamenANRE_Setup.exe
```

---

## Flux auto-update in aplicatie

```
Pornire aplicatie
       │
       ▼
Verifica app_version.txt (GitHub raw)
       │
       ├─ versiune noua? ──► Dialog "Versiune noua disponibila"
       │                           │
       │                     Da ──► Descarca installer din Releases
       │                           │
       │                           └─► Lanseaza installer, inchide app
       │
       └─ la zi ──► Verifica actualizare baza de date (questions DB)
                           │
                           └─► Flux existent de update DB
```

---

## Cerinte

- Windows 10/11
- Python 3.11+ (detectat si instalat automat de installer daca lipseste)
- Conexiune internet pentru verificarea actualizarilor (optional — functioneaza si offline)
