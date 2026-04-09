# FakeLikes Library

**Versi:** 1.0.0
**Format:** JSON Array
**Jumlah Level:** 8

---

## 📖 Deskripsi

`FakeLikes` adalah library dataset statis yang menyediakan data jumlah *likes* untuk konten berdasarkan ID. Dataset ini dibagi menjadi **8 level** dengan rentang nilai yang berbeda, dirancang untuk simulasi, testing, atau fallback saat API likes utama tidak tersedia.

Setiap level memiliki karakteristik distribusi nilai likes yang berbeda untuk mensimulasikan berbagai skala popularitas konten.

---

## 🎯 Tujuan Penggunaan

| Use Case | Deskripsi |
| :--- | :--- |
| **Development** | Mengisi UI dengan data dummy saat backend belum siap. |
| **Testing** | Simulasi berbagai skala engagement (rendah, sedang, viral). |
| **Fallback** | Placeholder saat endpoint likes production gagal. |
| **Demo/Prototype** | Menampilkan tampilan antarmuka dengan data realistis. |

---

## 📦 Struktur Data

Setiap file JSON memiliki struktur identik: **array of objects**.

```json
[
  {
    "id": 1,
    "likes": 129
  },
  {
    "id": 2,
    "likes": 176
  }
]
```

| Field | Tipe | Deskripsi |
| :--- | :--- | :--- |
| `id` | `integer` | Unique identifier konten (1 - 310). |
| `likes` | `integer` | Jumlah likes (fiktif) untuk konten tersebut. |

---

## 📊 Level & Karakteristik

| Level | Rentang Likes | Karakteristik | Endpoint |
| :--- | :--- | :--- | :--- |
| **Level 1** | 1 - 25 | Engagement sangat rendah | `fakelikes-level-1.json` |
| **Level 2** | 1 - 38 | Engagement rendah | `fakelikes-level-2.json` |
| **Level 3** | 1 - 100 | Engagement sedang-rendah | `fakelikes-level-3.json` |
| **Level 4** | 1 - 200 | Engagement sedang | `fakelikes-level-4.json` |
| **Level 5** | 1 - 300 | Engagement sedang-tinggi | `fakelikes-level-5.json` |
| **Level 6** | 1 - 400 | Engagement tinggi | `fakelikes-level-6.json` |
| **Level 7** | 1 - 498 | Engagement sangat tinggi | `fakelikes-level-7.json` |
| **Level 8** | 1 - 998 | Engagement viral/maksimal | `fakelikes-level-8.json` |

---

## 🔗 Endpoint Raw GitHub

```
https://raw.githubusercontent.com/amnottdevv/news-json-rawcontent-opensource/refs/heads/main/api/lib/fake-likes/fakelikes-level-1.json
https://raw.githubusercontent.com/amnottdevv/news-json-rawcontent-opensource/refs/heads/main/api/lib/fake-likes/fakelikes-level-2.json
https://raw.githubusercontent.com/amnottdevv/news-json-rawcontent-opensource/refs/heads/main/api/lib/fake-likes/fakelikes-level-3.json
https://raw.githubusercontent.com/amnottdevv/news-json-rawcontent-opensource/refs/heads/main/api/lib/fake-likes/fakelikes-level-4.json
https://raw.githubusercontent.com/amnottdevv/news-json-rawcontent-opensource/refs/heads/main/api/lib/fake-likes/fakelikes-level-5.json
https://raw.githubusercontent.com/amnottdevv/news-json-rawcontent-opensource/refs/heads/main/api/lib/fake-likes/fakelikes-level-6.json
https://raw.githubusercontent.com/amnottdevv/news-json-rawcontent-opensource/refs/heads/main/api/lib/fake-likes/fakelikes-level-7.json
https://raw.githubusercontent.com/amnottdevv/news-json-rawcontent-opensource/refs/heads/main/api/lib/fake-likes/fakelikes-level-8.json
```

---

## 🛠️ Panduan Integrasi

### Fetch Data Berdasarkan Level

```javascript
const BASE_URL = 'https://raw.githubusercontent.com/amnottdevv/news-json-rawcontent-opensource/refs/heads/main/api/lib/fake-likes/';

async function fetchFakeLikes(level = 1) {
    const url = `${BASE_URL}fakelikes-level-${level}.json`;
    const response = await fetch(url);
    return response.json();
}
```

### Dapatkan Likes Berdasarkan ID

```javascript
async function getLikesById(id, level = 1) {
    const data = await fetchFakeLikes(level);
    const entry = data.find(item => item.id === id);
    return entry ? entry.likes : 0;
}
```

### Format Angka untuk UI

```javascript
function formatLikes(likes) {
    if (likes >= 1000) return (likes / 1000).toFixed(1) + 'K';
    return likes.toString();
}

// Contoh: formatLikes(998) -> "998"
// Contoh: formatLikes(1500) -> "1.5K"
```

---

## ⚠️ Catatan Penting

| Poin | Keterangan |
| :--- | :--- |
| **Static Data** | Data tidak berubah. Cocok untuk development/testing, bukan production. |
| **ID Range** | Semua file mencakup ID 1 - 310. |
| **Pemilihan Level** | Pilih level sesuai skala engagement yang ingin disimulasikan. |
| **Fallback** | Gunakan sebagai fallback saat API likes utama timeout/error. |

---

## 📂 Struktur Direktori

```
api/
└── lib/
    └── fake-likes/
        ├── fakelikes-level-1.json
        ├── fakelikes-level-2.json
        ├── fakelikes-level-3.json
        ├── fakelikes-level-4.json
        ├── fakelikes-level-5.json
        ├── fakelikes-level-6.json
        ├── fakelikes-level-7.json
        └── fakelikes-level-8.json
```
