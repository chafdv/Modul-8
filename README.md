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

Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme queue Alternatif 1 (head diam, tail bergerak).

```cpp
#include <iostream>
using namespace std;

#define MAX 5

typedef int infotype;

struct Queue {
    infotype info[MAX]; 
    int head;
    int tail;
};

void CreateQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
    } else {
        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q) {
    infotype x; 

    if (isEmptyQueue(Q)) {
        return -1; 
    } else {
        x = Q.info[Q.head];

        if (Q.head == Q.tail) {
            CreateQueue(Q); 
        } else {
            for (int i = Q.head; i < Q.tail; i++) {
                Q.info[i] = Q.info[i + 1];
            }
            Q.tail--; 
        }
        return x;
    }
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << "\t| ";
    if (isEmptyQueue(Q)) { 
        cout << "empty queue";
    } else {
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
} 

int main() {
    cout << "Hello world!" << endl; 
    Queue Q;                       
    CreateQueue(Q);               

    cout << "-----------------------------------" << endl; 
    
    cout << " H - T \t| Queue Info" << endl;             
    
    cout << "-----------------------------------" << endl; 

    printInfo(Q); 
    
    enqueue(Q, 5);  printInfo(Q); 
    enqueue(Q, 2);  printInfo(Q); 
    enqueue(Q, 7);  printInfo(Q); 

    dequeue(Q);     printInfo(Q); 

    enqueue(Q, 4);  printInfo(Q); 

    dequeue(Q);     printInfo(Q); 
    
    dequeue(Q);     printInfo(Q);
    
    dequeue(Q);     printInfo(Q); 

    return 0;
}
```

Output
	⁠![Output Soal 1](https://github.com/chafdv/Modul-6/blob/main/Output/maincpp1.png)

Program ini membuat dan mengelola queue berbasis array dengan operasi dasar seperti membuat antrian, mengecek kosong/penuh, menambah elemen enqueue, menghapus elemen dequeue, dan menampilkan isi antrian. Di fungsi main, program hanya mendemonstrasikan perubahan isi queue setelah beberapa operasi enqueue dan dequeue dilakukan.

---

### Soal 2

Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme queue Alternatif 2 (head bergerak, tail bergerak).

```cpp
#include <iostream>
using namespace std;

#define MAX 5

typedef int infotype;

struct Queue {
    infotype info[MAX]; 
    int head;
    int tail;
};

void CreateQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    return (Q.head == 0 && Q.tail == MAX - 1);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
    } else {
        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
            Q.info[Q.tail] = x;
        } else {
            if (Q.tail == MAX - 1) {
                int n = 0; 
                for (int i = Q.head; i <= Q.tail; i++) {
                    Q.info[n] = Q.info[i];
                    n++;
                }
                
                Q.head = 0;
                Q.tail = n - 1; 

                Q.tail++;
                Q.info[Q.tail] = x;

            } else {
                Q.tail++;
                Q.info[Q.tail] = x;
            }
        }
    }
}

infotype dequeue(Queue &Q) {
    infotype x; 

    if (isEmptyQueue(Q)) {
        return -1; 
    } else {
        x = Q.info[Q.head];
        if (Q.head == Q.tail) {
            CreateQueue(Q); 
        } else {
            Q.head++;
        }
        
        return x;
    }
}

void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << "\t| ";
    if (isEmptyQueue(Q)) { 
        cout << "empty queue";
    } else {
        for (int i = Q.head; i <= Q.tail; i++) {
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
} 

int main() {
    cout << "Hello world!" << endl; 
    Queue Q;                         
    CreateQueue(Q);                  

    cout << "-----------------------------------" << endl; 
    
    cout << " H - T \t| Queue Info" << endl;       
    
    cout << "-----------------------------------" << endl; 

    printInfo(Q); 
    
    enqueue(Q, 5);  printInfo(Q); 
    enqueue(Q, 2);  printInfo(Q); 
    enqueue(Q, 7);  printInfo(Q); 

    dequeue(Q);     printInfo(Q); 

    enqueue(Q, 4);  printInfo(Q); 

    dequeue(Q);     printInfo(Q); 
    
    dequeue(Q);     printInfo(Q);
    
    dequeue(Q);     printInfo(Q); 

    return 0;
```

Output 
	⁠![Output Soal 2](https://github.com/chafdv/Modul-6/blob/main/Output/maincpp2.png)

Program ini tersebut yaitu untuk membuat dan mengelola queue sederhana: bisa enqueue, dequeue, cek kosong/penuh, dan menampilkan isi antrian. Program juga otomatis menggeser data jika tail mentok supaya antrian tetap bisa dipakai.

---

### Soal 3

Buatlah implementasi ADT Queue pada file “queue.cpp” dengan menerapkan mekanisme queue Alternatif 3 (head dan tail berputar).

 ```cpp
#include <iostream>
using namespace std;

#define MAX 5

typedef int infotype;

struct Queue {
    infotype info[MAX]; 
    int head;
    int tail;
};

void CreateQueue(Queue &Q) {
    Q.head = -1;
    Q.tail = -1;
}

bool isEmptyQueue(Queue Q) {
    return (Q.head == -1 && Q.tail == -1);
}

bool isFullQueue(Queue Q) {
    return ((Q.tail + 1) % MAX == Q.head);
}

void enqueue(Queue &Q, infotype x) {
    if (isFullQueue(Q)) {
       
    } else {
        if (isEmptyQueue(Q)) {
            Q.head = 0;
            Q.tail = 0;
        } else {
            Q.tail = (Q.tail + 1) % MAX; 
        }
        Q.info[Q.tail] = x;
    }
}

infotype dequeue(Queue &Q) {
    infotype x; 

    if (isEmptyQueue(Q)) {
        return -1; 
    } else {
        x = Q.info[Q.head];

        if (Q.head == Q.tail) {
            CreateQueue(Q); 
        } else {
            Q.head = (Q.head + 1) % MAX;
        }
        
        return x;
    }
}
 
void printInfo(Queue Q) {
    cout << Q.head << " - " << Q.tail << "\t| ";
    if (isEmptyQueue(Q)) { 
        cout << "empty queue";
    } else {
        int i = Q.head;
        while (true) {
            cout << Q.info[i] << " ";
            if (i == Q.tail) {
                break; 
            }
            i = (i + 1) % MAX; 
        }
    }
    cout << endl;
} 

int main() {
    cout << "Hello world!" << endl; 
    Queue Q;                         
    CreateQueue(Q);                  

    cout << "-----------------------------------" << endl; 
    
    cout << " H - T \t| Queue Info" << endl;       
    
    cout << "-----------------------------------" << endl; 

    printInfo(Q); 
    
    enqueue(Q, 5);  printInfo(Q); 
    enqueue(Q, 2);  printInfo(Q); 
    enqueue(Q, 7);  printInfo(Q); 

    dequeue(Q);     printInfo(Q); 

    enqueue(Q, 4);  printInfo(Q); 

    dequeue(Q);     printInfo(Q); 
    
    dequeue(Q);     printInfo(Q);
    
    dequeue(Q);     printInfo(Q); 

    return 0;
}
```

Output 
	⁠![Output Soal 3](https://github.com/chafdv/Modul-6/blob/main/Output/maincpp3.png)

Program di atas adalah implementasi queue circular menggunakan array berkapasitas 5. Program dapat melakukan operasi dasar seperti membuat queue, mengecek kosong/penuh, menambah data (enqueue), menghapus data (dequeue), dan menampilkan isi antrian. Mekanisme circular dilakukan dengan operasi modulo sehingga head dan tail bisa berputar tanpa menggeser data.

---

## Referensi

1.⁠ ⁠[(https://www.dicoding.com/blog/struktur-data-queue-pengertian-fungsi-dan-jenisnya/)] [diakses 17-11-2025]
