niversite Ders Kaydı graphvize göre kod yazarmısın
ChatGPT:
Üniversite Ders Kaydı — Graphviz (DOT) örnek kodu

Aşağıda hem basit hem de biraz daha detaylı bir Graphviz DOT örneği var. İstersen bu kodu .dot dosyasına yapıştırıp dot -Tpng dosya.dot -o cikti.png ile görselleştirebilirsin.

1) Basit model — Öğrenci ⇄ Ders ⇄ Kayıt
// simple_course_registration.dot
digraph UniversityRegistration {
  rankdir=LR;
  node [shape=record, fontname="Helvetica"];

  Student [label="{Student|id: 1001\lname: Örnek Öğrenci\nyear: 2}"];
  CourseA [label="{Course|code: CSE101\ntitle: Giriş Programlama\ncredits: 4}"];
  CourseB [label="{Course|code: MTH101\ntitle: Calculus I\ncredits: 4}"];

  // Registration as an intermediate node (association)
  Registration1 [label="{Registration|reg_id: R0001\ndate: 2025-10-15\nstatus: enrolled}"];

  Student -> Registration1 [label="registers"];
  Registration1 -> CourseA [label="for"];
  Registration1 -> CourseB [label="for"]; // örnek: birden fazla ders için ayrı kayıt da olabilir
}

2) Daha detaylı model — Sınıflandırılmış (öğrenci, ders, dönem, önkoşul, çatışma, onay)
// detailed_course_registration.dot
digraph UniversityRegistrationDetailed {
  graph [splines=true, overlap=false];
  rankdir=TB;
  node [fontname="Helvetica"];

  subgraph cluster_students {
    label="Students";
    style=rounded;
    node [shape=record];
    S1 [label="{Student|id: S1001\name: Ayşe Yılmaz\year: 3\major: CSE}"];
    S2 [label="{Student|id: S1002\name: Mehmet Kara\year: 1\major: MATH}"];
  }

  subgraph cluster_courses {
    label="Courses";
    style=rounded;
    node [shape=record];
    CSE101 [label="{CSE101|Intro to Programming\ntime: Mon 09:00-11:00\ncredits:4}"];
    MTH101 [label="{MTH101|Calculus I\ntime: Mon 09:00-11:00\ncredits:4}"];
    CSE201 [label="{CSE201|Data Structures\ntime: Wed 14:00-16:00\ncredits:4}"];
  }

  subgraph cluster_terms {
    label="Term / Sections";
    style=dashed;
    node [shape=note];
    T2025F [label="Fall 2025"];
  }

  // Registration nodes (association with attributes)
  reg1 [shape=record, label="{Registration|reg_id: R001\ndate: 2025-09-02\nstatus: enrolled}"];
  reg2 [shape=record, label="{Registration|reg_id: R002\ndate: 2025-09-03\nstatus: pending\nauthorizer: advisor}"];

  // Edges
  S1 -> reg1 [label="registers"];
  reg1 -> CSE101 [label="for"];
  reg1 -> T2025F [label="term"];

  S2 -> reg2 [label="registers"];
  reg2 -> MTH101 [label="for"];
  reg2 -> T2025F [label="term"];

  // Prerequisite
  CSE101 -> CSE201 [label="prerequisite_of" style=dotted];

  // Schedule conflict (CSE101 and MTH101 same time)
  CSE101 -> MTH101 [label="time_conflict" color=red style=bold, arrowhead=none];

  // Approval flow
  advisor [shape=oval, label="Advisor"];
  reg2 -> advisor [label="requires approval" style=dashed];
  advisor -> reg2 [label="approves" style=dashed, color=green];

  // Legend (informal)
  Legend [shape=plaintext, label=<
    <TABLE BORDER="0" CELLBORDER="1" CELLSPACING="0">
      <TR><TD><B>Symbol</B></TD><TD><B>Meaning</B></TD></TR>
      <TR><TD>record node</TD><TD>Entity with attributes (Student / Course / Registration)</TD></TR>
      <TR><TD>dotted</TD><TD>Prerequisite relation</TD></TR>
      <TR><TD>bold red</TD><TD>Schedule conflict</TD></TR>
      <TR><TD>dashed</TD><TD>Approval / workflow</TD></TR>
    </TABLE>>];
  Legend -> S1 [style=invis];
