
## Problem - DDL ve DML Komutları
Bu senaryo içerisinde sizlere tahsis edilen makinelerde belirtilen dosya dizinine ulaşmanızı ve klasörlerin içerisine aşağıdaki talimatlar gereğince backup işlemlerini uyguladığınız bir senaryo hazırlamanız istenmektedir.
---

### Bilgi 

SQL DML (Data Manipulation Language) Veri İşleme Dili:
Veritabanında bilgi üzerinde çalışmayı sağlar. Bilgiyi çağırma, bilgiye yeni bir şeyler ekleme, bilgiden bir şeyler silme, bilgiyi güncelleştirme işlemlerini yapar.

Temel dört komutu vardır:

·SELECT : Veritabanındaki istenilen alanı çağırmayı ve gereken bilgiyi görebilmeyi sağlar.

· UPDATE : Veritabanındaki kayıtlar üzerinde bilgi güncellemeyi sağlar.

· INSERT : Veritabanına alan eklemeyi sağlar.

· DELETE : Veritabanından alan silmeyi sağlar.

SQL DDL (Data Definition Language) Veri Tanımlama Dili:
Verilerin tutulduğu nesneler olan tabloların yaratılmasını, silinmesini ve bazı temel özelliklerinin düzenlenmesini sağlar.

En yaygın kullanılan komutları şunlardır:

.CREATE TABLE : Veritabanı üzerinde bir tablo yaratmak için kullanılır.

.ALTER TABLE : Var olan nesnede değişiklik yapmak, yeni bir sütun eklemek, sütunun tipini veya uzunluğunu değiştirmek gibi yapısal değişiklikler için kullanılır.

.DROP TABLE : Tabloyu verilerle birlikte kalıcı olarak siler.

.TRUNCATE TABLE : Tablodaki veri içeriklerini siler fakat tablo yapısı kalır.

.CREATE INDEX : Index oluşturmak için, tablonun sütun adı üzerinde indeks oluşturur.

.CREATE VIEW : Görüntü oluşturmak için kullanılır.

.DROP VIEW : Görüntüyü siler.

Bu senaryoda, Alpine imajında çalışan bir MSSQL veritabanı oluşturacak ve ardından bir tablo oluşturup tablo içerisine kayıtlar atıp daha sonra bu koyutları sorgu ile çekeceğiz.

### Talimatlar

1. Servislerimizin çalıştığını `docker version` ile kontrol edelim.
2. Docker imajımızı `docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=password1" -p 5432:5432 -d mcr.microsoft.com/mssql/server:2022-latest` ile ayağa kaldıralım.
3. Docker containerımın `docker container ls` komutu ile ayağa kalktığını görebiliriz.
1. Ana dizinde `/home` bir dizinine gidin.
2. Postgresql veritabanını docker imajı ile ayağa kaldırabilmek için `docker run --name mypostgresdb -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d postgres` komutunu çalıştıralım. 
3. Docker imajının çalıştığından emin olduktan sonra `docker exec -it mypostgresdb bash` komutunu çalıştırıp postgresql veritabanına erişelim. 
4. `psql -U postgres` komutunu çalıştırarak bağlantı gerçekleşir ve burada psql komutlarını çalıştırabilirsiniz. 
5. Postgresql veritabanına bağlandıktan sonra aşağıdaki komutları çalıştırarak tablo oluşturup terminal üzerinden bir yedek alacağız.
6. `mydatabase` adında yeni bir veritabanı oluşturun sonrasında `\c mydatabase` diyerek veritabanınıza bağlanın. 
7. Bağlantı yapıldıktan sonra yeni bir tablo oluşturunuz ve bu tabloyu da oluşturulan SQL dosyasını kullanarak tabloyu oluşturmak için `psql -U postgres -f create_table.sql` komutunu çalıştırınız ve psql içinden `\q` komutu ile çıkınız. 
8. Tablo başarıyla oluşturulduktan sonra, `pg_dump` komutunu da kullanarak bir yedek alma işlemi gerçekleştirebilirsiniz. 
9. İşlemleri tamamladıktan sonra "Kontrol Et" butonuna basınız ve senaryoyu tamamlayınız.
