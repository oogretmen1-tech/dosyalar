# dosyalar

Dijital Öğretmen sitesinin (https://oogretmen1-tech.github.io) indirilebilir dosya deposu.
Ana depo GitHub Pages 1 GB sınırını aştığı için (5 Kasım 2026) PDF, Word ve diğer büyük dosyalar burada durur.

Yayın adresi: `https://oogretmen1-tech.github.io/dosyalar/<klasör>/<dosya-adı>`

## YÜKLEME KURALLARI (zamanlanmış görevler dahil herkes için)

### Hangi dosya nereye

| Dosya | Depo |
|---|---|
| PDF, Word (.docx), PowerPoint (.pptx), video (.mp4), büyük görseller, zip olmayan diğer indirilebilir dosyalar | **dosyalar** (bu depo) |
| HTML sayfalar, index.html, onizleme-kapaklar.js, istatistik dosyası, küçük ön izleme görselleri | **ana depo** (oogretmen1-tech.github.io) |

- Ana depoya bundan sonra hiçbir PDF, Word, PPTX veya MP4 eklenmez.
- HTML sayfalardaki indirme bağlantıları (Word / PDF düğmeleri, kart bağlantıları, ön izlemeler) tam adresle bu depoyu gösterir:
  `https://oogretmen1-tech.github.io/dosyalar/fasikul/o-sesi-fasikulu.pdf`
- Tek bir HTML sayfası 5 MB'ı geçmesin. İçine gömülen görselleri JPEG/WebP olarak sıkıştır.

### Klasörler

| Klasör | İçerik |
|---|---|
| `fasikul/` | Ses fasikülleri |
| `harf-atolyesi/` | Harf Atölyesi el işi setleri |
| `okuma-kitapcigi/` | Okuma Kitapçığım serisi |
| `degerlendirme/` | Öğrendiklerimizi Değerlendirelim paketleri (1-4. sınıf) |
| `kes-yapistir/` | Kes-Yapıştır Atölyesi etkinlikleri |
| `cedes/` | ÇEDES aylık paketleri |
| `dilimizin-zenginlikleri/` | Dilimizin Zenginlikleri setleri |
| `pano/` | Pano çalışmaları, belirli gün ve haftalar setleri |
| `ogretmen-dosyalari/` | Öğretmen evrakları, planlar, kapaklar |
| `tatil-odevleri/` | Ara tatil ve yaz tatili ödevleri |
| `diger/` | Hiçbirine uymayanlar |

Dosya adları küçük harf, Türkçe karaktersiz, boşluksuz: `n-sesi-fasikulu.pdf`, `1-sinif-degerlendirme-9-13-kasim-2026.docx`.

### Yükleme sırası

1. Depoyu ekle ve klonla: `add_repo` (owner `oogretmen1-tech`, repo `dosyalar`, access `push`), sonra `git clone --depth 1 https://github.com/oogretmen1-tech/dosyalar`.
2. Dosyaları doğru klasöre koy. Her dosya 25 MB'ın altında olsun (PDF'i Ghostscript ile 150 dpi'ye düşürmek yeterli).
3. `git fetch origin main` ve gerekirse rebase, sonra commit ve `main`e push. Büyük dosyaları birkaç commit'e böl. Commit mesajı Türkçe ve kısa.
4. **Önce bu depoya, sonra ana depoya** push et. Böylece sitedeki bağlantı açıldığında dosya hazır olur.
5. Push'tan sonra doğrula: `git log origin/main` ile iki depoda da commit'in olduğunu, ana depodaki her indirme bağlantısının gösterdiği dosya adının bu depoda birebir (büyük/küçük harf dahil) bulunduğunu kontrol et.

### Silme koruması (zorunlu, 7 Kasım 2026)

Kısmi klon (`--no-checkout`, `--filter=blob:none`, sparse) kullanılırken commit yanlışlıkla diğer dosyaları "silinmiş" gösterebilir. Bu iki kez oldu. Her commit'ten sonra ve push'tan önce, **iki depoda da**:

```
git diff --stat --diff-filter=D origin/main HEAD
```

Çıktı boş değilse (yani silinen dosya varsa) **push etme**. Hasan açıkça bir dosyanın silinmesini istemediyse hiçbir dosya silinmez. Düzeltmek için: `git reset --soft origin/main && git read-tree origin/main`, sonra yalnızca yeni/değişen dosyaları `git add` ile ekle ve tekrar kontrol et. Push'tan sonra `git diff --stat origin/main~1 origin/main` ile yalnızca beklenen dosyaların değiştiğini doğrula.

### Push olmazsa

- HTTP 429: 5 saniye bekle, bir kez daha dene. Döngüye sokma.
- HTTP 413: klon eskidir. `git fetch origin main`, rebase, tekrar push.
- Yine olmazsa: dosyaları sohbette **tek tek** gönder (zip yok). Her dosyanın yanına hangi depoya ve hangi klasöre yükleneceğini açıkça yaz, örneğin "dosyalar deposu → fasikul/" veya "ana depo". Nedeni bir satırla söyle.

Hasan yükleme işiyle uğraşmak istemiyor. Yüklemeyi elinden geldiğince kendin yap.
