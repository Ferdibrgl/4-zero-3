---
title: "T-Watch S3 Plus İncelemesi: 2.4 GHz LoRa Destekli Giyilebilir IoT Platformu"
datePublished: Wed Jul 23 2025 05:49:44 GMT+0000 (Coordinated Universal Time)
cuid: cmdfjnjok000j02jogjvlae4l
slug: t-watch-s3-plus-incelemesi-24-ghz-lora-destekli-giyilebilir-iot-platformu
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1753249763964/ca7afde4-d538-45bd-b1a9-4a89137b7832.png

---

Giyilebilir cihazlar, artık sadece saat veya bileklik olmanın ötesine geçti. LILYGO’nun geliştirdiği T-Watch S3 Plus, donanım meraklıları ve geliştiriciler için hem taşınabilir hem de özelleştirilebilir bir platform sunuyor. Özellikle 2.4 GHz frekansında çalışan SX1280 LoRa modülü, cihazı LoRa tabanlı iletişim projeleri için oldukça cazip hale getiriyor.

**🚀 Genel Bakış**

T-Watch S3 Plus, ESP32-S3 işlemci tabanlı, 2.4 GHz LoRa destekli, renkli dokunmatik ekranlı ve açık kaynak yazılım uyumlu bir akıllı saat formunda geliştirme kartı.

Geliştiriciler için tasarlanan bu cihaz; LoRa mesajlaşma, sensör verisi toplama, offline haberleşme ve daha fazlasını sağlayan bir IoT çözümü olarak öne çıkıyor.

**🔧 Donanım Özellikleri**

* Ekran: 1.54” IPS renkli dokunmatik ekran (240x240)
    
* İşlemci: ESP32-S3 (çift çekirdekli LX7, 240 MHz)
    
* Hafıza: 16 MB Flash + 8 MB PSRAM
    
* Bağlantı: Wi-Fi 4, Bluetooth 5.0 LE, 2.4 GHz LoRa (SX1280)
    
* Sensörler:  
    
    * Bosch BMA423 ivmeölçer
        
    * QMI8658C IMU
        
    * RTC, ışık sensörü
        

* Batarya: 450 mAh Li-Po (USB Type-C üzerinden şarj)
    
* Ekstralar: Titreşim motoru, dokunmatik ekran, AXP2101 güç yönetimi
    

**📡 2.4 GHz LoRa Özelliği**

Geleneksel 433/868/915 MHz LoRa modüllerinin aksine, T-Watch S3 Plus, SX1280 modülü sayesinde 2.4 GHz LoRa, FLRC ve GFSK gibi iletişim protokollerini destekler. Bu da daha yüksek veri hızı ve LoRa protokolünü Wi-Fi yoğun ortamlarda bile kullanabilme avantajı sağlar.

Özellikle Meshtastic 2.4 GHz sürümü, bu cihazda doğrudan denenebiliyor.

**💡 Geliştirme ve Yazılım**

Cihaz aşağıdaki geliştirme ortamlarını destekliyor:

* Arduino IDE
    
* PlatformIO
    
* ESP-IDF
    

LilyGO’nun GitHub sayfasında detaylı donanım şemaları, örnek projeler ve firmware dosyaları yer alıyor.

**🎯 Uygulama Senaryoları**

* LoRa üzerinden offline mesajlaşma saati
    
* Giyilebilir veri logger (IMU, ivmeölçer verisiyle)
    
* IoT cihazları için mobil kontrol arayüzü
    
* Adım sayar, gesture kontrol cihazı
    

**💰 Fiyat ve Satın Alma**

Cihaz, model ve satıcıya göre yaklaşık 59 – 69 USD fiyat aralığında bulunabiliyor.

Satın almak istersen:

🔗 [LilyGO Resmi Site](https://www.lilygo.cc/)

**🧪 Kişisel Deneyim**

Cihazı elime aldığım andan itibaren geliştirici dostu yapısını hissettirdi. 2.4 GHz LoRa testleri, ESP32-S3 ile yazılım esnekliği ve dokunmatik ekran entegrasyonu beni oldukça etkiledi. Özellikle Meshtastic gibi açık kaynak projelerde giyilebilir bir cihazla iletişim kurmak çok güçlü bir deneyim sunuyor.

**📲 Beni Takip Et:**

🛠 Daha fazla teknik içerik, donanım incelemesi ve proje için:

* Instagram: [@ferdibirgull](https://instagram.com/ferdibirgull)
    
* YouTube: [ferdibirgul](https://youtube.com/@ferdibirgul)
    
* TikTok: [@ferdibirgull](https://tiktok.com/@ferdibirgull)
    

T-Watch S3 Plus gibi cihazlar, sadece bir donanım değil, aynı zamanda açık kaynak geliştiriciler için yepyeni projelerin kapısını açan birer araç. Yakında bu cihazla yaptığım LoRa mesajlaşma ve sensör senaryolarını da paylaşacağım. Takipte kal!