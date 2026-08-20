# Forge — Haftalık Antrenman Programı

Forge, haftalık antrenman programlarını oluşturmanı, takip etmeni, istatistiklerini görmen ve tek bir kod ile paylaşmanı sağlayan, tamamen tarayıcıda çalışan (sunucusuz) bir fitness uygulamasıdır.

## Özellikler

- **Hoş geldin ekranı**: İlk açılışta animasyonlu FORGE karşılama ekranı — kod girişi, "Plan Olustur" ve "Plan Okuyucu" butonları.
- **7 günlük program sihirbazı**: Her güne kas grubu (etiket) ve hareketler ekleyerek kolayca program oluşturma. Boş günler **dinlenme günü** olarak işaretlenir.
- **TR / EN arayüz**: Sol üstteki geçişle Türkçe / İngilizce dil seçimi.
- **Antrenman takibi**: Hareket başına yapıldı (checkbox) ve kg girişi; program ilerlemesi otomatik kaydedilir.
- **Haftalık otomatik sıfırlama**: Tüm tikler her **Pazartesi** kendiliğinden sıfırlanır; kg değerlerine dokunulmaz.
- **İstatistikler**: Kod alanının altındaki "İstatistikler" butonuyla haftalık / aylık tamamlanma oranları, gün gün / hafta hafta / ay ay grafikler ve harekete tıklayınca haftalık **kilo artışı** grafiği.
- **Program kodları**: Programı tek satırlık sıkıştırılmış bir koda dönüştürür. Kodu paylaşan kişi, sitede yapıştırıp 1 saniyede programı yükler.
- **QR ile paylaşım**: Paylaş butonu; QR kod + cihaz paylaşımı (WhatsApp, mail vb.) + kopyalama seçenekleri sunan bir modal açar.
- **Sağlam paylaşım**: Kodlar LZ sıkıştırma + özel alfabe ile kısaltılır ve `checksum` ile korunur — kopyalamada bozulan kod anında yakalanıp kullanıcıya net uyarı verilir.
- **Geriye dönük uyumluluk**: Eski formatlardaki kodlar (`ANT1.`, `ANT2.`, `ANT4.`) da açılmaya devam eder.
- **Veri saklama**: Tüm programlar, ilerlemeler ve istatistik geçmişi tarayıcının `localStorage`'ında tutulur (hesap gerektirmez, veri cihazdan çıkmaz).
- **Modern arayüz**: Liquid Glass efekti, yumuşak köşeler, DM Sans yazı tipi ve buton animasyonları.

---

## Hızlı Başlangıç

Proje sunucusuzdur; tek yapman gereken HTML dosyalarını tarayıcıda açmak veya GitHub Pages üzerinden yayınlamak.

```
https://ahmetcode-p.github.io/Forge/forgev1.html
```

### Program oluştur

1. `forgev1.html` dosyasını aç.
2. Hoş geldin ekranında **"Plan Olustur"** de.
3. Her gün için kas grubunu ve hareketleri gir (isim, set, tekrar).
4. **"Bitir & Olustur"** de — program kaydedilir.

### Programı takip et

- Hareketin yanındaki kutuyu işaretleyerek yaptığın setleri kaydet.
- Her hareketin yanına çalıştığın kiloyu yaz.
- Tikler her Pazartesi otomatik sıfırlanır; kilolar kalır.

### İstatistikleri gör

1. Kod alanının altındaki **"İstatistikler"** butonuna tıkla.
2. **Haftalık / Aylık** sekmelerinden tamamlanma oranı grafiklerini gör.
3. **Hareketler** sekmesinde bir harekete tıkla — haftalık kilo artışı grafiği açılır.

### Programı paylaş

1. Program açıkken alttaki **"Paylas"** butonuna tıkla.
2. QR kodu telefonla tarat, **"Cihazdan Paylas"** (WhatsApp, mail vb.) ile gönder veya **"Kopyala"** ile kodu al.
3. Karşı taraf kodu sitedeki **"Program kodu"** kutusuna yapıştırır ve **"Kodu Ac"** der.

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
| `forgev1.html` | Ana uygulama: program oluşturucu + takipçi + istatistikler + kod paylaşımı |
| `manifest.json` | PWA tanımı (mobil ana ekran simgesi ve tema rengi) |
| `favicon.png` | Tarayıcı sekmesi logosu |
| `icon.png` | Mobil ana ekran simgesi |
| `kod.txt` | Paylaşıma hazır örnek program kodu (ANT5) |
| `Program Kodu.txt` | Örnek kodun yerel kopyası |

---

## Teknolojiler

- Saf HTML + CSS + JavaScript (harici framework yok)
- [lz-string](https://github.com/pieroxy/lz-string) — LZ tabanlı sıkıştırma (gömülü)
- [api.qrserver.com](https://goqr.me/api/) — QR kod üretimi
- `localStorage` — veri saklama
- GitHub Pages — yayınlama

---

## Not

Tüm veriler tarayıcıda saklandığı için tarayıcı verilerini temizlemek programları siler. Önemli programların kodlarını `kod.txt` gibi bir yerde saklamanı öneririz — kodu tekrar yapıştırınca program geri gelir.