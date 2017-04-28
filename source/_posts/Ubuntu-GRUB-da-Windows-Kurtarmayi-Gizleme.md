---
title: Ubuntu GRUB'da Windows Kurtarmayı Gizleme
date: 2014-05-03 00:00:00
update: 2017-04-28 00:00:00
tags:
  - Ubuntu
  - GRUB
---
Ubuntu önyükleyicisi 2. sürümle birlikte oldukça değişti. Eskiden sadece _/boot/grub/grub.cfg_ dosyası ile yapılan ayarlar artık birkaç parçalı aşamayla oluşturuluyor.

Yeni GRUB ile _/boot/grub/_ altındaki ayarlar _update-grub_ aracı kullanılarak oluşturuluyor. _update-grub_ çalıştırıldığında genel ayarları _/etc/defaults/grub_ dosyasından okuyor ve _/etc/grub.d/_ dizininin altındaki çalıştırılabilir betikleri sırayla çalıştırıyor. GRUB menüsünü sadeleştirmek için buradaki betikleri çalıştırılamaz yapmak yetiyor. Örneğin _Memtest+_ seçeneğini gizlemek için aşağıdaki yazmak yeterli;

{% codeblock lang:bash %}
$ sudo chmod -x /etc/grub.d/20_memtest86+
{% endcodeblock %}

Eğer bilgisayarınızda Windows 7 veya 8 varsa menüde Windows Recovery Environment (loader) gibi bir seçenek bulunacaktır. Bunu kaldırmak için `/etc/grub.d/30_os-prober` dosyasına eklenti yapmak gerekiyordu.

{% codeblock lang:bash %}
if [ -z "${LONGNAME}" ] ; then
LONGNAME="${LABEL}"
fi
# Windows Recovery Gizleme Eklentisi
if [ "$LONGNAME" = "Windows Recovery Environment (loader)" ] &amp;&amp; [ "${DEVICE}" = "/dev/sda4" ] ; then
continue
fi
# Eklenti Sonu
{% endcodeblock %}

Bende bu eklentiyi eklemek için dosyayı açtığımda _GRUB_OS_PROBER_SKIP_LIST_ gibi bir değişken kontrol edildiğini fark ettim. Bu değişkeni `/etc/defaults/grub` dosyasına aşağıdaki şekilde ekledikten sonra `update-grub` komutunu çalıştırarak menüdeki kurtarma seçeneğinden kurtulabilirsiniz.

{% codeblock lang:bash %}
GRUB_OS_PROBER_SKIP_LIST="0A76-0E4F@/dev/sda4"
{% endcodeblock %}

Değişkene verilen parametredeki ilk değer diskin UUID si, ikincisi de diskin sistemdeki dosya yolu. Bu bilgileri elde etmek için `blkid` komutunu kullanabilisiniz.

{% codeblock lang:bash %}
$ sudo blkid
{% endcodeblock %}

Son olarak da `/etc/defaults/grub` dosyasına aşağıdaki ayarları da yaparsanız en son seçtiğiniz seçeneği hatırlayacaktır.

{% codeblock lang:bash %}
GRUB_DEFAULT=saved
GRUB_SAVEDEFAULT=true
{% endcodeblock %}
