# BuxDU Scopus Rektor Dashboard

Bu paket `scopus.csv` + Elsevier API + GitHub Actions + GitHub Pages asosida ishlaydi.

## Birinchi marta sozlash

1. GitHub'da yangi repository yarating, masalan: `buxdu-scopus-dashboard`.
2. Ushbu ZIP ichidagi HAMMA fayl va papkalarni repository'ga yuklang.
3. Repository'da:
   `Settings -> Secrets and variables -> Actions -> New repository secret`
4. Secret nomi:
   `ELSEVIER_API_KEY`
5. Value maydoniga Elsevier API Key'ingizni kiriting.
6. `Actions` bo'limiga o'ting -> `Update Scopus enriched data` -> `Run workflow`.
7. Workflow tugagach `scopus_enriched.csv` API ma'lumotlari bilan yangilanadi.

## GitHub Pages yoqish

`Settings -> Pages -> Build and deployment`

- Source: `Deploy from a branch`
- Branch: `main`
- Folder: `/ (root)`
- Save

Bir ozdan keyin GitHub sizga dashboard URL beradi.

## Kundalik ishlash

Siz faqat yangi Scopus eksportini `scopus.csv` nomi bilan eski fayl ustiga yuklaysiz.

GitHub Actions avtomatik:
- noyob ISSNlarni oladi;
- Elsevier Serial Title API `view=CITESCORE` orqali jurnal metrikalarini tekshiradi;
- maqola yiliga mos CiteScore'ni topadi;
- subject kategoriyalar ichidagi ENG YUQORI percentile'ni oladi;
- Q1/Q2/Q3/Q4 ni hisoblaydi;
- `scopus_enriched.csv` ni yangilaydi;
- dashboard yangi CSVni o'qiydi.

## Kvartil qoidasi

- 75+ percentile = Q1
- 50-74 = Q2
- 25-49 = Q3
- 0-24 = Q4

Dashboarddagi Quartile `Best CiteScore subject percentile` usulida hisoblanadi.
Bir jurnal bir nechta subject category'ga ega bo'lishi mumkin.

## 2026 / In-Progress

API `MetricStatus=In-Progress` qaytarsa, u CiteScore Tracker hisoblanadi va yakuniy yillik metrika emas.
Dashboardda status alohida saqlanadi.

## Fayllar

- `index.html` — rektor dashboard
- `scopus.csv` — original Scopus eksporti
- `scopus_enriched.csv` — API bilan boyitilgan yakuniy CSV
- `scripts/update_scopus.py` — API va kvartil hisoblash dasturi
- `.github/workflows/update.yml` — GitHub Actions
- `data/api_cache/` — API so'rovlarini kamaytiradigan cache
- `data/update_status.json` — oxirgi yangilanish statistikasi

## Muhim xavfsizlik

API Key'ni `index.html`, `.py`, `.csv` yoki README ichiga yozmang.
Faqat GitHub Secret sifatida saqlang.
