# Zor Yoldan Haskell

TL, DR (Çok uzundu okumadım): Haskell öğrenmek için kısa ve yoğun bir rehber.

#### İçindekiler:
* [Giriş](#1-giri%C5%9F)
* [Kurulum](#11-kurulum)
* [Korkmayın](#12-korkmay%C4%B1n)
* [Haskell'e Giriş](#13-haskelle-giri%C5%9F)
    * [Fonksiyon tanımı](#131-fonksiyon-tan%C4%B1m%C4%B1)
    * [Tip örneği](#132-tip-%C3%B6rne%C4%9Fi)
* [Temel Haskell](#2-temel-haskell)
* Notasyon
    * Aritmetik
    * Mantıksal
    * Kuvvetler
    * Listeler
    * Karakter Dizileri
    * Demetler *(Tuple)*
    * Parantezlerle Baş Etmek
* Fonksiyonlar için Faydalı Notasyonlar
* Zor Kısım
* Fonksiyonel Stil
    * Üst Derece Fonksiyonlar
* Tipler
    * Tip Çıkarımı
    * Tip İnşası
    * Özyinelemeli Tipler *(Recursive types)*
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

***

Tüm geliştiricilerin Haskell öğrenmesi gerektiğine inanıyorum. Herkesin süper Haskell ninjası olması gerektiğini düşünmüyorum, ama herkes Haskell'in sahip olduğu farklı yönleri görmeli. Haskell öğrenmek zihninizi acar.

Anaakım diller aynı temelleri paylaşırlar:
* değişkenler
* döngüler
* işaretçiler *(pointer)*
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

Son olara, Haskell yolu da budur:
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
