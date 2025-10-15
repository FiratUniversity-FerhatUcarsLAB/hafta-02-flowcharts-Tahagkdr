
Şunu dedin:
akıllı ev güvenlik graphvize göre kod yazarmısın
ChatGPT:

4 saniye düşündüm
Harika — akıllı ev güvenlik sistemini görselleştiren Graphviz (DOT) kodunu aşağıya hazırladım. Bu şema; sensörler, kameralar, kilitler, ana kontrol ünitesi (hub), bulut, mobil uygulama, kayıt cihazı ve alarm/entegrasyon akışını gösterir. İsterseniz oda/kat bazlı alt kümeleme, renkler veya ekstra bileşenler ekleyebilirim — söylemeniz yeterli.

Kodu doğrudan Graphviz’e (dot) yapıştırıp çalıştırabilirsiniz (ör. dot -Tpng -o smarthome.png smarthome.dot).

Graphviz (DOT) — Akıllı Ev Güvenlik Şeması
digraph SmartHome {
  rankdir=LR;
  bgcolor="#ffffff";
  node [fontname="Helvetica", fontsize=10];

  // Hub & Cloud
  hub [label="Güvenlik Hub\n(Controller)", shape=box, style="rounded,filled", fillcolor="#f0f8ff", penwidth=1.2];
  cloud [label="Bulut / AI Analitik", shape=cloud, style=filled, fillcolor="#fff5e6"];

  // Mobile & Notifications
  mobile [label="Mobil Uygulama\n(Owner)", shape=ellipse, style=filled, fillcolor="#e8f5e9"];
  push [label="Push / SMS / E-Posta\nBildirimleri", shape=note];

  // Recording & Storage
  nvr [label="NVR / Video Kayıt\n(Edge Storage)", shape=cylinder, style=filled, fillcolor="#f3e5f5"];
  backup [label="Yedekleme\n(Cloud Storage)", shape=cylinder];

  // Alarm & Monitoring
  alarm [label="Alarm Sireni\n(Çevresel Alarm)", shape=octagon, style=filled, fillcolor="#ffebee"];
  monitoring [label="Profesyonel\nİzleme Hizmeti", shape=box];

  // Subgraphs: Rooms / Zones
  subgraph cluster_perimeter {
    label="Çevre / Dış";
    style=dashed;
    color="#cfd8dc";
    front_door [label="Ana Kapı Kilidi\n(Smart Lock)", shape=diamond, style=filled, fillcolor="#fff3e0"];
    door_cam [label="Kapı Kamerası\n(Doorbell Cam)", shape=rect];
    motion_out [label="Dış Hareket Sensörü", shape=triangle];
  }

  subgraph cluster_living {
    label="Salon";
    style=dashed;
    color="#cfd8dc";
    cam_living [label="Salon Kamera", shape=rect];
    motion_living [label="Hareket Sensörü", shape=triangle];
    window_sensor [label="Pencere/İvme Sensörü", shape=triangle];
  }

  subgraph cluster_bedroom {
    label="Yatak Odası";
    style=dashed;
    color="#cfd8dc";
    smoke [label="Duman/CO Sensörü", shape=triangle];
    door_sensor [label="Kapı Manyetik Sensör", shape=triangle];
  }

  // Connections: sensors -> hub
  front_door -> hub [label="durum", arrowhead=normal];
  door_cam -> hub [label="video & event", arrowhead=normal];
  motion_out -> hub;
  cam_living -> hub;
  motion_living -> hub;
  window_sensor -> hub;
  smoke -> hub;
  door_sensor -> hub;

  // Hub interactions
  hub -> nvr [label="kayıt akışı / yedek", arrowhead=vee];
  hub -> cloud [label="özet & analiz", style=dashed];
  cloud -> hub [label="AI karar / güncelleme", style=dashed, color="#6a1b9a"];

  hub -> alarm [label="alarm tetikle", color="#d32f2f", penwidth=1.2];
  alarm -> monitoring [label="alarm bildirimi"];
  hub -> mobile [label="anlık bildirim"];
  cloud -> mobile [label="özet raporları"];

  // Recording/backup flow
  nvr -> backup [label="periyodik yedek", style=dotted];

  // Redundant/Failover links
  front_door -> mobile [label="kapı çalması (doğrudan)", style=dotted];
  door_cam -> nvr [label="doğrudan RTSP", style=dotted];

  // Visual grouping tweaks
  { rank = same; hub; cloud; nvr; }
