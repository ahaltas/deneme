# Maç Kadrosu ve Takım Oluşturucu

Oyuncu katılımını, kaleci seçimini ve 1–5 arası oyuncu puanlarını yöneten; seçilen kadrodan dengeli iki takım oluşturan PHP/MySQL uygulaması.

## XAMPP kurulumu

1. XAMPP Control Panel'den **Apache** ve **MySQL** servislerini başlatın.
2. `http://localhost/phpmyadmin` adresinde `database.sql` dosyasını içe aktarın. Dosya `ders_takim` veritabanını ve oyuncu tablosunu oluşturur.
3. Proje klasörünü `C:\xampp\htdocs\DersTakip` altında tutun.
4. `config.php` varsayılan XAMPP ayarlarıyla (`127.0.0.1`, `3306`, `root`, boş parola) çalışır. Farklı bağlantı bilgileri için `DB_HOST`, `DB_PORT`, `DB_NAME`, `DB_USER` ve `DB_PASSWORD` ortam değişkenlerini ayarlayın.
5. `http://localhost/DersTakip/` adresini açın.

## GitHub Pages (tek HTML dosyası ve JSON)

- Arayüz, CSS, JavaScript ve ilk açılışta kullanılan oyuncu verileri kök dizindeki tek `index.html` dosyasındadır. Sayfayı `players.json`, `app.css` veya ayrı bir JavaScript dosyası olmadan yayımlayıp açabilirsiniz.
- Oyuncu ve takım değişiklikleri yalnızca o tarayıcının `localStorage` alanında saklanır; başka cihazlara veya PHP/MySQL sürümüne aktarılmaz.
- İçe aktarma biçimini görmek için sayfanın üstündeki **Örnek JSON indir** bağlantısını kullanın. Bu örnek 20 oyuncu içerir; 14 oyuncu (2 kaleci dahil) maça katılıyor olarak işaretlidir.
- JSON paylaşımı için düzenleme modunda **JSON yedeği indir** ile dışa aktarın; başka tarayıcıda **JSON içe aktar** ile yükleyin.
- Statik sürümün düzenleme şifresi `1234` değeridir. Bu yalnızca arayüzdeki düzenlemeleri yanlışlıkla engelleyen bir kilittir; HTML/JavaScript istemcisinde saklanan şifre güvenlik sağlamaz ve kaynak kodu görebilen herkes tarafından aşılabilir. Gerçek erişim kontrolü için PHP/MySQL sürümünü kullanın.

## Kullanım ve düzenleme şifresi

- Sayfa ve takım bilgileri herkes tarafından görüntülenebilir. Oyuncu ekleme/silme, puan ve katılım değişikliği, takım oluşturma işlemleri için üstteki düzenleme şifresiyle giriş yapın.
- Düzenleme şifresi kaynak kodda parola özeti olarak tutulur. Farklı bir şifre belirlemek için `config.php` içindeki `EDITOR_PASSWORD_HASH` değerini PHP `password_hash()` ile üretilen özetle değiştirin.
- Ortak şifreyi yalnızca güvendiğiniz kişilerle paylaşın. İnternete açık dağıtımda varsayılan şifreyi mutlaka değiştirin ve HTTPS kullanın.
- Değişiklikleri kaydedin veya takım oluşturma düğmesiyle kaydedip takımları aynı anda üretin.
- 6'ya 6 ile 11'e 11 arasında seçim yapın. Takım oluşturmak için seçilen oyuncu sayısı, takım başına oyuncu sayısının iki katı ve maça gelen kaleci sayısı tam olarak iki olmalıdır.
- Takım boyutunu seçtikten sonra her iki takım için sunulan saha dizilişlerinden birini seçin. Örneğin 8'e 8 için `3 + 3 + 1`, kaleci hariç saha oyuncularının dizilişidir; bu nedenle takım başına 7 saha oyuncusu ve 1 kaleci gerekir. Oyuncuların saha çizgilerindeki yerleri hücum, oyun kurma ve savunma puanlarına göre otomatik atanır.
- Takımlar oluşturulduktan sonra takım kartındaki iki oyuncu listesinden aynı takımdaki saha oyuncularını seçip “Yerlerini değiştir” düğmesine basın. Değişiklik düzenleme şifresiyle giriş yaptıktan sonra kullanılabilir; kaleciler taşınmaz, takım büyüklüğü ve diziliş hatlarındaki oyuncu sayısı korunur.
- Takımlar oyuncu puanı, kaleci puanı ve mevki dağılımı gözetilerek dengelenir. Tekrar oluştur düğmesi farklı bir dengeleme denemesi yapar.

Bu, kullanıcı hesabı olmayan ortak bir düzenleme şifresidir; parola bilen herkes aynı yetkilere sahiptir. Düzenleme yetkisi oturum sonunda sunucu oturumu kapatılana kadar açık kalır; üstteki kilitleme düğmesiyle erkenden kapatılabilir.
