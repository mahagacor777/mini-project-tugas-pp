#include <iostream>
#include <fstream>
#include <string>
using namespace std;
const string dataFile= "wash_data.txt"; //insisialisasi datafile txt sebagai memori atau penyimpanan
const int totalHari= 7;   // total hari sebagai batas input mingguan

//inisialisasi variabel haridata dengan struct yang berisi array jumlah pakaian dan cuaca
//array ini digunakan untuk menampung inputan dari user
struct HariData {
int pakaian;
string cuaca;
};

  //insisialisasi variabel untuk memberi nilai awal pada sisa pakaian minggulalu
int sisaMingguLalu= -1;   //nilai= -1, dibuat sekecil mungkin agar saat memulai input hari ke-1 , sisa pakaian pada datafile dianggap masih kosong

//fungsi load data untuk memuat inputan (membuka dan membaca) datafile secara berulang
void loadData(HariData data[], int &hariSekarang) {
    ifstream file(dataFile);

    if (!file.is_open()) {
        hariSekarang = 1;
        for (int i = 0; i < totalHari; i++) {
            data[i].pakaian = 0;
            data[i].cuaca = "-";
        }
        return;    //memberhentikan fungsi pada hari pertama karena datafile masih kosong
    }

    file >> hariSekarang;
    for (int i = 0; i < totalHari; i++) {
        file >> data[i].pakaian >> data[i].cuaca;
    }

    file.close();  //menutup datafile
}

void saveData(HariData data[], int hariSekarang) {
    ofstream file(dataFile);          // Membuka file untuk ditulis
    file << hariSekarang << endl;     // Simpan hari saat ini ke dalam file

    // Untuk menyimpan jumlah pakaian dan cuaca tiap hari ke file
    for (int i = 0; i < totalHari; i++) {
        file << data[i].pakaian << " " << data[i].cuaca << endl;
    }

    file.close();                    
}
// Untuk memberikan saran sesuai dengan kondisi yang telah ditetukan
string saranCuci(const HariData &hari) {
    if (hari.cuaca == "hujan")
        return "Hari hujan, disarankan TIDAK mencuci.";
    else if (hari.pakaian >= 10)
        return "Pakaian sudah menumpuk, disarankan mencuci.";
    else
        return "Pakaian masih sedikit, boleh mencuci atau menunda.";
}

// fungsi resetMingguBaru untuk melakukan reset data mingguan dan membawa sisa pakaian ke minggu selanjutnya 
void resetMingguBaru(HariData data[], int &hariSekarang) {    // & untuk agar nilai dapat berubah  
    int sisa = data[6].pakaian;      // mengambil sisa pakaian dari minggu sebelumnya
    sisaMingguLalu = sisa;           // menyimpan sisa pakaian untuk ditampilkan di hari pertama minggu selanjutnya

    for (int i = 0; i < totalHari; i++) {
        data[i].pakaian = 0;
        data[i].cuaca = "-";
    }

    data[0].pakaian = sisa;    // memindahkan sisa pakaian ke minggu baru
    hariSekarang = 1;          

cout << "\n=== Minggu Baru Dimuali ===\n";      // menampilkan teks ke layar terminal
cout << "Sisa pakaian dari minggu sebelumnya: " << sisa << " baju.\n";
}

// Fungsi inputHari digunakan untuk mengisi data pakaian dan cuaca
void inputHari(HariData data[], int &hariSekarang ) {

    if (hariSekarang == 1 && sisaMingguLalu >= 0){
        cout << "\n=== Hari Pertama Minggu Baru ===\n";
        cout << "Minggu lalu masih ada sisa pakaian :"
             << sisaMingguLalu << " baju.\n\n";
        sisaMingguLalu = -1;
}

    cout << "=== Input Hari Ke-" << hariSekarang << " ===\n";

    int tambahan;
    cout << "Masukkan jumlah pakaian hari ini: ";
    cin >> tambahan;

    string cuaca ;
    cout << "Masukkan cuaca (cerah/hujan/mendung): ";
    cin >> cuaca ;

    data[hariSekarang - 1].pakaian += tambahan ;
    data[hariSekarang - 1].cuaca = cuaca;

    cout << "\n--- Saran Hari Ini ---\n";
    cout << saranCuci (data[hariSekarang - 1]) << endl;

    int pilihan;
    cout << "\nApa yang ingin Anda lakukan?\n";
    cout << "1. Cuci sekarang\n";
    cout << "2. Tunda mencuci\n";
    cout << "Pilihan: ";
    cin >> pilihan;   // Menerima input pilihan dari user
      
    // Mengecek pilihan user
    if (pilihan == 1) {
    // Jika user memilih mencuci:
    cout << "Anda memilih mencuci. Semua pakaian hari ini dianggap selesai.\n";
      
    // Set jumlah pakaian hari ini menjadi 0 (karena sudah dicuci)
    data[hariSekarang - 1].pakaian = 0;
      
    } else {
    // Jika user memilih menunda:
        cout << "Anda memilih menunda. Pakaian menumpuk ke hari berikutnya.\n";
    }
      
    // Pindah ke hari berikutnya
    hariSekarang++;
      
    // Jika hari melewati 7 (lebih dari seminggu), reset minggu baru
    if (hariSekarang > 7) {
        resetMingguBaru(data, hariSekarang);
    }
} 

void tampilMinggu(HariData data[]) {
    // Menampilkan judul rekap data satu minggu
    cout << "\n=== Rekap Mingguan ===\n";

    // Perulangan untuk menampilkan data dari hari 1 sampai totalHari
    for (int i = 0; i < totalHari; i++) {

        // Menampilkan jumlah pakaian dan cuaca untuk setiap hari
        cout << "Hari " << i + 1 << ": "
             << data[i].pakaian << " baju, Cuaca: "
             << data[i].cuaca << endl;
    }
}
void menuUtama(HariData data[], int &hariSekarang){
int pilihan;
while(true){
cout << "\n===== WASH TRACK MENU =====\n";
cout << "1. Input data hari ini\n";
cout << "2. Lihat data minggu ini\n";
cout << "3. Simpan dan keluar\n";
cout << "Pilihan menu : ";
cin >> pilihan;

switch(pilihan){
case 1:
inputHari(data, hariSekarang);
break;
case 2:
tampilMinggu(data);
break;
case 3:
saveData(data, hariSekarang);
cout << "Data disimpan. Program selesai.\n";
return;
default:
cout << "Eror, Pilihan tidak valid!\n";
}
}
}
int main() {
    HariData minggu[totalHari];
    int hariSekarang;

    loadData(minggu, hariSekarang);
    menuUtama(minggu, hariSekarang);

    return 0;
}


    
