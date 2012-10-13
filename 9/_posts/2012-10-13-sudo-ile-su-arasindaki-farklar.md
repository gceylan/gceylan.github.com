---
layout: post
title: sudo ile su arasındaki farklılıklar
---

su
---
`su` sistemin tamamı için root yetkisi verir. Sistemden çıkış yapmadan kullanıcı
değiştirmeye yarar. `su` ile root olmak için **root(yönetici)** parolası
istenir.

sudo
----
`sudo` ile çalıştırılacak komut için anlık root yetkisi almış oluruz. Bir nevi
tek atımlık kurşun gibi düşünebiliriz. `sudo` ile anlık root yetkisi almak için,
sistem kullanıcısının parolası istenir. Sistem kullanıcısını öğrenmek için `$ whoami` kullanılır.

**Not:** `root` parolasını değiştirmek için `$ sudo passwd root` komutunu
kullanabiliriz.
