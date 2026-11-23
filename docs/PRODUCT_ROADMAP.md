# KODLAMATIC — Ürün Yol Haritası

## Ürün amacı
CNC torna atölyelerinin teknik resim ve parça tariflerinden üretim hazırlığını hızlandıran, Türkçe çalışan ve makineye özel doğrulama süreçlerini destekleyen abonelik tabanlı bir üretim asistanı.

## Kullanıcı profilleri
- CNC operatörü: parça ve tezgâh bilgilerini girer, hazırlık önerilerini inceler.
- Programcı / üretim mühendisi: operasyon sırası, takım ve kesme parametrelerini düzenler.
- Atölye yöneticisi: ekip, makineler, işler ve abonelikleri yönetir.

## Aşamalı geliştirme

### Aşama 0 — Sağlam temel (mevcut)
- React + TypeScript + Vite arayüzü
- GitHub ana kaynak kod deposu
- Her değişiklikte otomatik üretim derlemesi
- Gerçek G-kod üretiminin prototipte kapalı tutulması

### Aşama 1 — İş emri ve parça bilgi toplama
- Parça adı / iş emri numarası (isteğe bağlı)
- Teknik resim ve model dosyası yükleme
- Malzeme, ham parça ölçüleri, bitmiş ölçüler
- Tezgâh, kontrol ünitesi, ayna ve takım bilgileri
- Operasyon seçimi ve kullanıcı notları
- Eksik / çelişkili ölçüleri tahmin etmek yerine kullanıcıya sorma
- Girilen bilgileri düzenlenebilir iş kartı olarak gösterme

### Aşama 2 — Hesaplama ve üretim hazırlığı
- Birim ve ölçü tutarlılığı kontrolleri
- Temel torna geometrisi için deterministik hesaplama modülü
- Kesme hızı, devir, ilerleme ve paso hesaplayıcıları
- Malzeme ve takım veri tabloları; kaynak ve revizyon bilgisi
- Hesap sonuçlarının varsayımlarını açıkça gösterme
- Otomatik önerileri kullanıcı onayına sunma

### Aşama 3 — Teknik resim / model anlama
- PDF ve raster çizimlerden ölçü ve görünüş çıkarımı
- DXF geometrisi için ayrı, test edilebilir içe aktarma modülü
- STEP dosyaları için sunucu tarafı geometri işleme
- Ölçü çıkarımlarında güven seviyesi ve kullanıcı teyidi
- Belirsiz geometriyi sessizce tamamlamama

### Aşama 4 — CAM ve doğrulama
- Takım yolu üretimi için ayrı CAM/geometri motoru
- Stok, ayna, takım, tutucu ve taret modellemesi
- Makine limitleri ve çarpışma kontrolleri
- Simülasyon ve doğrulama raporu
- Kontrol ünitesine özel postprocessor
- G-kod çıktısı yalnızca doğrulama ve yetkili kullanıcı onayından sonra

### Aşama 5 — SaaS ve ticari işletim
- Kullanıcı hesabı, ekip ve rol yönetimi
- Atölye / firma bazlı veri ayrımı
- Abonelik, kullanım kotası ve faturalandırma entegrasyonu
- İş geçmişi, sürümleme, denetim kayıtları
- Yedekleme, dışa aktarma ve hesap kapatma süreçleri
- Türkçe arayüz; mimariyi çoklu dile hazır tutma

## Güvenlik ilkeleri
1. Yapay zekâ tek başına makineye çalıştırılabilir G-kod göndermez.
2. Bilinmeyen ölçü, takım, sıfır noktası veya tezgâh parametresi varsayılmaz.
3. Üretilen her öneri kullanılan girdileri, varsayımları ve birimleri gösterir.
4. G-kod üretimi; geometri, CAM, postprocessor, simülasyon ve uzman onayı olmadan etkinleştirilmez.
5. Her iş ve çıktı geriye dönük izlenebilir olmalıdır.

## Teknik mimari ilkeleri
- GitHub özel deposu kaynak kodun ana ve yetkili kopyasıdır.
- Arayüz, iş mantığı, geometri/CAM ve postprocessor katmanları birbirinden ayrılır.
- Kimlik doğrulama ve kalıcı veri için ayrı KODLAMATIC Supabase projesi oluşturulmadan mevcut başka projelerin veritabanı kullanılmaz.
- Gizli anahtarlar istemci koduna veya GitHub deposuna konulmaz.
- Harici AI servisleri yalnızca sunucu tarafı üzerinden, kontrollü ve kayıt altına alınmış isteklerle çağrılır.
- Önce ücretsiz / düşük maliyetli geliştirme ve test; ücretli servisler gerçek ihtiyaç ortaya çıktığında.

## Şu anki durum
Mevcut uygulama yalnızca arayüz prototipidir. Teknik resim geometrisi analiz etmez, CAM takım yolu oluşturmaz, gerçek G-kod üretmez ve CNC tezgâhına bağlanmaz.
