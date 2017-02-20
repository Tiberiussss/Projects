                    Specificatii proiect C++

                    Stackoverflow la consola

     Sa se implementeze o aplica?ie consola care sa permita interac?iunea unei comunita?i de
utilizatori în vederea rezolvarii de probleme.
     Aplica?ia implementeaza offline func?iile platformei online http://stackoverflow.com/. Se poate
imagina un terminal neconectat la Internet pe care utilizatorii îl folosesc asincron. Aplica?ia
trebuie sa poata fi utilizata offline pentru primele faze ale proiectului.
     Pentru ultima faza a proiectului se va pune la dispozi?ie un server si un client C++ prin care pot fi
primite întrebari ?i se pot da raspunsuri. În aceasta faza aplica?ie consola este folosita de catre
un singur utilizator activ (se autentifica la pornirea aplica?iei).
Componente obligatorii ce trebuie abstractizate ?i implementate prin clase:

1. Conturi Utilizatori; aplica?ia trebuie sa permita gestiunea unor tipuri diferite de utilizatori
(administrator, moderator subiect, utilizator obi?nuit);

2. Meniul aplica?iei consola; navigarea în aplica?ia consola se face prin mesaje afi?ate pe ecran;
alegerea unei op?iuni se face natural (scriu text in consola) sau prin indicarea op?iunii (cod
numeric, etc)

3. Subiecte/Probleme discutate; aplica?ia trebuie sa permita gestiunea unor tipuri diferite de
subiecte de discu?ie, clasificate în func?ie de domeniul in care se încadreaza problema (C++,
Java, .NET, etc); fiecare subiect de discu?ie are asociate raspunsuri de la diferi?i utilizatori; un
utilizator poate da un singur raspuns pe care îl poate modifica; în momentul în care autorul
subiectului/problemei marcheaza raspunsul corect, discu?ia se considera finalizata ?i nu mai
sunt permise alte modificari/interven?ii; prin op?iunile aplica?iei utilizatorii pot filtra discu?iile
dupa categorie, dupa cuvinte cheie din titlu, dupa data, etc.

4. Clase de utilizator; în func?ie de raspunsurile date ?i de corectitudinea lor, utilizatorii sunt
clasifica?i pe diferite categorii; astfel se implementeaza un sistem de bonificare a participarii
active.

Pot fi identificate ?i alte entita?i care sa permita implementare solu?iei.
Pentru a salva datele fiecarei sesiuni de lucru, se vor utiliza fi?iere binare sau text care sa stocheze
aceste entita?i. 