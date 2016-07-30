# vsftpd Hakında
vsftpd GPL lisanslı *NIX systemler için geliştirilmiş bir FTP (File Transfer Protokol) sunucusudur. İsmini very secure (çok güvenli) FTP'den alan sunucu Güvenlik, Performans ve Stabilite özelliklerini sunmak konusunda iddialıdır. 
#### Özellikleri
  * Sanal IP yapılandırması
  * Sanal kullanıcılar
  * Bağımsız veya inetd çalışma özelliği
  * Kullanıcı bazlı yapılandırma
  * Kaynak bazlı IP yapılandırması
  * Kaynak bazlı IP kısıtlama
  * IPv6 Desteği
  * SSL Desteği
  * ve daha fazlası

Daha detaylı bilgi, performans analizleri, güvenlik analizleri için geliştiricinin sitesine [burdan](https://security.appspot.com/vsftpd.html) göz atabilirsiniz.
  redhat,suse,debian,freebsd,gnu,gnome,kde,kernel ve çok daha fazla açık kaynak organizasyonları FTP server olarak vsftpd tercih etmektedir.

## vsftpd Sunucusu Sıkılaştırma Klavuzu
Bu klavuzda vsftpd sunucusunun sıkılaştırılması ve SSL/TLS desteğine kavuşturulması için adımlar anlatılacaktır. Bu adımları manul olarak yapabileceğiniz gibi hem sıkılaştırma işlemi için hemde SSL/TLS desteği için hazırlanmış betikleri kullanmaznızda mümkündür. Tüm adımlar Ubuntu 14.04.4 LTS ve Kali Linux 2016-1 işletim sistemleri üzerinde test edilmiştir.

###vsftp Sunucusunun Kurulumu
Sıkılaştırma işlemi paket yöneticisi yardımıyla yüklenen vsftpd sunucusuna uygulanmıştır. Kaynak kod üzerinden derleme yaparak kurulum yapılmış sunucu için birçok adım aynı olsada değişiklik yapılacak yapılandırma dosyanının dizini değişiklik gösterebilir. vsftpd sunucusunu yüklemek için terminalden aşağıdaki komutu girmek yeterlidir.

    sudo apt-get install vsftpd 


###vsftp Sunucusunun Sıkılaştırılması
Sıkılaştırma işlemini gerçekleştirebilmek için etc dizini altında vsftp sunucusunun yapılandırma dosyasında değişiklik yapılması gerekmektedir. Tercih ettiğiniz bir dosya editörü vasıtasıyla vsftpd.conf dosyasını açın.

   sudo nano /etc/vsftp.conf
 
 FTP sunucuları dosya paylaşımı amaçlı geliştirildiğinden anonim girişlere izinlidir. Ancak sunucunuzu güven altına alabilmek için bu özelliğin kapatılması gerekmetedir bu sebeple _anonymous_enable_ değişkenini bulup "NO" yapın.
 
    anonymous_enable=NO


###vsftp Sunucusunun SSL/TLS Desteği Eklenmesi
FTP yapısı gereği clear text bir protokoldür. Yani paketler şifrelenmeden açık metin şekilde ağ üzerinde gönderilirler. vsftpd sunucusu secure FTP desteği sunmaktadır. Hatta 3.03 sürümüyle SSL/TLS iyileştirmeleri yapılmıştır. Bu adımda vsftpd sunucusuna SSL/TLS desteğini nasıl ekleyebileceğimizi anlatacağım.
