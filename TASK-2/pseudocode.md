digraph ShoppingCart {
  rankdir=TB;
  node [fontname="Helvetica"];
  edge [fontname="Helvetica"];

  Start [label="Başla", shape=oval];
  Browse [label="Ürünleri Gez / Listele", shape=box];
  ViewProduct [label="Ürün Detayı Görüntüle", shape=box];
  AddToCart [label="Sepete Ekle", shape=box];
  ViewCart [label="Sepeti Görüntüle", shape=box];
  CartOptions [label="Sepet: Güncelle / Kaldır / Kupon / Devam Et", shape=diamond];
  UpdateQty [label="Adet Güncelle", shape=box];
  RemoveItem [label="Ürünü Kaldır", shape=box];
  ApplyCoupon [label="Kupon Uygula", shape=box];
  CheckoutDecision [label="Ödeme Yapmak İstiyor musun?", shape=diamond];
  EnterShipping [label="Adres & Kargo Seçimi", shape=box];
  ChoosePayment [label="Ödeme Yöntemi Seç", shape=box];
  ProcessPayment [label="Ödemeyi İşle", shape=box];
  PaymentSuccess [label="Ödeme Başarılı?", shape=diamond];
  ConfirmOrder [label="Siparişi Onayla & Oluştur", shape=box];
  OrderComplete [label="Sipariş Tamamlandı", shape=oval];
  PaymentFailed [label="Ödeme Başarısız -> Hata Mesajı", shape=box];

  Start -> Browse;
  Browse -> ViewProduct [label="ürün seçildi"];
  ViewProduct -> AddToCart [label="sepete ekle"];
  AddToCart -> ViewCart;
  ViewProduct -> Browse [label="geri"];
  ViewCart -> CartOptions;

  CartOptions -> UpdateQty [label="adet değiştir"];
  CartOptions -> RemoveItem [label="ürün kaldır"];
  CartOptions -> ApplyCoupon [label="kupon uygula"];
  CartOptions -> CheckoutDecision [label="ödeme"];

  UpdateQty -> ViewCart;
  RemoveItem -> ViewCart;
  ApplyCoupon -> ViewCart;

  CheckoutDecision -> EnterShipping [label="evet"];
  CheckoutDecision -> Browse [label="hayır"];

  EnterShipping -> ChoosePayment;
  ChoosePayment -> ProcessPayment;
  ProcessPayment -> PaymentSuccess;
  PaymentSuccess -> ConfirmOrder [label="evet"];
  PaymentSuccess -> PaymentFailed [label="hayır"];

  PaymentFailed -> ChoosePayment [label="yeni yöntem dene"];
  ConfirmOrder -> OrderComplete;
  OrderComplete -> Browse [label="ana sayfaya dön"];
}

