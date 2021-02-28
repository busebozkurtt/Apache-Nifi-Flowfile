# Apache-Nifi-Flowfile
Apache Nifi'de oluşturulan Flowfile verilerin enerji santral bilgilerini tek tek çekip , devam eden işlemcilerle birlikte gerekli işlemlerden geçirip SQL’e atma işlemini gerçekleştirir.

## Flowfile Processors

![aa](https://user-images.githubusercontent.com/50110116/109416858-b95df380-79d1-11eb-943e-f15eae80f3ce.png)

Öncelikle Invoke HTTP işelemcisine gerekli API izinleri verilerek enerji santralleri listesi santral id’si ile birlikte çekilmiştir. Daha sonra gelen veriler json arrayi şeklinde olduğundan dolayı array indexlerini parçalamak için Split Json işlemcisi kullanmıştır. Split Json işlemcisi ile birlikte arrayin tüm indexleri ayrı ayrı dosyalar olarak parçalanmıştır. Devam eden Evaulate Json Path işlemcisi ile birlikte verileri santral id’sine göre ayrı ayrı elde etmek için gerekli olan id değerleri santral listesinden çıkarılmıştır. İkinci Invoke HTTP’den sonra gelen Split JSon ve Evaulate JSon Path işlemcileri ile birlikte JSON dosyası parçalanmıştır ve gerekli değerler SQL’le atılmak üzere çıkarılmıştır. Son olarak put SQL ile birlikte değerler SQL’e atılmıştır. Invoke HTTP işlemcilerine Put Email bağlanmasının sebebi veriler çekilirken bir sorun oluşursa , eksik bilgi gelirse veya veriler istenilen formatta gelmezse bilgi mesajı göndermek içindir. Böylece hata mesajı alınır ve Flowfile durdurulur.
