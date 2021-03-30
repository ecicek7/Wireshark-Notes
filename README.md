# WIRESHARK

Kablolu ve Kablosuz Paket Yakalama

A --> <-- B  (Kablolu çift yönlü iletişim mevcut)

* Sniffer: Network kablosundan geçen trafiğin kopyasını yazılımsal olarak adresler ve iletir.
Wireshark yazılımsal bazlı bir sniffer uygulamasıdır.

LibPcap - WinPcap - Npcap - AirPcap --> Bahsedilenler bizim library'lerimizdir. 
Katman katman olan modüllerin hepsini kullanmak yerine kütüphane ile kod çağırabilir ve istediğimiz paketi yakalayabiliriz.

Trace Dosyası, kablolardan gelen paketleri yakalayan dosyalardır. Kablodan gelen paketleri yakalayan library'ler var. Bu library'ler trace dosyaları da kaydedebiliyor. 
Library'ler belirli işletim sistemlerinde çalışır ancak WireTap Library tüm sistemlerde tüm dosyaları açabilir ancak capture filter yapamıyor.
Birden fazla Capture seçimi yaparak birden fazla kablolu/kablosuz veri akış platformu takip edilebilir.

### Kısayol Sekmeleri

Sekmeler içerisinde en çok işimize yarayacak seçenekler aşağıda sunulmuştur. Bu sekmeler bizlere kullanım kolaylığı ve opsiyonel birkaç fonksiyon sağlamaktadır.

* Tablarda bulunan "File" sekmesi içerisinden Export Objects butonu ile istenilen formattaki verilerin nereye ait olup nereye gittikleri veri türü bazından ifade edilir. 
  *** Örneğin HTTP seçilirse gidilmiş olan web siteleri URL bazlı görüntülenirken, TFTP seçilmesi durumunda veri aktarımlarına ait sunucu adresleri görüntülenecektir.
      Ek olarak eğer URL içerisindeki HTTP veya görüntülenmiş bir görsel (PNG - JPG) var ise masaüstüne kaydetmek ve bu adresi / belgeyi görüntülemek mümkündür.

* Tablarda bulunan "Edit" sekmesi içerisindeki "Mark Packets" seçeneği ile paketler işaretlenebilir. İşaretli paketlerin de işaretleri kaldırılabilir.

* Tablarda bulunan "View" sekmesi ile uygulamanın ve arayüzün nasıl görüneceğine karar verebilirsiniz. Sütun ölçüleri, karakter boyutu veya görüntülenecek paket detayları buradan kararlaştırılabilir.

* Tablarda bulunan "Go" sekmesi ile seçili paketin bir önceki / bir sonraki aşamalarına ilerlemek mümkün.
  Ayrıca paketin kendisini incelemek için pakete gitmek veya paketi terk edip başa dönmek için kısayol sağlar.
  
* Kalan tablar daha detaylı olarak konu içerisinde işlenecektir.

### Filter Toolbar

Bookmarks    -->	Default filitrelerdir, En çok kullanılan filitreler bulunur.
Filter Input -->	Manuel olarak ifade girilir. Doğru ifade girildiğinde protokole ait renk görünür.
Clear        -->	Temizler ve tüm paketler görüntülenir.
Apply        -->	Yazılan filitreleri uygular.
Recent       -->	Geçmişte yazılmış olan filtreleri gösterir.
Add Button   -->	Çok kullanılan bir filtreyi kısayol olarak ekler ve kullanımını kolaylaştırır.

 * "Bookmark" sekmesi içerisinden "Manage Display Filters" seçeneği ile kendinize filtre oluşturup bookmark içerisine ekleyebilirsiniz.
Analyse - Display Filter Expressions - Bu kısımdan herhangi bir filtre için detaylı olarak kodları görüntüleme şansına sahipsiniz.
 -- Örneğin;  " icmp.type == 8 " bir echp request ve " icmp.type == 0 " bir echo reply için görüntüleme / filitreleme komutudur. 
  
### Display Filter Operatörleri

* Equal To: 					"==" veya "eq" ile ifade edilir.

* Or: 						"||" veya "or" ile ifade edilir.

* And:				 	  	"&&" veya "and" ile ifade edilir.

* Greater Than: 				">" veya "gt" ile ifade edilir.

* Less Than: 					"<" veya "lt" ile ifade edilir.

* Greater Than or Equal To: 	">=" veya "ge" ile ifade edilir.

* Less Than or Equal To: 		"<=" veya "le" ile ifade edilir.

* Not: 						"!" veya "not" ile ifade edilir.

* Not Equal To: 				"!=" veya "ne" ile ifade edilir.

* Contains: 					"contains" ile ifade edilir.

* Matches: 					"matches" ile ifade edilir.


    - Örneğin "tcp.port == 80" filitresi kullanıldığında Destination veya Source portları 80 olan tüm tcp paketleri listelenir.
	Eğer tek yön veya başka bir paket daha belirtilmek isteniyorsa ek filitre eklenebilir.
	
	- Örneğin "tcp.port == 80 || tcp.port == 443" filitresi ile Destination veya Source portları 80 veya 443 olan tüm tcp paketleri listelenir.

	- Örneğin "icmp and ip.ttl = 64" filitresi ile TTL değeri 64 olan tüm ICMP paketleri listelenir. 
	Böylece iki filitre şartını da sağlaması gerektiğini gözlemlemiş oluruz.
	
#### NOT
Filitreleme aşamasında öncelikli bir filitre mevcut ise parantezler kullanılır. Bu durumda önce mutlaka parantez içinde yer alan filitre şartı yerine getirilecektir.
Örneğin "(ip.src == 172.16.1.14 and udp.port == 53) or tcp.port == 80" filitresi ile belirtilen IP'ye ait DNS verileri ve tüm HTTP verilerine ait çıktılar görüntülenir.
Bu durum bizlere birden çok filitreleme operatörünü aynı filitreleme içerisinde kullanabilme kollaylığı sağlar.
	
Pakete tıkladıktan sonra paket numaralarının en solunda belirli işaretler görünüyor.
Bu işaretler paketin başlangıç, bitiş, aradaki ilgili ve ilgisiz paketleri, acknowledge gibi tüm paketlerin gösterimini sağlıyor.
Böylece gönderilen bir paketin gönderimine ait tüm detaylar görüntülenebiliyor.

### Mouse Sağ Klik İle;

* "Mark" edilerek öne çıkarılabilir.
* "Ignore" edilerek ilgili alanda görünmez hale getirilebilir.
* "Set" edilerek iki paketin arka arkaya yakalanma süreleri default olarak 0 değerine çekiilr ve inceleme açısından kolaylık sağlar.
* "Comment" edilerek paketin içerisine bir yorum bir not eklenebilir ve paket içerikleri arasında görüntülenebilir.
* "Edit Name Resolution" kısmında mevcut paketteki IP adreslerine -Gateway- veya -PC- gibi kısaltma isimler vererek IP adresi yerine bu isimlerin kullanılması sağlanır. 
CPU'dan yer, tercih edilmez.
* "Apply as Filter" butonu ile seçilen paketin MAC veya Ethernet vs.. gibi adreslerine ait tüm paketler kolayca filitrelenebilir.
* "Colorize Conversation" butonu ile karşılıklı olarak aynı görüşen cihazların konuşmasını tek renk altında görüntüleme imkanı sağlıyor.
* "Follow - TCP Stream" ile mevcut TCP paketinin tüm içeriğini görüntüleme imkanı sunuyor. Gönderilen ve yazılan veriler ekrana düşüyor.
* "Copy" butonu ile txt olarak kaydedebilir, Hexadecimal değerleri kopyalayabilir ve bu paketleri daha sonrasında tek başına açıp okuma imkanı bulabiliriz.
 
### Long Range Trafik Capture

Router ve Firewall arasında Shark Tap cihazlar koyularak ekstra trafik oluşturmadan üzerinden geçen trafiğin kopyasını alır ve incelenmesine uygun ortam hazırlar. (Sniffer)

Bir switch veya router üzerinden Port Mirroring yapmak için cihaza;
* 1- "monitor session 1 destination interface f0/1"

* 2- "monitor session 1 source interface f0/2"

* 3- "show monitor session 1" komutu ile komutlar ve durumları gözlemlenebilir

Komutları ile iki cihaz arasındaki iletişimin başka bir cihaza aktarılmasını sağlar ve iletişimi takip edebiliriz.

Sniff edilen switch'in arkasında bulunan bir kullanıcı veya başka bir switch trafiği takip edilmek isteniyorsa Rspan Config yapılabilir.
Veya uzak konumdaki bilgisayara WinPcap library ile birlikte Rpcap.exe yüklenmeli. Böylece bilgisayarı bir sunucu, wireshark'ı ise dinleyici olarak konumlandırabiliriz.
Bu durumda programın yüklü olduğu kullanıcı Port2003 üzerinden sunucu gibi, wireshark yüklü admin ise Port2002 üzerinden trafik listener olarak davranacaktır.
Cmd üzerinden "rpcapd -n" üzerinden sunucu tarafını çalıştırdıktan sonra wireshark'da Capture Options - Manage Interface - Remote Interface butonuyla uzaktaki kullanıcının IP ve Port bilgileri girilir.

Böylece interface girşi sağlanır ve uzaktaki bir trafik yakalanabilir.

***

##### Bir Packet Capture'ın ne zaman yakalanacağı hangi paketleri yakalayacağını ne kadar büyüklükte olacağı vb durumları bilerek paket yakalamaya başlayıp farklı farklı kaydedebilmek için;

- Capture - Output sekmesi üzerinden dosyanın hangi konuma ve hangi formatta kaydedileceği seçilir.
- Create a new file seçeneği seçilirse süreye veya büyüklüğe bağlı olarak belirli sınıra her ulaşıldığında yeni dosya olarak kaydedilmesini sağlar.
- Ring buffer seçeneği seçilmesi durumunda yazılan sayısal değer kadar dosya kaydeder. 

Trafiği yakalamaya devam ettikçe ilk paketi silip üzerine yazacaktır.  Rakamsal bazda sıralı ilerlerse de max 5 dosya kaydedecektir.
Yani 5 paket sınırı koyulduğunda ve 5 paket üretildiğinde trafik yakalanmaya ve kaydedilmeye devam ediyorsa 1'inci paket silinir ve 6. capture 1'in üzerine yazılır.

### Command Line Capture

* Cmd açıldığı zaman user directory açık olarak geliyor. Buradan çıkmak için "cd  \" yazıyoruz.
* Ardından "dir" komutu ile C:/ diski içerisinde bulunan tüm klasörleri görüntülüyoruz.
* Girmek istediğimiz klasörün adını cd komutuyla açabilirsiniz örneğin "cd Wireshark" komutu ile wireshark klasörüne giriyoruz.
* Tekrar "dir" komutu ile bu klasör içerisindeki dosyaları görüntülüyoruz. Burada kullanacağımız uygulamanın adı "tshark".
* Tshark altında trafik capture yapılabilecek interface'leri görüntülemek için "tshark -D" komutunu kullanıyoruz. 
* Bu komut bu durumda şekildeki gibidir; " C:\Program Files\Wireshark>tshark -D "
* Tshark altında aktif durumda olan interface'leri görüntüledikten sonra belirli parametreler ile paket yakalamayı başlatıyoruz.
* Örnek komut " C:\Program Files\Wireshark>tshark -i 9 -f "icmp" -a duration:15 -w TEST.pcap " şeklindedir.
    * --i : Kaçıncı interface takip edilmek isteniyor
    * --f : Yakalanacak olan paketin türü belirlenir
    * --a : Paket yakalama esnasında "duration" veya "packetsize" gibi capture durdurma operasyonlarının eklenebilirliğinin karar verilmesini sağlar.
    * --w : Yakalanan trafiğin hangi isim ve uzantı ile kaydedileceğini kararlaştıran komutur.
* Yakalanan ve kaydedilen bu paket programın kayıtlı olduğu noktaya kaydedilir. İçinde bulunduğunuz klasörler / dosyalar aynı zamanda save konumunuz olur.
* Hangi komutun ne anlama geldiğini öğrenmek için " tshark -h " komutu ile (help) bu uygulama içerisinde hangi komutun ne anlama geldiğini görebiliriz.
* Paket yakalama işlemi sona erdiğinde ise kaldığımız yere "TEST.pcap" yazarak yakalanan paketler görüntülenir.
* Bu aşamada açmak istediğiniz paketin adı ve formatının girilmesi yeterlidir.

### Capture Filtering - 

Trafiği veya trafik içerisinden istenilen yerleri daha kolay yakalamak ve depolama alanını gereksiz yere doldurmamak için filtering avantajdır.
Capture options kısmından istenilen interfacelere filter eklenebilir. 
Ayrıca ek olarak kendinize özel bir filterin eklemesi yapabilirsiniz. Bu aşamadaki formül " Primitive = Qualifier + Identifier "

Identifier : Decimal, hexadecimal, ascii, port 53, port 443, 192.168, 172.16 vs..
Qualifier  : host, port, destination, source, tcp, udp, arp vs..
Primitive  : destination host host, source host host, destination net 192.168.10.0/24 vs..

Örneğin gateway ve bir websitesi olan www.wireshark.org'a cmd üzerinden ping atalım. Ping atımlarında URL ve IP kullanılabilir.
Capture almadan önce interface seçerken görünen enter a capture filter kısmına "host wwww.wireshark.org" yazılması durumunda bu adrese giden paketler yakalanır.
* Eğer bu komut "destination host www.wireshark.org" şeklinde yazılmış olsaydı, sadece destination olarak wireshark'a iletilen trafik yakalanır.

* Eğer bu komut "source host www.wireshark.org" şeklinde yazılmış olsaydı, sadece source olarak wireshark'dan gelen paketler yakalanır.

* Ayrıca ether denilen bir komut mevcut. Örneğin; "ether dst 98-AF-65-30-05-11" şeklinde filitreleme yapıldığında bu MAC adresine yönelen (dest) trafik yakalanır.

* Ayrıca net denilen bir komut mevcut. Örneğin; "net 192.168" şeklinde filitreleme yapıldığı zaman bu IP bloğuna sahip networkten gelen trafik yakalanır.
Bu komutu "net 192.168.1.0/24" şeklinde IP ve Prefix bütünüyle filitreleme işlemine dahil edebilirsiniz.

* Ayrıca "not ether host 98-AF-65-30-05-11" komutu ile bu MAC adresine gelen paketler haricinde trafikte akan tüm veriler görüntülenebilir.

* Ayrıca uygulama tabanlı filitreleme yapılmak isteniyorsa "port 53" veya "dst port 53" gibi filitreler kullanılarak da trafik yakalanabilir.
Bu filitreleme sonrasında gelen cevaplar ile "A" IPv4 "AAAA" IPv6 bilgilerini sorgularken "PTR" Lokal için gönderim sağlamaktadır.
Herhangi bir web sitesine dair IP - Sunucu vb bilgilere erişmek için cmd üzerinden "nslookup www.wireshark.org" yazarak bu bilgilere ulaşmak mümkündür.

Birden fazla filtre  birleştirmek için and-or-not operatörleri kullanılır.
Örneğin; "host www.wireshark.org and not port 80" veya "host 192.168.1.103 and tcp dst 53" veya "host 192.168.1.101 or tcp dst 53"

* NOT - Belirli bir bölümün trafiği olsun ancak onun içerisinde şu kısım olmasın.
* AND - Belirli bir bölüm ve o bölümle birlikte şu uygulama da birlikte olsun. Yani ikisi aynı anda, kesişim durumunda olsun.
* OR  - Belirli bir bölüm olması durumundada da, başka bir durum olması durumunda da trafik yakalansın. Yani 2 durum için de tüm küme dahil olsun. Tek de olsa ortak da olsa yakalansın.

Hazır gelen filtreleri uygulama dışında da manuel olarak düzenlemek ve paylaşmak mümkün. 
Bunun için öncelikle uygulama menüsü içerisinden Help - Folders - Global Configuration kısmıına girilir.
Burada bulunan "cfilter" dosyasını Notepad++ vb uygulamalarla açıp düzenleyebilir, bu dosyayı başkalarıyla da paylaşabilirsiniz.

### Statistics Sekmesi -

Statistics sekmesi altında sağ klik ile protokol bazlı veya iki adresin haberleşmesi baz alınarak bir filitreleme uygulamak mümkündür. 

- Statistics sekmesi içerisinden "Protocol Hierarchy" bölümü ile mevcut trafik içerisinde Layer1 to Layer7 olmak üzere katman katman hangi protokollerin ne kadar büyüklükte iletildiği ve kaç tane iletildiği görüntülenir.
- Statistics sekmesi içerisinden "Conversations" bölümü ile mevcut trafik için hangi protokol ile hangi cihazlar arasında haberleşme sağlandığı görüntülenir.
- Statistics sekmesi içerisinden "Endpoints" bölümü ile Layer2 ve Layer3 üzerinden tespit ettiği cihazları kayıt altında tutar ve filitrelenirse sadece bu cihazlarla yapılan tüm iletişim görüntülenir.

Protokol bazlı sağ tıklayıp apply as filter denildiği zaman tüm trafik içerisinden seçili protokole ait tüm paketler filitrelenmiş şekilde ekranda görüntülenecektir.

- Statistics sekmesi içerisinden iletimdeki trafiğin yönünü belirterek iki cihaz arasında filitreleme yapmak mümkündür.
- Statistics sekmesi içerisinden "Packet Length" bölümü ile mevcut trafik içerisinde gönderilen tüm paketlerin ortalama olarak boyutu ve bu bazda ortalamaları görüntülenir.
- Statistics sekmesi içerisinden "I/O Graphs" bölümü ile mevcut trafik içerisindeki input ve output iletimler grafik olarak ekrana yansıtılır ve takip edilir.
- Statistics sekmesi içerisinden "Resolved Addresses" bölümü ile mevcut trafik içerisinde 

Apply as denilmesi filitreyi uygular, prepare as filter seçilmesi durumunda search tab üzerine filitre içeriği girilir ancak çalıştırılmaz.

### Follow Streams

Stream bir verinin aktarım esnasında oluşan ve geçtiği katmanlar sonrası gözlemlenen veri akışıdır.
Bir dosyanın download veya upload edilirken UDP / TCP protokolü ile iletimi Wireshark üzerinde görüntülenmektedir.
Belirli bir aralıkta bulunan UDP paketlerini sağ tıklayıp Follow Stream seçeneğini seçtikten sonra türüne göre görüntüleyebiliriz.

1. Eğer paketler UDP ile aktarılmışsa;

* Ses veya Görüntü paketidir. Stream üzerinde görüntülenen ilk harf G ise Graphical yani video, V ise Voice yani ses dosyasıdır.
* Görüntülenen stream içeriği "Raw" olarak, yani ham şekilde farklı kaydedeilebilir. 
* Kaydedilen veri VLC Player gibi bir uygulama aracılığı ile tekrar ses veya görüntü dosyasına dönüştürülebilir.
* Böylece trafik üzerinden gönderilen veya alınan bir Video - Ses dosyasını kaydetmek mümkündür.

Ayrıca voice trafiği bir IP telefon aracılığı ile yapılmışsa;
Sekmeler üzerinde bulunan "Telephony" sekmesi içerisinden "VoIP" seçeneği seçilerek çıkan ses mesajını çalıştıırmak mümkündür.

2. Eğer paketler TCP ile aktarılmışsa;

* TCP ile aktarım sağlayan görüntü, ses ve dosyaların yakalanması sağlanabilir. Örneğin FTP ile veri aktarımı.
* Stream üzerinde görüntülenen ilk satır dosyanın uzantısını göstermektedir ".PNG" şeklinde.
* Görüntülenen stream içeriği "Raw" olarak, yani ham şekilde farklı kaydedebilir. 
* Kaydedilen veri bir uygulama aracılığı ile tekrar dosya formatına dönüştürülebilir. Örneğin bir PNG dosyası fotoğraf görüntüleyici ile açılabilir.
* Böylece trafik üzerinden gönderilen veya alınan bir veriyi yakalamak ve kaydetmek mümkündür.

3. Eğer bir HTTP Stream yakalanmak isteniyorsa;

* HTTP protokolü web üzerinden ile haberleşme sağlanırken kullanıcı ve sunucu tarafından gerçekleştirilen istekler ve veri akışı takip edilebilir.
* Veri akışı sırasında oluşan "HTTP / GET" üzerine sağ tıklayarak Follow TCP seçeneği seçilir. Böylece Client ve Sunucu arası konuşma clear-text halinde görüntülenir.
Eğer bu web sitesi HTTP değil de HTTPS ise websitesine ve iletişime dair bilgileri bu şekilde görüntülemek mümkün değildir. 
* Bu web sitesi her şekilde görüntülenmek istenirse, File - Export Objecrt - HTTP seçenekleri takip edilerek web sayfasında bulunan tüm detaylar görüntülenebilir.
* Save All butonu ile HTML olarak tümü kaydedilirse, ve kaydedilen "%5c" dosyası "index.exe" diye değiştirilirse, web sayfasını tümüyle görüntüleyebilmek mümkündür. 
* Sayfa üzerindeki her bir görüntüleme farklı stream ile kaydedilir. Bu yüzden bu işlemler Stream0-1-2-3-4 için yapılırsa, animasyon vb. görselleri de adım adım takip etmek mümkündür.

##### NOT: Bu aşamada paket içerisinde görüntülenen bilgilerden bir tanesine sağ tıklayıp "Apply as Column" butonuna basılırsa bir sütun olarak bu seçenek ana ekrana eklenir.

***
