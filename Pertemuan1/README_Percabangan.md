# 📘 Praktikum Sistem Mikrokontroler

## Pertemuan 1 – Percabangan & Perulangan

**Nama:** Diva Syahita Mawarni
**NIM:** H1H024015

---

## 🔹 Percobaan 1A: Percabangan (If-Else)

### 📌 Tujuan

Memahami penggunaan percabangan (`if-else`) untuk mengatur kecepatan kedipan LED.

---

### ❓ Pertanyaan & Jawaban

#### 1. Pada kondisi apa program masuk ke blok `if`?

Program akan masuk ke blok `if` ketika:

```
timeDelay <= 100
```

Artinya, saat delay sudah sangat kecil (LED berkedip sangat cepat), maka:

* Program memberikan jeda `delay(3000)`
* Nilai `timeDelay` di-reset ke 1000

---

#### 2. Pada kondisi apa program masuk ke blok `else`?

Program masuk ke blok `else` ketika:

```
timeDelay > 100
```

Pada kondisi ini:

* Nilai `timeDelay` dikurangi 100
* LED akan berkedip semakin cepat secara bertahap

---

#### 3. Apa fungsi `delay(timeDelay)`?

Fungsi `delay(timeDelay)` digunakan untuk:

* Memberikan jeda waktu dalam milidetik
* Mengatur kecepatan kedipan LED

Keterangan:

* Delay besar → LED lambat
* Delay kecil → LED cepat

---

### 💻 Program Modifikasi (Cepat → Sedang → Mati)

```cpp
const int ledPin = 6;      // Menentukan pin LED
int timeDelay = 1000;      // Delay awal (lambat)
bool faseTurun = true;     // Penanda arah perubahan

void setup() {
  pinMode(ledPin, OUTPUT); // Set pin sebagai output
}

void loop() {
  digitalWrite(ledPin, HIGH); // LED menyala
  delay(timeDelay);

  digitalWrite(ledPin, LOW);  // LED mati
  delay(timeDelay);

  if (faseTurun) {
    timeDelay -= 100; // Mempercepat

    if (timeDelay <= 100) {
      faseTurun = false; // Ubah ke fase melambat
    }
  } else {
    timeDelay += 100; // Memperlambat

    if (timeDelay >= 1000) {
      delay(2000);      // Jeda sebelum mati
      timeDelay = 1000; // Reset
      faseTurun = true; // Ulang siklus
    }
  }
}
```

---

### 🧠 Penjelasan Program

* `faseTurun = true` → LED semakin cepat
* Saat delay minimum → arah berubah menjadi melambat
* Setelah kembali lambat → LED berhenti sejenak lalu mengulang
* Pola: **lambat → cepat → sedang → mati → ulang**

---

## 🔹 Percobaan 2A: Perulangan (Looping)

### 📌 Tujuan

Memahami penggunaan perulangan (`for`) untuk membuat efek running LED.

---

### 🔌 Rangkaian

* LED 1 → Pin 2
* LED 2 → Pin 3
* LED 3 → Pin 4
* LED 4 → Pin 5
* LED 5 → Pin 6
* LED 6 → Pin 7
* Semua LED menggunakan resistor 220Ω
* Kaki negatif LED → GND

---

### ❓ Pertanyaan & Jawaban

#### 1. Bagaimana efek LED berjalan dari kiri ke kanan?

Menggunakan perulangan:

```cpp
for (int ledPin = 2; ledPin < 8; ledPin++)
```

Penjelasan:

* Dimulai dari pin kecil ke besar (2 → 7)
* LED menyala satu per satu
* Memberikan efek berjalan ke kanan

---

#### 2. Bagaimana efek LED dari kanan ke kiri?

Menggunakan perulangan:

```cpp
for (int ledPin = 7; ledPin >= 2; ledPin--)
```

Penjelasan:

* Dimulai dari pin besar ke kecil (7 → 2)
* LED menyala berurutan
* Memberikan efek berjalan ke kiri

---

### 💻 Program LED 3 Kiri & 3 Kanan Bergantian

```cpp
int timer = 500; // Waktu delay

void setup() {
  for (int pin = 2; pin <= 7; pin++) {
    pinMode(pin, OUTPUT); // Set semua pin sebagai output
  }
}

void loop() {
  // Nyalakan LED kiri
  digitalWrite(2, HIGH);
  digitalWrite(3, HIGH);
  digitalWrite(4, HIGH);

  // Matikan LED kanan
  digitalWrite(5, LOW);
  digitalWrite(6, LOW);
  digitalWrite(7, LOW);

  delay(timer);

  // Matikan semua LED
  for (int pin = 2; pin <= 7; pin++) {
    digitalWrite(pin, LOW);
  }

  // Nyalakan LED kanan
  digitalWrite(5, HIGH);
  digitalWrite(6, HIGH);
  digitalWrite(7, HIGH);

  // Matikan LED kiri
  digitalWrite(2, LOW);
  digitalWrite(3, LOW);
  digitalWrite(4, LOW);

  delay(timer);

  // Reset semua LED
  for (int pin = 2; pin <= 7; pin++) {
    digitalWrite(pin, LOW);
  }
}
```

---

### 🧠 Penjelasan Program

* LED dibagi menjadi dua bagian:

  * Kiri → pin 2, 3, 4
  * Kanan → pin 5, 6, 7
* Program menyalakan kiri → mati → kanan → mati
* Menghasilkan efek **bergantian kiri dan kanan**

---

## 📊 Kesimpulan

* Percabangan (`if-else`) digunakan untuk mengatur logika perubahan kecepatan
* Perulangan (`for`) digunakan untuk membuat pola LED otomatis
* Kombinasi keduanya memungkinkan pembuatan animasi LED yang lebih kompleks

---

## ✨ Catatan

Kecepatan LED dapat diubah dengan mengganti nilai:

```
timeDelay atau timer
```

---
