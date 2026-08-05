# 📋 Referensi Model Gratis — Free Claude Code (fork Infron + Puter)

> Diperbarui: 5 Agustus 2026 · Status server: `http://127.0.0.1:8082` (sehat)

Dua jalur gratis yang tersedia di fork ini:

| Provider | Key | Syarat | Status Anda |
|---|---|---|---|
| **Infron** (`infron/`) | `INFRON_API_KEY` | Saldo akun **≥ $5** (model `:free` **tidak memotong kredit**) | 🟡 Tinggal top-up $5 di [infron.ai/dashboard/credits](https://infron.ai/dashboard/credits) |
| **Puter** (`puter/`) | `PUTER_API_KEY` (token gratis dari [puter.com/dashboard](https://puter.com/dashboard)) | Free **monthly allowance** (dipakai habis = 402) | 🔴 Kuota bulanan habis — reset otomatis tiap bulan |

---

## 1️⃣ Infron — 11 Model `:free` (GRATIS murni setelah saldo $5)

Model berakhiran `:free` **tidak memotong kredit** — saldo $5 hanya gerbang anti-spam.
Format untuk FCC: **`infron/<model-id>`**

| # | Model (id untuk FCC) | Vendor | Catatan |
|---|---|---|---|
| 1 | `infron/deepseek/deepseek-v4-pro:free` ⭐ | DeepSeek | **Terbaik untuk coding** — dipakai default |
| 2 | `infron/deepseek/deepseek-v4-flash:free` | DeepSeek | Ringan & cepat — cocok tier haiku |
| 3 | `infron/moonshotai/kimi-k2.6:free` | Moonshot AI | Kimi K2.6 — kuat untuk coding/reasoning |
| 4 | `infron/minimax/minimax-m2.7:free` | MiniMax | Model generasi terbaru |
| 5 | `infron/minimax/minimax-m2.5:free` | MiniMax | |
| 6 | `infron/qwen/qwen3.6-plus:free` | Alibaba Qwen | Bagus untuk bahasa & coding |
| 7 | `infron/inclusionai/ling-3.0-flash:free` | Inclusion AI | |
| 8 | `infron/mindai/macaron-v1-venti:free` | Mind AI | |
| 9 | `infron/poolside/laguna-s-2.1:free` | Poolside | Fokus coding |
| 10 | `infron/sapiens-ai/agnes-2.0-flash:free` | Sapiens AI | |
| 11 | `infron/xiaomi/mimo-v2.5:free` | Xiaomi | |

💡 Total 456 model di Infron (berbayar via kredit) + 11 gratis. Endpoint: `llm.onerouter.pro/v1` (OpenAI-compat).

---

## 2️⃣ Puter — Model Gratis

### 🟢 A. GRATIS MURNI (cost = $0/1M token — tidak memotong kuota)

Semua dari **Z.ai (GLM)**. Format: **`puter/<model-id>`**

| Model (id untuk FCC) | Context | Tools | Catatan |
|---|---|---|---|
| `puter/zai/glm-4.5-flash` | 128K | ✅ | ✅ Terverifikasi jalan |
| `puter/zai/glm-4.7-flash` | 200K | ✅ | Terbaru |
| `puter/zai/glm-4.6v-flash` | 128K | ✅ | Vision |
| `puter/zai/autoglm-phone-multilingual` | 4K | ✅ | Context kecil |

⚠️ **Penting GLM:** butuh `max_tokens` cukup besar — dengan budget kecil (mis. 100 token) model balas **kosong** karena reasoning internal memakan semua token.

### 🟡 B. Via Free Monthly Allowance (cost > 0, ditanggung kuota bulanan)

Model populer — dipakai seperti gratis sampai kuota bulanan habis (lalu 402 `No usage left`):

| Model (id untuk FCC) | Context | Harga/1M (in/out) |
|---|---|---|
| `puter/deepseek-v4-pro` | 1M | murah |
| `puter/deepseek-v3.2` | 1M | murah |
| `puter/claude-opus-4-6` | 1M | $5 / $25 (boros!) |
| `puter/claude-opus-5` | 1M | $5 / $25 |
| `puter/claude-sonnet-5` | 1M | $3 / $15 |
| `puter/claude-sonnet-4-6` | 1M | $3 / $15 |
| `puter/claude-haiku-4-5` | 200K | $1 / $5 (hemat) |
| `puter/claude-fable-5` | 1M | $10 / $50 |
| `puter/gpt-5.5` / `puter/gemini-3.5` / `puter/grok-4.5` / `puter/kimi-k2.6` | — | — |

⚠️ **Puter tidak punya endpoint daftar model** (`/models` → 404) — semua model harus diketik manual.

---

## 3️⃣ Cara Ganti Tier (Routing Model)

### Format model
Selalu `provider-id/model-id`, contoh: `infron/deepseek/deepseek-v4-pro:free`, `puter/claude-opus-4-6`.

### Mapping tier Claude Code → env var

| Tier Claude Code | Env var | Konfigurasi aktif saat ini |
|---|---|---|
| *(fallback)* | `MODEL` | `infron/deepseek/deepseek-v4-pro:free` |
| fable | `MODEL_FABLE` | `infron/moonshotai/kimi-k2.6:free` |
| opus | `MODEL_OPUS` | `infron/deepseek/deepseek-v4-pro:free` |
| sonnet | `MODEL_SONNET` | `infron/deepseek/deepseek-v4-pro:free` |
| haiku | `MODEL_HAIKU` | `infron/deepseek/deepseek-v4-flash:free` |

> Atur tier ke **None** (kosongkan) agar memakai `MODEL` (fallback).

### 🖥️ Cara 1 — Admin UI (paling mudah, tanpa edit file)

1. Buka **`http://127.0.0.1:8082/admin`** di browser
2. Tab **Providers** → isi key (`INFRON_API_KEY` / `PUTER_API_KEY`) → **Apply**
3. Tab **Model Config** (atau Models) → pilih model per tier dengan format `<provider>/<model-id>`
4. **Apply** — settings langsung tersimpan (ke `~/.fcc/.env`) & server reload

### 📝 Cara 2 — Edit `.env` manual

Edit **dua file** (yang kedua menimpa yang pertama):
- `D:\Project\free-claude-code\.env`
- `C:\Users\<Anda>\.fcc\.env` ← **file inilah yang paling berpengaruh**

```bash
MODEL=infron/deepseek/deepseek-v4-pro:free
MODEL_OPUS=infron/deepseek/deepseek-v4-pro:free
MODEL_SONNET=infron/deepseek/deepseek-v4-pro:free
MODEL_HAIKU=infron/deepseek/deepseek-v4-flash:free
MODEL_FABLE=infron/moonshotai/kimi-k2.6:free
```

Lalu **restart server** (PowerShell):

```powershell
Get-NetTCPConnection -LocalPort 8082 -State Listen | Select-Object -ExpandProperty OwningProcess | ForEach-Object { Stop-Process -Id $_ -Force }
cd D:\Project\free-claude-code
uv run fcc-server
```

### 🚀 Pakai dari Claude Code CLI

```powershell
cd D:\Project\free-claude-code
uv run fcc-claude                    # default (MODEL)
uv run fcc-claude --model opus       # paksa tier opus
uv run fcc-claude --model haiku      # tier haiku (hemat)
```

---

## 4️⃣ Tips & Troubleshooting

- **402 `No usage left` (Puter)** → kuota bulanan habis. Tunggu reset, atau pindah ke Infron `:free` (perlu saldo ≥ $5).
- **429 `Free model requires account balance greater than $4.999999` (Infron)** → top-up $5 di [infron.ai/dashboard/credits](https://infron.ai/dashboard/credits). Model `:free` lalu jalan tanpa memotong kredit.
- **Opus di Puter sangat boros kuota** ($25/1M output) — pakai `--model haiku`/`sonnet` untuk tugas ringan.
- **GLM di Puter balas kosong** → naikkan `max_tokens`.
- Server log: `C:\Users\<Anda>\.fcc\logs\server.log`
