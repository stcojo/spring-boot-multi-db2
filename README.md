# spring-boot-multi-db2

Exemplu de aplicatie Spring Boot ce ruleaza pe baze de date Oracle distribuite. 
Am evitat folosirea JPA ca urmare a constrangerilor cerintei proiectului.

Baza de date construita prin acest model, furnizeaza informatii privind functionarea unui magazin de electronice, cu tot ce inseamna posibilitatea de a gestiona clienti existenti si clienti noi, precum adaugarea de comenzi noi aferente clientilor. O comanda are o factura si o modalitate de plata asignata. Comanda poate avea multiple produse, iar un produs la randul sau, poate avea o categorie din care face parte, precum si o multitudine de inregistrari ale preturilor anterioare.

Pentru realizarea distribuirii, am folosit doua baze de date Oracle pe acelasi server. Prima baza este cea la care se conecteaza aplicatia noastra. Pe aceasta baza am creat tabele precum CLIENT_FIZIC, COMANDA_F, FACTURA_F, PRODUS_F, ISTORIC_PRET si view-uri la care are acces aplicatia, precum V_CLIENT, V_COMANDA, V_FACTURA, V_PRODUS, V_ISTORIC_PRET. 

Pe a doua baza am creat tabelele fragmentate orizontal, in oglinda,  CLIENT_JURIDIC, COMANDA_J, FACTURA_J, PRODUS_J, ISTORIC_PRET.

Tabela ISTORIC_PRET este cea pe care am stabilit fragmentarea verticala, atributele ISTORIC_PRET_ID si PRODUS_ID fiind in prima baza de date iar in a doua baza avem ISTORIC_PRET_ID, DATA si PRET.

Pentru tabelele CATEGORIE si MODALITATE_PLATA, deoarece nu aveau sens sa fie  fragmentate, am folosit replicarea, creand view-uri materializabile V_MAT_CATEGORIE si V_MAT_MODALITATE_PLATA pe ambele baze de date.
