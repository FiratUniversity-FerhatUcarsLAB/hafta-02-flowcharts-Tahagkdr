digraph ATM_ParaCekme {
  rankdir=TB;
  bgcolor="white";
  node [fontname="Arial", fontsize=12];

  // Node stilleri
  start [label="Başla", shape=circle, style=filled, fillcolor="#C6E2FF"];
  insert_card [label="Kartı Tak"];
  read_card [label="Kart Bilgilerini Oku"];
  ask_pin [label="PIN Gir"];
  verify_pin [label="PIN Doğrula", shape=diamond];
  pin_ok [label="PIN Doğru", shape=plaintext];
  pin_fail [label="PIN Yanlış", shape=plaintext];
  wrong_pin_count [label="Yanlış PIN sayısı >= 3?", shape=diamond];
  retain_card [label="Kartı Tut (Güvenlik)", shape=box, style=filled, fillcolor="#FFD7D7"];
  select_tx [label="İşlem Seç: Para Çekme / Bakiye / ...", shape=box];
  choose_withdraw [label="Para Çekme Seçildi?", shape=diamond];
  enter_amount [label="Çekmek İstenen Tutarı Gir"];
  check_balance [label="Bakiye ve Limit Kontrolü", shape=diamond];
  sufficient [label="Yeterli bakiye?", shape=diamond];
  dispense_cash [label="Nakit Ver ve Makbuz Sor", shape=box, style=filled, fillcolor="#DFF7D8"];
  print_receipt [label="Makbuz Yazdır (isteğe bağlı)"];
  eject_card [label="Kartı İade Et", shape=box];
  end [label="Bitiş", shape=doublecircle, style=filled, fillcolor="#C6E2FF"];
  insufficient_msg [label="Yetersiz bakiye - İşlem reddedildi", shape=box, style=filled, fillcolor="#FFF1C6"];
  cancel_tx [label="İşlem İptal Edildi"];
  timeout [label="Zaman Aşımı", shape=box];
  ask_another_tx [label="Başka işlem yapmak ister misiniz?", shape=diamond];
  yes [label="Evet", shape=plaintext];
  no [label="Hayır", shape=plaintext];

  // Kenarlar / akış
  start -> insert_card;
  insert_card -> read_card;
  read_card -> ask_pin;
  ask_pin -> verify_pin;
  verify_pin -> pin_ok [label="Evet", color=black];
  verify_pin -> pin_fail [label="Hayır", color=black];

  pin_fail -> wrong_pin_count;
  wrong_pin_count -> retain_card [label="Evet"];
  wrong_pin_count -> ask_pin [label="Hayır", style=dashed];

  pin_ok -> select_tx;
  select_tx -> choose_withdraw;

  choose_withdraw -> enter_amount [label="Evet"];
  choose_withdraw -> eject_card [label="Hayır - Diğer işlemler", style=dashed];

  enter_amount -> check_balance;
  check_balance -> sufficient [label="Kontrol Et"];
  sufficient -> dispense_cash [label="Evet"];
  sufficient -> insufficient_msg [label="Hayır"];

  insufficient_msg -> ask_another_tx;
  dispense_cash -> print_receipt;
  print_receipt -> ask_another_tx;
  eject_card -> ask_another_tx;

  ask_another_tx -> yes [label="Evet"];
  ask_another_tx -> no [label="Hayır"];

  yes -> select_tx [style=dotted];
  no -> eject_card;
  eject_card -> end;

  // Cancel / timeout paths
  ask_pin -> timeout [label="Zaman aşımı?", style=dotted];
  enter_amount -> timeout [label="Zaman aşımı?", style=dotted];
  select_tx -> cancel_tx [label="Kullanıcı İptal Etti", style=dotted];
  cancel_tx -> eject_card;

  timeout -> eject_card;

  // Görsel küçük düzenlemeler
  { rank = same; pin_ok; pin_fail; }
  { rank = same; yes; no; }
}

