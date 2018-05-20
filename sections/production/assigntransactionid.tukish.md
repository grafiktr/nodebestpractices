# Her log komutuna ‘TransactionId’ ataması

<br/><br/>


### Bir Paragraflık Açıklama

Sıradan bir log tüm bileşenlerden ve isteklerden gelen girdilerin ambarı gibidir. Şüpheli satır veya hataları tespit ederken, aynı akışa ait olan diğer satırları tespit etmek oldukça zor olmaktadır (örneğin, "Can" kullanıcısı bir şey satın almaya çalıştı). Bu durum mikroservis ortamında, bir istek/işlem birden fazla bilgisayar üzerinden yayıldığında çok daha kritik ve zorlayıcı olur. Aynı istekten gelen tüm girdilere, eşsiz bir işlem kimliği(uniqueidentifier) değeri atayarak bunu belirtin. Böylelikle bir satır tespit edildiğinde kişi işlem kimliğini kopyalayabilir ve her bir satırda o işlem kimliğini arayabilir. Bununla birlikte, tüm isteklere tek parçacık olarak(single thread) hizmet veren Node.js’de buna ulaşmak basit değildir -verileri istek seviyesinde gruplayabilen bir kütüphane kullandığınızı düşünün- bir sonraki slaytta kod örneğine bakın. Diğer mikroservisleri çağırırken, aynı içeriği tutmak için işlem kimliğinizi “x-transaction-id” gibi bir HTTP üst bilgisine ekleyin.

<br/><br/>


### Kod örneği: basit Express yapılandırması

```javascript
//yeni bir istek alırken, yeni bir izole içerik(session) oluşturun ve işlem kimliğini(transaction Id) ekleyin. Örnekte, izole içerik oluşturmak için NPM'in continuation-local-storage kütüphanesi kullanılıyor. 
 
const { createNamespace } = require('continuation-local-storage');
var session = createNamespace('my session');

router.get('/:id', (req, res, next) => {
    session.set('transactionId', 'some unique GUID');
    someService.getById(req.params.id);
    logger.info('Starting now to get something by Id');
});

//Şimdi diğer tüm servis ve bileşenler istek bazlı olarak aynı içerik/veriye erişebilecek.
class someService {
    getById(id) {
        logger.info(“Starting to get something by Id”);
        // other logic comes here
    }
}

//Logger her kayıt için işlem kimliğini ekleyebilecek, aynı istek için eklenen her kayıt aynı değere sahip olacak
class logger {
    info (message)
    {console.log(`${message} ${session.get('transactionId')}`);}
}
```


