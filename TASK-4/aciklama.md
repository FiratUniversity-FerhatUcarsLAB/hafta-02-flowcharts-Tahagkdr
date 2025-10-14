Muhammed Taha GÖKDERE
250541092


Öğrenci sisteme giriş yapar veya kayıt olur, ardından mevcut dersleri görüntüler ve almak istediği dersleri seçer; sistem seçilen derslerin kredi limitini kontrol eder, eğer kredi limiti uygunsa ders kaydı onaylanır, değilse öğrenci tekrar ders seçimine yönlendirilir ve işlem tamamlanana kadar bu süreç devam eder, son olarak ders kaydı başarıyla tamamlanır


digraph DersKayit {
    rankdir=TB;
    node [shape=box, style=rounded, color=blue];

    Baslangic [label="Baslangic"];
    OgrenciGiris [label="Ogrenci Girisi / Kayit"];
    DersListele [label="Dersleri Listele"];
    DersSec [label="Ders Secimi"];
    KontrolKredi [label="Kredi Kontrolu", shape=diamond, color=red];
    Onay [label="Ders Kaydi Onayi"];
    Bitis [label="Kayit Tamamlandi"];

    Baslangic -> OgrenciGiris;
    OgrenciGiris -> DersListele;
    DersListele -> DersSec;
    DersSec -> KontrolKredi;
    KontrolKredi -> Onay [label="Kredi uygun"];
    KontrolKredi -> DersSec [label="Kredi asimi"];
    Onay -> Bitis;
}

<img width="276" height="685" alt="graphviz (3)" src="https://github.com/user-attachments/assets/73ff8d1e-41fd-49ab-a2c5-f824cf649a46" />

