Muhammed Taha GÖkdere
250541092

Bu sistem, kullanıcının ürünleri gezerek seçmesini ve sepete eklemesini sağlar.
Kullanıcı sepetini görüntüler, miktar güncellemesi veya ürün silme işlemleri yapabilir.
Alışverişi tamamlamak istediğinde, giriş yapması veya misafir olarak devam etmesi istenir.
Ardından kargo ve ödeme bilgileri girilir, ödeme doğrulaması yapılır.
Ödeme başarılıysa sipariş oluşturulur, başarısızsa tekrar deneme imkânı sunulur.
Süreç tamamlandığında kullanıcıya sipariş onayı gösterilir.


digraph OnlineShoppingCart {
  rankdir=TB;
  node [fontname="Helvetica"];

  Start [shape=oval, label="Start"];
  Browse [shape=box, label="BrowseProducts()\nshow product list"];
  ViewProduct [shape=box, label="ViewProduct(id)\nshow details"];
  AddToCart [shape=box, label="AddToCart(id, qty)\ncart.add(id,qty)"];
  ViewCart [shape=box, label="ViewCart()\ndisplay cart items"];
  UpdateOrRemove [shape=box, label="UpdateQuantity(id,qty)\nRemoveItem(id)"];
  ContinueDecision [shape=diamond, label="continueShopping?"];
  Checkout [shape=box, label="Checkout()\nif cart.empty -> notify"];
  AuthDecision [shape=diamond, label="userLoggedIn?"];
  Login [shape=box, label="Login(username,password)\nauthenticate"];
  EnterShipping [shape=box, label="EnterShippingInfo(info)\nvalidate shipping"];
  EnterPayment [shape=box, label="EnterPaymentInfo(payment)\nvalidate fields"];
  ValidatePayment [shape=box, label="ProcessPayment(payment)\n-> paymentResult"];
  PaymentDecision [shape=diamond, label="paymentSuccess?"];
  ConfirmOrder [shape=box, label="CreateOrder(cart,shipping)\nsend confirmation"];
  FailureHandle [shape=box, label="HandleFailure()\nshow error / retry"];
  End [shape=oval, label="End"];

  /* flows */
  Start -> Browse;
  Browse -> ViewProduct;
  ViewProduct -> AddToCart [label="Add?"];
  AddToCart -> ViewCart;
  ViewProduct -> ContinueDecision [label="Back to list"];
  ViewCart -> UpdateOrRemove;
  UpdateOrRemove -> ContinueDecision;
  ContinueDecision -> Browse [label="Yes"];
  ContinueDecision -> Checkout [label="No"];
  Checkout -> ;AuthDecision;
  AuthDecision -> Login [label="No"];
  AuthDecision -> EnterShipping [label="Yes"];
  Login -> EnterShipping;
  EnterShipping -> EnterPayment;
  EnterPayment -> ValidatePayment;
  ValidatePayment -> PaymentDecision;
  PaymentDecision -> ConfirmOrder [label="Yes"];
  PaymentDecision -> FailureHandle [label="No"];
  FailureHandle -> EnterPayment [label="Retry Payment"];
  ConfirmOrder -> End

<img width="520" height="1727" alt="graphviz (1)" src="https://github.com/user-attachments/assets/0fb5ed6a-5a79-491c-a38d-dd2d5d7e1ba6" />


  
