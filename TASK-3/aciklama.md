Muhammedn Taha Gökdere
250541092

Hastane randevu sistemi sürecinde hasta önce sisteme giriş yapar veya kayıt olur, ardından görmek istediği doktoru seçer; doktorun müsait olup olmadığı kontrol edilir, eğer müsait değilse hasta tekrar doktor seçimine yönlendirilir, müsaitse randevu tarihi ve saati belirlenir ve onaylanır, son olarak hasta randevu bildirimini alır ve süreç tamamlanır.



digraph HastaneRandevu {
    rankdir=TB;
    node [shape=box, style=rounded, color=green];

    Baslangic [label="Baslangic"];
    HastaGiris [label="Hasta Girisi veya Kayit"];
    DoktorSec [label="Doktor Secimi"];
    DoktorMüsait [label="Doktor Musait mi?", shape=diamond, color=red];
    TarihSaatSec [label="Randevu Tarih ve Saat Secimi"];
    Onay [label="Randevu Onayi"];
    Bildirim [label="Randevu Bildirimi"];
    Bitis [label="Randevu Tamamlandi"];

    Baslangic -> HastaGiris;
    HastaGiris -> DoktorSec;
    DoktorSec -> DoktorMüsait;
    DoktorMüsait -> TarihSaatSec [label="Evet"];
    DoktorMüsait -> DoktorSec [label="Hayir"];
    TarihSaatSec -> Onay;
    Onay -> Bildirim;
    Bildirim -> Bitis;
<img width="329" height="783" alt="graphviz (2)" src="https://github.com/user-attachments/assets/1c286382-8141-401b-8ac9-c06412821d89" />


    
