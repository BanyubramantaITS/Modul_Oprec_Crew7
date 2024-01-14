## Daftar Isi

- [Instalasi MATLAB R2023b](#instalasi-matlab-r2023)
    + [Instalasi MATLAB R2023b Windows 10/11](#instalasi-matlab-r2023b-windows-10/11)
    + [Instalasi MATLAB R2023b Linux Ubuntu 22.04 LTS](#instalasi-matlab-r2023b-linux-ubuntu-22.04-lts)

- [Script](#script)
    + [Syntax Dasar](#syntax-dasar)
    + [Plot](#plot)
    + [Binary Occupancy Map](#binary-occupancy-map)
    + [Pathplanning](#pathplanning)
    + [Pathtracking](#pathtracking)

- [Simulink](#simulink)
    + [Diagram Blok Dasar](#diagram-blok-dasar)
    + [ROS2 Toolbox](#ros2-toolbox)
    + [Matlab Function](matlab-function)
    + [Pathplanning di Simulink](#pathplanning-di-simulink)

# Instalasi MATLAB R2023b

## Instalasi MATLAB R2023b Windows 10/11

Sign up akun MATLAB di https://www.mathworks.com/ menggunakan akun email ITS

![signup-account-matlab](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/1-1.png)

Download installer MATLAB R2023b untuk Windows di https://www.mathworks.com/downloads/

![download-installer-matlab](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/1-2.png)

Sign in & Install MATLAB R2023b sesuai lokasi yang diinginkan

Centang Toolbox dengan pilihan berikut :
- Simulink
- Audio Toolbox
- Computer Vision Toolbox
- Control System Toolbox
- HDL Coder
- Image Processing Toolbox
- Navigation Toolbox
- ROS Toolbox
- Robotics System Toolbox
- Simulink Desktop Real-Time
- Symbolic Math Toolbox

Jika ingin menambah toolbox diluar itu opsional

![toolbox-check-matlab](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/1-3.jpg)

MATLAB R2023b sudah dapat dijalankan

## Instalasi MATLAB R2023b di Linux Ubuntu 22.04 LTS

Sign up akun MATLAB di https://www.mathworks.com/ menggunakan akun email ITS

![signup-account-matlab](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/1-1.png)

Download installer MATLAB R2023b untuk Linux di https://www.mathworks.com/downloads/

![download-installer-linux-matlab](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/1-4.png)

Extract Zip File dengan masuk ke direktori download & install unzip

```
cd Downloads\
sudo apt install unzip
mkdir matlab
unzip -qq matlab*.zip -d matlab
```

Masuk ke direktori matlab/ dan install MATLAB
```
cd matlab\
sudo ./install
```

Sign in & Install MATLAB R2023b sesuai lokasi yang diinginkan

Centang Toolbox dengan pilihan berikut :
- Simulink
- Audio Toolbox
- Computer Vision Toolbox
- Control System Toolbox
- HDL Coder
- Image Processing Toolbox
- Navigation Toolbox
- ROS Toolbox
- Robotics System Toolbox
- Simulink Desktop Real-Time
- Symbolic Math Toolbox

Jika ingin menambah toolbox diluar itu opsional

![toolbox-check-matlab](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/1-3.jpg)

Create MATLAB Symbolic Link, dengan
```
sudo ln -s /usr/local/MATLAB/R2020b/bin/matlab /usr/local/bin/matlab
```

MATLAB R2023b sudah dapat dijalankan dengan cara launch dari terminal
```
matlab
```

# Script

## Syntax Dasar

Beberapa syntax dasar yang digunakan di MATLAB diantaranya

|     Syntax      |                                      Syntax                                      |
|-----------------|:---------------------------------------------------------------------------------|
| `clc`           | Untuk membersihkan Command Window dan posisi kursor                              |
| `load`          | Untuk membaca data dari file.mat dan memasukkannya ke dalam workspace matlab     |
| `sound`         | Untuk memutar audio yang ada dalam vektor atau matriks                           |
| `imshow`        | Untuk menampilkan gambar atau citra yang telah dimuat ke dalam workspace MATLAB  |
| `title`         | Untuk menampilkan gambar atau citra yang telah dimuat ke dalam workspace MATLAB  |
| `plot`          | Untuk membuat grafik atau plot data                                              |
| `subplot`       | Untuk membuat tata letak subplot dalam satu gambar                               |

## Plot

Plot digunakan untuk membuat grafik atau data dari suatu sinyal atau data yang berubah secara waktu kontinu maupun diskrit

Contoh

```
clc
load train.mat % Membuka file suara bawaan Matlab
whos           % Menampilkan informasi sinyal suara
sound(y,Fs)    % Memainkan file suara
plot(y)        % Menampilkan kurva sinyal suara
```

Maka hasilnya

![hasil-plot](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/2-plot.png)

## Omnidirectional

Gerak omnidireksional adalah Gerakan yang mampu ke segala arah. Secara umum memiliki 3-DoF serta dapat dikontrol dengan PID. Secara penggunaan juga lebih efisien, padat menggunakan 3 atau 4 penggerak saja untuk mencapainya

Pada desain AUV/ROV dengan konfigurasi thruster 45 derajat maka θ = π/4. Jika 60 derajat maka perlu penyesuaian sudut

![konfigurasi-4-thruster](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/2-2-1.jpg)

Terdapat 2 cara untuk mencari perhitungan Omnidirectional

### 1. Inverse-Pseudo Jacobian Matrix

Untuk mencari Vx, Vy, dan ω apabila diketahui V1, V2, V3, V4 dapat dengan rumus berikut

![persamaan-perhitungan-vx-vy-w](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/2-2-2.png)

atau dapat dengan metode augmentasi matrix

![matrix-perhitungan-vx-vy-w](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/2-2-3.png)

Sebaliknya, Untuk mencari V1, V2, V3, V4 apabila diketahui Vx, Vy, dan ω dapat dengan rumus berikut

![matrix-inverse-pseudo](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/2-2-4.png)

### 2. Simple Kinematic

Ada satu cara lagi yang dapat digunakan untuk mengkalkulasi Gerakan omni secara mudah tanpa menggunakan pseudo-inverse

Dimana perhitungan hanya mengandalkan perkalian matriks sederhana sehingga secara program lebih sederhana

![simple-kinematic-matrix-equation](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/2-2-5.png)

Jika konfigurasi thruster 45 derajat atau π/4, maka

![simple-kinematic-matrix-45-degree](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/2-2-6.png)

## Binary Occupancy Map
## Pathplanning
## Pathtracking


# Simulink