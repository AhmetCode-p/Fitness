# Forge — Haftalık Antrenman Programı

Forge, haftalık antrenman programlarını oluşturmanı, takip etmeni ve tek bir kod ile paylaşmanı sağlayan, tamamen tarayıcıda çalışan (sunucusuz) bir fitness uygulamasıdır.

## Özellikler

- **7 günlük program sihirbazı**: Her güne kas grubu (etiket) ve hareketler ekleyerek kolayca program oluşturma.
- **Antrenman takibi**: Hareket başına yapıldı (checkbox) ve kg girişi; program ilerlemesi otomatik kaydedilir.
- **Program kodları**: Programı tek satırlık sıkıştırılmış bir koda dönüştürür. Kodu paylaşan kişi, sitede yapıştırıp 1 saniyede programı yükler.
- **Sağlam paylaşım**: Kodlar LZ sıkıştırma + özel alfabe ile kısaltılır ve `checksum` ile korunur — kopyalamada bozulan kod anında yakalanıp kullanıcıya net uyarı verilir.
- **Geriye dönük uyumluluk**: Eski formatlardaki kodlar (`ANT1.`, `ANT2.`, `ANT4.`) da açılmaya devam eder.
- **Veri saklama**: Tüm programlar ve ilerlemeler tarayıcının `localStorage`'ında tutulur (hesap gerektirmez, veri cihazdan çıkmaz).

---

## Hızlı Başlangıç

Proje sunucusuzdur; tek yapman gereken HTML dosyalarını tarayıcıda açmak veya GitHub Pages üzerinden yayınlamak.

```
https://ahmetcode-p.github.io/Forge/forgev1.html
```

### Program oluştur

1. `Forgev1.html` dosyasını aç.
2. Her gün için kas grubunu ve hareketleri gir (isim, set, tekrar).
3. **"Bitir & Oluştur"** de — program kaydedilir.

### Programı takip et

- Hareketin yanındaki kutuyu işaretleyerek yaptığın setleri kaydet.
- Her hareketin yanına çalıştığın kiloyu yaz.
- **"Tumunu Sifirla"** ile haftalık ilerlemeyi temizle.

### Programı paylaş

1. Program açıkken alttaki kodu **"Kopyala"** ile kopyala.
2. Kod uzunluğu genelde ~680 karakterdir. Mail/WhatsApp gibi uygulamalardan paylaş**:

```

3. Karşı taraf linkteki kodu seçip kopyalar, sitede **"Program kodu"** kutusuna yapıştırır ve **"Kodu Ac"** der.

---

## Kod Sistemi (nasıl çalışır)

Program, JSON olarak LZ ile sıkıştırılır ve özel bir alfabeyle (URL-güvenli `A-Z a-z 0-9 - _ . ~`) paketlenir. Böylece kod hem çok kısa hem de her ortamda (link, mesaj, not) bozulmadan taşınır.

| Format | Açıklama |
|--------|----------|
| `ANT1.` | İlk sürüm — düz base64 (2100+ karakter) |
| `ANT2.` | LZ + base64 ile sıkıştırılmış |
| `ANT4.` | LZ + özel alfabe (URL-güvenli, ~680 karakter) |
| `ANT5.` | ANT4 + sağlamlık kontrolü (checksum) — güncel |

Sıkıştırma kazanımı (örnek 4 gün / 22 hareketlik program):

```
ANT1:  2101 karakter
ANT2:   805 karakter
ANT4:   681 karakter
ANT5:   683 karakter
```

---

## Dosyalar

| Dosya | Açıklama |
|-------|----------|
| `antrenmanv5.html` | Ana uygulama: program oluşturucu + takipçi + kod paylaşımı |
| `kod.txt` | Paylaşıma hazır örnek program kodu (ANT5) |
| `Program Kodu.txt` | Örnek kodun yerel kopyası |

---

## Teknolojiler

- Saf HTML + CSS + JavaScript (harici framework yok)
- [lz-string](https://github.com/pieroxy/lz-string) — LZ tabanlı sıkıştırma (gömülü)
- `localStorage` — veri saklama
- GitHub Pages — yayınlama

---

## Not

Tüm veriler tarayıcıda saklandığı için tarayıcı verilerini temizlemek programları siler. Önemli programların kodlarını `kod.txt` gibi bir yerde saklamanı öneririz — kodu tekrar yapıştırınca program geri gelir.
