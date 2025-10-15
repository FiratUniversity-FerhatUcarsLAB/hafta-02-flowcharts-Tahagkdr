// hastane_randevu_flow.dot
digraph RandevuAkis {
  rankdir=LR;
  node [shape=box, style=rounded];

  Reception [label="Resepsiyon / Web Portal"];
  Auth [label="Kimlik Doğrulama\n(M hasta / Kayıt)"];
  SearchDept [label="Bölüm / Doktor Seçimi"];
  CheckSlots [label="Uygunluk Kontrolü\n(Boş Saatler)"];
  SelectSlot [label="Saat Seçimi"];
  Confirm [label="Randevu Onayı"];
  Payment [label="Ödeme (opsiyonel)"];
  Notification [label="Bildirim Gönderimi\n(SMS / E-mail)"];
  CheckIn [label="Geldiğinde Check-in"];
  Cancel [label="İptal / Yeniden Planlama"];
  Waitlist [label="Bekleme Listesi"];

  // Akış
  Reception -> Auth -> SearchDept -> CheckSlots -> SelectSlot -> Confirm;
  Confirm -> Notification;
  Confirm -> Payment -> Notification;
  Confirm -> CheckIn [label="Gün geldiğinde"];
  CheckSlots -> Waitlist [label="Boş yoksa", style=dashed];
  Waitlist -> Notification [label="Yer açılınca bildirim"];
  Cancel -> Notification [label="İptal bildirimi"];

  // Hata/branch örneği
  Auth -> Reception [label="Hatalı / Yeni Kayıt", style=dotted];
  SelectSlot -> CheckSlots [label="Çakışma kontrolü", style=dotted];
}

