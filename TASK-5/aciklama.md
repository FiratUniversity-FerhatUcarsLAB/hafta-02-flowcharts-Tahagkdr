Muhammed Taha Gökdere
250541092
Akıllı ev güvenlik sisteminde önce sistemin aktif olup olmadığı kontrol edilir, eğer aktifse hareket algılanır, algılama sonrası alarm çalar, ardından ev sahibi bilgilendirilir ve kamera kaydı başlatılır, süreç sürekli takip edilerek durum güncel tutulur; eğer sistem aktif değilse takip bekleme modunda kalır.




digraph AkilliEvGuvenlik {
    rankdir=TB;
    node [shape=box, style=rounded, color=purple];

    Baslangic [label="Baslangic"];
    SistemAktif [label="Guvenlik Sistemi Aktif Mi?", shape=diamond, color=red];
    HareketAlgila [label="Hareket Algila"];
    Alarm [label="Alarm Cal"];
    Bildirim [label="Sahibi Bilgilendir"];
    KameraKayit [label="Kamera Kaydini Baslat"];
    Bitis [label="Durum Takibi Devam"];

    Baslangic -> SistemAktif;
    SistemAktif -> HareketAlgila [label="Evet"];
    SistemAktif -> Bitis [label="Hayir"];
    HareketAlgila -> Alarm;
    Alarm -> Bildirim;
    Alarm -> KameraKayit;
    KameraKayit -> Bitis;
}
<img width="596" height="567" alt="graphviz (4)" src="https://github.com/user-attachments/assets/72f9a246-1c6c-4ecb-9373-4f4bb1019365" />

