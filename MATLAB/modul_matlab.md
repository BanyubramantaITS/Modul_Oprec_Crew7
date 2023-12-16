## Daftar Isi

- [Instalasi MATLAB R2023b](#instalasi-matlab)
    + [Instalasi MATLAB R2023b Windows 10/11](#instalasi-matlab-windows)
    + [Instalasi MATLAB R2023b Linux Ubuntu 22.04 LTS](#instlasi-matlab-linux)

- [Script](#pengenalan-script)
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

# Instlasi MATLAB R2023b

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

MATLAB R2023b sudah dapat dijalankan

# Script

# Simulink