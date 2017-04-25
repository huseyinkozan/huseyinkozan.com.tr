---
title: Hareketli Qt Izgara Yerleşimi
date: 2012-11-22 00:00:00
tags:
  - "C/C++"
  - Qt
  - "Qt Layout"
---

&nbsp;

{% youtube FLRmCqM-Hn4 %}

Animasyon ile görsel nesneleri hareket ettirmek istediğimizde Qt‘de C++ için hazır bir çözüm bulamıyoruz. Nesnelere hareket verebilmek için kullanabileceğimiz birkaç seçeneğimiz var. Bunlardan biri yerleştirici (Layout) kullanmadan alt nesnelerin geometrilerini elle hesaplamak ve geometri geçişlerinde animasyon kullanmak. Bir diğer yöntem de özel bir yerleştirici yazarak geometri hesabı ve yer değiştirmeyi ona yaptırmak.

<!--more-->

Kodun tekrar kullanılması gerekmediği ve yapılacak görsel etkinliğin (animasyon ile geometri değişimi gibi) genelleştirilmesinin zor olduğu durumlarda yerleştirici içermeyen seçeneği kullanabiliriz. Bu durumda QWidget’tan türeyen ve [QWidget::resizeEvent()](http://doc.qt.io/qt-5/qwidget.html#resizeEvent) fonksiyonunu devralan bir fonksiyon yazarak alt nesneleri uygun şekilde boyutlandırmamız gerekiyor. Geometri geçişlerini sağlamak için de [Animation Framework](http://doc.qt.io/qt-5/animation-overview.html) kullanabiliriz. Bu yöntemle oluşturduğumuz görsel etkinliği başka bir yerde kullanmak istersek kodu kopya-yapıştır yapmak gerekecek ve yeni duruma göre tekrar zaman harcamamız gerekecek.

İkinci yöntemde bahsettiğim yeni bir yerleştirici ile bu işlemin yapılması durumunda kodumuzun tekrar kullanımı oldukça kolaylaşacaktır. Yeni bir yerleştirici yapmak için [QLayout](http://doc.qt.io/qt-5/qlayout.html) sınıfından yeni bir sınıf türetmemiz ve saf sanal (pure virtual) fonksiyonlarını devralmamız gerekiyor. Yeni yerleştirici yapmak için Qt belgelerindeki [Layout Management](http://doc.qt.io/qt-5/layout.html#manual-layout) sayfasına bakabilirsiniz. Sayfada bulabileceğiniz iki örnek yerleştirici bulabilirsiniz. Ayrıca Qt kaynak kodlarındaki temel yerleştiricilere de bakmak oldukça faydalı olacaktır.

Şirketimizde geliştirdiğimiz [microCOR Ekg Yazlımında](http://infron.com.tr/microcor-ekg-cihazi/bilgisayar-yazilimi/) kullandığımız ızgara şeklindeki Ekg grafiklerinin (bu şekle Ekg Görünümü diyoruz) daha iyi değerlendirilebilmesi için sadece bir grafiğe odaklanılmasını sağlıyoruz (buna da Kanal Görünümü diyoruz). Ekg Görünümünden Kanal Görünümüne geçişte basit bir şekilde ilgilenilmeyen grafikleri gizliyorduk. Görünen tek kanal grafik de Qt’nin yerleştirici sistemi sayesinde ana nesneyi kaplıyor ve büyütülmüş oluyordu. Kanal görünümüne yapılan bu geçişte ve Ekg Görünümüne geri dönüşünde kullanıcıya görsel ve mantıksal ilişkiyi sağlamak oldukça zorlaşıyordu. Geçişin daha rahat algılanabilmesi için animasyon yapan bir yerleştiriciye ihtiyacımız vardı. Bunun gibi bir yerleştirici gerektiğinde benim de faydalandığım kaynaklar yukarıda bahsettiğim Qt belgeleri ve kaynak kodları oldu.

QAnimatedGridLayout yerleştiricisi içine yerleştirilen nesneleri ızgara şeklinde yerleştiriyor ve ızgaradaki seçilen bir nesnenin ana nesneyi kaplanmasını sağlayabiliyor. Görünmemesi gereken diğer ızgara nesnelerini de ana nesnenin (veya belirtilen başka bir nesnenin) görünen alanının dışına taşıyarak gizlenmelerini sağlıyor. Bu taşıma ve büyütme işlemlerini de [Animation Framework](http://doc.qt.io/qt-5/animation-overview.html) kullanarak yapıyor. Animasyon tipi [QEasingCurve](http://doc.qt.io/qt-5/qeasingcurve.html) ile, geçiş süresi de bir fonksiyon ile belirlenebiliyor.

QAnimatedGridLayout kodlarını ve örnek bir programın içinde nasıl kullanıldığını görmek için [github.com/huseyinkozan/QAnimatedGridLayout](https://github.com/huseyinkozan/QAnimatedGridLayout) sayfasına bakabilirsiniz. Aşağıda da animasyonun nasıl çalıştığını gösteren bir ekran kaydı bulabilirsiniz.
