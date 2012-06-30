---
layout: post
title: eclipse - github plugin
---


GitHub' da kod incelerken `Eclipse GitHub Plugin 2.0 Released` diye bir link gördüm. Hemen tıklayıp içriğe baktım ve GitHub' a Eclipse ile proje gönderilebileceğini öğrendim. Hemen nasıl kurulup kullanılabileceğini araştırdım ve bu iletimde bu işleri nasıl yaptığımı anlatmak için hazırladım. Şimdi yavaş yavaş kuruluma geçelim.

İlk olarak Eclipse GitHub' ı tanıtmakla başlıyoruz:
Eclipse açalım. Menüden `Help -> Install New Software` seçelim. Gelen Ekrandan sağ üstteki `Add` butonuna tıklayalım. Gelen ekranda `Location` kısmına `http://download.eclipse.org/releases/juno` adresini yazalım. `Name` kısmına da `Eclipse GitHub Plugin` şeklinde bir isim verebiliriz.

![1](https://github.com/gceylan/gceylan.github.com/raw/master/images/eclipse_github_plugin/location.png)

Daha sonra aşağıdaki resimde seçili olan paketleri seçin:

![2](https://github.com/gceylan/gceylan.github.com/raw/master/images/eclipse_github_plugin/secim.png)

Resimdeki paketleri seçtikten sonra `finish` tıklayın. Kurulum tamamlandıktan sonra Eclipse yeniden başlatılmak isteyecek. Eclipse yeniden başlatın. Artık gerekli paketler Eclipse tanıtılmış durumda. Şimdi bir örnek yapalım:

İlk olarak sağ üstteki `Open Perspective`i tıklayın ve `other`ı seçin. Daha sonra gelen ekrandan `Git Repository Exploring`i seçin. Böyece GitHub' ı kullanacağımız ekrana geçmiş olacağız.

![3](https://github.com/gceylan/gceylan.github.com/raw/master/images/eclipse_github_plugin/other.png)

Şimdi github' a girerek istediğimiz bir deponun adresini kopyalayalım:

![4](https://github.com/gceylan/gceylan.github.com/raw/master/images/eclipse_github_plugin/copy_repo_url.png)

Daha sonra Eclipse de `Git Repositories` ekranına sağ tıklayalım ve `paste reposition...` seçelim.

![5](https://github.com/gceylan/gceylan.github.com/raw/master/images/eclipse_github_plugin/paste_repo_url.png)

Gelen ekranda şekildeki gibi `ssh`ı seçmeyi unutmayın. Sonra `next -> finish` diyerek devam edin.

![6](https://github.com/gceylan/gceylan.github.com/raw/master/images/eclipse_github_plugin/clone_git_repo.png)

Bu işlem sonunda seçilen github reposu kopyalanacaktır.
Şimdi `Open Perspective -> other` işleminden klasik Java ekranına geçelim ve örnek bir `HelloGitHub` projesi oluşturalım(içerisine basitçe ekrana `Hello GitHub!` yazan bir sınıf da siz koyun).
Şimdi sıra geldi bu `HelloGitHub` projesini Eclipse üzerinden GitHub' a göndermeye.

1) `HelloGitHub` projemizin üzerinde sağ tıklayalım ve `Team -> Share Project` yolunu izleyelim.
`Git`i seçip next diyelim. Ben HelloWorld pojesini `pro-lang/java` dizinin altına commitlemek için aşağıdaki gibi ayarlamaları yaptım. Daha sonra finish tıklayalım.

![7](https://github.com/gceylan/gceylan.github.com/raw/master/images/eclipse_github_plugin/configure_git_repo.png)

2) `HelloGitHub` projemizin üzerinde sağ tıklayalım ve `Team -> Add to Index` i seçelim. Böylece HelloWorld projemiz içerisindeki tüm dosyaları githuba gönderbilmek için seçmiş olacağız.

3) `HelloGitHub` projemizin üzerinde sağ tıklayalım ve `Team -> Commit` yolunu izleyelim. Açılan ekranda commit mesajını yazalım ve `Commit` butonuna tıklayalım.

![8](https://github.com/gceylan/gceylan.github.com/raw/master/images/eclipse_github_plugin/commit_git_repo.png)

4) Ve son işlem. `HelloGitHub` projemizin üzerinde sağ tıklayalım ve `Team -> Push...` seçeneğini seçelim. Böylece projemizi github' a göndermiş olacağız.
