# <h1 align="center">Laporan Praktikum Struktur Data<br> Modul 8 QUEUE </h1>
<p align="center">Osha Alfida Valyana / 103112430202</p>

## Dasar Teori

Queue atau dalam bahasa Indonesia yang berarti antrean adalah struktur data yang menyusun elemen-elemen data dalam urutan linier. Prinsip dasar dari struktur data ini adalah “First In, First Out” (FIFO) yang berarti elemen data yang pertama dimasukkan ke dalam antrean akan menjadi yang pertama pula untuk dikeluarkan.

## Guided

### Soal 1

```⁠ cpp
#include <iostream>
using namespace std;

#define MAX 5 // ukuran maksimal queue

// Struktur Queue
struct Queue {
    int data[MAX];
    int head;
    int tail;
};

// Membuat antrean kosong
void createQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

// Mengecek apakah queue kosong
bool isEmpty(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

// Mengecek apakah queue penuh
bool isFull(Queue Q) {
    return (Q.tail == MAX - 1);
}

// Menampilkan isi antrean
void printQueue(Queue Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong!" << endl;
    } else {
        cout << "Queue : ";
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.data[i] << " ";
        }
        cout << endl;
    }
}

// Menambah elemen ke dalam antrean (Enqueue)
void enqueue (Queue &Q, int x) {
    if (isFull(Q)) {
        cout << "Queue penuh! Tidak bisa menambah data." << endl;
    } else {
        if(isEmpty(Q)) {
            Q.head = Q.tail = 0;
        }else {
            Q.tail++;
        }
        Q.data[Q.tail] = x;
        cout << "Enqueue: " << x << endl;
    }
}

// Menghapus elemen dari antrean
void dequeue(Queue &Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong! Tiduk ada data yang dihapus." << endl;
    } else {
        cout << "Dequeue: " << Q.data[Q.head] << endl;

        if (Q.head == Q.tail) {
            Q.head = Q.tail = -1;
        } else {
            for (int i = Q.head; i < Q.tail; i++) {
                Q.data[i] = Q.data[i + 1];
            }
            Q.tail--;
        }
    }
}

// Program utama
int main() {
    Queue Q;
    createQueue(Q);

    enqueue(Q, 5);
    enqueue(Q, 2);
    enqueue(Q, 7);
    printQueue(Q);

    dequeue(Q);
    printQueue(Q);

    enqueue(Q, 4);
    enqueue(Q, 9);
    printQueue(Q);

    dequeue(Q);
    dequeue(Q);
    printQueue(Q);

    return 0;
}
```
 
Output
⁠![Output guided](https://github.com/chafdv/Modul-8/blob/main/output/guidedm8.png)

Program ini menerapkan struktur data Queue (antrian) dengan array statis yang dapat menampung hingga lima elemen.  Ini memiliki kemampuan untuk membuat antrian kosong, mengecek apakah kondisinya kosong atau penuh, menampilkan isi antrian, menambah elemen ke antrian, dan menghapus elemen dari antrian.  Prinsip FIFO, atau First In First Out, mengatur bahwa item yang masuk pertama akan keluar terlebih dahulu.  Dengan menambah, menghapus, dan menampilkan isi antrian secara berurutan, program utama kemudian menunjukkan penggunaan semua fungsi tersebut.
---

## Unguided

### Soal 1

Buatlah implementasi ADT Doubly Linked list pada file “Doublylist.cpp” dan coba hasil implementasi ADT pada file “main.cpp”.

```cpp
#ifndef DOUBLYLIST_H
#define DOUBLYLIST_H

#include <iostream>
#include <string>
using namespace std;

struct Kendaraan {
    string nopol;
    string warna;
    int thnBuat;
};

typedef Kendaraan infotype;

struct ElmList {
    infotype info;
    ElmList* next;
    ElmList* prev;
};

typedef ElmList* address;

struct List {
    address First;
    address Last;
};

void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertLast(List &L, address P);
address findElm(List L, string nopol);
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(address Prec, address &P);

#endif
```
 ⁠
 ⁠
Output
	⁠![Output Soal 1](https://github.com/chafdv/Modul-6/blob/main/Output/maincpp1.png)

Kode tersebut adalah header file untuk program Doubly Linked List yang menyimpan data kendaraan. Di dalamnya terdapat struktur node dengan pointer ke elemen sebelum dan sesudahnya, serta deklarasi fungsi untuk membuat, menambah, mencari, menampilkan, dan menghapus data pada list.

---

### Soal 2

Carilah elemen dengan nomor polisi D001 dengan membuat fungsi baru.

⁠ cpp
#include "doublylist.h"

void CreateList(List &L) {
    L.First = NULL;
    L.Last = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    P->info = x;
    P->next = NULL;
    P->prev = NULL;
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = NULL;
}

void printInfo(List L) {
    address P = L.First;
    while (P != NULL) {
        cout << "Nomor Polisi : " << P->info.nopol << endl;
        cout << "Warna        : " << P->info.warna << endl;
        cout << "Tahun        : " << P->info.thnBuat << endl;
        cout << "------------------------------" << endl;
        P = P->next;
    }
}

void insertLast(List &L, address P) {
    if (L.First == NULL) {
        L.First = P;
        L.Last = P;
    } else {
        L.Last->next = P;
        P->prev = L.Last;
        L.Last = P;
    }
}

address findElm(List L, string nopol) {
    address P = L.First;
    while (P != NULL) {
        if (P->info.nopol == nopol) {
            return P;
        }
        P = P->next;
    }
    return NULL;
}

void deleteFirst(List &L, address &P) {
    if (L.First != NULL) {
        P = L.First;
        if (L.First == L.Last) {
            L.First = NULL;
            L.Last = NULL;
        } else {
            L.First = L.First->next;
            L.First->prev = NULL;
        }
        P->next = NULL;
    }
}

void deleteLast(List &L, address &P) {
    if (L.First != NULL) {
        P = L.Last;
        if (L.First == L.Last) {
            L.First = NULL;
            L.Last = NULL;
        } else {
            L.Last = L.Last->prev;
            L.Last->next = NULL;
        }
        P->prev = NULL;
    }
}

void deleteAfter(address Prec, address &P) {
    if (Prec != NULL && Prec->next != NULL) {
        P = Prec->next;
        Prec->next = P->next;
        if (P->next != NULL) {
            P->next->prev = Prec;
        }
        P->next = NULL;
        P->prev = NULL;
    }
}

 ⁠

Output 
	⁠![Output Soal 2](https://github.com/chafdv/Modul-6/blob/main/Output/maincpp2.png)

Kode ini berisi fungsi untuk membuat, menambah, menampilkan, mencari, dan menghapus data pada doubly linked list yang berisi informasi kendaraan. Setiap node terhubung dua arah sehingga data bisa diakses dan dihapus dari depan maupun belakang dengan mudah.

---

### Soal 3

Hapus elemen dengan nomor polisi D003 dengan procedure delete.
•⁠  ⁠procedure deleteFirst( input/output L : List,
 P : address )
•⁠  ⁠procedure deleteLast( input/output L : List,
 P : address )
•⁠  ⁠procedure deleteAfter( input Prec : address,
 input/output P : address )

⁠ cpp
#include "DoublyList.h"

int main() {
    List L;
    CreateList(L);

    int n;
    cout << "Masukkan jumlah kendaraan: ";
    cin >> n;
    cin.ignore();

    for (int i = 0; i < n; i++) {
        infotype x;
        cout << "Masukkan nomor polisi: ";
        getline(cin, x.nopol);
        cout << "Masukkan warna kendaraan: ";
        getline(cin, x.warna);
        cout << "Masukkan tahun kendaraan: ";
        cin >> x.thnBuat;
        cin.ignore();
        insertLast(L, alokasi(x));
        cout << endl;
    }

    cout << "\nDATA LIST 1\n";
    printInfo(L);

    string cari;
    cout << "Masukkan Nomor Polisi yang dicari: ";
    getline(cin, cari);
    address found = findElm(L, cari);
    if (found != nullptr) {
        cout << "\nNomor Polisi : " << found->info.nopol << endl;
        cout << "Warna        : " << found->info.warna << endl;
        cout << "Tahun        : " << found->info.thnBuat << endl;
    } else {
        cout << "\nData tidak ditemukan.\n";
    }

    cout << "\nMasukkan Nomor Polisi yang akan dihapus: ";
    string hapus;
    getline(cin, hapus);

    address del = findElm(L, hapus);
    if (del != nullptr) {
        address P;
        if (del == L.First) {
            deleteFirst(L, P);
        } else if (del == L.Last) {
            deleteLast(L, P);
        } else {
            deleteAfter(del->prev, P);
        }
        cout << "Data dengan nomor polisi " << hapus << " berhasil dihapus.\n";
        dealokasi(P);
    } else {
        cout << "Data tidak ditemukan.\n";
    }

    cout << "\nDATA LIST 1 SETELAH HAPUS:\n";
    printInfo(L);

    return 0;
}

 ⁠
 
Output 
	⁠![Output Soal 3](https://github.com/chafdv/Modul-6/blob/main/Output/maincpp3.png)

Kode tersebut berfungsi untuk mengelola data kendaraan menggunakan doubly linked list. Program meminta pengguna memasukkan beberapa data kendaraan, lalu menampilkannya. Setelah itu, pengguna dapat mencari data berdasarkan nomor polisi dan menghapus data tersebut baik di awal, tengah, maupun akhir list.

## Referensi

1.⁠ ⁠[(https://www.dicoding.com/blog/struktur-data-queue-pengertian-fungsi-dan-jenisnya/)] [diakses 17-11-2025]
