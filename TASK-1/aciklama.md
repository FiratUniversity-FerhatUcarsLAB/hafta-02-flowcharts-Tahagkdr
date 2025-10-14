Muhammed Taha Gökdere
Öğrenci No:250541092

ATM Para Çekme Sistemi, kullanıcının kartını takıp şifre girmesiyle başlar.
Sistem kart ve şifre doğrulaması yaparak kullanıcının kimliğini onaylar.
Ardından kullanıcı çekmek istediği para miktarını girer.
Hesap bakiyesi ve ATM’deki nakit durumu kontrol edilir.
Her şey uygunsa para verilir ve hesap bakiyesi güncellenir.
Son olarak kart iade edilir ve işlem güvenle tamamlanır.

digraph ATM_Withdraw {
  rankdir=TB;
  node [fontname="Helvetica"];

  Start [shape=circle, label="Start"];
  InsertCard [shape=box, label="Kartı tak / Bekle (timeout)"];
  ReadCard [shape=diamond, label="Kart okunuyor mu?"];![87b2414b-4818-4e79-bf5a-0e7d3c84edce](https://github.com/user-attachments/assets/4ed848a3-93fe-47cc-b405-c2da42780c2f)

  InvalidCard [shape=box, label="Geçersiz kart -> Kartı çıkar"];

  PINPrompt [shape=box, label="PIN sor (max 3 deneme)"];
  PINValid [shape=diamond, label="PIN doğru mu?"];
  BlockCard [shape=box, label="Kart bloke et -> Bilgilendir"];

  ReadAmount [shape=box, label="Tutar gir"];
  CheckAmount [shape=diamond, label="Tutar geçerli mi?"];
  InsufficientAmount [shape=box, label="Geçersiz tutar -> İptal"];

  CheckBalance [shape=diamond, label="Bakiye yeterli mi?"];
  InsufficientBalance [shape=box, label="Yetersiz bakiye -> İptal"];

  CheckATMCash [shape=diamond, label="ATM nakit yeterli mi?"];
  NoATMCash [shape=box, label="ATM'de nakit yok -> İptal"];

  Confirm [shape=diamond, label="Onay? (Evet/Hayır)"];
  Dispense [shape=box, label="Nakit ver (dispense)"];
  DebitBank [shape=box, label="Banka hesabını güncelle (debit)"];
  Receipt [shape=box, label="Fiş yazdır / E-posta kaydı"];
  End [shape=doublecircle, label="End / Kartı çıkar"];

  NetworkError [shape=box, label="Ağ hatası -> Uyarı, kaydet, kartı çıkar"];
  HardwareError [shape=box, label="Donanım hatası -> Uyarı, kaydet, kartı çıkar"];

  // Akış bağlantıları (tüm hedef düğümler mevcut)
  Start -> InsertCard -> ReadCard;
  ReadCard -> PINPrompt [label="Evet"];
  ReadCard -> InvalidCard [label="Hayır"];
  InvalidCard -> End;

  PINPrompt -> PINValid;
  PINValid -> ReadAmount [label="Evet"];
  PINValid -> BlockCard [label="3 başarısız deneme"];
  BlockCard -> End;

  ReadAmount -> CheckAmount;
  CheckAmount -> ReadAmount [label="Geçersiz, tekrar sor", style=dashed];
  CheckAmount -> CheckBalance [label="Geçerli"];
  CheckAmount -> InsufficientAmount [label="Hayır"];
  InsufficientAmount -> End;

  CheckBalance -> CheckATMCash [label="Yeterli"];
  CheckBalance -> InsufficientBalance [label="Hayır"];
  InsufficientBalance -> End;

  CheckATMCash -> Confirm [label="Yeterli"];
  CheckATMCash -> NoATMCash [label="Hayır"];
  NoATMCash -> End;

  Confirm -> Dispense [label="Evet"];
  Confirm -> End [label="Hayır"];

  Dispense -> DebitBank;
  Dispense -> HardwareError [label="Donanım hata?", style=dashed];
  HardwareError -> End;

  DebitBank -> Receipt;
  DebitBank -> NetworkError [label="Ağ hata?", style=dashed];
  NetworkError -> End;

  Receipt -> End;
}

![Uploading 87b2414b-4818-4e79-bf5a-0e7d3c84edce.jpg…]()


