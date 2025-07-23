---
title: "LoRa ve E-Ink ile Güçlü Bir Terminal: LilyGO T-Deck Pro İncelemesi"
seoTitle: "T deck pro "
datePublished: Wed Jul 23 2025 05:28:24 GMT+0000 (Coordinated Universal Time)
cuid: cmdfiw3rz000402jlfhjmgbpe
slug: lora-ve-e-ink-ile-guclu-bir-terminal-lilygo-t-deck-pro-incelemesi
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1753248345447/ba73408a-4d2a-49d9-8119-ff66b2109e0b.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1753248483615/b8ab78ef-01ab-4e00-84d8-b12bfdf940bf.png
tags: hacking, cybersecurity-1, lilygo

---

**LILYGO, güçlü kablosuz özellikleri, güç tasarruflu e-kağıt ekranı ve çok yönlü iletişim arayüzlerini kompakt, elde taşınabilir bir form faktöründe birleştiren gelişmiş bir ESP32-S3 tabanlı LoRa mesajlaşma cihazı olan T-Deck Pro'yu** tanıttı . IoT ve şebeke dışı iletişim alanındaki geliştiriciler ve meraklılar için tasarlanan T-Deck Pro, T-Deck Plus'ın temelleri üzerine inşa edilerek ekran, bağlantı ve işlevsellik açısından önemli iyileştirmeler sunuyor.

### **E-Kağıt Ekranı ve Dokunmatik Giriş ile Gelişmiş Tasarım**

T-Deck Pro, **320x240 çözünürlüğe sahip 3,1 inç e-paper ekrana** (GDEQ031T10) ve CST328 çipi aracılığıyla kapasitif **dokunmatik ekran desteğine sahiptir. Önceki 2,8 inç IPS ekrana göre bu yükseltme, yalnızca daha ince bir profil sağlamakla kalmaz, aynı zamanda 1.400 mAh pille bile gelişmiş pil verimliliğine de katkıda bulunur. E-paper teknolojisi , 0,5 saniyeden (kısmi) 3 saniyeye (tam)** kadar değişen yenileme hızlarıyla güneş ışığında üstün okunabilirlik ve daha düşük güç tüketimi sağlar .

![Makale içeriği](https://media.licdn.com/dms/image/v2/D5612AQEofnxXpI21uA/article-inline_image-shrink_1000_1488/B56ZagRI8pGUAQ-/0/1746445571154?e=2147483647&v=beta&t=lDVE8ngl7xw_6Z56NDz7kOUQH24FhKYLZuZ-eQW2vvA align="left")

### **Donanım Özellikleri ve Çok Yönlü Bağlantı**

**ESP32-S3FN16R8 SoC** ile güçlendirilen T-Deck Pro, 240 MHz'e kadar hızlarda çalışan **çift çekirdekli Tensilica LX7 mikrodenetleyici , 8 MB PSRAM** ve **16 MB SPI flash** depolama alanı ve genişletme için bir **MicroSD kart yuvası içerir** . Kablosuz iletişim , **Wi-Fi 4 (802.11n)** ve **Bluetooth 5.0 LE aracılığıyla sağlanırken** , **LoRa desteği SX1262 modülü** aracılığıyla sağlanır ve 868/915 MHz frekanslarını ve +22 dBm'ye kadar Tx gücünü destekler.

Konumlandırma için cihaz, bir **u-blox MIA-M10Q GPS modülü ile donatılmıştır** . İki model seçeneği mevcuttur:

* **Simcom A7682E modemle** donatılmış 4G **LTE versiyonu** .
    
* **PCM5102A ses kodeğine** sahip, daha uygun fiyatlı **, ses odaklı bir versiyon** .
    

### **Ses ve Kullanıcı Arayüzü**

T-Deck Pro, eksiksiz bir ses arayüzü sağlayan **3,5 mm ses jakı** , **mikrofon** ve **hoparlör içerir** . Ses işleme özelliğinin modele göre değiştiği de dikkat çekicidir:

* **4G LTE versiyonunda** ses LTE modem tarafından yönetiliyor.
    
* **PCM5102A versiyonunda** ses işleme ESP32-S3 tarafından gerçekleştiriliyor ve bu, gelecekteki LoRa üzerinden seslendirme uygulamaları için faydalı olabilir.
    

Cihaz , mesajlaşma ve navigasyon için sezgisel bir yazma deneyimi sunan **Texas Instruments TCA8418 tuş takımı denetleyicisini** kullanan **Blackberry tarzı QWERTY klavyeye sahip.**

![Makale içeriği](https://media.licdn.com/dms/image/v2/D5612AQHvSx5t9QygAQ/article-inline_image-shrink_1500_2232/B56ZagRQwlGUAU-/0/1746445603622?e=2147483647&v=beta&t=pty-9dt_Kp6o5TkDj5vqNSL8faaPEHmrLphWn0F0U2o align="left")

### **Ek Özellikler**

Ana yerleşik sensörler arasında **Bosch BHI260AP AI akıllı sensör ve IMU** ve **Lite-on LTR-553ALS ışık sensörü yer alır** ve bu da T-Deck Pro'yu bağlamsal uygulamalar için uygun hale getirir. Diğer önemli özellikler şunlardır:

* Genişletme için **Qwiic konektörü**
    
* **Titreşim motoru**
    
* Güç ve programlama için **USB Type-C bağlantı noktası**
    
* **TP4065B pil şarj IC'si**
    
* **Sıfırla ve Önyükleme düğmeleri**
    
* Kompakt tasarım, boyutları: **120 x 66 x 13,5 mm**
    

### **Geliştirme ve Yazılım Desteği**

**Geliştiriciler, cihazı Arduino IDE** , **PlatformIO** veya **ESP-IDF** kullanarak programlayabilirle[r . LILYGO, **GitH**](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fgithub%2Ecom%2FXinyuan-LilyGO&urlhash=RLiQ&trk=article-ssr-frontend-pulse_little-text-block)[**ub deposunda**](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fgithub%2Ecom%2FXinyuan-LilyGO&urlhash=RLiQ&trk=article-ssr-frontend-pulse_little-text-block) ayrınt[ılı şemalar, ver](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fgithub%2Ecom%2FXinyuan-LilyGO&urlhash=RLiQ&trk=article-ssr-frontend-pulse_little-text-block)i s[ayfaları, donanı](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fgithub%2Ecom%2FXinyuan-LilyGO&urlhash=RLiQ&trk=article-ssr-frontend-pulse_little-text-block)m yazılımı ikili dosyaları ve örnek Ard[uino kodu sağlar](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fgithub%2Ecom%2FXinyuan-LilyGO&urlhash=RLiQ&trk=article-ssr-frontend-pulse_little-text-block) **.** Açık **do**[**nanım** ve **yazılım**](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fgithub%2Ecom%2FXinyuan-LilyGO&urlhash=RLiQ&trk=article-ssr-frontend-pulse_little-text-block) desteği **, T-Deck** [**Pro'yu** yakın gel](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fgithub%2Ecom%2FXinyuan-LilyGO&urlhash=RLiQ&trk=article-ssr-frontend-pulse_little-text-block)ecekte potansiyel **Meshtastic donan**[**ım yazılımı entegr**](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fgithub%2Ecom%2FXinyuan-LilyGO&urlhash=RLiQ&trk=article-ssr-frontend-pulse_little-text-block)**asyonu** da dahil [olmak üzere şeb](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fgithub%2Ecom%2FXinyuan-LilyGO&urlhash=RLiQ&trk=article-ssr-frontend-pulse_little-text-block)eke dışı iletişim projeleri için ideal bir platform haline getirir.

![Makale içeriği](https://media.licdn.com/dms/image/v2/D5612AQGA07asuq8ONg/article-inline_image-shrink_1000_1488/B56ZagRZNRHsAQ-/0/1746445640159?e=2147483647&v=beta&t=_Y9ZXyMJLfQy7wHf-xJ8XJCKtJp0_XDNDMKM1O7i7lI align="left")

### **Fiyatlandırma ve Kullanılabilirlik**

LILYGO T-Deck Pro şu anda satın alınabilir:

* **Sesli versiyon** : [**AliExpress'te 99,98 dolar veya Amazon'**](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Famzn%2Eto%2F4iLYSw9&urlhash=Z4ON&trk=article-ssr-frontend-pulse_little-text-block)[**da 94 dolar**](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Famzn%2Eto%2F4iLYSw9&urlhash=Z4ON&trk=article-ssr-frontend-pulse_little-text-block)
    
* [**4G LTE sürümü** : **AliExpress'te 114,98 dolar**](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Famzn%2Eto%2F4iLYSw9&urlhash=Z4ON&trk=article-ssr-frontend-pulse_little-text-block)
    

[**Cihaz ayrıca resmi LILYGO m**](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Famzn%2Eto%2F4iLYSw9&urlhash=Z4ON&trk=article-ssr-frontend-pulse_little-text-block)[**ağa**](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fs%2Eclick%2Ealiexpress%2Ecom%2Fe%2F_okqjRxR&urlhash=0ibK&trk=article-ssr-frontend-pulse_little-text-block)[**zasında** da listelenmiştir , ancak stok durumu](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Famzn%2Eto%2F4iLYSw9&urlhash=Z4ON&trk=article-ssr-frontend-pulse_little-text-block) [değişebilir.](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fs%2Eclick%2Ealiexpress%2Ecom%2Fe%2F_okqjRxR&urlhash=0ibK&trk=article-ssr-frontend-pulse_little-text-block)

[**Çözüm**](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fs%2Eclick%2Ealiexpress%2Ecom%2Fe%2F_okqjRxR&urlhash=0ibK&trk=article-ssr-frontend-pulse_little-text-block)

[E-kağ](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fs%2Eclick%2Ealiexpress%2Ecom%2Fe%2F_okqjRxR&urlhash=0ibK&trk=article-ssr-frontend-pulse_little-text-block)ıt [dokunmatik ekranı, zengin bağlantı seçene](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Famzn%2Eto%2F4iLYSw9&urlhash=Z4ON&trk=article-ssr-frontend-pulse_little-text-block)[kler](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fs%2Eclick%2Ealiexpress%2Ecom%2Fe%2F_okqjRxR&urlhash=0ibK&trk=article-ssr-frontend-pulse_little-text-block)[i ve modüler tasarımıyla **LILYGO T-Deck Pro,**](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Famzn%2Eto%2F4iLYSw9&urlhash=Z4ON&trk=article-ssr-frontend-pulse_little-text-block) [şebeke dışı iletişim, IoT](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fs%2Eclick%2Ealiexpress%2Ecom%2Fe%2F_okqjRxR&urlhash=0ibK&trk=article-ssr-frontend-pulse_little-text-block) geliştirme ve deneysel [ses uygulamaları için güçlü ve esnek bir platfor](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Famzn%2Eto%2F4iLYSw9&urlhash=Z4ON&trk=article-ssr-frontend-pulse_little-text-block)[m sunar. İster LoRa haberc](https://www.linkedin.com/redir/redirect?url=https%3A%2F%2Fs%2Eclick%2Ealiexpress%2Ecom%2Fe%2F_okqjRxR&urlhash=0ibK&trk=article-ssr-frontend-pulse_little-text-block)i, ister taşınabilir terminal veya sensör merkezi olarak kullanılsın, kompakt ve kablosuz elektronik alanında ileri görüşlü bir adımı temsil eder.

📹 Detaylı video çok yakında YouTube kanalımda olacak.

📦 Ürünü incelemek istersen: [lilygo.cc](https://www.lilygo.cc/)

📲 Bana ulaşmak, içerikleri takip etmek için:

🔗 Instagram: [@ferdibirgull](https://instagram.com/ferdibirgull)

🎥 YouTube: [ferdibirgul](https://youtube.com/@ferdibirgul)

🎯 TikTok: [@ferdibirgull](https://tiktok.com/@ferdibirgull)