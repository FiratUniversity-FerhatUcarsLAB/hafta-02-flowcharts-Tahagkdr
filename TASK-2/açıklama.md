Muhammed Taha GÖkdere
250541092

Bu sistem, kullanıcının ürünleri gezerek seçmesini ve sepete eklemesini sağlar.
Kullanıcı sepetini görüntüler, miktar güncellemesi veya ürün silme işlemleri yapabilir.
Alışverişi tamamlamak istediğinde, giriş yapması veya misafir olarak devam etmesi istenir.
Ardından kargo ve ödeme bilgileri girilir, ödeme doğrulaması yapılır.
Ödeme başarılıysa sipariş oluşturulur, başarısızsa tekrar deneme imkânı sunulur.
Süreç tamamlandığında kullanıcıya sipariş onayı gösterilir.


digraph AlisverisSepeti {
    rankdir=TB;
    node [shape=box, style=rounded, color=blue];

    Baslangic [label="Baslangic"];
    KullaniciGiris [label="Kullanici Girisi / Kayit"];
    UrunListele [label="Urunleri Listele"];
    UrunSec [label="Urun Secimi"];
    SepeteEkle [label="Sepete Ekle"];
    SepetiGor [label="Sepeti Gor"];
    Odeme [label="Odeme Bilgilerini Gir"];
    Onay [label="Siparis Onayi"];
    Bitis [label="Siparis Tamamlandi"];

    Baslangic -> KullaniciGiris;
    KullaniciGiris -> UrunListele;
    UrunListele -> UrunSec;
    UrunSec -> SepeteEkle;
    SepeteEkle -> SepetiGor;
    SepetiGor -> Odeme;
    Odeme -> Onay;
    Onay -> Bitis;
}
<img width="204" height="827" alt="graphviz (5)" src="https://github.com/user-attachments/assets/a3e1049a-f49a-46a0-a030-25ceac062a51" />
