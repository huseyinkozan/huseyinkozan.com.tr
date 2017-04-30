---
title: Sabit Oranlı Qt Yerleşimi
date: 2009-07-22 00:00:00
tags:
  - "C/C++"
  - Qt
  - "Qt Layout"
category:
  - Qt
---

Qt4 ile sabit oranlı bir layout doğrudan desteklenmiyor. Sabit oranlı bir layout yapabilmek için QLayout’dan yeni bir sınıf türetmemiz gerekiyor. Türetme işlemi yapılırken orantı ile ilgili olmayan, fakat layout a nesne ekleyip çıkarabimek için bazı fonksiyonları da devralmamız gerekiyor.

Nokia forumlarında geçen** yazıda bu işlemi ayrıntılı olarak açıklanmış. Yazıda merkeze konan tek bir kare nesne için bir layout tasarımı gösterilmiş. Yapılan bu tasarımı altın oranı veya A4 oranını sağlayacak şekile getirebilmek için birkaç fonksiyon ekledim.

** Kırık olan bağlantı şu şekilde:
http://wiki.forum.nokia.com/index.php/CS001309_-_Maintaining_square_form_for_a_widget_in_Qt

* {% asset_link FixedRatioExample.zip FixedRatioExample.zip %} : Kaynak kodu.
