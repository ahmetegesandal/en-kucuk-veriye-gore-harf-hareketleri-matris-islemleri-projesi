// Ahmet Ege Sandal - 231030015


#include <iostream>
#include <fstream>
#include <sstream>
#include <string>
#include <cmath>
#include <cstdlib>
#include <ctime>
#include <windows.h>

using namespace std;

#define gen 71 // genişik değeri
#define yuk 51 // yükseklik değeri
#define PI 3.14159 // pi değeri

class Arazi {
public:
    int matris[yuk][gen];

    // Arazi matrisini dosyadan oku
    void DosyadanAraziOku(const char* dosyaAdi) {
        ifstream dosya(dosyaAdi);
        string metin;

        cout << "Arazi Yükseklikleri:\n";

        for (int i = 0; i < yuk; i++) {
            if (getline(dosya, metin)) {
                istringstream ss(metin);
                for (int j = 0; j < gen; j++) {
                    string eleman;
                    if (getline(ss, eleman, ';')) {
                        matris[i][j] = stoi(eleman);
                    }
                }
            }
        }

        dosya.close();
    }

    // Matrisi ekrana yazdır
    void DosyayiYazdir() {
        for (int i = 0; i < yuk; i++) {
            for (int j = 0; j < gen; j++) {
                cout << matris[i][j] << " ";
            }
            cout << endl;
        }
    }
};

class Harf {
public:
    char harfMatris[yuk][gen];

    // Harf matrisini başlangıç değerleriyle doldur
    void HarfMatrisiniDoldur() {
        for (int i = 0; i < yuk; i++) {
            for (int j = 0; j < gen; j++) {
                harfMatris[i][j] = ' ';
            }
        }
    }

    // Harfi harfMatris dizisine yerleştir
    void HarfiMatriseYerlestir(char harf, int x, int y) {
        if (x >= 0 && x < gen && y >= 0 && y < yuk) {
            harfMatris[y][x] = harf;
        }
    }

    // Harf matrisini ekrana yazdır
    void HarfMatrisiniYazdir() {
        cout << "\nHarf Matrisi:\n";
        for (int i = 0; i < yuk; i++) {
            for (int j = 0; j < gen; j++) {
                if (harfMatris[i][j] == 'X') {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_RED); // kırmızı konsol rengi
                    cout << harfMatris[i][j];
                }
                else if (harfMatris[i][j] != '+') {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_BLUE); // mavi konsol rengi
                    cout << harfMatris[i][j];
                }
                else if (harfMatris[i][j] != ' ') {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_GREEN); // yeşil konsol rengi
                    cout << harfMatris[i][j];
                }
                else {
                    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_RED | FOREGROUND_GREEN | FOREGROUND_BLUE); // konsol rengi sıfırlama
                    cout << "  ";
                }
            }

            // Renkleri varsayılan renklere çevir
            SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), FOREGROUND_INTENSITY | FOREGROUND_RED | FOREGROUND_GREEN | FOREGROUND_BLUE); 
            cout << endl;
        }
    }
};

// Kutupsal koordinatları hesapla
void kutupsalKoordinatlariHesapla(double& x, double& y, double aci, double yaricap, double merkezX, double merkezY) {
    aci = aci * PI / 180.0;
    x = merkezX + yaricap * cos(aci);
    y = merkezY + yaricap * sin(aci);
}



int main() {
    setlocale(LC_ALL, "Turkish"); // türkçe yap

    Arazi arazi; // arazi nesnesini kullan 
    Harf harf; // harf nesnesini kullan

    arazi.DosyadanAraziOku("Veri.csv"); // 
    arazi.DosyayiYazdir();
    harf.HarfMatrisiniDoldur();

    const char* isim = "AHMETSANDAL"; // yerleştirilecek ismin harfleri
    const int isimuzunluk = 11; // isim uzunluğu bilerek strlen ile alınmadı
    
    double merkezX = gen / 2; // ortaya hizalama genişlik/2
    double merkezY = yuk / 2; // ortaya hizalama yükseklik/2

    srand(time(0)); // rastgele oluşturma için
    

    double aciArtis = 360.0 / strlen(isim);
    double yaricap = rand() % 6 + 15; // Yarıçapı 15 ve 20 arasında rastgele alır

    // Harflerin başlangıç konumlarını saklar
    int baslangicKonumlar[isimuzunluk][2];

    // Harflerin ilk konumlarını al ve harf matrisine yerleştir
    for (int i = 0; i < strlen(isim); i++) {
        double gecerliAci = i * aciArtis;

        double x, y;
        kutupsalKoordinatlariHesapla(x, y, gecerliAci, yaricap, merkezX, merkezY); // açı hesap ve konum bilgisi

        int xIndeks = static_cast<int>(round(x)); // gelen konumu int türüne çevirip hassas şekilde yuvarlama tam sayıya denk gelmesi önemli
        int yIndeks = static_cast<int>(round(y)); // gelen konumu int türüne çevirip hassas şekilde yuvarlama tam sayıya denk gelmesi önemli
        

        if (xIndeks >= 0 && xIndeks < gen && yIndeks >= 0 && yIndeks < yuk) { // matristen taşmaması için
            harf.HarfiMatriseYerlestir(isim[i], xIndeks, yIndeks); // koordinatları hesaplayıp harfleri yerleştirme
            baslangicKonumlar[i][0] = xIndeks; // başlangıç konumlarını diziye atama
            baslangicKonumlar[i][1] = yIndeks; // başlangıç konumlarını diziye atama
        }
    }

    harf.HarfMatrisiniYazdir(); // harfli olan matrisi yerleştirilmiş halini yazar

    harf.HarfMatrisiniDoldur(); 

    // Harflerin konumlarını ve güncellenen harf matrisini ekrana yazdır
    cout << "\nHarflerin Konumlarının Takibi:\n";
    for (int i = 0; i < strlen(isim); i++) {
        int xIndeks = baslangicKonumlar[i][0]; // başlangıç konumlarını alma
        int yIndeks = baslangicKonumlar[i][1]; // başlangıç konumlarını alma

        if (xIndeks >= 0 && xIndeks < gen && yIndeks >= 0 && yIndeks < yuk) { // matristen taşmaması için
            int& harfinVerisi = arazi.matris[yIndeks][xIndeks];
            cout << "Harf: " << isim[i] << ", Konum: (" << yIndeks + 1 << ", " << xIndeks + 1 << "), Veri: " << harfinVerisi << "\n"; // başlangıç konum bilgileri

            // Harfin etrafındaki en küçük veriyi bul ve güncelle
            while (true) {
                int enKucukVeri = harfinVerisi;
                int yeniX = xIndeks;
                int yeniY = yIndeks;
                bool geriDondu = false;

                // Sağ, sol, üst, alt, çapraz kontrol et
                for (int dx = -1; dx <= 1; dx++) {
                    for (int dy = -1; dy <= 1; dy++) {
                        int xKomsu = xIndeks + dx;
                        int yKomsu = yIndeks + dy;

                        if (xKomsu >= 0 && xKomsu < gen && yKomsu >= 0 && yKomsu < yuk) {
                            if (arazi.matris[yKomsu][xKomsu] < enKucukVeri) {
                                enKucukVeri = arazi.matris[yKomsu][xKomsu];
                                yeniX = xKomsu;
                                yeniY = yKomsu;
                                geriDondu = false;
                            }
                            else if (arazi.matris[yKomsu][xKomsu] == enKucukVeri && rand() % 2 == 0 && (xKomsu != xIndeks || yKomsu != yIndeks)) {
                                // Eğer aynı en küçük veriye sahip iki komşu varsa rastgele birine geç (ancak aynı konuma iki kez gitme)
                                yeniX = xKomsu;
                                yeniY = yKomsu;
                                geriDondu = true;
                            }
                        }
                    }
                }

                // Kontrol: Eğer çevresindeki en küçük veri, mevcut veriden küçükse ve yeni konumda harfMatris'te boşsa veya içeriği güncellenmemişse konumu güncelle
                if (enKucukVeri < harfinVerisi && (harf.harfMatris[yeniY][yeniX] == ' ' || harf.harfMatris[yeniY][yeniX] == isim[i])) {
                    // Yeni konumu ve güncellenmiş veriyi ekrana yazdır
                    cout << "Harf: " << isim[i] << " güncellendi -> Yeni Konum: (" << yeniY + 1 << ", " << yeniX + 1 << "), Yeni Veri: " << enKucukVeri << "\n"; // güncellenen konum bilgisi

                    // Harfi yeni konumuna ve güncellenmiş veriye yerleştir
                    if (yeniX >= 0 && yeniX < gen && yeniY >= 0 && yeniY < yuk) {
                        harf.HarfiMatriseYerlestir('X', xIndeks, yIndeks); // geçtiği yola x yerleştirme
                        harf.HarfiMatriseYerlestir('+', yeniX, yeniY); // son bulunduğu noktaya + yerleştirme
                        harfinVerisi = enKucukVeri;

                        // Yeni konumu değerlendir
                        xIndeks = yeniX;
                        yIndeks = yeniY;
                    }
                    else
                    {
                        break;
                    }

                    
                }
                else {
                    // Eğer çevresindeki en küçük veri, mevcut veriden büyükse veya yeni konumda harfMatris'te başka bir harf varsa döngüden çık
                    break;
                }
                
            }
        }
    }

    // Başlangıç konumlarına geri dön ve orijinal harfleri yerleştir
    for (int i = 0; i < strlen(isim); i++) {
        int xIndeks = baslangicKonumlar[i][0];
        int yIndeks = baslangicKonumlar[i][1];
        harf.HarfiMatriseYerlestir(isim[i], xIndeks, yIndeks); // başlangıç noktasında hangi harf varsa onu yazma
    }

    harf.HarfMatrisiniYazdir(); // harf matrisini yazdırma

    return 0;
}
