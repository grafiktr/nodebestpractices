# Asenkron hata denetiminde Async-Await ya da promise kullanımı 


### Bir Paragraflık Açıklama

Çoğu programcı aşına olmadığı için geri-çağırımlar pek de iyi ölçeklenemedi.Her yerde hata kontrolünün yapılmasını zorunlu kılıyor, yanlış yuvalanmış kod blokları ile uğraşmak zorunda bırakıyor ve kod akışından bir anlam çıkarmayı zor bir hale getiriyor. Async, Q pack ve BlueBird gibi Promise kütüphaneleri program akışını kontrol etmek için RETURN ve THROW kullanan standart kod sitili paketleridir. Özellikle, ana kodun tüm fonksiyonlardaki hatalarla başa çıkmasını sağlayan try-catch tarzı hata denetimini desteklerler.


### Kod Örneği - hataları yakalamak için vaatleri kullanmak


```javascript
doWork()
 .then(doWork)
 .then(doOtherWork)
 .then((result) => doWork)
 .catch((error) => {throw error;})
 .then(verify);
```

### Anti patern kod örneği - geri arama türü hata denetimi 

```javascript
getData(someParameter, function(err, result){
    if(err != null)
      // do something like calling the given callback function and pass the error
    getMoreData(a, function(err, result){
          if(err != null)
            // do something like calling the given callback function and pass the error
        getMoreData(b, function(c){ 
                getMoreData(d, function(e){ 
		 if(err != null)
            	// you get the idea? 
            });
        });
```

### Blog Alıntısı: "Promiseler ile ilgili problemlerimiz var"
blog pouchdb.com'dan
 
 > ……Aslında gerçekte, geri-çağırımlar(callback) çok daha kötü bir şey yapar; bizi programlama dillerinde kanıksadığımız yığından mahrum bırakır. Yığın olmadan kod yazmak fren pedalı olmadan araba sürmek gibidir: uzanıp orada olmadığını anlayana kadar, ona ne kadar ihtiyacınız olduğunu anlayamazsınız. Promiselerin tüm amacı asenkronluğu düştüğümüzde kaybettiğimiz dil temellerini bize geri vermektir: return, throw, ve yığın. Fakat promislerden avantaj sağlamak için onların nasıl kullanılması gerektiğini bilmek gerekir.

### Blog Alıntısı: "Promise metodu çok daha kompakttır"
blog gosquared.com'dan
 
 > ………Promise metodu çok daha kompakt, açık ve yazması hızlıdır. Eğer işlemler arasında bir hata veya istisna gerçekleşirse .catch() denetleyicisiyle denetlenir. Tüm hataların denetimi için tek bir komut olması çalışmanın her adımında hata kontrolü yapılmasına gerek olmadığı anlamına gelmektedir.

### Blog Alıntısı: "Promiseler üreteçler(generators) ile kullanılabilen yerli ES6'lardır"
blog StrongLoop'dan
 
 > ….Geri çağırımlar kötü bir hata-denetimi geçmişine sahiptir. Promiseler daha iyidir. Express'teki yerleşik hata denetimiyle promisleri birleştirin ve yakalanmayan istisnaların olma ihtimalini önemli ölçüde azaltın. Promisler ES6'da doğuştan vardır. Üreteçler ile ve ES7'nin Babel gibi asyn/await destekleyen derleyiciler gibi önermeleri ile kullanılabilir.

### Blog Alıntısı: "Alıştığınız bütün düzenli akış kontrol yapıları tamamen yıkılmış durumda"
blog Benno’s'dan
 
 > ……Asenkron ile ilgili en iyi şeylerden biri, geri çağırım temelli programlama da temel olarak alıştığınız ve tamamen yıkılmış durumda olan düzenli akış kontrol yapısı olmasıdır. Ama, en bozuk durumda bulduğum şey ise istisnaları denetlemedir. İstisnaları denetlemek için Javascript çok tanıdık bir try-catch yapısı sağlar. İstisnalarla ilgili problem ise, bir çağrı yığınının üstünden kısa-yol hataları sağlarlar, fakat hata tamamen farklı bir yığında gerçekleştiğinde tamamen işe yaramaz olarak sonlanır…
