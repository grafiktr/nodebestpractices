# Kodunuzu canlı ortam için hazır hale getirin

<br/><br/>


### Bir Paragraflık Açıklama

Canlı ortam istikrarını ve bakım yapılabilirliği oldukça etkileyecek geliştirme ipuçlarının listesi:

* On iki-faktör kılavuzu – [On iki faktör] kılavuzunu öğrenin (https://12factor.net/)
* Durumsuz olun(stateless) – Lokal olarak hiçbir spesifik web sunucusuna veri kaydetmeyin (ayrı madde imine bakın – ‘Durum bilgisiz olma’)
* Önbellek – Önbelleği çokça kullanın fakat önbellek uyuşmazlığından başarısızlığa uğramayın
* Belleği test edin – Gelişimsel akışınızın bir parçası olarak hafıza kullanımını ve sızıntıları ölçün, 'memwatch' gibi araçlar bu görevi bir hayli basitleştirebilir
* Fonksiyonları isimlendirin – Anonim fonksiyonların kullanımını en aza indirgeyin (satır içi geri arama gibi) çünkü sıradan bir hafıza profiler, method adı başına hafıza kullanım bilgisi sağlayacaktır
* CI araçlarını kullanın – Canlıya çıkmadan hataları tespit etmek için CI aracını kullanın. Örneğin, referans hatalarını ve tanımsız değişkenleri tespit etmek için ESLint kullanın. Senkronize APIleri (async versiyonu yerine) kullanan kodu tanımlamak için -trace-sync-io kullanın Use –trace-sync-io to identify code that uses synchronous APIs
* Log takibini akıllıca yapın – Herbir log komutunda içeriksel bilgilere yer verin, tercihen JSON formatında olsun çünkü bu şekilde Elastic gibi log toplayabilen araçlar bu özelliklere göre arama yapabilir (ayrı madde imine bakın - '‘Increase visibility using smart logs').Ayrıca, her isteği belirten ve aynı işlemi belirten satırları ilişkilendirmenizi sağlayan işlem kimliğini(transaction-Id) de ekleyin(ayrı madde imine bakın - 'Include Transaction-ID')

Hata yönetimi –  Hata işleme, Node.JS canlı ortamının Aşil tendonudur - birçok Node işlemi küçük hatalar yüzünden çöküyor, bazıları ise çökmek yerine hatalı olarak var olmaya devam ediyor. Hata denetleme stratejisi belirlemek kesinlikle kritiktir, yazımı okuyun [en iyi hata denetim uygulamaları] (http://goldbergyoni.com/checklist-best-practices-of-node-js-error-handling/)
