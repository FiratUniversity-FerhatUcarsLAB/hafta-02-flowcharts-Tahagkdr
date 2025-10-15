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

