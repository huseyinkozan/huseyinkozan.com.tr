---
title: QtCreator Klavye Sorunu
date: 2014-05-17 00:00:00
update: 2017-04-30 00:00:00
tags:
  - Qt
  - Qt Creator
category:
  - Qt
---

Qt5.3.0-RC ile gelen Qt Creator’ı kullanmak istediğimde klavyem çalışmadı. Sebebini araştırdığımda libxkbcommon kitaplığından kaynaklandığını ve bu sürümde çözülmüş olmasını gerektiğini düşünerek [QTBUG-32760][1] hata kaydına durumu raporladım.

Konu ile ilgili yeni bir hata kaydı açmam istenince birkaç deneme yaparak [QTBUG-38946][2] hata kaydına klavyemin çalışmasını sağlayan durumu da raporladım. Klavye sorununu çözmek için programı çalıştırmadan önce aşağıdaki gibi komut satırından yerel ayarlarını vererek başlatabilirsiniz;
{% codeblock lang:bash %}
$ LANG=en_US.UTF-8 [kurulum_dizini]/Qt5.3.0/Tools/QtCreator/bin/qtcreator.sh
{% endcodeblock %}

<!-- more -->

Ubuntudaki başlatma simgesini değiştirmek için de simge dosyasını metin düzenleyici ile açarak parametreyi ekleyebilirsiniz. Gedit ile simge dosyasını açalım:
{% codeblock lang:bash %}
$ gedit .local/share/applications/DigiaQtOpenSource-qtcreator.desktop
{% endcodeblock %}

Dosyayı açtıktan sonra şu satırı
{% codeblock lang:bash %}
Exec=[kurulum_dizini]/Qt5.3.0/Tools/QtCreator/bin/qtcreator
{% endcodeblock %}

Şununla değiştirelim
{% codeblock lang:bash %}
Exec=env LANG=en_US.UTF-8 [kurulum_dizini]/Qt5.3.0/Tools/QtCreator/bin/qtcreator
{% endcodeblock %}

Değişikliği yaptıktan sonra oturumu kapatıp açmanız gerekebilir. [kurulum_dizini] kısmına kurulum yaptığınız dizini girmeye dikkat edin.

## Eski Siteden Yorumlar:

### 2014-06-26 - Hüseyin Kozan
Yeni yayınlanan Qt 5.3.1 ile gelen Qt Creator Qt 5.3.1 ile derlendiğinden hata giderilmiş görünüyor.
İlgili midir, değil midir bilmiyorum ama klavyedeki Home tuşu imleci satır başına götürmüyor. Düzeltmek için _Tools > Options > Environment > Keyboard_ yolunu izleyerek `GotoLineStart` değerine Home tuşunu atadım.

### 2014-10-18 - Ömer Göktaş
Türkçe klavye problemini ben de yaşadım Ubuntu 14.04 LTS üzerinde Qt Creator 5.3 de. Sizin burada anlattıklarınızı yaparak düzelttim. Çok teşekkür ederim. Ülkemizde bu işlere ciddiyet veren insanların olduğunu görmek çok güzel.

### 2014-06-26 - Hüseyin Kozan
Qt 5.4 ile dağıtılan QtCreator 3.3’te sorun düzelmiş görünüyor.

### 2017-04-12 - Hüseyin Kozan
Tekrar ortaya çıkmış görünüyor.
https://groups.google.com/forum/#!topic/qtturkiye/XFpgHUDuzmU

[1]: https://bugreports.qt.io/browse/QTBUG-32760
[2]: https://bugreports.qt.io/browse/QTBUG-38946
[1]: https://bugreports.qt.io/browse/
