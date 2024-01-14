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

![hasil-plot](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/2-plot.jpg)

## Omnidirectional
## Binary Occupancy Map
## Pathplanning
## Pathtracking


# Simulink