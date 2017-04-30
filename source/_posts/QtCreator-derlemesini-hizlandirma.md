---
title: QtCreator derlemesini hızlandırma
date: 2014-12-17 00:00:00
tags:
  - Qt
  - Qt Creator
category:
  - Qt
---

İşlemcinizin tüm çekirdeklerini kullanabilmek için QtCreator projelerine her seferinde `make e -j` parametresi vermek yerine aşağıdakini bir kereliğine desktop dosyasında değiştirin :
{% codeblock lang:bash %}
$ nano ~/.local/share/applications/DigiaQt-qtcreator-community.desktop
{% endcodeblock %}

<!-- more -->

Şu satırı :
{% codeblock lang:bash %}
Exec=/path/to/qt5.4.0/Tools/QtCreator/bin/qtcreator
{% endcodeblock %}

Bununla değiştirin :
{% codeblock lang:bash %}
Exec= env MAKEFLAGS="-j $(grep -c ^processor /proc/cpuinfo) $MAKEFLAGS" /path/to/qt5.4.0/Tools/QtCreator/bin/qtcreator
{% endcodeblock %}

Eğer biraz daha hız lazımsa ccache i kurun:
{% codeblock lang:bash %}
$ sudo apt-get install ccache
{% endcodeblock %}

Devamında proje dosyasına aşağıdakileri ekleyin:
{% codeblock %}
linux-*:exists(/usr/bin/ccache):QMAKE_CXX=ccache g++
macx:exists(/usr/bin/ccache):QMAKE_CXX=ccache g++
{% endcodeblock %}
