#include<iostream>
#include<conio.h>
#include<string>
using namespace std;

typedef struct data
	{

	string NamaPemain;
	string PosisiPemain;
	int Nopemain;
	}
dData;

class simpul
{
	public :
		dData datapemain;
		simpul* pBerikutnya;
		
		
		simpul(string NP,string PP, int Np)
			{
			datapemain.NamaPemain = NP;
			datapemain.PosisiPemain = PP;
			datapemain.Nopemain = Np;
			pBerikutnya = NULL;
			}
		
		void tampilSimpul()
			{
			cout << datapemain.Nopemain << "--->" << datapemain.NamaPemain << "--->" << datapemain.PosisiPemain<<endl;
			}
};

class linkedlist
{
	private :
		simpul* pPertama;
		simpul* pAkhir;
	
	public :
		linkedlist() : pPertama(NULL)
		{}
		
		~linkedlist()
		{
		simpul* pSekarang = pPertama;
		while(pSekarang!=NULL)
			{
			simpul* pLama = pSekarang;
			pSekarang = pSekarang->pBerikutnya;
			delete pLama;
			}
		}
		
		bool kosong()
			{
			return (pPertama==NULL);
			}
		
		void sisipAkhir(string NP, string PP, int Np)
			{
			simpul* pSimpulBaru = new simpul(NP,PP,Np);
			if(apaKosong())
				{
				pPertama = pSimpulBaru;
				}
			else
				{
				pAkhir->pBerikutnya=pSimpulBaru;
				}
			pAkhir=pSimpulBaru;
			}
		
		void hapusPertama()
			{
			simpul* pTemp = pPertama;
			pPertama = pPertama->pBerikutnya;
			delete pTemp;
			}
		
		void tampilSenarai()
			{
			simpul* pSekarang = pPertama;
			if(pSekarang==NULL)
				{
				cout << "STACK KOSONG";
				}
			while(pSekarang!=NULL)
				{
				pSekarang->tampilSimpul();
				pSekarang = pSekarang->pBerikutnya;
				}
			cout << endl;
			}
};

class queuelist
{
	private :
		linkedlist* pSenarai;
	
	public :
		queuelist()
			{
			pSenarai = new linkedlist;
			}
		
		~queuelist()
			{
			delete pSenarai;
			}
		
		void push(string NP, string PP, int Np)
			{
			pSenarai->sisipAkhir(NP,PP,Np);
			}
		
		void pop()
			{
			pSenarai->hapusPertama();	
			}
		
		bool kosong()
			{
			return (pSenarai->kosong());
			}
		
		void tampilTumpukan()
			{
			pSenarai->tampilSenarai();
			}
};

int main()
{
	queuelist queue;
	int pilih, nomor;
	string nama, posisi;
	do 
	{
		cout << "\n=====================================================" << endl;
		cout << "Queue menggunakan linked list (data pemain sepakbola)" << endl << endl;
		cout << "1. Enqueue" << endl;
		cout << "2. Dequeue" << endl;
		cout << "3. Tampil data" << endl;
		cout << "4. Exit" << endl << endl;
		cout << "Masukkan pilihan anda : ";
		cin >> pilih;
		cout << "=====================================================" << endl;
	
		switch(pilih)
		{
			case 1 :
				cout << "\nMasukkan nomor punggung pemain : "; cin >> no;
				cin.ignore(256,'\n');
				cout << "Masukkan nama pemain : "; getline(cin,nama);
				cout << "Masukkan posisi pemain : "; getline(cin,posisi);
				queue.push(nama,posisi,nomor);
				break;
				
			case 2 :
				queue.pop();
				break;
			
			case 3 :
				queue.tampilTumpukan();
				break;
				
			case 4 :
				exit(0);
				break;
				
			default :
				cout << "Pilihan yang anda masukkan salah"<<endl;
		}
	} while (true);
	getch();
	return 0;
}
