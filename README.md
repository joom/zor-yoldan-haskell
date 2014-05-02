# Zor Yoldan Haskell

TL, DR: Haskell öğrenmek için kısa ve yoğun bir rehber.

İçindekiler:
* Giriş
* Kurulum
* Korkmayın
* Haskell'e Giriş
    * Fonksiyon tanımı
    * Tip örneği
* Temel Haskell
* Notasyon
    * Aritmetik
    * Mantıksal
    * Kuvvetler
    * Listeler
    * Karakter Dizileri
    * Demetler (Tüple)
    * Parantezlerle Baş Etmek
* Fonksiyonlar için Faydalı Notasyonlar
* Zor Kısım
* Fonksiyonel Stil
    * Üst Derece Fonksiyonlar
* Tipler
    * Tip Çıkarımı
    * Tip İnşası
    * Özyinelemeli Tipler (Recursive types)
    * Ağaçlar
* Sonsuz Yapılar
* Çok Zor Kısım
* IO ile Baş Etmek
* IO Hileleri
* Monad
    * Maybe Monad'ı
    * Liste Monad'ı
* Ek
* Sonsuz Ağaçlar Hakkında

Tüm geliştiricilerin Haskell öğrenmesi gerektiğine inanıyorum. Herkesin süper Haskell ninjası olması gerektiğini düşünmüyorum, ama herkes Haskell'in sahip olduğu farklı yönleri görmeli. Haskell öğrenmek zihninizi acar.

Anaakım diller aynı temelleri paylaşırlar:
* değişkenler
* döngüler
* işaretçiler (pointer)
* veri yapıları, nesneler ve sınıflar (genellikle)

Haskell çok farklıdır. Bu dil daha önce hiç duymamış olduğum bir sürü kavram kullanıyor. Bu kavramların çoğu daha iyi bir programcı olmanızda yardımcı olacaktır.

Ama Haskell öğrenmek zor olabilir. Benim için öyleydi. Bu yazıda ben öğrenirken eksik olan şeyleri size sağlamaya çalışacağım.

Bu yazıyı takip etmek zor olacak. Bunu bilerek yapıyorum. Haskell öğrenmenin kısayolu yoktur. Zordur ve çaba ister. Ama bunun iyi bir şey olduğuna inanıyorum. Haskell, zor olduğu için ilginç.

Haskell öğrenmenin klasik yolu iki kitap okumaktır. İlk önce ["Learn You a Haskell"](http://learnyouahaskell.com/) (Haskell Öğrenin) ve sonrasında da ["Real World Haskell"](http://www.realworldhaskell.org/) (Gerçek Dünyada Haskell). Ben de bunun doğru yol olduğuna inanıyorum. Haskell'in doğru düzgün öğrenmek için, bu kitapları ayrıntılı şekilde okumalısınız.

Tersi şekilde, bu yazı Haskell'in ana konularının oldukça kısa ve yoğun bir özeti. Kendim Haskell öğrenirken ihtiyaç duyup bulamadığım bazı bilgileri de ekledim.

Bu yazının beş bölümü var:
* Giriş: Haskell'in insancıl olabildiğini göstermek için bir kısa örnek.
* Temel Haskell: Haskell şöz dizimi ve bazı temel kavramlar.
* Zor Bölüm:
    * Fonksiyonel stil; ımperatif stilden fonksiyonel stile kademeli bir örnek.
    * Tipler; tipler ve standard bir ikili ağaç (binary tree) örneği.
    * Sonsuz Yapılar; sonsuz bir ikili ağacı işleyin.
* Çok Zor Bölüm:
    * IO ile baş edin; minimal bir örnek.
    * IO hileleri açıklaması, IO'yu anlamak için ihtiyaç duyduğum gizli detay
    * Monad'ler, inanılmaz genellenebilirlikleri
* Ek:
    * Sonsuz ağaçlar hakkında matematik tabanlı bir tartışma.

> Her `.lhs` ile biten bir dosya isimli ayırıcı gördüğünüzde, dosyaya ulaşmak için tıklayabilirsiniz. Dosyayı `dosyaismi.lhs` diye kaydederseniz, `runhaskell dosyaismi.lhs` komutuyla çalıştırabilirsiniz. Bazıları çalışmayabilir ama çoğu çalışacaktır. Aşağıda bir link görebilirsiniz.
[01_basic/10_İntroduction/00_hello_world.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/00_hello_world.lhs)
(Çevirmen notu: Kodlardaki karakter dizileri Turkçeleştirilmiş, ancak değişken isimleri aynı bırakılmıştır. İndirilen kodlar İngilizce kaynaktan olup Türkçeleştirilmemiş olacaktır.)

# 1. Giriş

## 1.1. Kurulum
![Haskell](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/Haskell-logo.png)

Araçlar:
* `ghc`: `C`'deki gcc gibi bir derleyici.
* `ghci`: İnteraktif Haskell yorumlayıcısı. (REPL)
* `runhaskell`: Bir programı derlemeden çalıştırmak için kullanılır. Kolaydır, ama derlenen programlara göre çok yavaştır.

## 1.2. Korkmayın
![Scream](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/munch_TheScream.jpg)

Haskell hakkındaki pek çok kitap/makale az bilinen bir formülü (quick sort, Fibonacci, vs.) yazmakla başlıyor, bense tam tersini yapacağım. İlk önce size Haskell'in süper güçlerini göstermeyeceğim. Haskell ve diğer programlama dilleri arasındaki benzerliklerle başlayacağım. Zorunlu "Merhaba Dünya" programıyla başlayalım.
```haskell
main = putStrLn "Merhaba Dünya!"
```
Çalıştırmak için, kodu `merhaba.hs` olarak kaydedip şu komutları kullanabilirsiniz:
```
~ runhaskell ./merhaba.hs
Merhaba Dünya!
```
Doğrudan kaynak kodunu da indirebilirsiniz. Aşağıdaki komutların hemen altında linki görüp, `00_hello_world.lhs` olarak kaydedip bu komutlarla çalıştırabilirsiniz:
```
~ runhaskell 00_hello_world.lhs
Hello World!
```
[01_basic/10_Introduction/00_hello_world.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/00_hello_world.lhs)
