#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

struct Produk {
    int id;
    std::string nama;
    int jumlah;
    float harga;
};

void tambahProduk(std::vector<Produk>& daftar) {
    Produk produkBaru;
    std::cout << "Masukkan ID Produk: ";
    std::cin >> produkBaru.id;
    std::cin.ignore();
    std::cout << "Masukkan Nama Produk: ";
    std::getline(std::cin, produkBaru.nama);
    std::cout << "Masukkan Jumlah Produk: ";
    std::cin >> produkBaru.jumlah;
    std::cout << "Masukkan Harga Produk: ";
    std::cin >> produkBaru.harga;
    daftar.push_back(produkBaru);
    std::cout << "Produk berhasil ditambahkan.\n";
}

void tampilkanProduk(const std::vector<Produk>& daftar) {
    if (daftar.empty()) {
        std::cout << "Daftar produk kosong.\n";
        return;
    }
    std::cout << "Daftar Produk:\n";
    for (const auto& produk : daftar) {
        std::cout << "ID: " << produk.id << ", Nama: " << produk.nama
                  << ", Jumlah: " << produk.jumlah
                  << ", Harga: " << produk.harga << "\n";
    }
}

void hapusProduk(std::vector<Produk>& daftar, int id) {
    auto it = std::remove_if(daftar.begin(), daftar.end(), [id](const Produk& p) {
        return p.id == id;
    });
    if (it != daftar.end()) {
        daftar.erase(it, daftar.end());
        std::cout << "Produk dengan ID " << id << " berhasil dihapus.\n";
    } else {
        std::cout << "Produk dengan ID " << id << " tidak ditemukan.\n";
    }
}

int main() {
    std::vector<Produk> daftarProduk;
    int pilihan;
    do {
        std::cout << "\nMenu:\n";
        std::cout << "1. Tambah Produk\n";
        std::cout << "2. Tampilkan Produk\n";
        std::cout << "3. Hapus Produk\n";
        std::cout << "4. Keluar\n";
        std::cout << "Masukkan pilihan: ";
        std::cin >> pilihan;

        switch (pilihan) {
            case 1:
                tambahProduk(daftarProduk);
                break;
            case 2:
                tampilkanProduk(daftarProduk);
                break;
            case 3: {
                int idHapus;
                std::cout << "Masukkan ID Produk yang ingin dihapus: ";
                std::cin >> idHapus;
                hapusProduk(daftarProduk, idHapus);
                break;
            }
            case 4:
                std::cout << "Terima kasih! Program selesai.\n";
                break;
            default:
                std::cout << "Pilihan tidak valid. Coba lagi.\n";
        }
    } while (pilihan != 4);

    return 0;
}
