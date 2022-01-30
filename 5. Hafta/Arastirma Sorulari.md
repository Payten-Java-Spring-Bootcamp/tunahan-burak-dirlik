HOMEWORK 5 
# 1. Concurrent programlama ve Parallel Programlama nedir ? Aralarında çalışma şekli olarak nasıl bir fark bulunmaktadır ? 

### Concurrent programmimg 

Concurrent programming; (eş zamanlı programlama) aşina olduğumuz multithreaded programmingdir. Bize aynı aynı anda birden fazla processi işlemeyi sağlar. 
Concurrent programmingde, tek bir işlem ünitesinde birden çok işlemi yapmaya yöneliriz. 

### Parallelism 
Parallelism; gelen taskların birden fazla işlem ünitesi ile aynı anda çalıştırılmasıdır. Daha hızlı sonuç verebilir. Taskların birden fazla işlem ünitesinde çalıştırılması demek, taskların birden fazla cpu üzerinde çalışması demektir. Bu da daha fazla donanım kaynağının kullanılması anlamına gelir.

Concurrency ve parallelism arasındaki fark en sade şekliyle şudur; Concurrency aynı anda bir çok taskı aynı anda yürütmek, parallelism aynı anda bir çok taskı yan yana yürütmektir.

<p align="center">    <img src="miro.medium.com/max/1400/1*cFUbDHxooUtT9KiBy-0SXQ.jpeg"/>  </p>


# 2. Mutex ve Semaphore kavramlarını açıklayınız. Hangi tür durumlarda bunlara başvurmamız gerekir ?
### Mutex
Açılımı mutual exclusion dur. Multitasking sistemlerde deadlock denilen durumu engellemek için kullanılan bir mekanizma.
### Deadlock
Deadlockda birçok thread birbirini bekliyor ve ilerleme gerçekleşmiyor.
Bir işlemi gerçekleştirmek için 2 tane anahtara ihtiyacımız var diyelim. 2 tane threadden biri bir locku diğeride diğer locku alınca her 2 thread de 2 lock a aynı anda sahip olamıyor. 
Hiçkimse de bir lock u bırakıp diğerine vermediği için ilerleme gerçekleşmiyor ve deadlock oluşuyor. Deadlock adından anlaşılacağı üzere işlemlerin kilitlenmesidir. 
Threadler yürümez bu durumu engellemek için mutex denilen mekanizma geliştirilmiş.

Şöyle özetleyelim elimizde bir task var bunu en iyi maliyetle bitirmek için threadleri kullanıyoruz. Fakat 2 thread aynı anda bir dosya üzerinde çalışırsa dosyanın yapısı bozulur 
ve çalışamaz hale gelir. Bu yüzden threadler, dosya üzerinde sırayla çalışmalı, bir thread bir dosya üzerinde çalışırken başka bir thread çalışmamalıdır. 
Threadlerin sırayla çalışmasını sağlamak, aralarındaki senkronizasyon problemini halletmek için mutex denilen yapılar geliştirilmiştir. 
Mutex bir iş parçacığını alır ve kilitler. Ve o iş parçacığı işini halledene kadar başka thread tarafından kullanılamaz. 
Bir mutex'e ayni anda sadece bir thread sahip olabilir. Digerleri sahip olmak isterlerse beklemek zorundadır.

### Semaphore
Semaphore u anlatmak için otel örneği kullanılabilir.
Otelin resepsiyoncusu semaphore'u; odaları müşterilere vermek için kullanır. Aklında otel tamamen boşken otelde kaç odanın müsait olduğunu tutar, ki bu otelin oda sayısıdır. 
Müşteri geldikçe aklındaki bu oda sayısını düşürür, insanlar çıkış yaptığında bu sayıyı arttırır. Bu rakam sıfıra ulaştığında boşta odasının olmadığını ve 
isterlerse lobide beklemelerini söyler. Bu bekleyenler sırayla alınırlar, tabi resepsiyoncu bu insanlara statü veya para gibi etkenlere bağlı öncelikler vermediyse.

Mutex'ler Critical Section yönetimi sağlamak üzere tasarlandığı için kendilerini bırakan Thread'in alan Thread olmasını gerekli tutmaktadır. 
Semaphore'da ise böyle bir kısıtlama yoktur hatta birçok durumda Semaphore'u bırakan Thread alan Thread'den farklıdır.
Lock ve mutex'in aksine senkronize erişimi tamamen bekletmek için değil sınırlandırmak için kullanılabilir denilebilir.
Sınırlı bir resource a sahipsiniz, aynı anda 3 thread'in bu kaynağa erişmesini istiyorsunuz daha fazlası sizin için bir sorun oluşturuyor.
Kodun o kısmını bütün thread'lerin kullanımına açmıyorsunuz, orada sayaca sahip bir lock kullanıyorsunuz. İşte semaphore bu.

Semaforların çalışması sırasında bölünmezlik (atomicity) ön plandadır. Yani bir semafor’un içerisinde yapılan birden fazla iş, program tarafından sanki tek bir iş gibi algılanmalı 
ve araya başka işin girmesine izin verilmemelidir. Semaphore , belirli bir kaynak için tüketici sayısını sınırlamanın bir yoludur

# 3. Java’da Error ve Exception arasındaki fark nedir ? Throwable ile ilişkileri nasıldır ? Hangi tür durumlarda Error hangi tür durumlarda Exception meydana gelebilir ? Örneklerler açıklayınız. 

### Error
Error handle edilemeyen hatalardır. Program akışının durmasına sebep olur. Uygulamanın yakalamaya çalışmaması gereken ciddi sorunları gösteren Throwable dan türeyen bir alt sınıftır.
### Exception
Exceptio -ı ise try catch bloklarıyla yakalayabiliriz. Program akışı; exception eğer yakalandıysa devam eder. Exception yaşandığında; bunun program için arasıra yaşansa da sorun olmayacağı
uygulamanın devam edebileceği anlaşılır. Exception ve Error; ikisi de Throwable sınıfından türer. Aşağıdaki görsel ile aralarındaki ilişkiyi daha net görebiliriz.
<p align="center">    <img src="https://www.fatalerrors.org/images/blog/7bba3f7352c8c8b15be1f90568857dce.jpg " /> </p>
<p align="center">    <img src="https://i.stack.imgur.com/v2NAj.png" /> </p>
Exception programın kodlanmasında yapılan hataların sonucudur, Error sistemin yanlış çalışmasının sonucudur.

4. Spring’te yer alan @Scheduled anotasyonunun kullanım amaçlarını ve kullanım şeklini açıklayınız.

5. Spring’te yer alan @Async anotasyonunun kullanım amaçlarını ve kullanım şeklini açıklayınız.

6. High Availability (HA) kavramını kısa açıklayınız. 
Yüksek erişilebilirlik, 7×24 çalışan sistemlerin gerek otomatik gerekse manual sebeplerden dolayı yazılım veya donanımdan kaynaklanacak kesintilere uğramaksızın hizmet vermesidir. 
Internet gibi dağıtık ortamlarda hizmet veren sistemlerin kısa da sürse kesintiye uğraması önemsenecek maddi kayıplara neden olabilir. 
Büyük yazılım firmaları sistemlerin 7×24×365 hizmet vermesini garanti etmek için yani high availability sağlamak için çeşitli teknikler kullanırlar. Bazıları ; 
-	Failover Clustering (Yedekli Kümeleme )
-	Log Shipping (Günlük Gönderme)
-	Data Replication (Veri Yineleme)
-	Database Mirroring (Veritabanı Aynalama)

Herhangi bir sistemin yüksek düzeyde erişilebilirlik sunması için, sistemin parçalarının kullanılmadan önce iyi tasarlanmış ve kapsamlı bir şekilde test edilmiş olması gerekir. 
https://www.ahmetkaymaz.com/2008/01/02/sql-server-yuksek-erisilebilirlik-high-availability/
7. Entity ve Value Object kavramlarını Domain Driven Design (DDD) kapsamında açıklayınız. 
DDD, karmaşık yazılım projelerine belli başlı çözümler getiren bir yaklaşımdır. Var olan ve yaşanan problemlerin Domain esas alınarak analiz edilmesi ve çözülmesi gerektiğini 
savunan ve bunun için Domain’in net bir şekilde anlaşılmasının gerekli olduğunu söyleyen bir programlama yaklaşımıdır.
### Entity & Value Object
Unique(Benzersiz) bir kimliği olan nesneler entity olarak adlandırılır. Entity herhangi bir şey için modellenmiş nesnelere karşılık gelmektedir. 
Bahsedilen kimlik ise bu nesnelerin her biri için yaratıldığı süreçten itibaren diğerlerinden ayırmamızı sağlayan ve değişmeden taşınan Id değeridir.
Kendine ait bir kimliği olmayanlar ise value object olarak adlandırılır.
Value object, herhangi bir kimlik(Id) değeri olmayan ve böylece aynı değerlere sahip iki value object nesnesinin değersel açıdan aynı olarak kabul edilebilir olmasını sağlayan 
ve dolayısıyla birbirlerinin yerine geçebilecekleri anlamına gelen bir nesnedir. İşte bu nedenle value object’ler her daim değişmez(immutable)dirler

https://www.gencayyildiz.com/blog/domain-driven-design-stratejik-ve-taktiksel-olarak-derinlemesine-inceleme/
8. Ubiquitous Language kavramını DDD kapsamında açıklayınız. Sizce neden önemli olabileceğini belirtiniz.
Ubiquitous Language; domain expert ile developer arasındaki ortak dildir. Domain expert; hangi alanda yazılım yapılacaksa o alan ile ilgili bilgiye tecrübeye sahip kişidir. 
Bir araziyi sulamak için bir makinaya yazılım yapalım diyelim. O araziye ne aralıkta ne kadar süre ile su verileceğinin bilen kişi çiftçidir. 
Çiftçi domain expert oluyor. Bu bilgileri yazılımcıya ortak anlaşabilecekleri bir dil ile developera aktarır. 
Ve developer bu bilgileri kullanarak yazılımı geliştirir. Kısaca müşterinin yazılımcıya işi nasıl yapacağını anlatması Ubiquitous Language dir. 
İşin yazılımcıya nasıl yapılacağının Ubiquitous Language diye şaşalı bi şekilde isimlendirilmesinin gereği varmıydı, bence yoktu. 
Fakat bu kavram önemli midir, tabiki de önemlidir. Yazılımın nasıl yapılacağını domain expert güzel bir şekilde şekil falan çizerek anlatacak ki developer konuyu anlayabilsin ve 
yazılımı yapabilsin.
9. Core Domain, Supporting Domain, Generic Domain kavramlarını DDD kapsamında açıklayınız. 

10. Anemic Domain Model ve Rich Domain Model kavramlarını kıyaslayarak açıklayınız. Araştırma 
Anemic Domain Model : Yine DDD kullanmıyorsak ya da DDD’yi ilk implemente edişimiz ise sık karşılaşabileceğimiz bir durum. Anemic domain model, hiç bir fonksiyonelliği olmayan içerisinde hiç bir fonksiyon barındırmayan sadece propertylerden oluşmuş bir modeldir ve düşünüldüğünde OOP’e aykırı bir yapı teşkil eder.

Rich Domain Model
