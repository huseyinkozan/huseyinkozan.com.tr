---
title: Ubuntu'da QtCreator ile hata ayıklama
date: 2014-07-06 00:00:00
tags:
  - Qt
  - Qt Creator
  - Ubuntu
category:
  - Qt
---

Ubuntu 10.10’dan sonra malware koruması için eklenen [bir ayar][0] sebebiyle QtCreator’da _gdb_ ile hata ayıklamaya çalışınca hata alınıyor. Ayarı kalıcı olarak kapatmak için `/etc/sysctl.d/10-ptrace.conf` dosyasındaki değeri _1_’den _0’a çekmek yeterli oluyor.

[0]: https://wiki.ubuntu.com/SecurityTeam/Roadmap/KernelHardening#ptrace%20Protection
