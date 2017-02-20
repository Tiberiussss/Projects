#include<vector>
#include<iostream>
#include<stdio.h>
#include<string.h>
#include<fstream>
using namespace std;

class ContUtilizator
{  protected:

    int id;
    char *nume;
    float varsta;
    char domeniuActivitate[30];
    char sex;
    int nrLocuriMunca;
    char **locuriMunca;
    int telefon[10];


public:
    ContUtilizator()
    {   id=0;
        nume=new char[strlen("Anonim")+1];
        strcpy(nume, "Anonim");
        varsta=0;
        strcpy(domeniuActivitate, "Necunoscut");
        sex='M';
        nrLocuriMunca=1;
        locuriMunca=new char*[nrLocuriMunca];
        locuriMunca[0]=new char[strlen("Necunoscut")+1];
        strcpy(locuriMunca[0], "Necunoscut");
        for(int i=0;i<10;i++)
            telefon[i]=0;
    }





    ContUtilizator(int cod, char* n, float v, char da[30], char s, int nr,
                    char ** l, int t[10])
    {   id=cod;
        nume=new char[strlen(n)+1];
        strcpy(nume, n);
        varsta=v;
        strcpy(domeniuActivitate, da);
        sex=s;
        nrLocuriMunca=nr;
        locuriMunca=new char*[nrLocuriMunca];
        for(int i=0;i<nrLocuriMunca;i++)
       {
           locuriMunca[i]=new char[strlen(l[i])+1];
           strcpy(locuriMunca[i], l[i]);
        }
        for(int i=0;i<10;i++)
            telefon[i]=t[i];
    }





    ~ContUtilizator()
    {
        delete[] nume;
        for(int i=0;i<nrLocuriMunca;i++)
            delete[] locuriMunca[i];
        delete[] locuriMunca;
    }




     int getId()
     {return id;}

     void setVarsta(int v)
    {
        if(v>=0)
          varsta=v;
    }

    int getVarsta()
    {return varsta;}

    void setNume(char *n)
    {    if(nume!=NULL)
        {delete[] nume;
        nume=new char[strlen(n)+1];
        strcpy(nume,n);}
    }

    char* getNume()
    {return nume;}

    void setDomeniu(char da[30])
    {   if(domeniuActivitate!=NULL)
        strcpy(domeniuActivitate, da);}

    char* getDomeniu()
    {return domeniuActivitate;}

    void setSex(char t)
    {sex=t;}

    char getSex()
    {return sex;}

     void setNrLocuriMunca(int nr)
    {
        if(nrLocuriMunca>=1)
            nrLocuriMunca=nr;
    }

    int getNrLocuriMunca()
    {return nrLocuriMunca;}

    void setLocuriMunca(char **l, int nr)
    {
        if(nrLocuriMunca!=nr)
        nrLocuriMunca=nr;
        for(int i=0;i<nrLocuriMunca;i++)
        delete[] locuriMunca[i];
    delete[] locuriMunca;
    locuriMunca=new char*[nrLocuriMunca+1];
    for(int i=0;i<nrLocuriMunca;i++)
        {locuriMunca[i]=new char[strlen(l[i])+1];
    strcpy(locuriMunca[i], l[i]);}
    }

    char * getLocuriMunca(int i)
    {
            return locuriMunca[i];
    }

    void setTelefon(int t[10])
    {
        for(int i=0;i<10;i++)
            telefon[i]=t[i];
    }

    int getTelefon(int i)
    {
        return telefon[i];
    }





    ContUtilizator(ContUtilizator &u)
    {   id=u.id;
        nume=new char[strlen(u.nume)+1];
        strcpy(nume, u.nume);
        varsta=u.varsta;
        strcpy(domeniuActivitate, u.domeniuActivitate);
        sex=u.sex;
        nrLocuriMunca=u.nrLocuriMunca;
        locuriMunca=new char*[nrLocuriMunca];
        for(int i=0;i<nrLocuriMunca;i++)
       {
           locuriMunca[i]=new char[strlen(u.locuriMunca[i])+1];
           strcpy(locuriMunca[i], u.locuriMunca[i]);
        }
        for(int i=0;i<10;i++)
            telefon[i]=u.telefon[i];
    }





    void operator = (ContUtilizator u)
    {
        id=u.id;
        delete[] nume;
        nume=new char[strlen(u.nume)+1];
        strcpy(nume, u.nume);
        varsta=u.varsta;
        strcpy(domeniuActivitate, u.domeniuActivitate);
        sex=u.sex;
        nrLocuriMunca=u.nrLocuriMunca;
        for(int i=0;i<nrLocuriMunca;i++)
            delete[] locuriMunca[i];
        delete[] locuriMunca;
        locuriMunca=new char*[nrLocuriMunca];
        for(int i=0;i<nrLocuriMunca;i++)
       {
           locuriMunca[i]=new char[strlen(u.locuriMunca[i])+1];
           strcpy(locuriMunca[i], u.locuriMunca[i]);
        }
        for(int i=0;i<10;i++)
            telefon[i]=u.telefon[i];
    }





    friend ofstream & operator<< (ofstream& iesire, ContUtilizator &u)
    {
        iesire<<"Utilizatorul "<<u.nume<<"cu id-ul "<<u.id<<", varsta "<<u.varsta;
              iesire<<", domeniu de activitate "<<u.domeniuActivitate;
              iesire<<", sex ";
              if(u.sex=='M')
                iesire<<"masculin"; else iesire<<"feminin";
              iesire<<" si are "<<u.nrLocuriMunca;
              iesire<<" locuri de munca:"<<endl;

        for(int i=0;i<u.nrLocuriMunca;i++)
        {iesire<<u.locuriMunca[i];
            iesire<< endl;}
             iesire<<"si telefonul: ";
            for(int i=0;i<10;i++)
                iesire<<u.telefon[i];
            cout<<endl;
        return iesire;
    }






friend ifstream & operator >> (ifstream & intrare, ContUtilizator &u)
    {   intrare>>u.id;        //getline(char*sir,int n,
                                //char delim=’\n’)
        char buffer[30];
        intrare.get();
        intrare.getline(buffer, 30);
        delete[] u.nume;
        u.nume=new char[strlen(buffer)+1];
        strcpy(u.nume, buffer);
        intrare>>u.varsta;
        intrare>>u.domeniuActivitate;
        intrare>>u.sex;
        intrare>>u.nrLocuriMunca;
        for(int i=0;i<u.nrLocuriMunca;i++)
            delete[] u.locuriMunca[i];
        delete[] u.locuriMunca;
        u.locuriMunca=new char*[u.nrLocuriMunca];
        for(int i=0;i<u.nrLocuriMunca;i++)
           {
               char buffer1[100];
                intrare>>buffer1;
                u.locuriMunca[i]=new char[strlen(buffer1)+2];
                strcpy(u.locuriMunca[i], buffer1);
           }
           for(int i=0;i<10;i++)
            intrare>>u.telefon[i];
        return intrare;
    }





   virtual void afisare1()
    {
        cout<<"Utilizatorul "<<nume<<" cu varsta "<<varsta<<", id "<<id ;
              cout<<", domeniu de activitate "<<domeniuActivitate;
              cout<<", sex ";
              if(sex=='M')
                cout<<"masculin"; else cout<<"feminin";
              cout<<", are "<<nrLocuriMunca;
              cout<<" locuri de munca:"<<endl;

        for(int i=0;i<nrLocuriMunca;i++)
        {cout<<locuriMunca[i];
            cout<< endl;}
            cout<<"si telefonul: ";
            for(int i=0;i<10;i++)
                cout<<telefon[i];
            cout<<endl;
    }



         ContUtilizator operator++() //postfixata
	{
		this->varsta++;
		return *this;

	}

     friend ContUtilizator operator ++(ContUtilizator &co, int)  //varianta prefixata
	{
		ContUtilizator temp = co;
		co.varsta++;
		return temp;
        }

         char* operator[](int index)
	{
		if (index >= 0 && index < this->nrLocuriMunca)
                        return this->locuriMunca[index];
		else
			return NULL;
	}


};

 class ContModerator:public ContUtilizator
 {
     char tipUtilizator;
     char *email;

 public:
    ContModerator(): ContUtilizator()
    {
        email=new char[strlen("necunoscut")+1];
        strcpy(email, "necunoscut");
        tipUtilizator='?';
    }





     ContModerator(int cod, char* n, float v, char da[30], char s, int nr,
                    char ** l, int t[10], char *e, char tu):ContUtilizator(cod, n, v,da, s, nr,l, t)
                    {
                        email=new char[strlen(e)+1];
                        strcpy(email, e);
                        tipUtilizator=tu;
                    }





    ContModerator(ContModerator &cm):ContUtilizator(cm)
    {
        email=new char[strlen(cm.email)+1];
        strcpy(email, cm.email);
        tipUtilizator=cm.tipUtilizator;
    }





    void operator = (ContModerator cm)
    {
        id=cm.id;
        delete[] nume;
        nume=new char[strlen(cm.nume)+1];
        strcpy(nume, cm.nume);
        varsta=cm.varsta;
        strcpy(domeniuActivitate, cm.domeniuActivitate);
        sex=cm.sex;
        nrLocuriMunca=cm.nrLocuriMunca;
        for(int i=0;i<nrLocuriMunca;i++)
            delete[] locuriMunca[i];
        delete[] locuriMunca;
        locuriMunca=new char*[nrLocuriMunca];
        for(int i=0;i<nrLocuriMunca;i++)
       {
           locuriMunca[i]=new char[strlen(cm.locuriMunca[i])+1];
           strcpy(locuriMunca[i], cm.locuriMunca[i]);
        }
        for(int i=0;i<10;i++)
            telefon[i]=cm.telefon[i];

        delete[] email;
        email=new char[strlen(cm.email)+1];
        strcpy(email, cm.email);

        tipUtilizator=cm.tipUtilizator;
    }





    ~ContModerator()
    {
        delete[] email;
    }





    virtual void afisare1()
    {
        cout<<"Utilizatorul "<<nume<<" cu varsta "<<varsta<<", id "<<id ;
              cout<<", domeniu de activitate "<<domeniuActivitate;
              cout<<", sex ";
              if(sex=='M')
                cout<<"masculin"; else cout<<"feminin";
              cout<<" si are "<<nrLocuriMunca;
              cout<<" locuri de munca:"<<endl;

        for(int i=0;i<nrLocuriMunca;i++)
        {cout<<locuriMunca[i];
            cout<< endl;}
            cout<<"telefonul ";
            for(int i=0;i<10;i++)
                cout<<telefon[i];
            cout<<endl;
            cout<<"tipul utilizatorului ";
            if(tipUtilizator=='m')
                cout<<"moderator"<<endl;
            cout<<"si emailul ";
            cout<<email;

    }




    friend ifstream &operator >> (ifstream &intrare, ContModerator &m)
    {
       intrare>>m.id;
       char buffer[30];
       intrare.get();
       intrare.getline(buffer,30);
       delete[] m.nume;
       m.nume=new char[strlen(buffer)+1];
       strcpy(m.nume, buffer);
       intrare>>m.varsta;
       intrare>>m.domeniuActivitate;
        intrare>>m.sex;
        intrare>>m.nrLocuriMunca;
        for(int i=0;i<m.nrLocuriMunca;i++)
            delete[] m.locuriMunca[i];
        delete[] m.locuriMunca;
        m.locuriMunca=new char*[m.nrLocuriMunca];
        for(int i=0;i<m.nrLocuriMunca;i++)
           {
               char buffer1[20];
                intrare>>buffer1;
                m.locuriMunca[i]=new char[strlen(buffer1)+2];
                strcpy(m.locuriMunca[i], buffer1);
           }
           for(int i=0;i<10;i++)
            intrare>>m.telefon[i];
            intrare>>m.tipUtilizator;
            char buffer2[100];
            intrare>>buffer2;
            delete[] m.email;
            m.email=new char[strlen(buffer2)+1];
            strcpy(m.email,buffer2);
            return intrare;
    }

 };

 class ContAdmin:public ContUtilizator
 {
     char * data;       //data la care a devenit admin
     int nrFunctii;
     char ** functii;  //ce functii poate inteplini acesta
     char tipUtilizator;

 public:
    ContAdmin():ContUtilizator()
    {
        data=new char[strlen("01.01.1900")+1];
        strcpy(data, "01.01.1900");
        nrFunctii=1;
        functii=new char*[nrFunctii];
        functii[0]=new char[strlen("niciuna")+1];
        strcpy(functii[0],"niciuna");
        tipUtilizator='a';
    }





    ContAdmin(int cod, char* n, float v, char da[30], char s, int nr,
                    char ** l, int t[10], char* d, int nrf,char **f,char tu):ContUtilizator(cod,n,v,da,s,nr,l,t)
    {
        data=new char[strlen(d)+1];
        strcpy(data, d);
        nrFunctii=nrf;
        functii=new char*[nrFunctii];
        for(int i=0;i<nrFunctii;i++)
        {functii[i]=new char[strlen(f[i])+1];
        strcpy(functii[i],f[i]);}
        tipUtilizator=tu;
    }





    ContAdmin(ContAdmin &a):ContUtilizator(a)
    {
        data=new char[strlen(a.data)+1];
        strcpy(data, a.data);
        nrFunctii=a.nrFunctii;
        functii=new char*[nrFunctii];
        for(int i=0;i<nrFunctii;i++)
        {functii[i]=new char[strlen(a.functii[i])+1];
        strcpy(functii[i],a.functii[i]);}
        tipUtilizator=a.tipUtilizator;
    }





    void operator = (ContAdmin a)
    {
        id=a.id;
        delete[] nume;
        nume=new char[strlen(a.nume)+1];
        strcpy(nume, a.nume);
        varsta=a.varsta;
        strcpy(domeniuActivitate, a.domeniuActivitate);
        sex=a.sex;
        nrLocuriMunca=a.nrLocuriMunca;
        for(int i=0;i<nrLocuriMunca;i++)
            delete[] locuriMunca[i];
        delete[] locuriMunca;
        locuriMunca=new char*[nrLocuriMunca];
        for(int i=0;i<nrLocuriMunca;i++)
       {
           locuriMunca[i]=new char[strlen(a.locuriMunca[i])+1];
           strcpy(locuriMunca[i], a.locuriMunca[i]);
        }
        for(int i=0;i<10;i++)
            telefon[i]=a.telefon[i];

        delete[] data;
        data=new char[strlen(a.data)+1];
        strcpy(data, a.data);
        for(int i=0;i<nrFunctii;i++)
        delete[] functii[i];
        delete[] functii;
        functii=new char*[nrFunctii];
        for(int i=0;i<nrFunctii;i++)
        {
            functii[i]=new char[strlen(a.functii[i])+1];
            strcpy(functii[i], a.functii[i]);
        }
        tipUtilizator=a.tipUtilizator;
    }





     virtual void afisare1()
    {
        cout<<"Utilizatorul "<<nume<<" cu varsta "<<varsta<<", id "<<id ;
              cout<<", domeniu de activitate "<<domeniuActivitate;
              cout<<", sex ";
              if(sex=='M')
                cout<<"masculin"; else cout<<"feminin";
              cout<<" si are "<<nrLocuriMunca;
              cout<<" locuri de munca:"<<endl;

        for(int i=0;i<nrLocuriMunca;i++)
        {cout<<locuriMunca[i];
            cout<< endl;}
            cout<<"telefonul ";
            for(int i=0;i<10;i++)
                cout<<telefon[i];
            cout<<endl;
            cout<<"tipul utilizatorului ";
            if(tipUtilizator=='a')
                cout<<"admin"<<endl;
            cout<<"data de cand acesta are functia de admin ";
            cout<<data<<endl;
            cout<<"si dispune de "<<nrFunctii<<" functii:"<<endl;
            for(int i=0;i<nrFunctii;i++)
                {cout<<functii[i];
                cout<<endl;}


    }





    ~ContAdmin()
    {
        delete[] data;
        for(int i=0;i<nrFunctii;i++)
            delete[] functii[i];
        delete[] functii;
    }





    friend ifstream & operator >> (ifstream & intrare, ContAdmin &a)
    {   intrare>>a.id;        //getline(char*sir,int n,
                                //char delim=’\n’)
        char buffer[30];
        intrare.get();
        intrare.getline(buffer, 30);
        delete[] a.nume;
        a.nume=new char[strlen(buffer)+1];
        strcpy(a.nume, buffer);
        intrare>>a.varsta;
        intrare>>a.domeniuActivitate;
        intrare>>a.sex;
        intrare>>a.nrLocuriMunca;
        for(int i=0;i<a.nrLocuriMunca;i++)
            delete[] a.locuriMunca[i];
        delete[] a.locuriMunca;
        a.locuriMunca=new char*[a.nrLocuriMunca];
        for(int i=0;i<a.nrLocuriMunca;i++)
           {
               char buffer1[20];
                intrare>>buffer1;
                a.locuriMunca[i]=new char[strlen(buffer1)+2];
                strcpy(a.locuriMunca[i], buffer1);
           }

           for(int i=0;i<10;i++)
            intrare>>a.telefon[i];
            intrare>>buffer;
            delete[] a.data;
            a.data=new char[strlen(buffer)+1];
            strcpy(a.data, buffer);
            intrare>>a.nrFunctii;
            for(int i=0;i<a.nrFunctii;i++)
                delete[] a.functii[i];
            delete[] a.functii;
            char buffer5[100];
            a.functii=new char*[a.nrFunctii];
            for(int i=0;i<a.nrFunctii;i++)
            {
                intrare.get();
                intrare.getline(buffer5,100);
                a.functii[i]=new char[strlen(buffer5)+1];
                strcpy(a.functii[i], buffer5);
            }
            intrare>>a.tipUtilizator;

        return intrare;
    }
 };

 class ContObisnuit: public ContUtilizator
 {protected:
     char *adresa;
     char *stareCivila;
     char *dataNastere;
     char tipUtilizator;

 public:
    ContObisnuit():ContUtilizator()
    {
        adresa=new char[strlen("necunoscuta")+1];
        strcpy(adresa, "necunoscuta");
        stareCivila=new char[strlen("necunoscuta")+1];
        strcpy(stareCivila, "necunoscuta");
        dataNastere=new char[strlen("necunoscuta")+1];
        strcpy(dataNastere, "necunoscuta");
        tipUtilizator='u';
    }





    ContObisnuit(int cod, char* n, float v, char da[30], char s, int nr,
                    char ** l, int t[10], char *a, char*sc, char*dn, char tu):
                        ContUtilizator(cod,n,v,da,s, nr,l, t)
    {
        adresa=new char[strlen(a)+1];
        strcpy(adresa, a);
        stareCivila=new char[strlen(sc)+1];
        strcpy(stareCivila, sc);
        dataNastere=new char[strlen(dn)+1];
        strcpy(dataNastere, dn);
        tipUtilizator=tu;
    }





    ContObisnuit(ContObisnuit &co):ContUtilizator(co)
    {
        adresa=new char[strlen(co.adresa)+1];
        strcpy(adresa, co.adresa);
        stareCivila=new char[strlen(co.stareCivila)+1];
        strcpy(stareCivila, co.stareCivila);
        dataNastere=new char[strlen(co.dataNastere)+1];
        strcpy(dataNastere, co.dataNastere);
        tipUtilizator=co.tipUtilizator;
    }





    void operator = (ContObisnuit co)
    {
        id=co.id;
        delete[] nume;
        nume=new char[strlen(co.nume)+1];
        strcpy(nume, co.nume);
        varsta=co.varsta;
        strcpy(domeniuActivitate, co.domeniuActivitate);
        sex=co.sex;
        nrLocuriMunca=co.nrLocuriMunca;
        for(int i=0;i<nrLocuriMunca;i++)
            delete[] locuriMunca[i];
        delete[] locuriMunca;
        locuriMunca=new char*[nrLocuriMunca];
        for(int i=0;i<nrLocuriMunca;i++)
       {
           locuriMunca[i]=new char[strlen(co.locuriMunca[i])+1];
           strcpy(locuriMunca[i], co.locuriMunca[i]);
        }
        for(int i=0;i<10;i++)
            telefon[i]=co.telefon[i];

            delete[] adresa;
            adresa=new char[strlen(co.adresa)+1];
        strcpy(adresa, co.adresa);
        delete[] stareCivila;
        stareCivila=new char[strlen(co.stareCivila)+1];
        strcpy(stareCivila, co.stareCivila);
        delete[] dataNastere;
        dataNastere=new char[strlen(co.dataNastere)+1];
        strcpy(dataNastere, co.dataNastere);
        tipUtilizator=co.tipUtilizator;
    }





    ~ContObisnuit()
    {
        delete[] adresa;
        delete[] stareCivila;
        delete[] dataNastere;
    }





    virtual void afisare1()
    {
        cout<<"Utilizatorul "<<nume<<" cu varsta "<<varsta<<", id "<<id ;
              cout<<", domeniu de activitate "<<domeniuActivitate;
              cout<<", sex ";
              if(sex=='M')
                cout<<"masculin"; else cout<<"feminin";
              cout<<" si are "<<nrLocuriMunca;
              cout<<" locuri de munca:"<<endl;

        for(int i=0;i<nrLocuriMunca;i++)
        {cout<<locuriMunca[i];
            cout<< endl;}
            cout<<"telefonul ";
            for(int i=0;i<10;i++)
                cout<<telefon[i];
            cout<<endl;
            cout<<"tipul utilizatorului ";
            if(tipUtilizator=='o')
                cout<<" - utilizator obisnuit"<<endl;
           cout<<"data nasterii ";
            cout<<dataNastere<<endl;
            cout<<"adresa "<<adresa<<endl;
            cout<<"si starea civila "<<stareCivila<<endl;
    }





    friend ifstream & operator >> (ifstream & intrare, ContObisnuit &o)
    {
        intrare>>o.id;
        char buffer[30];
        intrare.get();
        intrare.getline(buffer, 30);
        delete[] o.nume;
        o.nume=new char[strlen(buffer)+1];
        strcpy(o.nume, buffer);
        intrare>>o.varsta;
        intrare>>o.domeniuActivitate;
        intrare>>o.sex;
        intrare>>o.nrLocuriMunca;
        for(int i=0;i<o.nrLocuriMunca;i++)
            delete[] o.locuriMunca[i];
        delete[] o.locuriMunca;
        o.locuriMunca=new char*[o.nrLocuriMunca];
        for(int i=0;i<o.nrLocuriMunca;i++)
           {
               char buffer1[20];
                intrare>>buffer1;
                o.locuriMunca[i]=new char[strlen(buffer1)+2];
                strcpy(o.locuriMunca[i], buffer1);
           }
           for(int i=0;i<10;i++)
            intrare>>o.telefon[i];
        char buffer2[80];
        delete[] o.adresa;
        intrare.get();
        intrare.getline(buffer2,80);

        o.adresa=new char[strlen(buffer2)+1];
        strcpy(o.adresa, buffer2);
        delete[] o.dataNastere;
        char buffer3[20];
        intrare>>buffer3;
        o.dataNastere=new char[strlen(buffer3)+1];
        strcpy(o.dataNastere, buffer3);
        delete[] o.stareCivila;
        intrare>>buffer;
        o.stareCivila=new char[strlen(buffer)+1];
        strcpy(o.stareCivila, buffer);
        intrare>>o.tipUtilizator;
        return intrare;
    }

 };

 class Meniu
{
    int id;
    char * numeCont;
     char *parola;





public:
    Meniu()
    {   id=0;
        numeCont=new char[strlen("utilizator")+1];
        strcpy(numeCont,"utilizator");
        parola=new char[strlen("0000")+1];
        strcpy(parola, "0000");
    }





    Meniu(int cod, char*nn, char *p)
    {   id=cod;
        numeCont=new char[strlen(nn)+1];
        strcpy(numeCont, nn);
        parola=new char[strlen(p)+1];
        strcpy(parola,p);
    }






    ~Meniu()
    {
        delete[] numeCont;
        delete[] parola;
    }






    void afisare2()
    {
        cout<<"Utilizatorul are numele de cont "<<numeCont<<endl;

    }





    void setNumeCont(char *nu)
    {
        if(numeCont!=NULL)
        {
            delete[] numeCont;
            numeCont=new char[strlen(nu)+1];
            strcpy(numeCont,nu);
        }
    }

    char * getNumeCont()
    {
        return numeCont;
    }

    void setParola( char *pn)
    {    if(parola=="0000")
        {delete[] parola;
        parola=new char[strlen(pn)+1];
        strcpy(parola, pn);}
    }

     char * getParola()
    {
        return parola;
    }

    int getId()
    {
        return id;
    }






    Meniu(Meniu &m)
    {   id=m.id;
        numeCont=new char[strlen(m.numeCont)+1];
        strcpy(numeCont, m.numeCont);
        parola=new char[strlen(m.parola)+1];
        strcpy(parola, m.parola);
    }





    void operator = (Meniu m)
    {
        id=m.id;
        delete[] numeCont;
        numeCont=new char[strlen(m.numeCont)+1];
        strcpy(numeCont, m.numeCont);
        delete[] parola;
        parola=new char[strlen(m.parola)+1];
        strcpy(parola, m.parola);
    }





    friend ostream & operator <<(ostream& iesire2, Meniu &m)
    {
        iesire2<<"Utilizatorul are numele de cont "<<m.numeCont<<endl;
        iesire2<<"parola "<<m.parola<< " id "<<m.id<<endl;
        return iesire2;
    }





    friend istream& operator >>(istream& in, Meniu &m)
    {

        delete[] m.numeCont;
        char buffer[20];
        in>>buffer;
        m.numeCont=new char[strlen(buffer)+1];
        strcpy(m.numeCont, buffer);
        delete[] m.parola;
        char buffer2[20];
        in>>buffer2;
        m.parola=new char[strlen(buffer2)+1];
        strcpy(m.parola, buffer2);
        in>>m.id;
        return in;
    }
};

class Intrebari
{  protected:

    int idi;
    int nrIntrebariP;
    char ** intrebariPropuse;
    int *dificultate;          //fiecare intrebare va primi o nota de la
                               //1 la 5, in functie de dificultatea intrebarii




public:
    Intrebari()
    {    idi=0;
        nrIntrebariP=1;
        intrebariPropuse=new char*[nrIntrebariP+1];
        intrebariPropuse[0]=new char[strlen("Nu s-a introdus intrebarea")+1];
        strcpy(intrebariPropuse[0],"Nu s-a introdus intrebarea");
        dificultate=new int[nrIntrebariP];
        dificultate[0]=1;
    }





     Intrebari(int cod,int nri, char** ip, int *dif)
     {   idi=cod;
         nrIntrebariP=nri;
         intrebariPropuse=new char*[nrIntrebariP+1];
         for(int i=0;i<nrIntrebariP;i++)
         {
             intrebariPropuse[i]=new char[strlen(ip[i])+1];
             strcpy(intrebariPropuse[i], ip[i]);
         }
         dificultate=new int[nrIntrebariP];
         for(int i=0;i<nrIntrebariP;i++)
            dificultate[i]=dif[i];
     }







     ~Intrebari()
     {
          for(int i=0;i<nrIntrebariP;i++)
            delete[] intrebariPropuse[i];
         delete[] intrebariPropuse;
         delete[] dificultate;
     }






     virtual void afisare3()
     {
         cout<<"Exista urmatoarele "<<nrIntrebariP<<" intrebari:"<<endl;
         for(int i=0;i<nrIntrebariP;i++)
         {
             //puts(intrebariPropuse[i]);
             cout<<intrebariPropuse[i]<<endl;
             cout<<" cu dificultatea "<<dificultate[i]<<endl;
         }
         //cout<<"id "<<idi<<endl;
     }






     void setIntrebariPropuse (char ** intp, int nip)
     {
         if(nip!=nrIntrebariP)
            nrIntrebariP=nip;
         for(int i=0;i<nrIntrebariP;i++)
            delete[] intrebariPropuse[i];
         delete intrebariPropuse;
         intrebariPropuse=new char*[nrIntrebariP+1];
         for(int i=0;i<nrIntrebariP;i++)
         {
             intrebariPropuse[i]=new char[strlen(intp[i])+1];
             strcpy(intrebariPropuse[i], intp[i]);
         }
     }

     char* getIntrebariPropuse(int i)
     {
         return intrebariPropuse[i];
     }

     void setDificultate(char*df, int nip)
     {
         if (nip!=nrIntrebariP)
            nrIntrebariP=nip;
         delete[] dificultate;
         dificultate=new int[nrIntrebariP];
         for(int i=0;i<nrIntrebariP;i++)
            dificultate[i]=df[i];
     }

     int  getDificultate(int i)
     {
         return dificultate[i];
     }
     int getIdi()
     {
         return idi;
     }
     void setIdi(int i)
     {
         idi=i;
     }
     int getNrIntrebariP()
     {
         return nrIntrebariP;
     }
     void setNrIntrebariP(int nr)
     {
         nrIntrebariP=nr;
     }







    Intrebari(Intrebari &i)
     {    idi=i.idi;
         nrIntrebariP=i.nrIntrebariP;
         intrebariPropuse=new char*[nrIntrebariP+1];
         for(int j=0;j<nrIntrebariP;j++)
         {
             intrebariPropuse[j]=new char[strlen(i.intrebariPropuse[j])+1];
             strcpy(intrebariPropuse[j], i.intrebariPropuse[j]);
         }
         dificultate=new int[nrIntrebariP];
         for(int j=0;j<nrIntrebariP;j++)
            dificultate[j]=i.dificultate[j];
     }





     void operator = (Intrebari i)
     {    idi=i.idi;
         nrIntrebariP=i.nrIntrebariP;
         for(int j=0;j<nrIntrebariP;j++)
            delete[] intrebariPropuse[j];
         delete[] intrebariPropuse;
         intrebariPropuse=new char*[nrIntrebariP+1];
         for(int j=0;j<nrIntrebariP;j++)
         {
             intrebariPropuse[j]=new char[strlen(i.intrebariPropuse[j])+1];
             strcpy(intrebariPropuse[j], i.intrebariPropuse[j]);
         }
         delete[] dificultate;
         dificultate=new int[nrIntrebariP];
         for(int j=0;j<nrIntrebariP;j++)
            dificultate[j]=i.dificultate[j];

     }





     friend ofstream& operator <<(ofstream& iesire3, Intrebari &i)
     {
          iesire3<<"Exista urmatoarele ";
          iesire3<<i.nrIntrebariP;
          iesire3<<" intrebari:";
          iesire3<<endl;
         for(int j=0;j<i.nrIntrebariP;j++)
         {
             puts(i.intrebariPropuse[j]);
             iesire3<<" cu dificultatea ";
             iesire3<<i.dificultate[j];
             iesire3<<endl;
         }
         return iesire3;
     }






     /*friend ifstream& operator >>(ifstream& intrare3, Intrebari &i )
     {   intrare3>>i.idi;
         intrare3>>i.nrIntrebariP;
         for(int j=0;j<i.nrIntrebariP;j++)
            delete[] i.intrebariPropuse[j];
         delete[] i.intrebariPropuse;
         char buffer[200];
         i.intrebariPropuse=new char*[i.nrIntrebariP];
         for(int j=0;j<i.nrIntrebariP;j++)
            {
                intrare3.get();
               intrare3.getline(buffer, 200);
               //intrare3.get(buffer,100);

            i.intrebariPropuse[j]=new char[strlen(buffer)+1];
            strcpy(i.intrebariPropuse[j], buffer);}
                delete[] i.dificultate;
                i.dificultate=new int[i.nrIntrebariP];
          for(int j=0;j<i.nrIntrebariP;j++)
            intrare3>>i.dificultate[j];

            return intrare3;
     }*/



     friend ifstream & operator >>(ifstream & intr, Intrebari &i)
     {
          intr>>i.idi;
          intr>>i.nrIntrebariP;
         // for(int j=0;j<i.nrIntrebariP;j++)
           // delete[] i.intrebariPropuse[j];
         // delete[] i.intrebariPropuse;
          char buffer[500];
          i.intrebariPropuse=new char*[i.nrIntrebariP];
          for(int j=0;j<i.nrIntrebariP;j++)
          {
              intr.get();
              intr.getline(buffer,500);
              i.intrebariPropuse[j]=new char[strlen(buffer)+1];
              strcpy(i.intrebariPropuse[j], buffer);
          }
          //delete[] i.dificultate;
          i.dificultate=new int[i.nrIntrebariP];
          for(int j=0;j<i.nrIntrebariP;j++)
            intr>>i.dificultate[j];

          return intr;

     }





     bool operator ==(Intrebari i)
	{
		if (this->idi == i.idi)
			return true;
		else return false;
	}


	void afisaree(int i)
	{
	    char buffer[100];
	    for(int j=0;j<this->nrIntrebariP;i++)
	    {cout<<this->intrebariPropuse[i];
	    cin>>buffer;}

	}
};

class Raspunsuri:public ContObisnuit, public Intrebari
{
    int id_r;
    int nrRaspunsuri;
    char ** raspunsuri;

  //  char **formaRaspuns;      //daca raspunsul este unul simplu(alegere varianta)
                                // sau complex (raspuns liber)
   // int varianteRaspuns[30];    //cate variante de raspuns are intrebarea




public:
    Raspunsuri(): ContObisnuit(), Intrebari()
    {   id_r=0;
        nrRaspunsuri=1;
        raspunsuri=new char*[nrRaspunsuri+1];
        raspunsuri[0]=new char[strlen("Nu exista raspuns inca")+1];
        strcpy(raspunsuri[0],"Nu exista raspuns inca");
       // formaRaspuns=new char*[nrRaspunsuri+1];
        //formaRaspuns[0]=new char[strlen("simpla")+1];
      //  strcpy(formaRaspuns[0], "simpla");
       // varianteRaspuns[0]=1;
    }





    Raspunsuri( int nrr, char** rasp, int coddd,
                int cod, char* n, float v, char da[30], char s, int nr,
                    char ** l, int t[10], char *a, char*sc, char*dn, char tu,
                    int codd,int nri, char** ip, int *dif):

                   ContObisnuit(cod, n, v, da,  s, nr,
                     l,  t, a, sc, dn, tu),
                     Intrebari(codd,nri, ip,dif)
                       // ContUtilizator(cod,n,v,da,s, nr,l, t)

    {   id_r=coddd;
        nrRaspunsuri=nrr;
        raspunsuri=new char*[nrRaspunsuri+1];
        for(int i=0;i<nrRaspunsuri;i++)
        {raspunsuri[i]=new char[strlen(rasp[i])+1];
        strcpy(raspunsuri[i],rasp[i]);}
       // formaRaspuns=new char*[nrRaspunsuri+1];
        //for(int i=0;i<nrRaspunsuri;i++)
        //{formaRaspuns[i]=new char[strlen(fr[i])+1];
        //strcpy(formaRaspuns[i], fr[i]);}
        //for(int i=0;i<nrRaspunsuri;i++)
        //varianteRaspuns[i]=vr[i];
    }




    ~Raspunsuri()
    {    for(int i=0;i<nrRaspunsuri;i++)
         delete[] raspunsuri[i];
        delete[] raspunsuri;

    }





    void afisare4()
    {   cout<<"Utilizatorul "<<nume<<" cu varsta "<<varsta;
              cout<<", domeniu de activitate "<<domeniuActivitate;
              cout<<", sex ";
              if(sex=='M')
                cout<<"masculin"; else cout<<"feminin";
              cout<<", are "<<nrLocuriMunca;
              cout<<" locuri de munca:"<<endl;

        for(int i=0;i<nrLocuriMunca;i++)
        {cout<<locuriMunca[i];
            cout<< endl;}
            cout<<", telefonul: ";
            for(int i=0;i<10;i++)
                cout<<telefon[i];
                cout<<endl;
    cout<<" De asemenea, are adresa "<<adresa<<", stare civila "<<stareCivila
            <<", data nasterii "<<dataNastere<<" si tipul utilizatorului "<<tipUtilizator;
            cout<<endl;
            cout<<"Exista "<<nrIntrebariP<<" intrebari, iar acestea sunt:"<<endl;
        for(int i=0;i<nrIntrebariP;i++)
                {puts(intrebariPropuse[i]);
                cout<<endl;}
        cout<<"si urmatoarele raspunsuri: "<<endl;
        for(int i=0;i<nrRaspunsuri;i++)
            {
                puts(raspunsuri[i]);

            }

    }




    void setRaspunsuri(int numar, char **raspun)
    {
        if(nrRaspunsuri!=numar)
            nrRaspunsuri=numar;
        for(int i=0;i<nrRaspunsuri;i++)
            delete[] raspunsuri[i];
        delete[] raspunsuri;
        raspunsuri=new char*[nrRaspunsuri+1];
        for(int i=0;i<nrRaspunsuri;i++)
        {
            raspunsuri[i]=new char[strlen(raspun[i])+1];
            strcpy(raspunsuri[i], raspun[i]);
        }
    }

    char* getRaspunsuri(int i)
    {
        return raspunsuri[i];
    }

   /* void setFormaRaspunsuri(int numar, char **fraspun)
    {
        if(nrRaspunsuri!=numar)
            nrRaspunsuri=numar;
        for(int i=0;i<nrRaspunsuri;i++)
            delete[] formaRaspuns[i];
        delete[] formaRaspuns;
        formaRaspuns=new char*[nrRaspunsuri+1];
        for(int i=0;i<nrRaspunsuri;i++)
        {
            formaRaspuns[i]=new char[strlen(fraspun[i])+1];
            strcpy(formaRaspuns[i], fraspun[i]);
        }
    }

    char* gerFormaRaspunsuri(int i)
    {
        return formaRaspuns[i];
    }

    void setVarianteRaspuns (int numar, int var[30])
    {
        if(nrRaspunsuri!=numar)
            nrRaspunsuri=numar;
        for(int i=0;i<nrRaspunsuri;i++)
            varianteRaspuns[i]=var[i];
    }

    int getVarianteRaspuns ()
    {
        return varianteRaspuns[30];
    }
*/

     int getId_r()
     {
         return id_r;
     }

     int getNrRaspunsuri()
     {
         return nrRaspunsuri;
     }



    Raspunsuri(Raspunsuri &r): ContObisnuit(r), Intrebari(r)
    {    id_r=r.id_r;
        nrRaspunsuri=r.nrRaspunsuri;
        raspunsuri=new char*[nrRaspunsuri+1];
        for(int i=0;i<nrRaspunsuri;i++)
        {raspunsuri[i]=new char[strlen(r.raspunsuri[i])+1];
        strcpy(raspunsuri[i],r.raspunsuri[i]);}
       // formaRaspuns=new char*[nrRaspunsuri+1];
        //for(int i=0;i<nrRaspunsuri;i++)
        //{formaRaspuns[i]=new char[strlen(r.formaRaspuns[i])+1];
        //strcpy(formaRaspuns[i], r.formaRaspuns[i]);}
        //for(int i=0;i<nrRaspunsuri;i++)
        //varianteRaspuns[i]=r.varianteRaspuns[i];
    }






    void operator = (Raspunsuri r)
    {   id_r=r.id_r;
        nrRaspunsuri=r.nrRaspunsuri;
        for(int i=0;i<nrRaspunsuri;i++)
            delete[] raspunsuri[i];
        delete[] raspunsuri;
        raspunsuri=new char*[nrRaspunsuri+1];
        for(int i=0;i<nrRaspunsuri;i++)
        {
            raspunsuri[i]=new char[strlen(r.raspunsuri[i])+1];
            strcpy(raspunsuri[i], r.raspunsuri[i]);
        }
       /* for(int i=0;i<nrRaspunsuri;i++)
            delete[] formaRaspuns[i];
        delete[] formaRaspuns;
        formaRaspuns=new char*[nrRaspunsuri+1];
        for(int i=0;i<nrRaspunsuri;i++)
        {
            formaRaspuns[i]=new char[strlen(r.formaRaspuns[i])+1];
            strcpy(formaRaspuns[i], r.formaRaspuns[i]);
        }
         for(int i=0;i<nrRaspunsuri;i++)
            varianteRaspuns[i]=r.varianteRaspuns[i];*/


            delete[] nume;
        nume=new char[strlen(r.nume)+1];
        strcpy(nume, r.nume);
        varsta=r.varsta;
        strcpy(domeniuActivitate, r.domeniuActivitate);
        sex=r.sex;
        nrLocuriMunca=r.nrLocuriMunca;
        for(int i=0;i<nrLocuriMunca;i++)
            delete[] locuriMunca[i];
        delete[] locuriMunca;
        locuriMunca=new char*[nrLocuriMunca];
        for(int i=0;i<nrLocuriMunca;i++)
       {
           locuriMunca[i]=new char[strlen(r.locuriMunca[i])+1];
           strcpy(locuriMunca[i], r.locuriMunca[i]);
        }
        for(int i=0;i<10;i++)
            telefon[i]=r.telefon[i];

            delete[] adresa;
            adresa=new char[strlen(r.adresa)+1];
        strcpy(adresa, r.adresa);
        delete[] stareCivila;
        stareCivila=new char[strlen(r.stareCivila)+1];
        strcpy(stareCivila, r.stareCivila);
        delete[] dataNastere;
        dataNastere=new char[strlen(r.dataNastere)+1];
        strcpy(dataNastere, r.dataNastere);
        tipUtilizator=r.tipUtilizator;




    nrIntrebariP=r.nrIntrebariP;
         for(int j=0;j<nrIntrebariP;j++)
            delete[] intrebariPropuse[j];
         delete[] intrebariPropuse;
         intrebariPropuse=new char*[nrIntrebariP+1];
         for(int j=0;j<nrIntrebariP;j++)
         {
             intrebariPropuse[j]=new char[strlen(r.intrebariPropuse[j])+1];
             strcpy(intrebariPropuse[j], r.intrebariPropuse[j]);
         }
         delete[] dificultate;
         dificultate=new int[nrIntrebariP];
         for(int j=0;j<nrIntrebariP;j++)
            dificultate[j]=r.dificultate[j];

     }





  /*  friend ofstream & operator<< (ofstream& iesire4, Raspunsuri &r)
    {   iesire4<<"Utilizatorul are adresa "<<r.adresa<<", stare civila "<<r.stareCivila
            <<", data nasterii "<<r.dataNastere<<" si tipul utilizatorului "<<r.tipUtilizator;
            iesire4<<endl;
            iesire4<<"Exista "<<r.nrIntrebariP<<" intrebari, iar acestea sunt:"<<endl;
        for(int i=0;i<r.nrIntrebariP;i++)
                {puts(r.intrebariPropuse[i]);
                cout<<endl;}
        iesire4<<"si urmatoarele raspunsuri: "<<endl;
        for(int i=0;i<r.nrRaspunsuri;i++)
            {
                puts(r.raspunsuri[i]);
               // iesire4<<" si este o intrebare "<<r.formaRaspuns[i];
                 //  iesire4 <<" cu "<<r.varianteRaspuns[i]<<" variante de raspuns"<<endl;
            }
   return iesire4;
    }*/






    friend ofstream & operator<< (ofstream& iesire, Raspunsuri &r)
    {
        iesire<<r.nume<<endl;
        iesire<<r.id<<endl;
        for(int i=0;i<r.nrRaspunsuri;i++)
            iesire<<r.raspunsuri[i]<<endl;
    }





      friend istream & operator >> (istream & intrare, Raspunsuri &r)
      {
          //intrare>>r.id;
        char buffer[30];
        intrare.get();
        intrare.getline(buffer, 30);
        delete[] r.nume;
        r.nume=new char[strlen(buffer)+1];
        strcpy(r.nume, buffer);
        /*intrare>>r.varsta;
        intrare>>r.domeniuActivitate;
        intrare>>r.sex;
        intrare>>r.nrLocuriMunca;
        for(int i=0;i<r.nrLocuriMunca;i++)
            delete[] r.locuriMunca[i];
        delete[] r.locuriMunca;
        r.locuriMunca=new char*[r.nrLocuriMunca];
        for(int i=0;i<r.nrLocuriMunca;i++)
           {
               char buffer1[20];
                intrare>>buffer1;
                r.locuriMunca[i]=new char[strlen(buffer1)+2];
                strcpy(r.locuriMunca[i], buffer1);
           }
           for(int i=0;i<10;i++)
            intrare>>r.telefon[i];
        char buffer2[80];
        intrare.get();
        intrare.getline(buffer2,70);
        delete[] r.adresa;

        r.adresa=new char[strlen(buffer2)+1];
        strcpy(r.adresa, buffer2);
        delete[] r.dataNastere;
        char buffer3[20];
        intrare>>buffer3;
        r.dataNastere=new char[strlen(buffer3)+1];
        strcpy(r.dataNastere, buffer3);
        delete[] r.stareCivila;
        intrare>>buffer;
        r.stareCivila=new char[strlen(buffer)+1];
        strcpy(r.stareCivila, buffer);
        intrare>>r.tipUtilizator;
        return intrare;*/

        intrare>>r.idi;
        /* intrare>>r.nrIntrebariP;
         for(int j=0;j<r.nrIntrebariP;j++)
            delete[] r.intrebariPropuse[j];
         delete[] r.intrebariPropuse;
         char buffer1[200];
         r.intrebariPropuse=new char*[r.nrIntrebariP];
         for(int j=0;j<r.nrIntrebariP;j++)
            {
                intrare.get();
                intrare.getline(buffer1, 200);
            r.intrebariPropuse[j]=new char[strlen(buffer1)+1];
            strcpy(r.intrebariPropuse[j], buffer1);}
                delete[] r.dificultate;
                r.dificultate=new int[r.nrIntrebariP];
          for(int j=0;j<r.nrIntrebariP;j++)
            intrare>>r.dificultate[j];*/



          intrare>> r.nrRaspunsuri;
          for(int i=0;i<r.nrRaspunsuri;i++)
            delete[] r.raspunsuri[i];
          delete[] r.raspunsuri;
          r.raspunsuri=new char*[r.nrRaspunsuri];
          char buffer4[200];
          for(int i=0;i<r.nrRaspunsuri;i++)
           {
               intrare.get();
               intrare.getline(buffer4,200);
               r.raspunsuri[i]=new char[strlen(buffer4)+1];
               strcpy(r.raspunsuri[i], buffer4);
           }


            return intrare;
      }
};

template <class T1,class T2> class Clasificare
{
     T1 nrIntrebari;
       int* noteIntrebari;      //se vor acorda note incepand de la 1 la 10 pt fiecare intrebare
    T2 categorii;        //exista 5 categorii: 1-cel mai slab; 5-cel mai bun



public:
    Clasificare()
    {
        nrIntrebari=1;
        noteIntrebari=new int[nrIntrebari];
        noteIntrebari[0]=1;
        categorii=1;
    }



     Clasificare(T1 ni, int* note, T2 c)
    {
        nrIntrebari=ni;
        noteIntrebari=new int[nrIntrebari];
        for(int i=0;i<nrIntrebari;i++)
        noteIntrebari[i]=note[i];
        categorii=c;
    }




    ~Clasificare()
    {
        delete[] noteIntrebari;
    }




    void afisare5()
    {
        cout<<"Utilizatorul a raspuns la "<<nrIntrebari
             <<" intrebari si a primit urmatoarele calificative pt cele "
             <<nrIntrebari<<" note:"<<endl;
             for(int i=0;i<nrIntrebari;i++)
                cout<<noteIntrebari[i]<<" ";
             cout<<endl;
             cout<<"Acesta se claseaza in categoria "<<categorii;
             cout<<endl;
    }





    void setNoteIntrebari(T1 nrNou, int* note)
    {
        if(nrNou!=nrIntrebari)
            nrIntrebari=nrNou;
        delete[] noteIntrebari;
        noteIntrebari=new int[nrIntrebari];
        for(int i=0;i<nrIntrebari;i++)
            noteIntrebari[i]=note[i];
    }

    int * getNoteIntrebari()
    {
        return noteIntrebari;
    }

    T1 getNrIntrebari()
    {
        return nrIntrebari;
    }

    void setCategorii(T2 categ)
    {
        if(categ!=categorii)
            categorii=categ;
    }

    T2 getCategorii()
    {
        return categorii;
    }




    Clasificare(Clasificare &c)
    {
        nrIntrebari=c.nrIntrebari;
        noteIntrebari=new int[nrIntrebari];
        for(int i=0;i<nrIntrebari;i++)
        noteIntrebari[i]=c.noteIntrebari[i];
        categorii=c.categorii;
    }




    void operator = (Clasificare c)
    {
        nrIntrebari=c.nrIntrebari;
        delete[] noteIntrebari;
        noteIntrebari=new int[nrIntrebari];
        for(int i=0;i<nrIntrebari;i++)
            noteIntrebari[i]=c.noteIntrebari[i];
        categorii=c.categorii;
    }



    friend ofstream & operator<< (ofstream& iesire5, Clasificare &c)
    {
        iesire5<<"Utilizatorul a raspuns la ";
        iesire5<<c.nrIntrebari;
             iesire5<<" intrebari si a primit urmatoarele calificative pt cele ";
             iesire5<<c.nrIntrebari;
             iesire5<<" note:";
             iesire5<<endl;
             for(int i=0;i<c.nrIntrebari;i++)
                iesire5<<c.noteIntrebari[i]<<" ";
             iesire5<<endl;
             iesire5<<"Acesta se claseaza in categoria "<<c.categorii;

             return iesire5;
    }





    friend istream & operator>> (istream& intrare5, Clasificare &c)
    {
        intrare5>>c.nrIntrebari;
        for(int i=0;i<c.nrIntrebari;i++)
        intrare5>>c.noteIntrebari[i];
        intrare5>>c.categorii;

        return intrare5;
    }};







int main()
{
            //URMATOAREA SECVENTA COMENTATA ESTE PENTRU VERIFICAREA METODELOR DIN CLASA; EX: OPERATORUL =
     ContUtilizator u1;
    char **locuri;
    locuri=new char *[2];
    locuri[0]="Fisc";
    locuri[1]="BCR";
    int t[10]={0,7,4,5,3,6,4,4,2,1};
    ContUtilizator u2(1, "Gigel", 29, "economic", 'M', 2, locuri, t);
   /* u1.afisare1();
    cout<<endl;
    u2.afisare1();
    cout<<endl;
    cout<<"Operattorul de copiere:"<<endl;
    ContUtilizator u3=u2;     //copiere
    u3.afisare1();
    cout<<endl;
    cout<<"Operatorul =:"<<endl;
    u1=u3;                    //operator =
    u1.afisare1();
    cout<<endl;
    ofstream fisier("fisieer.txt", ios_base::out);
    fisier<<u1;
    fisier.close(); */



                                                         //STL URI
       /* vector<ContUtilizator> cstl;
        cstl.push_back(u1);
        vector<ContUtilizator> cstl;
        cstl.push_back(u2);*/




                                               //++,[]
   /* cout<<u2[1];

    (u2++).afisare1();
    (++u2).afisare1();*/



                                       //IFSTREAM PENTRU CLASA CONTUTILIZATOR
  /*  ContUtilizator listaConturiUtilizatori[20];
    int catiUtilizatori;
    ifstream fisierIntrare("ContUtilizator.txt", ios_base::in);
     if(fisierIntrare.is_open())
        cout<<"S-a deschis fisierul cu datele de utilizator"<<endl;
    else
        cout<<"Nu s-a deschis fisierul cu datele de utilizator"<<endl;
    fisierIntrare>>catiUtilizatori;
        for(int i=0;i<catiUtilizatori;i++)
    fisierIntrare>>listaConturiUtilizatori[i];
    fisierIntrare.close();
    for(int i=0;i<catiUtilizatori;i++)
        {listaConturiUtilizatori[i].afisare1();
    cout<<endl;}
    cout<<endl;

*/


                          //APELURI IN CLASA CONTMODERATOR PENTRU OPERATORII BASIC (EX. =)
  /*  ContModerator m1;
    m1.afisare1();
    ContModerator m2(1, "Gigel", 29, "economic", 'M', 2, locuri, t, "gig@gmail.com", 'm');
    m2.afisare1();
    ContModerator m3=m2;
    m3.afisare1();
    m1=m2;
    m1.afisare1(); */


                                       //IFSTREAM PENTRU CLASA CONTMODERATOR
     /*  ContModerator listaConturiModerator[20];
    int catiModeratori;
    ifstream fisierIntraree("ContModerator.txt", ios_base::in);
     if(fisierIntraree.is_open())
        cout<<"S-a deschis fisierul cu datele de utilizator"<<endl;
    else
        cout<<"Nu s-a deschis fisierul cu datele de utilizator"<<endl;
    fisierIntraree>>catiModeratori;
        for(int i=0;i<catiModeratori;i++)
    fisierIntraree>>listaConturiModerator[i];
    fisierIntraree.close();
    for(int i=0;i<catiModeratori;i++)
        {listaConturiModerator[i].afisare1();
    cout<<endl;}
    cout<<endl;*/


                                      //APELURI BASIC PENTRU CLASA CONTADMIN
/*
     ContAdmin a1;
    a1.afisare1();
    char** fctii;
    fctii=new char*[2];
    fctii[0]="posteaza";
    fctii[1]="comenteaza";
    char *data;
    data=new char[strlen("12.03.2012")+1];
    strcpy(data, "12.03.2012");
    ContAdmin a2(1, "Gigel", 29, "economic", 'M', 2, locuri, t,data, 2,fctii, 'a');
    a2.afisare1();
    ContAdmin a3=a2;
    a3.afisare1();
    a1=a2;
    a1.afisare1();


                                        //IFSTREAM PENTRU CLASA CONTADMIN
    cout<<endl<<endl<<endl<<endl;
    int catia;
    ContAdmin listaca[10];
    ifstream f("ContAdmin.txt", ios_base::in);
    f>>catia;
    for(int i=0;i<catia;i++)
        {
            f>>listaca[i];
            listaca[i].afisare1();
        }
        f.close();


                                 //APELURI BASIC PENTRU CLASA CONTOBISNUIT
    ContObisnuit co1;
    co1.afisare1();
    ContObisnuit co2(1, "Gigel", 29, "economic", 'M', 2, locuri, t,"str. c a rosetti","casatorit","13.10.1980", 'o');
    co2.afisare1();
    ContObisnuit co3=co2;
    co3.afisare1();
    co1=co2;
    co1.afisare1();*/


                                     //IFSTREAM PENTRU CLASA CONTOBISNUIT
    /* cout<<endl<<endl<<endl;
    ContObisnuit listaContObisnuit[20];
    ifstream fisierObisnuit("ContObisnuit.txt", ios_base::in);
    int CatiUtilizatoriObisnuiti;
    fisierObisnuit>>CatiUtilizatoriObisnuiti;
    for(int i=0; i<CatiUtilizatoriObisnuiti;i++)
   {fisierObisnuit>>listaContObisnuit[i];
     listaContObisnuit[i].afisare1();
    }
    fisierObisnuit.close();*/


                                    //APELURI BASIC PENTRU CLASA MENIU
  /*   Meniu me1;
    me1.afisare2();
    Meniu me2(1,"abcd", "parolanoua");
    me2.afisare2();
    Meniu me3=me2;
    me3.afisare2();
    Meniu me4(me3);
    me4.afisare2();
    me1=me3;
    me1.afisare2();


                                     //APELURI BASIC PENTRU CLASA INTREBARI
    Intrebari i1;
    i1.afisare3();
    int mm=2;
    char **intrb=new char*[2];
    intrb[0]={"Ce este C++?"};
    intrb[1]={"Cat de util il considerati?"};
    int diff[2];
    diff[0]=1;
    diff[1]=2;
    Intrebari i2(1,mm,intrb, diff);
    i2.afisare3();
    Intrebari i3=i2;
    i3.afisare3();
    i1=i3;
    i1.afisare3();
    ofstream fisier2 ("fisier.txt", ios_base::out);
    fisier2<<i1;
    fisier2.close();
    cout<<endl<<endl<<endl;*/


    /*                                      //IFSTREAM PENTRU CLASA INTREBARI
    int catei;
    Intrebari listai[10];
    ifstream ff("Intrebari.txt", ios_base::in);
    ff>>catei;
    for(int i=0;i<catei;i++)
    {
        ff>>listai[i];
        listai[i].afisare3();
    }
    ff.close();
*/


                                           //APELURI BASIC PENTRU CLASA CLASIFICARE
    /*Clasificare<int,int> c1;
    c1.afisare5();
    int note[2]={4,3};
    Clasificare<int,int> c2(2,note,3);
    c2.afisare5();
    ofstream fisier5("fisier.txt", ios_base::out);
    fisier5<<c2;
    fisier5.close();*/



                                    //APELURI BASIC PENTRU CLASA RASPUNSURI
   /* Raspunsuri r1;
    r1.afisare4();
    int rr=2;
    char **rsp;
    char **frm;
    rsp=new char*[2];
    rsp[0]={"Da"};
    rsp[1]={"NU"};
    frm=new char*[2];
    frm[0]={"simpla"};
    frm[1]={"simpla"};
    int var[2];
    var[0]=1; var[1]=1;
    Raspunsuri r2(rr,rsp, frm, var,3,"gigel",29,"economic",'M',2,locuri,t, "str. parc",
                  "necasatorit","12.03.1967",'u',3,mm, intrb, diff);
                  cout<<endl<<endl<<endl;
    r2.afisare4();
    ofstream fisier4 ("fisier.txt", ios_base::out);
    fisier4<<r1;
    fisier4.close(); */












    cout<<endl<<endl<<"                                 HELLO!"<<endl<<endl<<endl<<endl<<endl;
    cout<<"     Pentru a efectua alte comenzi, va rog sa va logati"<<endl<<endl;
    cout<<"        username: ";

    char buffer[25];
    char bufferp[25];
    int idLogare;
    cin>>buffer;
     cout<<"        parola: ";
    cin>>bufferp;
     cout<<"        id-ul de logare: ";
     cin>>idLogare;
     if(idLogare<=0 || idLogare>=101)
        cout<<endl<<"     Ati introdus un id gresit! ";
        cout<<endl;
     Meniu m(idLogare,buffer, bufferp);

     Meniu listaMeniu[10];
     ifstream fisierMeniu("Conturi.txt", ios_base::in);
     int nrConturi;
     fisierMeniu>>nrConturi;
     int k=0;
     for(int i=0;i<nrConturi;i++)
     {
         fisierMeniu>>listaMeniu[i];
         if(strcmp(listaMeniu[i].getNumeCont(),m.getNumeCont())==0)
             if(listaMeniu[i].getId()==m.getId())
                if(strcmp(listaMeniu[i].getParola(),m.getParola())==0)
                    k=1;
     }
     fisierMeniu.close();
     if(k==0)
        cout<<"     Ne pare rau, contul dvs. nu exista sau ati introdus valori gresite."<<endl;
       else
        {
            cout<<"     La ce categorie de intrebari doriti sa raspundeti?"<<endl<<endl;
            cout<<"         Pentru categoria 1, raspundeti cu 1"<<endl;
            cout<<"         Pentru categoria 2, raspundeti cu 2"<<endl;
            cout<<"         Pentru categoria 3, raspundeti cu 3"<<endl<<endl;
            cout<<"                      raspuns: ";

            int raspunsUtilizator;
            cin>>raspunsUtilizator;

        if(raspunsUtilizator==1 || raspunsUtilizator==2 || raspunsUtilizator==3)
            {
                int cateIntrebari;
                Intrebari listaIntrebari[10];
                ifstream fisierIn("Intrebari.txt", ios::in);
                //fisierIn>>cateIntrebari;


                   // int c=1;
                   // cout<<"c";
              for(int i=0;i<3;i++)
             {  // cout<<c;
             //c++;
                fisierIn>>listaIntrebari[i];
                //listaIntrebari[i].afisare3();

             }

            fisierIn.close();
            char buffer[500];
            for(int i=0;i<3;i++)
                if(listaIntrebari[i].getIdi()==raspunsUtilizator)
                {
                    ofstream fisierRaspunsuri("Raspunsuri.txt", ios_base::out);
                    fisierRaspunsuri<<raspunsUtilizator<<endl;
                    fisierRaspunsuri<<listaIntrebari[i].getNrIntrebariP()<<endl;

                    int punctaj=0;
                    int dificultate;

                    for(int j=0;j<listaIntrebari[i].getNrIntrebariP();j++)
                        {
                           cout<<endl;
                           cout<<"              ";
                           puts(listaIntrebari[i].getIntrebariPropuse(j));

                           cout<<" ";
                           cout<<"              ";
                           cin>>buffer;
                           fisierRaspunsuri<<buffer<<endl;

                           dificultate=listaIntrebari[i].getDificultate(j);
                           punctaj=punctaj+dificultate;
                        }

                    fisierRaspunsuri.close();

                    cout<<endl<<endl<<endl<<endl<<endl
                         <<"                Felicitari, ai obtinut un punctaj de "<<punctaj<<"p!"<<endl<<endl;

                    ofstream fisierCalificativ("Calificative.txt", ios_base::out);
                    fisierCalificativ<<"S-a obtinut un punctaj de "<<punctaj<<"p.";
                    fisierCalificativ.close();
                }




        }
        else cout<<endl<<"                   S-a introdus un raspuns gresit!"<<endl<<endl;}







}
