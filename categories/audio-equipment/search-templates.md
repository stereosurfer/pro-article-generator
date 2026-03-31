# Search Query Templates: Audio Equipment / 搜尋查詢模板：音頻設備

> Last updated / 最後更新: 2026-03-31
> Category: audio-equipment
> Usage: Phase 1 search, applied with `{brand}`, `{model}`, `{origin_language}` substitutions

---

## How to Use / 使用方式

Replace placeholders before searching:
執行搜尋前替換佔位符：

- `{brand}` — Manufacturer name, e.g., "Neumann", "Shure", "Sony"
- `{model}` — Full model number, e.g., "U87 Ai", "SM58", "C-800G"
- `{brand_model}` — Combined, e.g., "Neumann U87 Ai", "Shure SM58"
- `{origin_lang}` — Origin language keyword, e.g., "German", "American", "Japanese"

---

## Round 1: Official & Technical Documentation / 第 1 輪：官方與技術文件

```
{brand_model} official manual filetype:pdf
{brand_model} user guide specifications
{brand_model} service manual schematic
{brand} {model} datasheet "frequency response"
{brand_model} patent site:patents.google.com
{brand_model} AES paper site:aes.org
"{brand_model}" "self-noise" OR "EIN" OR "equivalent noise"
"{brand_model}" "frequency response" specifications site:{brand official domain}
```

---

## Round 2: Professional Media Reviews / 第 2 輪：專業媒體評測

```
{brand_model} review site:soundonsound.com
{brand_model} review site:stereophile.com
{brand_model} measurement site:audiosciencereview.com
{brand_model} test OR review site:prosoundweb.com
{brand_model} review site:emusician.com
{brand_model} "Sound on Sound" review
{brand_model} test Messung site:amazona.de
{brand_model} レビュー 測定 site:rittor-music.co.jp
```

---

## Round 3: Professional Community Discussions / 第 3 輪：專業社群討論

```
{brand_model} site:gearspace.com
{brand_model} capsule OR circuit OR "mod" site:gearspace.com
{brand_model} measurements site:audiosciencereview.com
{brand_model} schematic OR "circuit topology" site:groupdiy.com
{brand_model} site:reddit.com/r/audioengineering
{brand_model} vintage OR mod OR recap site:reddit.com/r/vintageaudio
{brand_model} 5ch.net OR 2ch.net レビュー
{brand_model} site:ptt.cc
{brand_model} ptt.cc OR mobile01.com 評測
```

---

## Round 4: Market & Pricing Data / 第 4 輪：市場與價格資訊

```
{brand_model} sold price site:reverb.com
{brand_model} completed listings site:ebay.com
{brand_model} 落札 site:page.auctions.yahoo.co.jp
{brand_model} 中古 site:mercari.com
{brand_model} 二手 site:ruten.com.tw OR site:shopee.tw
{brand_model} vintage worth investment value
{brand_model} serial number production year guide
```

---

## Language-Specific Supplement Queries / 語系補充查詢

### German-origin equipment (add to Round 1-2)
```
{brand} {model} Test Messung Bewertung
{brand} {model} Frequenzgang Eigenrauschen Technische Daten
{brand} {model} Vergleich
```

### Japanese-origin equipment (add to Round 1-2)
```
{brand} {model} スペック 仕様 測定
{brand} {model} レビュー 評価 音質
{brand} {model} 比較 おすすめ
```

---

## Minimum Source Requirements / 最低來源要求

After all 4 rounds, verify:
完成 4 輪搜尋後驗證：

| Language / 語系 | L1 | L2 | L3 |
|---|---|---|---|
| English / 英文 | ≥ 3 | ≥ 3 | ≥ 5 |
| Origin language / 原產地語言 | ≥ 1 | ≥ 1 | ≥ 2 |
| Japanese / 日文 | ≥ 0 | ≥ 1 | ≥ 2 |
| Chinese / 中文 | ≥ 0 | ≥ 1 | ≥ 1 |
| **Total / 合計** | | | **≥ 20 valid after URL audit** |
