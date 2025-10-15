hastane randevu sistemi graphvize göre kod yazarmısın
ChatGPT:
4 saniye düşündüm
Hastane Randevu Sistemi — Graphviz (DOT) kodları

Aşağıda iki farklı Graphviz DOT örneği var — biri randevu akış (flowchart), diğeri veritabanı ER (entity-relationship) diyagramı. Her ikisini de dot ile PNG/SVG olarak render edebilirsiniz (ör. dot -Tpng flow.dot -o flow.png).

1) Randevu akış diyagramı (kullanıcı-akış / süreç)

Bu diyagram hasta kaydı → randevu oluşturma → onay/iptal ve hatırlatma süreçlerini gösterir.

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

2) Veritabanı ER diyagramı (kavramsal)

Temel tablolar: Patient, Doctor, Department, Appointment, Slot, Payment, Notification. Record şekliyle gösterim.

// hastane_randevu_er.dot
digraph ER {
  graph [splines=ortho];
  node [shape=record, fontname="Helvetica"];

  Patient [label="<id> PatientID | <name> Name | <dob> DOB | <tel> Phone | <email> Email"];
  Department [label="<id> DeptID | <name> DeptName | <loc> Location"];
  Doctor [label="<id> DoctorID | <name> Name | <spec> Specialty | <dept> DeptID"];
  Slot [label="<id> SlotID | <doctor> DoctorID | <start> StartTime | <end> EndTime | <status> Status"];
  Appointment [label="<id> AppID | <patient> PatientID | <slot> SlotID | <status> Status | <created> CreatedAt | <notes> Notes"];
  Payment [label="<id> PaymentID | <app> AppID | <amount> Amount | <method> Method | <status> Status"];
  Notification [label="<id> NotifID | <app> AppID | <type> Type | <sent> SentAt | <status> Status"];

  // İlişkiler
  Department:<id> -> Doctor:<dept> [label=" 1..* belongs to", arrowhead=none];
  Doctor:<id> -> Slot:<doctor> [label=" 1..* has slots", arrowhead=none];
  Slot:<id> -> Appointment:<slot> [label=" 0..1 reserved by", arrowhead=none];
  Patient:<id> -> Appointment:<patient> [label=" 0..* makes", arrowhead=none];
  Appointment:<id> -> Payment:<app> [label=" 0..1 may have", arrowhead=none];
  Appointment:<id> -> Notification:<app> [label=" 0..* sends", arrowhead=none];
}
