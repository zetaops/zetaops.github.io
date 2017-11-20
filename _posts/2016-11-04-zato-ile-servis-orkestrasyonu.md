---
layout: post
title: Zato ile Servis Orkestrasyonu
author: Ali Riza Keles
---

Mikro servisler dünyasinda yaşıyoruz. İrili ufaklı projelerde bir veya birden çok servis ile konuşmak ihtiyacı duyuyoruz. Bunlar kimi zaman REST, SOAP gibi web servisleriyken, kimi zaman bir iş kuyruğu yöneticisi, bir log servisi veya bir veritabanı, kimi zaman da bir bildirim servisi (smtp, sms etc..) olabiliyor. Her geçen gün daha fazla sayıda işlevsellik servis şeklinde tüketilebilir hale geldikçe, bu servislerin yönetimi de oldukça önemli bir problem haline geliyor.

Öte yandan başka bir problem de kendi uygulamamızın yeniden kullanılabilir, anlamlı parçalara bölünüp birbirleri arasında veri alışverişinin düzenlenmesi ve gerektiğinde bu parçalar tarafından üretilen verilerin 3. taraflar ile güvenli bir şekilde paylaşılmasıdır. Özetle servisleştirilmiş iç veya dış uygulama parçaları arasındaki orkestrasyon kritik bir hal almaktadır.

Zato projesi, bu servisler dünyasında, Python severlerin büyük bir eksiğini tamamlamaya adamış kendisini. Türlü çeşit servislerin ortasinda durup, sizin isteklerinize göre bu servilerin orkestrasyonu işini yapıyor. Kendisini Enterprise Service Bus (Kurumsal Veri Yolu) uygulaması olarak tarif ediyor. Fakat tanıdıkça, yeteneklerini keşfettikçe bambaşka ihtiyaçlar için kullanılabilir olduğunu farkediyorsunuz.

Zato GPL ile dağıtılan özgür bir yazılım. Python ile geliştiriliyor. Bu yazının yazıldığı Şubat 2016 itibariyle 2.0.7 sürümünde ve kararlı bir şekilde çalşıyor. Birçok platformda kurulabilir. Daha baştan ölçeklenebilir bir mimari tercih edilmiş. Clustera ekleyeceğiniz yeni üyelerle kolayca ölçeklenebiliyor.

Zato birçok kaynak ile konuşabiliyor. HTTP, REST, Soap, AMQP, Solr, ElasticSearch, Cassandra, Pub/Sub, Smtp, Imap, S3, OpenStack Swift, ve daha birçok protokol ve standart ile konuşabilme yeteneğine sahip. Tam bir listeyi dökümantasyonunda bulmak mümkün.

Kullanım Örnekleri
Uygulamanızı çalışması için ihtiyaç duyduğu 3. taraf servislere erişim
Uygulamanın parçaları arasındaki iletişim
Uygulamanın 3. taraflara açılacak servislere bölünmesi
İç veya dış servisler arasında farklı veri yapıları arasında uyumluluk için dönüşüm
Bağlanacağınız kaynakların yetkilendirme seçenekleri de destekleniyor. Siz bu kaynaklara erişirek kendi servislerinizi oluşturuyorsunuz ve uygulamalarınızdan bu servisler aracılığı ile kaynaklara erişiyorsunuz.

http://www.ulakbus.org/wiki/zato_doc.html

http://www.ulakbus.org/wiki/zato_ipuclari.html
