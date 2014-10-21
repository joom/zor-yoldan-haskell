> This is the Turkish translation of Yann Esposito's article [Learn Haskell Fast and Hard](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/).

> Yann Esposito'nun [Learn Haskell Fast and Hard](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/) başlıklı yazısının Türkçe çevirisidir.

# Zor Yoldan Haskell

> TL, DR (Çok uzundu okumadım): Haskell öğrenmek için kısa ve yoğun bir rehber.

#### İçindekiler:
* [Giriş](#1-giri%C5%9F)
    * [Kurulum](#11-kurulum)
    * [Korkmayın](#12-korkmay%C4%B1n)
    * [Haskell'e Giriş](#13-haskelle-giri%C5%9F)
        * [Fonksiyon tanımı](#131-fonksiyon-tan%C4%B1m%C4%B1)
        * [Tip örneği](#132-tip-%C3%B6rne%C4%9Fi)
* [Temel Haskell](#2-temel-haskell)
    * [Notasyon](#21-notasyon)
        * [Aritmetik](#aritmetik)
        * [Mantıksal](#mant%C4%B1ksal)
        * [Üslü Sayılar](#%C3%9Csl%C3%BC-say%C4%B1lar)
        * [Listeler](#listeler)
        * [Karakter Dizileri](#karakter-dizileri)
        * [Demetler *(Tuple)*](#demetler-tuple)
        * [Parantezlerle Baş Etmek](#parantezlerle-ba%C5%9Fa-%C3%87%C4%B1kmak)
    * [Fonksiyonlar için Faydalı Notasyonlar](#22-fonksiyonlar-i%C3%A7in-faydal%C4%B1-notasyonlar)
* [Zor Kısım](#3-zor-k%C4%B1s%C4%B1m)
    * [Fonksiyonel Stil](#31-fonksiyonel-stil)
        * [Üst Derece Fonksiyonlar](#311-%C3%9Cst-derece-fonksiyonlar)
    * [Tipler](#32-tipler)
        * [Tip Çıkarımı](#321-tip-%C3%87%C4%B1kar%C4%B1m%C4%B1)
        * [Tip Oluşturma](#322-tip-olu%C5%9Fturma)
        * [Özyinelemeli Tipler *(Recursive types)*](#323-%C3%96zyinelemeli-tipler-recursive-types)
        * [Ağaçlar](#324-a%C4%9Fa%C3%A7lar)
    * [Sonsuz Yapılar](#33-sonsuz-yap%C4%B1lar)
* [Çok Zor Kısım](#4-%C3%87ok-zor-k%C4%B1s%C4%B1m)
    * [IO ile Baş Etmek](#41-io-ile-ba%C5%9F-etmek)
    * [IO'nun Püf Noktası](#42-ionun-p%C3%BCf-noktas%C4%B1)
    * [Monad](#43-monad)
        * [Maybe Monad'ı](#431-maybe-monad%C4%B1)
        * [Liste Monad'ı](#432-liste-monad%C4%B1)
* [Ekler](#5-ekler)
    * [Sonsuz Ağaçlar Hakkında](#51-sonsuz-a%C4%9Fa%C3%A7lar-hakk%C4%B1nda)

***

Tüm geliştiricilerin Haskell öğrenmesi gerektiğine inanıyorum. Herkesin süper Haskell ninjası olması gerektiğini düşünmüyorum, ama herkes Haskell'in sahip olduğu farklı yönleri görmeli. Haskell öğrenmek zihninizi acar.

Anaakım diller aynı temelleri paylaşırlar:
* değişkenler
* döngüler
* işaretçiler *(pointer)* [^fn-1]
* veri yapıları, nesneler ve sınıflar (genellikle)

Haskell çok farklıdır. Bu dil daha önce hiç duymamış olduğum bir sürü kavram kullanıyor. Bu kavramların çoğu daha iyi bir programcı olmanızda yardımcı olacaktır.

Ama Haskell öğrenmek zor olabilir. Benim için öyleydi. Bu yazıda ben öğrenirken eksik olan şeyleri size sağlamaya çalışacağım.

Bu yazıyı takip etmek zor olacak. Bunu bilerek yapıyorum. Haskell öğrenmenin kısayolu yoktur. Zordur ve çaba ister. Ama bunun iyi bir şey olduğuna inanıyorum. Haskell, zor olduğu için ilginç.

Haskell öğrenmenin klasik yolu iki kitap okumaktır. İlk önce ["Learn You a Haskell"](http://learnyouahaskell.com/) (Haskell Öğrenin) ve sonrasında da ["Real World Haskell"](http://www.realworldhaskell.org/) (Gerçek Dünyada Haskell). Ben de bunun doğru yol olduğuna inanıyorum. Haskell'in doğru düzgün öğrenmek için, bu kitapları ayrıntılı şekilde okumalısınız.

Tersi şekilde, bu yazı Haskell'in ana konularının oldukça kısa ve yoğun bir özeti. Kendim Haskell öğrenirken ihtiyaç duyup bulamadığım bazı bilgileri de ekledim.

Bu yazının beş bölümü var:
* Giriş: Haskell'in insancıl olabildiğini göstermek için bir kısa örnek.
* Temel Haskell: Haskell söz dizimi ve bazı temel kavramlar.
* Zor Bölüm:
    * Fonksiyonel stil; imperatif stilden fonksiyonel stile kademeli bir örnek.
    * Tipler; tipler ve standard bir ikili ağaç *(binary tree)* örneği.
    * Sonsuz Yapılar; sonsuz bir ikili ağacı işleyin.
* Çok Zor Bölüm:
    * IO ile baş edin; minimal bir örnek.
    * IO hileleri açıklaması, IO'yu anlamak için ihtiyaç duyduğum gizli detay
    * Monad'ler, inanılmaz genellenebilirlikleri
* Ek:
    * Sonsuz ağaçlar hakkında matematik tabanlı bir tartışma.

> Her `.lhs` ile biten bir dosya isimli ayırıcı gördüğünüzde, dosyaya ulaşmak için tıklayabilirsiniz. Dosyayı `dosyaismi.lhs` diye kaydederseniz, `runhaskell dosyaismi.lhs` komutuyla çalıştırabilirsiniz. Bazıları çalışmayabilir ama çoğu çalışacaktır. Aşağıda bir link görebilirsiniz.
[01_basic/10_Introduction/00_hello_world.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/00_hello_world.lhs)
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

***

[01_basic/10_Introduction/10_hello_you.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/10_hello_you.lhs)
Şimdi, adınızı soran ve aldığı cevapla size "Merhaba" diyen bir program yazalım:
```haskell
main = do
    print "Adiniz nedir?"
    name <- getLine
    print ("Merhaba " ++ name ++ "!")
```
Öncelikle, bunu birkaç imperatif dildeki benzer programlarla karşılaştıralım:
```python
# Python
print "Adiniz nedir?"
name = raw_input()
print "Merhaba %s!" % name
```

```ruby
# Ruby
puts "Adiniz nedir?"
name = gets.chomp
puts "Merhaba #{name}!"
```

```c
// In C
#include <stdio.h>
int main (int argc, char **argv) {
    char name[666]; // <- musibetli sayi!
    // Adim 665 karakterden fazlaysa ne olacak?
    printf("Adiniz nedir?\n"); 
    scanf("%s", name);
    printf("Merhaba %s!\n", name);
    return 0;
}
```

Yapı aynı, ama söz dizimsel farklılıklar var. Bu yazının ana kısmı bu farkların sebebini açıklamak üzerine olacak.

Haskell'de bir `main` fonksiyonu vardır ve her nesnenin bir tipi vardır. `main`'in tipi `IO ()`'dur. Bu, `main` yan etkilerde bulunacak demektir.

Şimdilik, Haskell'in anaakım imperatif dillere benzer görünebileceğini hatırlamanız yeterli.

[01_basic/10_Introduction/10_hello_you.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/10_hello_you.lhs)

***
[01_basic/10_Introduction/20_very_basic.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/20_very_basic.lhs)

## 1.3. Haskell'e Giriş
![Very Basic](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/picasso_owl.jpg)

Devam etmeden önce, Haskell'in bazı temel özelliklerinin farkına varmanız gerekiyor.

#### Fonksiyonel
Haskell fonksiyonel bir dildir. Eğer imperatif bir dilde geçmişiniz varsa, yeni bir sürü şey öğrenmeniz gerekiyor. Umarım bu yeni kavramlar size imperatif dillerde program yazarken bile yardımcı olur.

#### Akıllı Statik Tip Sistemi

Tip sistemi, `C`'de, `C++`'ta, `Java`'da olduğu gibi sizi engellemek yerine, size yardım etmek için var.

#### Saflık
Genellikle fonksiyonlarınız dış dünyada bir şeyi değiştirmeyecekler. Bu demek oluyor ki, bir değişkenin değerini değiştiremeyecekler, kullanıcıdan girdi alamayacaklar, ekrana yazı yazamayacaklar, veya bir füzeyi ateşleyemeyecekler. Diğer yandan, paralellik sağlamak çok kolay olacak. Haskell nerede yan etkilerin olduğunun ve nerede kodunuzun saf olduğunun ayrımını çok açık bir şekilde yapar. Ayrıca, programınız hakkında mantık yürütmek de çok daha kolay olur. Çoğu hata, kodunuzun saf kısmında engellecektir.

Daha da ötesi, Haskell'de saf fonksiyonlar temel bir kural izlerler:
> Bir fonksiyona aynı parametreleri vermek her zaman aynı değerleri döndürür.

#### Tembellik
Tembellik, genelde alışılmadık bir dil tasarım tercihidir. Haskell'de varsayılan olarak her şey sadece ihtiyaç olduğunda hesaplanır / işlenir. Bunun sonuçlarından biri de sonsuz yapıları işlemek için çok mükemmel bir yol sunmasıdır.

Son uyarı da Haskell kodunu nasıl okumanız gerektiğiyle ilgili. Benim için, bilimsel makaleleri okumak gibi. Bazı kısımları çok açık, ama bir formül gördünüzde odaklanın ve yavaşça okuyun. Ayrıca, Haskell öğrenirken, garip söz dizimsel detayları anlamamanız *gerçekten* önemli değil. Ama eğer `>>=`, `<$>`, `<-` v.b. herhangi bir garip sembol görürseniz, görmezden gelin ve kodun akışını takip edin.

### 1.3.1. Fonksiyon tanımı
Şu şekilde fonksiyon tanımlamaya alışmış olabilirsiniz:

`C`'de:
```c
int f(int x, int y) {
    return x*x + y*y;
}
```

`JavaScript`'te:
```javascript
function f(x,y) {
    return x*x + y*y;
}
```

`Python`'da:
```python
def f(x,y):
    return x*x + y*y
```

`Ruby`'de:
```ruby
def f(x,y)
    x*x + y*y
end
```

`Scheme`'de:
```scheme
(define (f x y)
    (+ (* x x) (* y y)))
```

Son olarak, Haskell yolu da budur:
```haskell
f x y = x*x + y*y
```

Tertemiz. Parantez yok, `def` yok.

Unutmayın, Haskell fonksiyonları ve tipleri sıkça kullanır. Bu yüzden, onları tanımlamak oldukça kolaydır. Söz dizimi, özellikle öyle düşünülmüştür.

### 1.3.2. Tip örneği

Zorunlu olmamasına rağmen, fonksiyonlar için tip bilgisi genellikle ayrıca girilir. Zorunlu değildir, çünkü derleyici sizin için çıkarım yapacak kadar akıllıdır. Yine de tipleri yazmak iyi bir fikirdir, çünkü kodun anlaşılmasına yardımcı olur.

Bakalım nasıl oluyormuş:

```haskell
-- Tipleri belirtmek icin :: isaretini kullaniyoruz
f :: Int -> Int -> Int
f x y = x*x + y*y

main = print (f 2 3)
```

```
~ runhaskell 20_very_basic.lhs
13
```
[01_basic/10_Introduction/20_very_basic.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/20_very_basic.lhs)

***
[01_basic/10_Introduction/21_very_basic.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/21_very_basic.lhs)

Şimdi bunu deneyelim:

```haskell
f :: Int -> Int -> Int
f x y = x*x + y*y

main = print (f 2.3 4.2)
```

Şu hatayı almış olmalısınız:

```
21_very_basic.lhs:6:23:
    No instance for (Fractional Int)
      arising from the literal `4.2'
    Possible fix: add an instance declaration for (Fractional Int)
    In the second argument of `f', namely `4.2'
    In the first argument of `print', namely `(f 2.3 4.2)'
    In the expression: print (f 2.3 4.2)
```
Sorun şu: `4.2` bir tam sayı (Int) değil.

[01_basic/10_Introduction/21_very_basic.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/21_very_basic.lhs)

***

[01_basic/10_Introduction/22_very_basic.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/22_very_basic.lhs)

Çözümü de şu: `f` fonksiyonu için şimdilik bir tip belirtmeyelim ve Haskell'in tip çıkarımı yapmasına izin verelim.

```haskell
f x y = x*x + y*y

main = print (f 2.3 4.2)
```

Çalışıyor! Ne şanslıyız ki, her tip için yeni bir fonksiyon tanımlamak zorunda değiliz. Örneğin `C`'de, `int` için, `float` için, `long` için, `double` için vs. ayrı ayrı fonksiyon tanımlamak zorundayız.

Peki hangi tipi belirtmeliydik? Haskell'in bizim için bulduğu tipi görmek için `ghci`'yi başlatın:

```
% ghci
GHCi, version 7.0.4: http://www.haskell.org/ghc/  :? for help
Loading package ghc-prim ... linking ... done.
Loading package integer-gmp ... linking ... done.
Loading package base ... linking ... done.
Loading package ffi-1.0 ... linking ... done.
Prelude> let f x y = x*x + y*y
Prelude> :type f
f :: Num a => a -> a -> a
```

Hi? Bu garip tip de neyin nesi?

```
Num a => a -> a -> a
```

İlk önce, sağdaki `a -> a -> a` kısmına bakalım. Anlamak için kademeli olarak şu örnekleri inceleyelim:

| Yazılı Tip   | Anlamı                                                                  |
| ------------ | ----------------------------------------------------------------------- |
| Int          | Int tipi                                                                |
| Int -> Int   | Int'ten Int'e olan fonksiyon tipi                                       |
| Float -> Int | Float'tan Int'e olan fonksiyon tipi                                     |
| a -> Int     | herhangi bir tipten Int'e olan fonksiyon tipi                           |
| a -> a       | herhangi bir a tipinden aynı a tipine olan fonksiyon tipi               |
| a -> a -> a  | herhangi bir a tipinden iki argümanın aynı a tipine olan fonksiyon tipi |

`a -> a -> a` tipinde, `a` harfine tip değişkeni diyoruz. *(type variable)*. Bu `f`'nin iki argümanı olduğu, ve girilen argümanlar ve fonksiyon sonucunun aynı tipten olduğu anlamına geliyor. Tip değişkeni `a`, başka bir sürü değer alabilir. Örneğin `Int`, `Integer`, `Float`...

Yani `C`'deki gibi zorunlu olarak bir fonksiyon için `int`, `long`, `float`, `double` vs. gibi tip belirtmek yerine, herhangi bir dinamik tip sistemli dil gibi sadece bir fonksiyon tanımlıyoruz.

Buna bazen parametrik çokşekillilik *(parametric polymorphism)* de deniyor. Hayatta her istediğinizin olması gibi bir şey.

Genellikle `a` herhangi bir tip olabilir, örneğin `String` veya `Int`, ama `Trees` gibi daha karışık tipler, başka fonksiyonlar da olabilir. Ama buradaki tipimiz `Num a =>` ile başlıyor.

`Num` bir tip sınıfı. *(type class)*. Tip sınıfları tip grupları gibi düşünülebilir. `Num` sınıfı sadece sayı gibi davranan tipleri içerir. Daha doğrusu, `Num`, belli bir fonksiyon listesinin, özellikle `(+)` ve `(*)` fonksiyonlarının, etki ettiği sınıftır.

Tip sınıfları güçlü bir dil yapısıdır. Onlarla inanılmaz güçlü şeyler yapabiliriz. Buna daha sonra tekrar değineceğiz.

Sonuç olarak, `Num a => a -> a -> a` şu demek oluyor:

Diyelim ki `a`, `Num` tip sınıfına ait bir tip. Bu da `a` tipinden `a -> a` tipine bir fonksiyon.

Evet, garip. Aslında Haskell'de hiçbir fonksiyonun gerçekten iki argümanı yoktur. Onun yerine, her fonksiyonun sadece bir argümanı vardır. Ama hatırlamalıyız ki iki argüman almakla, bir argüman alıp ikinci argümanı bir parametre olarak alan bir fonksiyon döndürmek denk şeylerdir.

Daha açık olmak gerekirse, `f 3 4`, `(f 3) 4`'e denktir. `f 3`'un de bir fonksiyon olduğuna dikkat edin:

```haskell
f :: Num a => a -> a -> a

g :: Num a => a -> a
g = f 3

g y ⇔ 3*3 + y*y
```

Fonksiyonlar için bir notasyon daha var. Lambda notasyonu isimsiz fonksiyonlar yaratmamıza olanak sağlar. Bunlara anonim fonksiyonlar diyoruz. Aynı şeyi lambda notasyonuyla şöyle de yazabilirdik:

```haskell
g = \y -> 3*3 + y*y
```

Burada `\` kullanılıyor, çünkü `λ` (lambda) harfine benziyor, ve aynı zamanda ASCII dizisine dahil.

Eğer fonksiyonel programlamaya alışık değilseniz beyniniz yanmaya başlamış olmalı. Artık gerçek bir uygulama yazma zamanı.

[01_basic/10_Introduction/22_very_basic.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/22_very_basic.lhs)

***

[01_basic/10_Introduction/23_very_basic.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/23_very_basic.lhs)

Ama ondan önce, tip sisteminin beklediğimiz gibi çalıştığını doğrulayalım:

```haskell
f :: Num a => a -> a -> a
f x y = x*x + y*y

main = print (f 3 2.4)
```

Çalışıyor, çünkü `3` hem `Float` gibi kesirli *(Fractional)* sayılar için, hem de `Integer` (tam sayı tipi) için geçerli bir gösterim. `2.4` kesirli bir sayı olduğu için `3` de kesirli bir sayı olarak yorumlanıyor.

[01_basic/10_Introduction/23_very_basic.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/23_very_basic.lhs)

***

[01_basic/10_Introduction/24_very_basic.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/24_very_basic.lhs)

Eğer fonksiyonumuzu farklı tiplerle çalışmaya zorlarsak, hata verecektir:

```haskell
f :: Num a => a -> a -> a
f x y = x*x + y*y

x :: Int
x = 3
y :: Float
y = 2.4
main = print (f x y) -- calismayacak, cunku tip x ≠ tip y
```

Derleyici hata veriyor. İki parametre de aynı tipten olmak zorunda.

Eğer bunun kötü bir fikir olduğunu ve derleyicinin sizin için bir tipten diğerine dönüşümü yapması gerektiğini düşünüyorsanız, bu müthiş (ve komik) videoyu mutlaka izlemelisiniz: [WAT](https://www.destroyallsoftware.com/talks/wat)

[01_basic/10_Introduction/24_very_basic.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/10_Introduction/24_very_basic.lhs)


# 2. Temel Haskell

![Essential](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/kandinsky_gugg.jpg)

Bu kısma yalnızca göz gezdirmenizi tavsiye ediyorum. Her zaman yararlanacağınız bir kaynak gibi düşünün. Haskell'in birçok özelliği vardır. Burada da pek çoğu eksik. Eğer notasyon garip gelirse tekrar buraya dönün.

İki ifadenin denk olduğunu belirtmek için `⇔` işaretini kullanıyorum. Bu sahte bir notasyon, `⇔` Haskell'de mevcut değil. Aynı şekilde, bir ifadenin hesaplanan değerinin ne olduğunu belirtmek için de `⇒` işaretini kullanacağım.

## 2.1. Notasyon

### Aritmetik

``` haskell
3 + 2 * 6 / 3 ⇔ 3 + ((2*6)/3)
```

### Mantıksal

```haskell
True || False ⇒ True
True && False ⇒ False
True == False ⇒ False
True /= False ⇒ True  (/=) esit degildir operatorudur
```

### Üslü Sayılar

```haskell
x^n     herhangi bir n integral tipi icin (Int veya Integer olarak anlayin)
x**y    herhangi bir y sayi tipi icin (ornegin Float)
```

`Integer`'ın bilgisayarınızın kapasitesi dışında bir sınırı yoktur.

```
4^103
102844034832575377634685573909834406561420991602098741459288064
```

Evet! Ayrıca rasyonel sayılar da var! Ama önce `Data.Ratio` modülünü içeri aktarmanız gerekiyor:

```
$ ghci
....
Prelude> :m Data.Ratio
Data.Ratio> (11 % 15) * (5 % 3)
11 % 9
```

### Listeler

```
[]                      ⇔ bos liste
[1,2,3]                 ⇔ integral listesi
["foo","bar","baz"]     ⇔ String listesi
1:[2,3]                 ⇔ [1,2,3], (:) bir elemani one ekleme
1:2:[]                  ⇔ [1,2]
[1,2] ++ [3,4]          ⇔ [1,2,3,4], (++) birlestirme
[1,2,3] ++ ["foo"]      ⇔ HATA String ≠ Integral
[1..4]                  ⇔ [1,2,3,4]
[1,3..10]               ⇔ [1,3,5,7,9]
[2,3,5,7,11..100]       ⇔ HATA! O kadar da akilli degilim!
[10,9..1]               ⇔ [10,9,8,7,6,5,4,3,2,1]
```

### Karakter Dizileri

Haskell'de `String` tipi, `Char` tipinden oluşmuş listeye denktir.

```
'a' :: Char
"a" :: [Char]
""    ⇔ []
"ab"  ⇔ ['a','b'] ⇔  'a':"b" ⇔ 'a':['b'] ⇔ 'a':'b':[]
"abc" ⇔ "ab"++"c"
```

> Dikkat: Gerçek kodda, yazıyı temsil etmek için `Char` listesi kullamamalısınız. Genel olarak `Data.Text` kullanmalısınız. Eğer ASCİİ karakter akımını *(stream)* temsil etmek istiyorsanız, onun için de `Data.ByteString` kullanmalısınız.

### Demetler *(Tuple)*

Bir ikili demetin tipi `(a,b)`'dir. Demetlerdeki elemanlar farklı tipte olabilirler.

```haskell
-- Tum bu demetler gecerlidir
(2,"foo")
(3,'a',[2,3])
((2,"a"),"c",3)

fst (x,y)       ⇒  x
snd (x,y)       ⇒  y

fst (x,y,z)     ⇒  HATA: fst :: (a,b) -> a
snd (x,y,z)     ⇒  HATA: snd :: (a,b) -> b
```

### Parantezlerle Başa Çıkmak

Bazı parantezlerden kurtulmak için `($)` ve `(.)` fonksiyonlarını kullanabilirsiniz.

```haskell
-- Aslinda:
f g h x         ⇔  (((f g) h) x)

-- $ isareti kendisinden ifadenin sonuna
-- kadar olan parantezin yerine gecer
f g $ h x       ⇔  f g (h x) ⇔ (f g) (h x)
f $ g h x       ⇔  f (g h x) ⇔ f ((g h) x)
f $ g $ h x     ⇔  f (g (h x))

-- (.) kompozisyon fonksiyonu
(f . g) x       ⇔  f (g x)
(f . g . h) x   ⇔  f (g (h x))
```

***

[01_basic/20_Essential_Haskell/10a_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/20_Essential_Haskell/10a_Functions.lhs)

## 2.2. Fonksiyonlar için Faydalı Notasyonlar

Hatırlatma:

```haskell
x :: Int            ⇔ x Int tipinde herhangi bir deger alabilir
x :: a              ⇔ x herhangi bir tip olabilir
x :: Num a => a     ⇔ x Num tip sinifina dahil olan 
                         herhangi bir a tipi olabilir
f :: a -> b         ⇔ f a'dan b'ye bir fonksiyondur
f :: a -> b -> c    ⇔ f a'dan (b→c)'ye bir fonksiyondur
f :: (a -> b) -> c  ⇔ f (a→b)'den c'ye bir fonksiyondur
```

Hatırlayın ki bir fonksiyonu tanımlamadan önce tipini belirtmek zorunlu değil. Haskell genelde tip çıkarımını sizin için kendisi yapar. Ama genelde tipleri belirtmek iyi uygulama olarak görülür.

#### Orta notasyon

```haskell
square :: Num a => a -> a  
square x = x^2
```

`^` işaretinin orta notasyon kullandığına dikkat edin. Her orta notasyon için bir başta notasyon vardır. Sadece parantez içine koymak durumundasınız.

```haskell
square' x = (^) x 2

square'' x = (^2) x
```

Soldaki ve sağdaki `x`'leri silebiliriz. Buna η sadeleştirmesi deniyor.

```haskell
square''' = (^2)
```

Değişken isimlerinde `'` kullanabildiğimize dikkat edin.

> `square` ⇔ `square'` ⇔ `square''` ⇔ `square'''`

### Testler

Mutlak değer fonksiyonu yazalım:

```haskell
absolute :: (Ord a, Num a) => a -> a
absolute x = ıf x >= 0 then x else -x
```

Dikkat edin ki Haskell'deki `if .. then .. else` notasyonu, C'deki `¤?¤:¤` operatörüne çokça benziyor. `else` kısmını unutmanız mümkün değil.

Denk başka bir versiyonu:

```haskell
absolute' x
    | x >= 0 = x
    | otherwise = -x
```

> Haskell'de paragraf başı / boşluklar önemlidir. Python'daki gibi, kötü boşluklar kodunuzu bozabilir.

[01_basic/20_Essential_Haskell/10a_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/01_basic/20_Essential_Haskell/10a_Functions.lhs)

# 3. Zor Kısım

Zor kısım şimdi başlıyor.

## 3.1. Fonksiyonel Stil

![Functional](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/hr_giger_biomechanicallandscape_500.jpg)

Bu bölümde, Haskell'in etkileyici yeniden yapılandırma *(refactoring)* yeteneklerini göreceğiz. Bir problem seçip önce standart imperatif yolla çözeceğiz. Daha sonra kodun evrimini göreceğiz, son hali çok daha zarif ve kolay anlaşılabilir olacak.

Aşağıdaki problemi çözelim:

> Verilen bir tam sayı listesindeki çift sayıların toplamını alın.
> Örnek: `[1,2,3,4,5] ⇒ 2 + 4 ⇒ 6`

Fonksiyonel ve imperatif yaklaşımların arasındaki farkı göstermek için, imperatif çözümü göstererek başlayacağım: (JavaScript'te)

```javascript
function evenSum(list) {
    var result = 0;
    for (var i=0; i< list.length ; i++) {
        if (list[i] % 2 ==0) {
            result += list[i];
        }
    }
    return result;
}
```

Haskell'de, farklı olarak, değişkenler veya `for` döngüleri yoktur. Döngüler olmaksızın aynı sonucu elde etmenin bir yolu özyinelemedir. *(recursion)*

> Dikkat: Özyineleme imperatif dillerde genellikle yavaş olarak algılanır. Fonksiyonel programlamada genellikle durum bu değildir. Çoğu zaman Haskell özyinelemeli fonksiyonları verimli şekilde işler.

İşte özyinelemeli fonksiyonun `C` versiyonu. Basitlik için tam sayı listesinin ilk `0` değeri ile bittiğini varsaydığıma dikkat edin.

```c
int evenSum(int *list) {
    return accumSum(0,list);
}

int accumSum(int n, int *list) {
    int x;
    int *xs;
    if (*list == 0) { // eger liste bossa
        return n;
    } else {
        x = list[0]; // x listenin ilk elemani olsun
        xs = list+1; // xs listenin ilk elemani haric geri kalani olsun
        if ( 0 == (x%2) ) { // eger x ciftse
            return accumSum(n+x, xs);
        } else {
            return accumSum(n, xs);
        }
    }
}
```

Bu kodu aklınızda tutun. Şimdi onu Haskell'e çevireceğiz. Ama ilk önce, size burada kullanacağımız üç basit ama kullanışlı fonksiyonu tanıtmam gerekiyor:

```haskell
even :: Integral a => a -> Bool
head :: [a] -> a
tail :: [a] -> [a]
```

`even` bir sayının çift olduğunu doğrular.

```haskell
even :: Integral a => a -> Bool
even 3  ⇒ False
even 2  ⇒ True
```

`head` bir listenin ilk elemanını döndürür.

```haskell
head :: [a] -> a
head [1,2,3] ⇒ 1
head []      ⇒ HATA
```

`tail` bir listenin ilk elemanı hariç tüm elemanlarını döndürür.

```haskell
tail :: [a] -> [a]
tail [1,2,3] ⇒ [2,3]
tail [3]     ⇒ []
tail []      ⇒ HATA
```

Görebileceğiniz üzere, herhangi bir boş olmayan `l` listesi için, `l ⇔ (head l):(tail l)`

***

[02_Hard_Part/11_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/11_Functions.lhs)


İlk Haskell çözümümüz. `evenSum` fonksiyonu bir listedeki tüm çift sayıların toplamını döndürür.

```haskell
-- Versiyon 1
evenSum :: [Integer] -> Integer

evenSum l = accumSum 0 l

accumSum n l = if l == []
                  then n
                  else let x = head l 
                           xs = tail l 
                       in if even x
                              then accumSum (n+x) xs
                              else accumSum n xs
```

Fonksiyonu denemek için `ghci`'ı kullanabilirsiniz.

```
% ghci
GHCi, version 7.0.3: http://www.haskell.org/ghc/  :? for help
Loading package ghc-prim ... linking ... done.
Loading package integer-gmp ... linking ... done.
Loading package base ... linking ... done.
Prelude> :load 11_Functions.lhs 
[1 of 1] Compiling Main             ( 11_Functions.lhs, interpreted )
Ok, modules loaded: Main.
*Main> evenSum [1..5]
6
```

Burada çalıştırılma örneğini görebilirsiniz: [^fn-2]

```
*Main> evenSum [1..5]
accumSum 0 [1,2,3,4,5]
1 is odd
accumSum 0 [2,3,4,5]
2 is even
accumSum (0+2) [3,4,5]
3 is odd
accumSum (0+2) [4,5]
4 is even
accumSum (0+2+4) [5]
5 is odd
accumSum (0+2+4) []
l == []
0+2+4
0+6
6
```

İmperatif bir dilden geliyorsanız her şey doğru gözüküyor olmalı. Aslında burada pek çok şey geliştirilebilir. Öncelikle, tipi genelleyebiliriz.

```haskell
evenSum :: Integral a => [a] -> a
```

[02_Hard_Part/11_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/11_Functions.lhs)

***

[02_Hard_Part/12_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/12_Functions.lhs)

Daha sonra, `where` veya `let` kullanarak alt fonksiyonlar tanımlayabiliriz. Bu şekilde `accumSum` fonksiyonu modülümüzün üst seviye isim uzayını *(namespace)* kirletmemiş olur.

```haskell
-- Versiyon 2
evenSum :: Integral a => [a] -> a

evenSum l = accumSum 0 l
    where accumSum n l = 
            if l == []
                then n
                else let x = head l 
                         xs = tail l 
                     in if even x
                            then accumSum (n+x) xs
                            else accumSum n xs
```

[02_Hard_Part/12_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/12_Functions.lhs)

***

[02_Hard_Part/13_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/13_Functions.lhs)

Sonra, örüntülü eşleme *(pattern matching)* kullanabiliriz.

```haskell
-- Versiyon 3
evenSum l = accumSum 0 l
    where 
        accumSum n [] = n
        accumSum n (x:xs) = 
             if even x
                then accumSum (n+x) xs
                else accumSum n xs
```

Peki örüntülü eşleme nedir? Genel parametre isimleri yerine değerlerin kendisini kullanın. [^fn-3]

`foo l = if l == [] then <x> else <y>` demek yerine, basitçe şöyle diyorsunuz:

```haskell
foo [] =  <x>
foo l  =  <y>
```

Ama örüntülü eşleme bundan daha fazlası. Aynı zamanda karmaşık bir değerin iç verişini takip etmenin bir yolu. Şu kodun yerine:

```haskell
foo l =  let x  = head l 
             xs = tail l
         in if even x 
             then foo (n+x) xs
             else foo n xs
```

şunu yazabiliriz:

```haskell
foo (x:xs) = if even x 
                 then foo (n+x) xs
                 else foo n xs
```

Bu çok kullanışlı bir özellik. Aynı zamanda kodumuzu daha kısa ve okunaklı kılıyor.

[02_Hard_Part/13_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/13_Functions.lhs)

***

[02_Hard_Part/14_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/14_Functions.lhs)

Haskell'de η sadeleştirmesi yaparak fonksiyonları basitleştirebilirsiniz. Örneğin, şunu yazmak yerine:

```
f x = (some expression) x
```

basitçe şunu yazabilirsiniz:

```
f = some expression
```

Bu metodu `l`'yi kaldirmak icin kullanalim:

```haskell
-- Version 4
evenSum :: Integral a => [a] -> a

evenSum = accumSum 0
    where 
        accumSum n [] = n
        accumSum n (x:xs) = 
             if even x
                then accumSum (n+x) xs
                else accumSum n xs
```

[02_Hard_Part/14_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/14_Functions.lhs)

***

[02_Hard_Part/15_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/15_Functions.lhs)

### 3.1.1. Üst Derece Fonksiyonlar

![Higher Order](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/escher_polygon.png)

Her şeyi daha da iyi yapmak için, üst derece fonksiyonları kullanmalıyız. Peki bu canavarlar nelerdir? Üst derece fonksiyonlarlar, başka fonksiyonları parametre olarak alan fonksiyonlardır.

Bazı örnekleri şöyledir:

```haskell
filter :: (a -> Bool) -> [a] -> [a]
map :: (a -> b) -> [a] -> [b]
foldl :: (a -> b -> a) -> a -> [b] -> a
```

Ufak adımlarla ilerleyelim.

```haskell
-- Version 5
evenSum l = mysum 0 (filter even l)
    where
      mysum n [] = n
      mysum n (x:xs) = mysum (n+x) xs
```

ki burada,

```haskell
filter even [1..10] ⇔  [2,4,6,8,10]
```

`filter` fonksiyonu `a -> Bool` tipinde bir fonksiyonu  ve `[a]` tipinde bir listeyi argüman olarak alır. Bu listeden sadece bu fonksiyon çalıştırıldığında `True` dönen elemanları dondurur.

Sonraki adımımız, döngüye benzer bir şeyi başarmak. `foldl` fonksiyonunu listede adım adım ilerlerken yanda bir değer biriktirmek için kullanacağız. `foldl` fonksiyonu aslında şu kalıbı alıp:

```haskell
myfunc list = foo initialValue list
    foo accumulated []     = accumulated
    foo tmpValue    (x:xs) = foo (bar tmpValue x) xs
```

Şu hale çevirir:

```haskell
myfunc list = foldl bar initialValue list
```

Eğer gerçekten bu sihirli şeyin nasıl çalıştığını görmek istiyorsanız, `foldl`'in tanımı şöyledir:

```haskell
foldl f z [] = z
foldl f z (x:xs) = foldl f (f z x) xs
```

```haskell
foldl f z [x1,...xn]
⇔  f (... (f (f z x1) x2) ...) xn
```

Ama Haskell tembel olduğu için `(f z x)`'in değerini hesaplamaz ve sadece yığının üstüne koyar. Bu yüzden genelde `foldl` yerine `foldl'` kullanırız; `foldl'`, `foldl` fonksiyonunun tembel olmayan versiyonudur. Eğer tembel ve tembel olmayan kavramlarını anlamıyorsanız, tasalanmayın, kodu `foldl` ve `foldl'` aynı şeylermiş gibi takip edin.

Şimdi `evenSum` fonksiyonumuzun yeni hali şöyle oldu:

```haskell
-- Versiyon 6
-- foldl' dogrudan erisilebilir
-- erismek icin once Data.List modulunu iceri almamiz gerekiyor
import Data.List
evenSum l = foldl' mysum 0 (filter even l)
  where mysum acc value = acc + value
```

Doğrudan lambda notasyonu kullanarak daha da basitleştirebiliriz. Böylece `mysum` isminde geçici bir fonksiyon yaratmak zorunda kalmayız.

```haskell
-- Versiyon 7
-- Genelde sadece ihtiyac duydugunuz fonksiyonlari
-- iceri almak daha iyi bir yontemdir
import Data.List (foldl')
evenSum l = foldl' (\x y -> x+y) 0 (filter even l)
```

Ve tabii ki, dikkat edelim ki:

```haskell
(\x y -> x+y) ⇔ (+)
```

[02_Hard_Part/15_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/15_Functions.lhs)

***

[02_Hard_Part/16_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/16_Functions.lhs)

Son olarak,

```haskell
-- Versiyon 8
import Data.List (foldl')
evenSum :: Integral a => [a] -> a
evenSum l = foldl' (+) 0 (filter even l)
```

`foldl'` anlaması kolay bir fonksiyon sayılmaz. Eğer alışık değilseniz, üzerinde biraz çalışmalısınız.

Burada ne olduğunu anlamanız için adım adım neler olduğuna bakalım:

```haskell
  evenSum [1,2,3,4]
⇒ foldl' (+) 0 (filter even [1,2,3,4])
⇒ foldl' (+) 0 [2,4]
⇒ foldl' (+) (0+2) [4] 
⇒ foldl' (+) 2 [4]
⇒ foldl' (+) (2+4) []
⇒ foldl' (+) 6 []
⇒ 6
```

Başka bir kullanışlı üst derece fonksiyon da `(.)` fonksiyonudur. `(.)` fonksiyonu matematiksel bileşimi *(composition)* ifade eder.

```haskell
(f . g . h) x ⇔  f ( g (h x))
```

Bu operatörden fonksiyonumuzda η sadeleştirmesi yapmak için faydanalabiliriz:

```haskell
-- Versiyon 9
import Data.List (foldl')
evenSum :: Integral a => [a] -> a
evenSum = (foldl' (+) 0) . (filter even)
```

Ayrıca, bazı kısımları daha iyi açıklamak için yeniden isimlendirebiliriz:

```haskell
-- Versiyon 10 
import Data.List (foldl')
sum' :: (Num a) => [a] -> a
sum' = foldl' (+) 0
evenSum :: Integral a => [a] -> a
evenSum = sum' . (filter even)
```

Şimdi bu fonksiyonel ifadelerle kodumuzun ne yöne doğru gittiğini tartışalım. Üst derece fonksiyonları kullanmak bize ne kazandırdı?

İlk önce, düşünebilirsiniz ki temel fark kısalık. Ama aslında, fark daha çok doğru düşünmeyle ilgili. Fonksiyonumuzu biraz değiştirmek istediğimizi varsayalım, örneğin bir listedeki tüm elemanların karesini alıp o çift kareleri toplamak istediğimizi.

```
[1,2,3,4] ▷ [1,4,9,16] ▷ [4,16] ▷ 20
```

Versiyon 10'u değiştirmek oldukça kolay:

```haskell
squareEvenSum = sum' . (filter even) . (map (^2))
squareEvenSum' = evenSum . (map (^2))
squareEvenSum'' = sum' . (map (^2)) . (filter even)
```

Sadece bir tane daha transformasyon fonksiyonu ekledik, o kadar. [^fn-4] 

```haskell
map (^2) [1,2,3,4] ⇔ [1,4,9,16]
```

`map` fonksiyonu basitçe bir listenin tüm elemanlarını etkiler.

Fonksiyon tanımının *içinde* herhangi bir şey değiştirmek zorunda kalmadık. Ama ek olarak, fonksiyonunuz hakkında daha matematiksel olarak akıl yürütebiliyorsunuz. Ayrıca fonksiyonunuzu diğerleriyle değişmeli de kullanabiliyorsunuz. Yani, yeni fonksiyonunuzu kullanarak `compose`, `map`, `fold`, `filter` işlemlerini yapabilirsiniz.

Versiyon 1'i değiştirmek de okura bir alıştırma olarak kalsın. ☺.

Eğer genellemenin sonuna geldiğimizi düşünüyorsanız, oldukça yanılıyorsunuz. Örneğin, bunu sadece liste değil başka herhangi bir özyinelemeli türde kullanmanın yolları var. Eğer nasıl olduğunu bilmek istiyorsanız, size şu eğlenceli makaleyi okumanızı öneriyorum: [Müz, Mercek, Zarf ve Dikenli Tellerle Fonksiyonel Programlama - Meijer, Fokkinga ve Paterson.](http://eprints.eemcs.utwente.nl/7281/01/db-utwente-40501F46.pdf)

Bu örnek size saf fonksiyonel programlamanın ne kadar güzel olduğunu göstermeli. Ne yazık ki, saf fonksiyonel programlama her kullanıma tam uygun değil. Ya da en azından öyle bir programlama dili henüz mevcut değil.

Haskell'in büyük güçlerinden biri de alana özel dil *(domain specific language)* yaratma yeteneğidir, böylece programlama paradigmasını değiştirebilirsiniz.

Aslında, Haskell imperatif stilde program yazmak istediğinizde de güzeldir. İlk Haskell öğrenmeye başladığımda bunu anlamak oldukça zor olmuştu. Genelde herkes fonksiyonel yaklaşımın üstünlüğünü anlatmaya çalışır. Daha sonra Haskell'le imperatif stil kullanmaya başlayınca, nasıl ve ne zaman öyle olacağını anlamak zor olabiliyor.

Bu Haskell süper gücüyle ilgili konuşmadan önce, Haskell'in başka bir temel yönünden bahsetmeliyiz: Tipler.

[02_Hard_Part/16_Functions.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/16_Functions.lhs)

## 3.2. Tipler

![Types](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/salvador-dali-the-madonna-of-port-lligat.jpg)

> TL, DR (Çok uzundu okumadım):
> * `type Ad = BaskaTip` sadece bir takma addir ve derleyici `Ad` ve `BaskaTip` arasında bir fark gözetmez.
> * `data Ad = AdYapısı BaskaTip` yapısında fark vardır.
> * `data` anahtar kelimesi özyinelemeli yapılar yaratabilir.
> * `deriving` sihirlidir ve sizin için fonksiyonlar yaratır.

Haskell'de tipler güçlü ve statiktir.

Peki bu neden önemli? Çünkü bu, hatalardan kaçınmanıza *yüksek derecede* yardımcı olur. Haskell'de hataların çoğu henüz derleme aşamasında yakalanır. Bunun asıl sebebi de tip çıkarımının derleme sırasında yapılmasıdır. Örneğin tip çıkarımı nerede yanlış parametreyi yanlış yerde kullandığınızı yakalar.

### 3.2.1. Tip Çıkarımı

Statik tip sistemi hızlı çalıştırma için genelde önemlidir. Ama çoğu statik tip sistemli diller kavramları genellemede kötüdür. Haskell'in kurtarıcı lütfü, tipleri kendi kendine *çıkarım* yaparak bulabilmesidir.

Basit bir örnekle başlayalım, Haskell'deki `square` fonksiyonu:

```haskell
square x = x * x
```

`square` fonksiyonu Haskell'deki herhangi bir sayısal değerin karesini alabilir. `square` fonksiyonuna parametre olarak `Int`, `Integer`, `Float`, `Fractional`, hatta `Complex` tipinde veri bile verebilirsiniz. Örnekle kanıtlayalım:

```
% ghci
GHCi, version 7.0.4:
...
Prelude> let square x = x*x
Prelude> square 2
4
Prelude> square 2.1
4.41
Prelude> -- load the Data.Complex module
Prelude> :m Data.Complex
Prelude Data.Complex> square (2 :+ 1)
3.0 :+ 4.0
```

`x :+ y` kompleks sayıların gösteriminde kullanılır. (x + iy)

Şimdi C'deki gerekli kod miktarıyla karşılaştıralım:

```c
int     int_square(int x) { return x*x; }

float   float_square(float x) {return x*x; }

complex complex_square (complex z) {
    complex tmp;
    tmp.real = z.real * z.real - z.img * z.img;
    tmp.img = 2 * z.img * z.real;
}

complex x,y;
y = complex_square(x);
```

C'de her tip için yeni bir fonksiyon yazmanız gerekiyor. Bunu aşmanın tek yolu ön-işlemciyi kullanarak üst-programlama hilelerine başvurmak. C++'ta daha iyi bir yol var, C++ şablonları:

```cpp
#include <iostream>
#include <complex>
using namespace std;

template<typename T>
T square(T x)
{
    return x*x;
}

int main() {
    // int
    int sqr_of_five = square(5);
    cout << sqr_of_five << endl;
    // double
    cout << (double)square(5.3) << endl;
    // complex
    cout << square( complex<double>(5,3) )
         << endl;
    return 0;
}
```

C++ bu yönden C'den çok daha iyi iş çıkartıyor. Ama daha karmaşık fonksiyonlar için söz dizimini takip etmek biraz daha zor olabilir: örnek için [bu makaleye](http://bartoszmilewski.com/2009/10/21/what-does-haskell-have-to-do-with-c/) bakabilirsiniz.

C++'ta bir fonksiyonun farklı tiplerle çalışması için ayrıca belirtmelisiniz. Haskell'de durum tam tersi. Fonksiyon varsayılan olarak olabildiğince genel tanımlanır.

Tip çıkarımı Haskell'de dinamik tip sistemli dillerin yarattığı özgürlük hissini yaratır. Ama dinamik tip sistemli dillerden farklı olarak çoğu hata çalışma zamanından önce yakalanır. Genelde Haskell kodu
> derleniyorsa, mutlaka kastettiğiniz şeyi yapıyordur.

***

[02_Hard_Part/21_Types.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/21_Types.lhs)

### 3.2.2. Tip Oluşturma

Kendi tiplerinizi oluşturabilirsiniz. İlk önce takma adlarla, yani tip eşanlamlılarıyla başlayalım. 

```haskell
type Name   = String
type Color  = String

showInfos :: Name ->  Color -> String
showInfos name color =  "Isim: " ++ name
                        ++ ", Renk: " ++ color
name :: Name
name = "Ahmet"
color :: Color
color = "Mavi"
main = putStrLn $ showInfos name color
```

[02_Hard_Part/21_Types.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/21_Types.lhs)

***

[02_Hard_Part/22_Types.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/22_Types.lhs)

Ancak bu çok fazla koruma yaratmıyor. `showInfos` fonksiyonuna verdiğiniz parametrelerin yerini değiştirip çalıştırmayı deneyin:
```
putStrLn $ showInfos color name
```

Derlenecek ve çalışacak. Aslında, `Name`, `Color` ve `String` tiplerini birbiriyle değiştirebilirsiniz, bir fark yaratmayacak. Derleyici hepsine aynıymış gibi muamele edecek.

Diğer bir yöntem de `data` anahtar kelimesini kullanarak kendi tiplerinizi yaratmak.

```haskell
data Name   = NameConstr String --NameConstr : isim yapicisi
data Color  = ColorConstr String --ColorConstr : renk yapicisi

showInfos :: Name ->  Color -> String
showInfos (NameConstr name) (ColorConstr color) =
      "Name: " ++ name ++ ", Color: " ++ color

name  = NameConstr "Ahmet"
color = ColorConstr "Mavi"
main = putStrLn $ showInfos name color
```

Ama şimdi `showInfos` için parametrelerin yerlerini değiştirirseniz, derleyici hata verecek! Yani bu bir daha yapmayacağınız muhtemel bir hata, ve kaçınmak için tek yapmanız gereken biraz daha uzun yazmak.

Yapıcıların da birer fonksiyon olduğuna dikkat edin:

```haskell
NameConstr  :: String -> Name
ColorConstr :: String -> Color
```

`data` anahtar kelimesinin genel söz dizimi de şöyledir:

```haskell
data TipAdi =   YapiciAdi  [tipler]
                | YapiciAdi2 [tipler]
                | ...
```

Genel kullanım tip adının ve yapıcı adının aynı olması yönündedir.

Örnek:

```haskell
data Complex = Num a => Complex a a
```

Kayıt *(record)* söz dizimini de kullanabilirsiniz:

```haskell
data VeriTipiAdi = VeriYapicisi {
                      alan_1 :: [alan_1 tipi]
                    , alan_2 :: [alan_2 tipi]
                    ...
                    , alan_n :: [alan_n tipi] }
```

Daha da iyisi, alanlara erişim sağlayan fonksiyonlar sizin için oluşturuluyor. Ayrıca bu tipte bir veri oluştururken alanların sırasını da kullanabilirsiniz.

Örnek:

```haskell
data Complex = Num a => Complex { real :: a, img :: a}
c = Complex 1.0 2.0
z = Complex { real = 3, img = 4 }
real c ⇒ 1.0
img z ⇒ 4
```

[02_Hard_Part/22_Types.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/22_Types.lhs)

***

[02_Hard_Part/23_Types.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/23_Types.lhs)

### 3.2.3. Özyinelemeli Tipler *(Recursive types)*

Daha önce özyinelemeli bir tiple karşılaşmıştık: listeler. Liste tipini -biraz daha uzun bir söz dizimiyle de olsa- kendimiz de oluşturabiliriz:

```haskell
data List a = Empty | Cons a (List a)
```

Eğer daha kolay bir söz dizimi yaratmak istiyorsanız, yapıcılar için iç notasyon *(infix)* tanımlayabilirsiniz.

```haskell
infixr 5 :::
data List a = Nil | a ::: (List a)
```

`infixr`'dan sonraki sayı önceliği belirtiyor.

Eğer bu veri tipini ekrana yazdırmak (`Show`), karakter dizisinden çevirmek (`Read`), eşitliğini test etmek (`Eq`) ve karşılaştırmak (`Ord`) istiyorsanız, Haskell'e sizin için gerekli fonksiyonları oluşturmasını söyleyebilirsiniz.

```haskell
infixr 5 :::
data List a = Nil | a ::: (List a) 
              deriving (Show,Read,Eq,Ord)
```

Veri tipi tanımınıza `deriving (Show)`'u eklediğinizde, Haskell sizin için bir `show` fonksiyonu yaratır. (*(deriving)* İngilizce'de türeme demektir.) Yakında kendi `show` fonksiyonunuzu nasıl kullanabileceğinizi göreceğiz.

```haskell
convertList [] = Nil
convertList (x:xs) = x ::: convertList xs

main = do
      print (0 ::: 1 ::: Nil)
      print (convertList [0,1])
```

Bu şu çıktıyı verir:

```
0 ::: (1 ::: Nil)
0 ::: (1 ::: Nil)
```

[02_Hard_Part/23_Types.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/23_Types.lhs)

***

[02_Hard_Part/30_Trees.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/30_Trees.lhs)

### 3.2.4. Ağaçlar

![Trees](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/magritte-l-arbre.jpg)

Başka bir standart örnek verelim: ikili ağaçlar.

```haskell
import Data.List

data BinTree a = Empty
                 | Node a (BinTree a) (BinTree a)
                              deriving (Show)
```

Şimdi de bir listeyi sıralı bir ikili ağaca dönüştüren bir fonksiyon yazalım:

```haskell
treeFromList :: (Ord a) => [a] -> BinTree a
treeFromList [] = Empty
treeFromList (x:xs) = Node x (treeFromList (filter (<x) xs))
                             (treeFromList (filter (>x) xs))
```

Fonksiyonun ne kadar okunaklı olduğunu görebiliyor musunuz? Düz Türkçe olarak yazarsak:
* boş liste, boş ağaca çevrilir.
* bir liste `(x:xs)`, bir ağaca çevrilir ki,
    * kok `x`'tır.
    * sol alt ağaç, `xs`'in `x`'ten kesin olarak küçük elemanlarından oluşturulur.
    * sağ alt ağaç, `xs`'in `x`'ten kesin olarak büyük elemanlarından oluşturulur.

```haskell
main = print $ treeFromList [7,2,4,8]
```

Şu sonucu alıyor olmalısınız:

```haskell
Node 7 (Node 2 Empty (Node 4 Empty Empty)) (Node 8 Empty Empty)
```

Bu ağacımızın düzgün ama zor anlaşılır bir temsili notasyonu.

[02_Hard_Part/30_Trees.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/30_Trees.lhs)

***

[02_Hard_Part/31_Trees.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/31_Trees.lhs)

Öylesine, ağacımız için daha iyi bir gösterim kodu yazalım. Ben genel olarak ağaçları daha iyi göstermek için bir fonksiyon yazarken eğlendim, eğer bu kısmı takip etmeyi zor buluyorsanız atlayabilirsiniz, bir sorun olmaz.

Değiştirmemiz gereken bazı şeyler var. `BinTree` tipımizden `deriving (Show)` kısmını kaldırıyoruz. Ayrıca, BinTree tipimizi (`Eq` ve `Ord`)'un sınıflarından türetmek de eşitlik ve karşılaştırma testleri yapmamızı sağlayacaktır.

```haskell
data BinTree a = Empty
                 | Node a (BinTree a) (BinTree a)
                  deriving (Eq,Ord)
```

`deriving (Show)` kısmı olmadan Haskell sizin için bir `show` metodu yaratmaz. Biz `show` metodu için kendi versiyonumuzu yazacağız. Bunu başarmak için, yeni yarattığımız `BinTree a`'nin `Show` tip sınıfının bir üyesi olduğunu belirtmemiz gerekiyor. Bunun için genel söz dizimi şöyle:

```haskell
instance Show (BinTree a) where
   show t = ... -- burada kendi fonksiyonunuzu tanimliyorsunuz
```

Benim bir ikili ağacı göstermek için yazdığım versiyon aşağıda. Karmaşıkmış gibi görünüyor ama endişelenmeyin. Daha garip nesneleri de göstermesi için bazı iyileştirmeler yaptım.

```haskell
-- BinTree'a nin Show tip sinifina uye oldugunu belirtin
instance (Show a) => Show (BinTree a) where
  -- kokten once bir '<' ile baslayacagiz
  -- satir basina da : koyacagiz
  show t = "< " ++ replace '\n' "\n: " (treeshow "" t)
    where
    -- treeshow pref Tree
    --   bu fonksiyon her satira pref ile baslayarak bir agaci gosterecek
    -- Bos agaci gostermeyecek
    treeshow pref Empty = ""
    -- Yaprak
    treeshow pref (Node x Empty Empty) =
                  (pshow pref x)

    -- Sag alt agac bos
    treeshow pref (Node x left Empty) =
                  (pshow pref x) ++ "\n" ++
                  (showSon pref "`--" "   " left)

    -- Sol alt agac bos
    treeshow pref (Node x Empty right) =
                  (pshow pref x) ++ "\n" ++
                  (showSon pref "`--" "   " right)

    -- Sol ve sag alt agaclari bos olmayan agac
    treeshow pref (Node x left right) =
                  (pshow pref x) ++ "\n" ++
                  (showSon pref "|--" "|  " left) ++ "\n" ++
                  (showSon pref "`--" "   " right)

    -- Agaci guzel gostermek icin on ekler kullan
    showSon pref before next t =
                  pref ++ before ++ treeshow (pref ++ next) t

    -- pshow "\n"'i' "\n"++pref ile degistiriyor
    pshow pref x = replace '\n' ("\n"++pref) (show x)

    -- bir karakteri diger karakter dizisi ile degistiriyor
    replace c new string =
      concatMap (change c new) string
      where
          change c new x
              | x == c = new
              | otherwise = x:[] -- "x"
```

`treeFromList` metodu tamamen aynı kalıyor.

Şimdi, görelim nasıl oluyormuş:

```haskell
main = do
  putStrLn "Tam sayi ikili agaci:"
  print $ treeFromList [7,2,4,8,1,3,6,21,12,23]
```

```
Tam sayi ikili agaci:
< 7
: |--2
: |  |--1
: |  `--4
: |     |--3
: |     `--6
: `--8
:    `--21
:       |--12
:       `--23
```

Çok daha iyi, değil mi? Ağacın kökü `<` karakteriyle başlayan satırda gösteriliyor. Takip eden her satır `:` işareti ile başlıyor. Ağacımızda başka tiplerde veri de kullanabilirdik.

```haskell
  putStrLn "\nKarakter dizisi ikili agaci:"
  print $ treeFromList ["foo","bar","baz","gor","yog"]
```

```
Karakter dizisi ikili agaci:
< "foo"
: |--"bar"
: |  `--"baz"
: `--"gor"
:    `--"yog"
```

Ağaçların eşitliğini ve büyük/küçüklüğünü test edebildiğimiz için, ağaçlardan ağaç da yapabiliriz!

```haskell
  putStrLn "\nKarakter ikili agaclarinin ikili agaci:"
  print ( treeFromList
           (map treeFromList ["baz","zara","bar"]))
```

```
Karakter ikili agaclarinin ikili agaci:
< < 'b'
: : |--'a'
: : `--'z'
: |--< 'b'
: |  : |--'a'
: |  : `--'r'
: `--< 'z'
:    : `--'a'
:    :    `--'r'
```

Ağacın her satırını bu yüzden `:` ile başlatmıştım. (kök hariç)

![Yo](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/yo_dawg_tree.jpg)

```haskell
  putStrLn "\nKarakter ikili agaclarinin ikili agaci:"
  print $ (treeFromList . map (treeFromList . map treeFromList))
             [ ["YO","DAWG"]
             , ["I","HEARD"]
             , ["I","HEARD"]
             , ["YOU","LIKE","TREES"] ]
```

ki bu da şuna denk:

```haskell
print ( treeFromList (
          map treeFromList
             [ map treeFromList ["YO","DAWG"]
             , map treeFromList ["I","HEARD"]
             , map treeFromList ["I","HEARD"]
             , map treeFromList ["YOU","LIKE","TREES"] ]))
```

ve şu çıktıyı vermeli:

```
Karakter ikili agaclarinin ikili agaci:
< < < 'Y'
: : : `--'O'
: : `--< 'D'
: :    : |--'A'
: :    : `--'W'
: :    :    `--'G'
: |--< < 'I'
: |  : `--< 'H'
: |  :    : |--'E'
: |  :    : |  `--'A'
: |  :    : |     `--'D'
: |  :    : `--'R'
: `--< < 'Y'
:    : : `--'O'
:    : :    `--'U'
:    : `--< 'L'
:    :    : `--'I'
:    :    :    |--'E'
:    :    :    `--'K'
:    :    `--< 'T'
:    :       : `--'R'
:    :       :    |--'E'
:    :       :    `--'S'
```

Tekrar edilen ağaçların eklenmediğine dikkat edin; `"I","HEARD"`'e denk gelen sadece bir ağaç var. Bunun için (neredeyse) hiçbir şey yapmadık, çünkü Tree yapısını `Eq` tip sınıfından türettik.

Bu yapının ne kadar müthiş olduğunu görebiliyor musunuz: Sadece sayılardan, karakter dizilerinden, karakterlerden değil, başka ağaçlardan da ağaçlar yapabiliyoruz. İstersek ağaçlardan oluşan ağaçlardan oluşan ağaç bile yapabiliriz!

[02_Hard_Part/31_Trees.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/31_Trees.lhs)

***

[02_Hard_Part/40_Infinites_Structures.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/40_Infinites_Structures.lhs)

## 3.3. Sonsuz Yapılar

![Infinite](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/escher_infinite_lizards.jpg)

Haskell'in *tembel* olduğu sıkça söylenir.

Aslında, eğer biraz titizseniz, Haskell'in [*non-strict*](http://www.haskell.org/haskellwiki/Lazy_vs._non-strict) (aceleci olmayan, kesin olmayan) olduğunu söylemelisiniz. Tembellik sadece *non-strict* dillerin ortak bir tatbikidir.

Öyleyse "non-strict" tam olarak ne anlama geliyor? Haskell vikisiden alıntılayalım:

> Sadeleştirme (hesaplama için matematiksel terim) dıştan içe doğru ilerler.
>
> yani eğer `(a+(b*c))`'yi ele alıyorsanız, önce `+`'yi sadeleştirirsiniz, sonra iç `(b*c)`'yi sadeleştirirsiniz.

Örneğin Haskell'de şunu yapabilirsiniz:

```haskell
-- numbers = [1,2,..]
numbers :: [Integer]
numbers = 0:map (1+) numbers

take' n [] = []
take' 0 l = []
take' n (x:xs) = x:take' (n-1) xs

main = print $ take' 10 numbers
```

Sonra duruyor.

Neden?

`numbers` değişkeninin tamamını hesaplamak yerine, sadece ihtiyacı olan elemanları, ihtiyacı olduğu zaman hesaplıyor.

Ayrıca, Haskell'de sonsuz listeler için bir notasyon olduğunu da söylemiş olayım:

```haskell
[1..]   ⇔ [1,2,3,4...]
[1,3..] ⇔ [1,3,5,7,9,11...]
```

ve çoğu fonksiyon da onlarla çalışır. Ayrıca, Haskell'de, bizim `take'` fonksiyonumuza denk bir `take` fonksiyonu mevcuttur.

[02_Hard_Part/40_Infinites_Structures.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/40_Infinites_Structures.lhs)

***

[02_Hard_Part/41_Infinites_Structures.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/41_Infinites_Structures.lhs)

Sıralı ikili ağaç yaptığımızı varsayalım. Sonsuz bir ikili ağaç şöyle olur:

```haskell
nullTree = Node 0 nullTree nullTree
```

Her düğümün 0'a eşit olduğu, geçerli ve tam bir ikili ağaç. Şimdi bu objeyi aşağıdaki fonksiyonla işleyebileceğimi kanıtlayacağım:

```haskell
-- bir BinTree'nin tum elemanlarini
-- belli bir derinlige kadar al
treeTakeDepth _ Empty = Empty
treeTakeDepth 0 _     = Empty
treeTakeDepth n (Node x left right) = let
          nl = treeTakeDepth (n-1) left
          nr = treeTakeDepth (n-1) right
          in
              Node x nl nr
```

Bu programın sonucunu görelim.

```haskell
main = print $ treeTakeDepth 4 nullTree
```

Kodumuz derleniyor, çalışıyor ve şu sonucu vererek duruyor:

```
<  0
: |-- 0
: |  |-- 0
: |  |  |-- 0
: |  |  `-- 0
: |  `-- 0
: |     |-- 0
: |     `-- 0
: `-- 0
:    |-- 0
:    |  |-- 0
:    |  `-- 0
:    `-- 0
:       |-- 0
:       `-- 0
```

Nöronlarınızı biraz daha ısındırmak için daha ilginç bir ağaca bakalım:

```haskell
iTree = Node 0 (dec iTree) (inc iTree)
        where
           dec (Node x l r) = Node (x-1) (dec l) (dec r) 
           inc (Node x l r) = Node (x+1) (inc l) (inc r) 
```

Bu ağacı oluşturmanın başka bir yolu da üst derece fonksiyonları kullanmaktır. Bu fonksiyon `map` fonksiyonuna benziyor, ama listeler yerine `BinTree`'ler üzerinde çalışıyor. Ortaya şöyle bir fonksiyon çıkacak:

```haskell
-- bir fonksiyonu agacin her dugumune uygular
treeMap :: (a -> b) -> BinTree a -> BinTree b
treeMap f Empty = Empty
treeMap f (Node x left right) = Node (f x) 
                                     (treeMap f left) 
                                     (treeMap f right)
```

*Not:* Bunun hakkında burada daha fazla konuşmayacağım. Eğer `map`'in diğer veri yapılarına genellemesiyle ilgileniyorsanız, *functor*ları ve `fmap`'i araştırın.

Şimdi tanımımız şöyle oldu:

```haskell
infTreeTwo :: BinTree Int
infTreeTwo = Node 0 (treeMap (\x -> x-1) infTreeTwo) 
                    (treeMap (\x -> x+1) infTreeTwo) 
```

Şunun sonucuna bakalım:

```haskell
main = print $ treeTakeDepth 4 infTreeTwo
```

```
<  0
: |-- -1
: |  |-- -2
: |  |  |-- -3
: |  |  `-- -1
: |  `-- 0
: |     |-- -1
: |     `-- 1
: `-- 1
:    |-- 0
:    |  |-- -1
:    |  `-- 1
:    `-- 2
:       |-- 1
:       `-- 3
```

[02_Hard_Part/41_Infinites_Structures.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/02_Hard_Part/41_Infinites_Structures.lhs)

# 4. Çok Zor Kısım

Buraya kadar geldiyseniz tebrikler! Şimdi gerçekten çok zor kısım başlayabilir.

Eğer benim gibiyseniz, fonksiyonel stili anlamış olmalısınız. Ayrıca tembelliğin varsayılan olmasının avantajlarını da biraz anlamış olmalısınız. Ama gerçek bir program yapmaya nereden başlamanız gerektiğini bilmiyorsunuz. Özellikle de şu soruların cevaplarını:
* Yan etkilerle nasıl bas edilir?
* Neden IO (girdi-çıktı) ile baş etmek için imperatifliğe benzer bir notasyon var?

Karmaşık cevaplara hazır olun. Ama hepsi sonunda çok faydalı.

***

[03_Hell/01_IO/01_progressive_io_example.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/01_IO/01_progressive_io_example.lhs)

## 4.1. IO ile Baş Etmek

![IO](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/magritte_carte_blanche.jpg)

> TL;DR: (Çok uzundu okumadım)

> IO ile uğraşan tipik bir fonksiyon imperatif bir programa çok benzer:

```haskell
f :: IO a
f = do
  x <- action1
  action2 x
  y <- action3
  action4 x y
```

> * Bir nesnenin değerini belirtmek için `<-` kullanıyoruz.
> * Her satırın tipi `IO *`, bu örnekte:
   * `action1 :: IO b`
   * `action2 x :: IO ()`
   * `action3 :: IO c`
   * `action4 x y :: IO a`
   * `x :: b, y :: c`
   * Az sayıda nesnenin tipi `IO a`'dir, bu seçmenize yardım eder. Farklı olarak, burada saf fonksiyonları doğrudan kullanamazsınız. Saf fonksiyonları kullanmak için örneğin `action2 (saffonksiyon x)` yazabilirsiniz.

Bu bölümde size IO kullanmayı anlatacağım, ama nasıl çalıştığını değil. Haskell'in nasıl saf ve saf olmayan kısımları ayırdığını göreceksiniz.

Söz dizimindeki detayları anlamaya çalışmak için durmayın. Cevaplar ilerleyen bölümde gelecek.

Ne yapalım?

> Kullanıcıdan bir sayı listesi girmesini isteyin. Sayıların toplamını ekrana yazdırın.

```haskell
toList :: String -> [Integer]
toList input = read ("[" ++ input ++ "]")

main = do
  putStrLn "Bir sayi listesi girin (virgulle ayirin):"
  input <- getLine
  print $ sum (toList input)
```

Bu programın ne yaptığı oldukça açık olmalı. Tiplere biraz daha ayrıntılı bakalım.

```
putStrLn :: String -> IO ()
getLine  :: IO String
print    :: Show a => a -> IO ()
```

Daha da ilginç şekilde, `do` bloğunun içindeki her ifadenin `IO a` tipinde olduğuna dikkat edelim.

```haskell
main = do
  putStrLn "Enter ... " :: IO ()
  getLine               :: IO String
  print Something       :: IO ()
```

Ayrıca `<-` işaretinin etkisine de dikkat edelim.

```
do
 x <- something -- bir seyler  
```

Eğer `something :: IO a` tipinde ise `x :: a`'dir.

`IO` kullanımıyla ilgili başka bir önemli nokta da şudur: `do` bloğunun içindeki tüm satırlar şu iki şekilden birinde olmalı:

```haskell
action1             :: IO a
                    -- bu durumda, a = ()
```

veya

```haskell
deger <- action2    -- ki burada
                    -- bar z t :: IO b
                    -- deger   :: b
```

Bu iki çeşit komut aksiyonları sıralamanın iki farklı yolunu ifade ediyor. Bu cümlenin anlamı önümüzdeki bölümün sonunda netleşecek.

[03_Hell/01_IO/01_progressive_io_example.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/01_IO/01_progressive_io_example.lhs)

***

[03_Hell/01_IO/02_progressive_io_example.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/01_IO/02_progressive_io_example.lhs)

Simdi programimizin nasil davrandigina bakalim. Ornegin, eger kullanici garip bir sey girerse ne olacak? Deneyelim:

```
    % runghc 02_progressive_io_example.lhs
    Enter a list of numbers (separated by comma):
    foo
    Prelude.read: no parse
```

Püf! Garip bir hata mesajından sonra programımız çöktü! İlk iyileştirmemiz daha anlaşılır bir hata mesajı vermek olsun.

Bunu yapmak için önce bir şeylerin yanlış gittiğini tespit edebilmemiz gerekiyor. İşte bunu yapmanın bir yolu: `Maybe` (Türkçesi: belki) tipini kullanmak. Bu Haskell'de sık kullanılan bir tiptir.

```haskell
import Data.Maybe
```

Peki bu nedir ki? `Maybe` bir parametre alan bir tiptir. Tanımı da şudur:

```haskell
data Maybe a = Nothing | Just a
```

Bu bir değer okumaya veya yaratmaya çalışırken bir hata olduğunu ifade etmenin güzel bir yoludur. `maybeRead` fonksiyonu bunun iyi bir örneği. Bu `read`'e [^fn-5] benzer bir fonksiyon, ama eğer bir şeyler yanlış giderse dönen değer `Nothing` olacak. Eğer bir değer okuyabilirse, dönen değer `Just <değer>` olacak. Bu fonksiyonu çok anlamaya çalışmayın; `read`'den daha alt seviye bir fonksiyon olan `reads`'i kullanıyorum.

```haskell
maybeRead :: Read a => String -> Maybe a
maybeRead s = case reads s of
                  [(x,"")]    -> Just x
                  _           -> Nothing
```

Biraz daha okunaklı olması için, şu şekilde giden bir fonksiyon tanımlayalım: Eğer karakter dizisinin formatı yanlışsa, `Nothing` döndürülecek. Aksi halde, örneğin "1,2,3" için `Just [1,2,3]` döndürülecek.

```haskell
getListFromString :: String -> Maybe [Integer]
getListFromString str = maybeRead $ "[" ++ str ++ "]"
```

Sonrasında tek yapmamız gereken dönen değeri ana fonksiyonumuzda test etmek.

```haskell
main :: IO ()
main = do
  putStrLn "Bir sayi listesi girin (virgulle ayirin):"
  input <- getLine
  let maybeList = getListFromString input in
      case maybeList of
          Just l  -> print (sum l)
          Nothing -> error "Kotu format. Hoscakalin."
```

Hata durumunda, iyi sayılabilecek bir hata mesajı göstermiş olalım.

`main` fonksiyonunun `do` bloğundaki her ifadenin tipinin `IO a` formatında olduğuna dikkat edin. Tek bilmediğiniz yapı `error`. Ama `error msg` de gerekli tipi alıyor. (burada `IO ()`).

Bu programda fark etmeniz gereken şey tanımladığımız fonksiyonların tipleri. Yazdığımız fonksiyonlar arasında sadece bir tanesinin tipinde `IO` var: `main`. Bu demek oluyor ki `main` saf olmayan bir fonksiyon. Ama `main` içinde saf bir fonksiyon olan  `getListFromString` kullanılıyor. Yani sadece bakarak bile fonksiyonların saf olup olmadıklarını anlayabilirsiniz.

Peki saflık neden önemlidir? Bir sürü avantajının ucu şunlar:

* Saf kod hakkında mantık yürütmek saf olmayan kod hakkında mantık yürütmekten çok daha kolaydır.
* Saflık sizi yan etkilerden ötürü kolayca test edemeyeceğiniz hatalardan korur.
* Saf fonksiyonları herhangi bir sırayla veya eşzamanlı olarak hiçbir risk olmadan hesaplayabilirsiniz.

İşte bu yüzden, olabildiğince fazla kodunuzu saf fonksiyonlarla yazmalısınız.

[03_Hell/01_IO/02_progressive_io_example.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/01_IO/02_progressive_io_example.lhs)

***

[03_Hell/01_IO/03_progressive_io_example.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/01_IO/03_progressive_io_example.lhs)

Sonraki adımımız kullanıcı geçerli bir cevap girene kadar tekrar tekrar sormak olsun.

İlk bölümü aynen kullanabiliriz:

```haskell
import Data.Maybe

maybeRead :: Read a => String -> Maybe a
maybeRead s = case reads s of
                  [(x,"")]    -> Just x
                  _           -> Nothing
getListFromString :: String -> Maybe [Integer]
getListFromString str = maybeRead $ "[" ++ str ++ "]"
```

Şimdi kullanıcı doğru bir girdi yazana kadar tekrar soran bir fonksiyon yazalım:

```
askUser :: IO [Integer]
askUser = do
  putStrLn "Bir sayi listesi girin (virgulle ayirin):"
  input <- getLine
  let maybeList = getListFromString input in
      case maybeList of
          Just l  -> return l
          Nothing -> askUser
```

Fonksiyonumuzun tipi `IO [Integer]`. Bu demek oluyor ki belirli IO aksiyonları sonucu `[Integer]` tipinde bir değer elde ediyoruz. Bazıları bunu şöyle açıklıyor:

> «IO içinde [Integer] var.»

Eğer bunun arkasındaki detayları anlamak istiyorsanız, sonraki bölümü okumanız gerekecek. Ama eğer IO'yu sadece *kullanmak* istiyorsanız, biraz tekrar yapın ve tipler hakkında düşünmeniz gerektiğini hatırlayın.

Son olarak, `main` fonksiyonumuz çok daha basit:

```haskell
main :: IO ()
main = do
  list <- askUser
  print $ sum list
```

IO'ya girişimizi bitirdik. Biraz hızlıydı, değil mi? Hatırlamamız gereken temel şeyler sunlar:

* `do` bloğunun içinde, her ifade `IO a` tipinde olmalı. Bu sizi belli ifadelerle kısıtlıyor. Örneğin, `getLine`, `print`, `putStrLn`, vs.
* Saf fonksiyonları olabildiğince saf olmayan kısımların dışında tutmaya çalışın, işin mümkün olduğunca büyük kısmını saf fonksiyonlara yaptırın.
* `IO a`, `a` tipinde bir eleman döndüren IO aksiyonu demektir. `IO` aksiyonu temsil eder, `IO a` aslında bir fonksiyonun tipidir. Daha fazlasını merak ediyorsanız sonraki bölümü okuyun.

Biraz çalışırsanız, `IO` kullanabiliyor olmalısınız.

> Alıştırma: Tüm argümanlarının toplamını alan bir program yazın. İpucu: `getArgs` fonksiyonunu kullanın.

[03_Hell/01_IO/03_progressive_io_example.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/01_IO/03_progressive_io_example.lhs)

## 4.2. IO'nun Püf Noktası

![Bu bir pipo degildir](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/magritte_pipe.jpg)

> Bu bölüm için TL; DR (Çok uzundu okumadım)

> Saf ve saf olmayan kısımları ayırmak için, `main` dünyanın durumunu değiştiren bir fonksiyon olarak tanımlanır.

```haskell
main :: World -> World
```

> Bir fonksiyon, sadece ve sadece bu tipe sahipse yan etkide bulunur. Tipik bir `main` fonksiyonuna bakalım:

```haskell
main w0 =
    let (v1,w1) = action1 w0 in
    let (v2,w2) = action2 v1 w1 in
    let (v3,w3) = action3 v2 w2 in
    action4 v3 w3
```

> Sonraki aksiyona aktarmamız gereken bir sürü geçici elemanımız var. (burada `w1`, `w2` ve `w3`)

> `bind` veya `(>>=)` fonksiyonu yaratıyoruz. `bind` ile artık geçici isimlere ihtiyacımız yok.

```haskell
main =
  action1 >>= action2 >>= action3 >>= action4
```

> Bonus: Haskell'in şöyle bir söz dizimsel kolaylığı var:

```haskell
main = do
  v1 <- action1
  v2 <- action2 v1
  v3 <- action3 v2
  action4 v3
```

***

Neden böyle garip bir söz dizimi kullandık ve bu `IO` tipi tam olarak nedir? Anlaşılmaz duruyor ama, değil.

Şimdilik, programımızın saf kısımlarını bir kenara bırakıp saf olmayan kısımlar üzerinde yoğunlaşalım:

```haskell
askUser :: IO [Integer]
askUser = do
  putStrLn "Bir sayi listesi girin (virgulle ayirin):"
  input <- getLine
  let maybeList = getListFromString input in
      case maybeList of
          Just l  -> return l
          Nothing -> askUser

main :: IO ()
main = do
  list <- askUser
  print $ sum list
```

İlk tepki: İmperatif duruyor. Haskell saf olmayan kodu imperatif gösterecek kadar güçlüdür. Örneğin, isterseniz Haskell'de `while` yapısı yaratabilirsiniz. Hatta, `IO` ile uğraşman için imperatif stip genellikle daha uygundur.

Ama notasyonun alışılmışın dışında olduğunu fark etmiş olmalısınız. Şimdi bunun sebeplerini detaylıca tartışalım.

Saf olmayan bir dilde, dünyanın durumu devasa ve gizli bir global değişken olarak görülebilir. Bu gizli değişkene dildeki tüm fonksiyonlar tarafından erişilebilir. Örneğin herhangi bir fonksiyon içinde bir dosya ile okuma/yazma işlemleri yapabilirsiniz. Dosyanın var olup olmaması "dünya"nızın alabileceği olası durumlardır.

Haskell'de bu durum gizli değildir. Tam tersine, Haskell'de `main`'in dünyanızın durumunu değiştirme olasılığı olduğu özellikle ayrıca söylenir. Bu fonksiyonun tipi şunun gibi bir şeydir:

```haskell
main :: World -> World
```

Bu değişkene tüm fonksiyonların erişimi yoktur. Erişimi olan fonksiyonlar saf değildir. Dünya değişkenine erişimi olmayan fonksiyonlar ise saftır. [^fn-6]

Haskell, dünyanın durumunu `main` fonksiyonuna bir girdi değişkeni olarak görür. Ama `main`'in asıl tipi suna daha yakındır: [^fn-7]

```haskell
main :: World -> ((),World)
```

`()` tipi birim tipidir. Burda görülecek bir şey yok.

Şimdi bunu aklımızda tutarak `main` fonksiyonumuzu baştan yazalım:

```haskell
main w0 =
    let (list,w1) = askUser w0 in
    let (x,w2) = print (sum list,w1) in
    x
```

İlk olarak, yan etkisi olan tüm fonksiyonların şu tipte olması gerektiğini hatırlayalım:

```haskell
World -> (a,World)
```

Burada `a` sonucun tipi oluyor. Örneğin `getChar` fonksiyonu bu durumda `World -> (Char,World)` tipindedir.

Dikkat edilmesi gereken diğer bir şey ise hesaplama/değerlendirme sırası. Örneğin `f a b`'yi hesaplarken birden fazla seçeneğiniz var:

* önce `a`'yi, sonra `b`'yi, sonra da `f a b`'yi hesapla.
* önce `b`'yi, sonra `a`'yi, sonra da `f a b`'yi hesapla.
* `a`'yi ve `b`'yi paralel olarak, sonra da `f a b`'yi hesapla.

Bu böyle çünkü dilin saf kısmında çalışıyoruz.

Şimdi, eğer `main` fonksiyonuna bakarsanız, ilk satırı ikinci satırdan önce hesaplamanız gerektiği açık, çünkü ikinci satırda birinci satırda elde ettiğiniz bir değeri parametre olarak kullanıyorsunuz.

Bu işe yarıyor. Derleyici her adımda yeni bir gerçek dünya tanımı/kodu (*id*) sağlıyor. Gizli olarak, `print` şöyle işliyor:

* ekrana bir şey yazdır
* dünyanın id'sini değiştir.
* `((), yeni dünya id'si)` değerini döndür.

Şimdi, eğer `main` fonksiyonunun stiline bakarsanız, biraz garip olduğunu göreceksiniz. Aynısını `askUser` fonksiyonuna da uygulayalım:

```haskell
askUser :: World -> ([Integer],World)
```

Öncesi:

```haskell
askUser :: IO [Integer]
askUser = do
  putStrLn "Bir sayi listesi girin:"
  input <- getLine
  let maybeList = getListFromString input in
      case maybeList of
          Just l  -> return l
          Nothing -> askUser
```

Sonrası:

```haskell
askUser w0 =
    let (_,w1)     = putStrLn "Bir sayi listesi girin:" in
    let (input,w2) = getLine w1 in
    let (l,w3)     = case getListFromString input of
                      Just l   -> (l,w2)
                      Nothing  -> askUser w2
    in
        (l,w3)
```

Benzer, ama biraz daha garip. Tüm şu geçici `w?`'lere bakın.

Çıkarılacak ders şu: Saf fonksiyonel dillerdeki naif IO uygulamaları gariptir!

Şanslıyız ki, bu sorunu halletmek için daha iyi bir yol var. Bir kalip goruyoruz, her satir su sekilde:

```haskell
let (y,w') = action x w in
```

Herhangi bir satır için ilk `x` argümanı gerekmese bile. Dönen sonucun tipi bir ikili, `(sonuç, yeniDünyaDeğeri)`. Her `f` fonksiyonu şuna benzer bir tipe sahip olmak zorunda:

```haskell
f :: World -> (a,World)
```

Her zaman aynı kalıbı takip ettiğimize dikkat edin:

```haskell
let (y,w1) = action1 w0 in
let (z,w2) = action2 w1 in
let (t,w3) = action3 w2 in
...
```

Her aksiyon 0'dan n'ye kadar parametre alabilir. Ve özellikle, her aksiyon bir üstündeki satırın sonucundan parametre alabilir.

Örneğin, şöyle diyebiliriz:

```haskell
let (_,w1) = action1 x w0   in
let (z,w2) = action2 w1     in
let (_,w3) = action3 x z w2 in
...
```

Ve tabii ki `actionN w :: (World) -> (a,World)`.

> Önemli: Dikkat edilmesi gereken iki kalıp var:

```haskell
let (x,w1) = action1 w0 in
let (y,w2) = action2 x w1 in
```

> ve

```haskell
let (_,w1) = action1 w0 in
let (y,w2) = action2 w1 in
```

***

![Joker](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/jocker_pencil_trick.jpg)

Şimdi biraz sihirbazlık yapalım. Geçici dünya sembolünü "yok edelim". İki satırı `bind` ile birbirine bağlayacağız. İşe `bind` fonksiyonunu tanımlayarak başlayalım. Fonksiyonun tipi başta biraz korkutucu gelebilir:

```haskell
bind :: (World -> (a,World))
        -> (a -> (World -> (b,World)))
        -> (World -> (b,World))
```

Ama hatırlayın ki `(World -> (a,World))` IO aksiyonlarının tipidir. Daha açık olması için ona yeni bir isim verelim:

```haskell
type IO a = World -> (a, World)
```

Bazı fonksiyon örnekleri:

```haskell
getLine :: IO String
print :: Show a => a -> IO ()
```

`getLine` dünyayı parametre olarak alan ve `(String,World)` ikilisini döndüren bir IO aksiyonudur. Bu şöyle özetlenebilir: `getLine`, `IO String` tipindedır, ki bunu "IO içine gömülmüş" String döndüren bir IO aksiyonu olarak görebiliriz.

`print` fonksiyonu da ayrıca ilginçtir. Gösterilebilir bir argüman alır, ama aslında iki argüman almaktadır. İlki ekrana yazdırılacak değerdir, ikincisi de dünyanın durumudur. Sonrasında ise `((),World)` ikilisini döndürür. Bu fonksiyonun dünyanın durumunu değiştirdiği ama başka bir veri üretmediği anlamına gelir.

Bu tip, `bind` fonksiyonun tipini basitleştirmemize yardımcı olur:

```haskell
bind :: IO a
        -> (a -> IO b)
        -> IO b
```

Bu demek oluyor ki `bind` fonksiyonu iki IO aksiyonunu parametre olarak alıyor ve başka bir IO aksiyonunu geri döndürüyor.

Önemli kalıpları tekrar hatırlayın. İlki şuydu:

```haskell
let (x,w1) = action1 w0 in
let (y,w2) = action2 x w1 in
(y,w2)
```

Fonksiyonların tiplerine bakalım:

```haskell
action1  :: IO a
action2  :: a -> IO b
(y,w2)   :: IO b
```

Tanıdık gelmiyor mu?

```haskell
(bind action1 action2) w0 =
    let (x, w1) = action1 w0
        (y, w2) = action2 x w1
    in  (y, w2)
```

Amacımız World argümanını bu fonksiyonla gizlemek. Örnek olarak, şunu gerçekleştirmek istediğimizi varsayalım:

```haskell
let (line1,w1) = getLine w0 in
let ((),w2) = print line1 in
((),w2)
```

Şimdi, `bind` fonksiyonunu kullanarak:

```haskell
(res,w2) = (bind getLine (\l -> print l)) w0
```

`print` fonksiyonu `(World -> ((),World))` tipinde olduğu için, `res = ()` (boş tip) Eğer bundaki sihirbazlığı görmediyseniz, bu sefer üç satırla deneyelim:

```haskell
let (line1,w1) = getLine w0 in
let (line2,w2) = getLine w1 in
let ((),w3) = print (line1 ++ line2) in
((),w3)
```

Bu da şuna denk:

```haskell
(res,w3) = (bind getLine (\line1 ->
             (bind getLine (\line2 ->
               print (line1 ++ line2))))) w0
```

Bir şey fark ettiniz mi? Evet, artık hiçbir yerde geçici World değişkenleri kullanılmıyor. Sihirbazlık gibi.

Daha iyi bir notasyon kullanabiliriz. `bind` yerine `(>>=)` kullanalım. `(>>=)`, `(+)` gibi bir iç notasyonlu fonksiyondur; ki şöyle çalışır: `3 + 4 ⇔ (+) 3 4`

Ho Ho Ho! Herkese Mutlu Noeller! Haskell bize söz dizimsel kolaylık sağlıyor:

```haskell
do
  x <- action1
  y <- action2
  z <- action3
  ...
```

yerine, şöyle yazabiliriz:

```haskell
action1 >>= (\x ->
action2 >>= (\y ->
action3 >>= (\z ->
...
)))
```

`action2` içinde `x`, `action3` içinde hem `x` hem de `y` değişkenlerini kullanabildiğinize dikkat edin.

Peki `<-` kullanmayan satırlarda ne yapacağız? Kolay, `blindBind` diye başka bir fonksiyon tanımlayalım:

```haskell
blindBind :: IO a -> IO b -> IO b
blindBind action1 action2 w0 =
    bind action (\_ -> action2) w0
```

Bu tanımı daha açık olması için basitleştirmedim. Tabii daha basit bir notasyon kullanabiliriz, bunun için `(>>)` operatörü var.

```haskell
do
    action1
    action2
    action3
```

Şuna dönüşüyor:

```haskell
action1 >>
action2 >>
action3
```

Kullanışlı bir fonksiyon daha var.

```haskell
putInIO :: a -> IO a
putInIO x = IO (\w -> (x,w))
```

Bu saf değerleri IO bağlamına sokmak için kullanılan genel bir yoldur. `putInIO` için kullanılan genel isim `return`'dür. Haskell öğrenirken bu oldukça kötü bir isim, çünkü Haskell'deki `return` alışık olduğunuzden çok farklıdır.

[03_Hell/01_IO/21_Detailled_IO.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/01_IO/21_Detailled_IO.lhs)

Örneğimizi çevirerek bu bölümü bitirelim:

```haskell
askUser :: IO [Integer]
askUser = do
  putStrLn "Bir sayi listesi girin (virgullerle ayirin):"
  input <- getLine
  let maybeList = getListFromString input in
      case maybeList of
          Just l  -> return l
          Nothing -> askUser

main :: IO ()
main = do
  list <- askUser
  print $ sum list
```

Şu hale geliyor:

```haskell
import Data.Maybe

maybeRead :: Read a => String -> Maybe a
maybeRead s = case reads s of
                  [(x,"")]    -> Just x
                  _           -> Nothing
getListFromString :: String -> Maybe [Integer]
getListFromString str = maybeRead $ "[" ++ str ++ "]"
askUser :: IO [Integer]
askUser = 
    putStrLn "Bir sayi listesi girin (virgullerle ayirin):" >>
    getLine >>= \input ->
    let maybeList = getListFromString input in
      case maybeList of
        Just l -> return l
        Nothing -> askUser

main :: IO ()
main = askUser >>=
  \list -> print $ sum list
```

Çalıştığını doğrulamak için derleyebilirsiniz.

`(>>)` ve `(>>=)` olmadan nasıl olacağını düşünün.


[03_Hell/01_IO/21_Detailled_IO.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/01_IO/21_Detailled_IO.lhs)

***

[03_Hell/02_Monads/10_Monads.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/02_Monads/10_Monads.lhs)

## 4.3. Monad

![Monad](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/dali_reve.jpg)

Artık bu sırrı açıklayabiliriz: `IO` bir *monad*dir. Monad olmak, `do` notasyonu ile belirli söz dizimsel kolaylıklara sahip olmak demektir. Ama temel olarak, kodunuzun akışını kolaylaştıracak belirli kod kalıplarına erişim sağlar.

> Önemli noktalar:
> * Monadlar etkilerle ilgili olmak zorunda değildir! Saf monadlar da vardır.
> * Monadlar daha çok sıralama ile ilgilidir.

Haskell'de `Monad` bir tip sınıfıdır. Bu sınıfın bir üyesi olmak için `(>>=)` ve `return` fonksiyonlarını sağlamalısınız. `(>>)` fonksiyonu `(>>=)` fonksiyonundan türer. Basit olarak `Monad` tip sınıfı şöyle belirtilir:

```haskell
class Monad m  where
  (>>=) :: m a -> (a -> m b) -> m b
  return :: a -> m a

  (>>) :: m a -> m b -> m b
  f >> g = f >>= \_ -> g

  -- Sadece tarihsel sebeplerden dolayi oldugunu dusundugum
  -- bu fonksiyonu dikkate almayabilirsiniz
  fail :: String -> m a
  fail = error
```

> Notlar:
> * `class` anahtar kelimesi dostunuz değildir. Haskell'deki class nesne yönelimli programlamada karşılaştığınız class gibi değildir. Haskell'deki class Java'daki interface'le benzeşir. `typeclass` daha iyi bir isimlendirme olurdu, çünkü o tip grubu anlamına geliyor. Bir tipin bir sınıfa ait olması için, bir sınıfın tüm fonksiyonlarının o tip için sağlanabilir olması gerekiyor.
> * Tip sınıflarının bu örneğinde, `m` tipinin argüman alan bir tip olması gerekiyor, örneğin `IO a`, ama aynı zamanda `Maybe a`, `[a]`, vs.
> * Fonksiyonunuzun kullanışlı bir monad olması için bazı kurallara uyması gerekiyor. Eğer yapınız bu kurallara uymuyorsa garip şeyler gerçekleşebilir: `~ return a >>= k == k a m >>= return == m m >>= (-> k x >>= h) == (m >>= k) >>= h ~`

### 4.3.1 Maybe Monad'ı

`Monad` tip sınıfının üyesi olan bir sürü farklı tip vardır. Tarif etmesi en kolay olanlarından biri de `Maybe`'dir. Eğer `Maybe` değerlerinden oluşan bir diziniz varsa, etkilemek için monadları kullanabilirsiniz. Uzayıp giden `ıf..then..else..` yapılarından kurtulmak için oldukça kullanışlı bir yoldur.

Karmaşık bir banka işlemi düşünün. Eğer bakiyeniz sıfırın altına düşmeden belli işlemleri yapabilecek kadar paranız varsa, 700€ kazanma hakkınız olsun.

```haskell
deposit  value account = account + value --para yatirma
withdraw value account = account - value --para cekme

--para kazanmaya hak kazanip kazanmadiginizi donduren fonksiyon
eligible :: (Num a,Ord a) => a -> Bool
eligible account =
  let account1 = deposit 100 account in
    if (account1 < 0)
    then False
    else
      let account2 = withdraw 200 account1 in
      if (account2 < 0)
      then False
      else
        let account3 = deposit 100 account2 in
        if (account3 < 0)
        then False
        else
          let account4 = withdraw 300 account3 in
          if (account4 < 0)
          then False
          else
            let account5 = deposit 1000 account4 in
            if (account5 < 0)
            then False
            else
              True

main = do
  print $ eligible 300 -- True
  print $ eligible 299 -- False
```

[03_Hell/02_Monads/10_Monads.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/02_Monads/10_Monads.lhs)

***

[03_Hell/02_Monads/11_Monads.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/02_Monads/11_Monads.lhs)

Şimdi `Maybe` kullanarak ve monadlardan faydalanarak iyileştirelim:

```haskell
deposit :: (Num a) => a -> a -> Maybe a
deposit value account = Just (account + value)

withdraw :: (Num a,Ord a) => a -> a -> Maybe a
withdraw value account = if (account < value) 
                         then Nothing 
                         else Just (account - value)

eligible :: (Num a, Ord a) => a -> Maybe Bool
eligible account = do
  account1 <- deposit 100 account 
  account2 <- withdraw 200 account1 
  account3 <- deposit 100 account2 
  account4 <- withdraw 300 account3 
  account5 <- deposit 1000 account4
  Just True

main = do
  print $ eligible 300 -- Just True
  print $ eligible 299 -- Nothing
```

[03_Hell/02_Monads/11_Monads.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/02_Monads/11_Monads.lhs)

***

[03_Hell/02_Monads/12_Monads.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/02_Monads/12_Monads.lhs)

Kötü değil, ama daha da iyileştirebiliriz:

```haskell
deposit :: (Num a) => a -> a -> Maybe a
deposit value account = Just (account + value)

withdraw :: (Num a,Ord a) => a -> a -> Maybe a
withdraw value account = if (account < value) 
                         then Nothing 
                         else Just (account - value)

eligible :: (Num a, Ord a) => a -> Maybe Bool
eligible account =
  deposit 100 account >>=
  withdraw 200 >>=
  deposit 100  >>=
  withdraw 300 >>=
  deposit 1000 >>
  return True

main = do
  print $ eligible 300 -- Just True
  print $ eligible 299 -- Nothing
```

Monadların kodumuzu daha zarifleştirmenin iyi bir yolu olduğunu gösterdik. Dikkat edin ki, bu tip bir kod düzenlemesi, özellikle `Maybe`, pek çok imperatif dilde de uygulanabilir. Aslında, bu tip bir yapıyı normalde de yapıyoruz.

> Önemli bir nokta: Dizideki ilk elemanın `Nothing` olarak hesaplanması tüm hesaplamayı durduracaktır. Bu demek oluyor ki, tüm satırları hesaplamıyorsunuz. Tembellik sayesinde bunun için fazladan bir şey yapmanıza gerek yok.

Bunu göz önünde bulundurarak `Maybe` için `(>>=)` fonksiyonunu şöyle tanımlayabilirsiniz:

```haskell
instance Monad Maybe where
    (>>=) :: Maybe a -> (a -> Maybe b) -> Maybe b
    Nothing  >>= _  = Nothing
    (Just x) >>= f  = f x

    return x = Just x
```

Bu basit örnek ile `Maybe` monadının ne kadar kullanışlı olabileceğini ve nasıl kullanılabileceğini gördük. Ama daha iyi bir örnek için listelere bakalım.

[03_Hell/02_Monads/12_Monads.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/02_Monads/12_Monads.lhs)

***

[03_Hell/02_Monads/13_Monads.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/02_Monads/13_Monads.lhs)

### 4.3.2. Liste Monad'ı

![liste](http://yannesposito.com/Scratch/img/blog/Haskell-the-Hard-Way/golconde.jpg)

Liste monadı deterministik (belirlenimci) olmayan hesaplamaları simüle etmemize yardımcı olur. Şöyle:

```haskell
import Control.Monad (guard)

allCases = [1..10]

resolve :: [(Int,Int,Int)]
resolve = do
              x <- allCases
              y <- allCases
              z <- allCases
              guard $ 4*x + 2*y < z
              return (x,y,z)

main = do
  print resolve
```

Resmen sihirbazlık.

```haskell
[(1,1,7),(1,1,8),(1,1,9),(1,1,10),(1,2,9),(1,2,10)]
```

Liste monadı için, şöyle bir söz dizimsel kolaylık da vardır:

```haskell
  print $ [ (x,y,z) | x <- allCases,
                      y <- allCases,
                      z <- allCases,
                      4*x + 2*y < z ]
```

Tüm monadları sıralamayacağım, ancak bir sürü monad bulunmakta. Saf dillerdeki belli kavramlar monad kullanımı ile basitleştirilebilir. Özellikle monadlar şunlar için kullanışlıdır:

* IO
* deterministik olmayan hesaplamalar
* (sözde) rastgele sayı üretimi
* konfigürasyon durumunu tutma
* yazma durumu
* ..

Eğer buraya kadar beni takip edebildiyseniz, başardınız! Monadları öğrendiniz! [^fn-8]

[03_Hell/02_Monads/13_Monads.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/03_Hell/02_Monads/13_Monads.lhs)

# 5. Ekler

Bu bölüm doğrudan Haskell'le ilgili değil. Bazı ayrıntılı açıklamalar için okuyabilirsiniz.

[04_Appendice/01_More_on_infinite_trees/10_Infinite_Trees.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/04_Appendice/01_More_on_infinite_trees/10_Infinite_Trees.lhs)

## 5.1. Sonsuz Ağaçlar Hakkında

[Sonsuz Yapılar](#33-sonsuz-yap%C4%B1lar) kısmında bazı basit yapılar görmüştük. Ancak ağacımızdan iki özellik çıkartmıştık:

1. tekrar eden düğümlerin olmaması
2. düzgün sıralı ağaç olması

Bu bölümde ilk özelliği sağlamaya çalışacağız. İkincisiyle ilgili olarak da şimdilik bir şey yapmayacağız ama nasıl olabildiğince sıralı tutabileceğimizi tartışacağız.

İlk adımımız (sözde) rastgele bir sayı listesi oluşturmak olsun:

```haskell
shuffle = map (\x -> (x*3123) `mod` 4331) [1..]
```

`treeFromList` fonksiyonunun tanımını hatırlayalım:

```haskell
treeFromList :: (Ord a) => [a] -> BinTree a
treeFromList []    = Empty
treeFromList (x:xs) = Node x (treeFromList (filter (<x) xs))
                             (treeFromList (filter (>x) xs))
```

`treeTakeDepth` de şöyleydi:

```haskell
treeTakeDepth _ Empty = Empty
treeTakeDepth 0 _     = Empty
treeTakeDepth n (Node x left right) = let
          nl = treeTakeDepth (n-1) left
          nr = treeTakeDepth (n-1) right
          in
              Node x nl nr
```

Programımız da şu şekilde:

```haskell
main = do
      putStrLn "take 10 shuffle"
      print $ take 10 shuffle
      putStrLn "\ntreeTakeDepth 4 (treeFromList shuffle)"
      print $ treeTakeDepth 4 (treeFromList shuffle)
```

```
% runghc 02_Hard_Part/41_Infinites_Structures.lhs
take 10 shuffle
[3123,1915,707,3830,2622,1414,206,3329,2121,913]
treeTakeDepth 4 (treeFromList shuffle)

< 3123
: |--1915
: |  |--707
: |  |  |--206
: |  |  `--1414
: |  `--2622
: |     |--2121
: |     `--2828
: `--3830
:    |--3329
:    |  |--3240
:    |  `--3535
:    `--4036
:       |--3947
:       `--4242
```

Hey! Sonlanıyor! Ama dikkat edin, program sadece dallara koyacak veri olduğu sürece çalışacak.

Örneğin:

```haskell
treeTakeDepth 4 (treeFromList [1..]) 
```

sonsuza kadar çalışacak, çünkü `filter (<1) [2..]` ifadesinin ilk elemanını almaya çabalayacak. Ama `filter` fonksiyonu sonucun boş liste olduğunu anlayacak kadar akıllı değil.

Bunlar da okur için alıştırma olarak kalsın:

* `treeTakeDepth n (treeFromList shuffle)` ifadesini sonsuz döngüye sokacak bir `n` değeri olduğunu kanıtlayın.
* `n` için bir üst sınır bulun.
* Hiçbir `shuffle` listesinin programı bitiremeyeceğini kanıtlayın.

[04_Appendice/01_More_on_infinite_trees/10_Infinite_Trees.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/04_Appendice/01_More_on_infinite_trees/10_Infinite_Trees.lhs)

***

[04_Appendice/01_More_on_infinite_trees/11_Infinite_Trees.lhs](http://yannesposito.com/Scratch/en/blog/Haskell-the-Hard-Way/code/04_Appendice/01_More_on_infinite_trees/11_Infinite_Trees.lhs)

Bu sorunları çözmek için `treeFromList` ve `shuffle` fonksiyonlarımızı biraz değiştireceğiz.

İlk sorunumuz, `shuffle` fonksiyon tanımımızda sonsuz farklı sayı üreten bir yapı olmaması. Sadece `4331` farklı sayı ürettik. Bunu çözmek için daha iyi bir `shuffle` fonksiyonu yazalım.

```haskell
shuffle = map rand [1..]
          where 
              rand x = ((p x) `mod` (x+c)) - ((x+c) `div` 2)
              p x = m*x^2 + n*x + o -- bir polinom
              m = 3123    
              n = 31
              o = 7641
              c = 1237
```

Bu `shuffle` fonksiyonunun (umarız ki) bir alt veya üst limiti yok. Ama daha iyi bir rastgele sayı fonksiyonu sonsuz döngüye girmeyi engellemiyor.

Genel olarak, `filter (<x) xs`'in boş liste olup olmadığını anlamıyoruz. Öyleyse bu sorunu çözmek için, ikili ağacımızı oluştururken hata vermeyi deneyelim. Kodumuzun bu yeni versiyonu düğümleri için şu özelliğe sahip olan bir ikili ağaç oluşturacak:

> Sol alt ağaçtaki herhangi bir eleman, kökün değeriden daha küçük olmalı.

Dikkat edin ki genel olarak sıralı bir ikili ağaç olarak kalacak. Ayrıca, yapı itibarıyla, her düğüm değeri ağaçta tek olacak, tekrarlanmayacak.

```haskell
treeFromList :: (Ord a, Show a) => [a] -> BinTree a
treeFromList []    = Empty
treeFromList (x:xs) = Node x left right
          where 
              left = treeFromList $ safefilter (<x) xs
              right = treeFromList $ safefilter (>x) xs
```

Bu yeni `safefilter` fonksiyonu `filter` fonksiyonuna neredeyse denk, ancak eğer liste sonsuzsa sonsuz döngüye girmiyor. Eğer art arda 10000 değerin testi olumsuz çıkarsa, bunu aramanın sonu sayıyor.

```haskell
safefilter :: (a -> Bool) -> [a] -> [a]
safefilter f l = safefilter' f l nbTry
  where
      nbTry = 10000
      safefilter' _ _ 0 = []
      safefilter' _ [] _ = []
      safefilter' f (x:xs) n = 
                  if f x 
                     then x : safefilter' f xs nbTry 
                     else safefilter' f xs (n-1) 
```

Şimdi programı çalıştırıp mutlu olabilirsiniz:

```haskell
main = do
      putStrLn "take 10 shuffle"
      print $ take 10 shuffle
      putStrLn "\ntreeTakeDepth 8 (treeFromList shuffle)"
      print $ treeTakeDepth 8 (treeFromList $ shuffle)
```

Ekrana yazdırılan her değerin yazma zamanının farklı olduğunu fark etmelisiniz. Bunun sebebi Haskell'in her değeri sadece ihtiyacı olduğu zaman hesaplaması. Ve bu durumda, bu zaman ekrana yazdırılacağı zaman.

Daha da etkileyici bir şey görmek için `depth` değerini `8`'den `100`'e cikarın. RAM'inizi boğmadan çalışacak! Akış ve hafıza yönetimi Haskell tarafından doğal olarak yapılıyor.

Bu da okura alıştırma olarak kalsın:

* `deep` ve `nbTry` için yüksek sabit değer ile bile, iyi şekilde çalışıyor gibi gözüküyor. Ama en kötü durumda üstel olabilir. `treeFromList` için olabilecek kötü bir liste oluşturun. *ipucu*: [0,-1,-1,....,-1,1,-1,...,-1,1,...] listesini düşünün.
* `safefilter` fonksiyonunu şöyle tanımlamayı denedim:

```haskell
  safefilter' f l = if filter f (take 10000 l) == []
                    then []
                    else filter f l
```
Neden çalışmadığını ve sonsuz döngüye girebileceğini açıklayın.
* `shuffle`'in artan sınırlarla gerçek bir rastgele liste olduğunu farz edin. Bu yapı üzerinde biraz çalışırsanız, bu yapının 1 olasılıkla sonlu olduğunu fark edeceksiniz. Aşağıdaki kodu kullanarak (hiç `safefilter` yokmuş gibi doğrudan `safefilter'` kullanın) `f` için 1 olasılıkla treeFromList' shuffle'ın sonlu olduğu bir tanım bulun, ve kanıtlayın. Dikkat: bu sadece bir konjektür.

# 6. Teşekkürler

[r/haskell](http://reddit.com/r/haskell) ve [r/programming](http://reddit.com/r/programming) gruplarına teşekkür ediyorum. Yorumları bana çok yardımcı oldu.

Özellikle, [Emm](https://github.com/Emm)'e, İngilizce'mi düzeltmekle uğraştığı zaman için binlerce kez teşekkür ederim.

> Çevirmen Notu: Yazıda herhangi bir Türkçe karakter veya çeviri hatası bulursanız, beni bilgilendirirseniz, veya *pull request* yollayarak düzeltirseniz çok sevinirim. Daha iyi çevirilebileceğini düşündüğünüz bölümler için de bu geçerli. Teşekkürler.

***

#### Dipnotlar

[^fn-1]: Son zamanda çıkan diller onları saklamaya çalışsa da, onlar oradalar.

[^fn-2]: Hile yaptığımı biliyorum. Ama tembellikle ilgili sonra konuşacağız.

[^fn-3]: Daha cesur olanlarınız için örüntülü eşlemeyle ilgili daha kapsamlı bir açıklama [şuradan](http://www.cs.auckland.ac.nz/references/haskell/haskell-intro-html/patterns.html) okunabilir.

[^fn-4]: `squareEvenSum''` fonksiyonunun diğer ikisinden daha verimli olduğuna dikkat edin. `(.)` fonksiyonunun sırası önemlidir.

[^fn-5]: Ki kendisi JavaScript'te JSON bulunduran bir karakter dizisi üzerinde `eval` çalıştırmaya çok benzer. (Çevirmen notu: `JSON.parse` daha iyi çözüm olabilir.)

[^fn-6]: Bu kurala bazı güvenli olmayan istisnalar da var. Ama belki hata ayıklama amacı dışında hiçbir gerçek uygulamada böyle bir kullanım görmezsiniz.

[^fn-7]: Merak edenler için: gerçek tip şöyle: `data IO a = IO {unIO :: State# RealWorld -> (# State# RealWorld, a #)}`. `#` işareti optimizasyonla ilgili, ve ben örneğimde alan yerlerini değiştirdim. Ama ana fikir bu.

[^fn-8]: Tabii ki alışana ve tamamen anlayana kadar çalışmanız gerekiyor. Ama bu yönde büyük bir adım attınız bile.
