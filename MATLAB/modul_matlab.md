## Daftar Isi

- [Instalasi MATLAB R2023b](#instalasi-matlab-r2023)
    + [Instalasi MATLAB R2023b Windows 10/11](#instalasi-matlab-r2023b-windows-10/11)
    + [Instalasi MATLAB R2023b Linux Ubuntu 22.04 LTS](#instalasi-matlab-r2023b-linux-ubuntu-22.04-lts)

- [Script](#script)
    + [Syntax Dasar](#syntax-dasar)
    + [Plot](#plot)
    + [Omnidirectional](#omnidirectional)
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

Dengan menggunakan matriks tersebut, maka untuk menghitung V1, V2, V3, V4 menggunakan Inverse-Pseudo Jacobian Matrix yaitu

```
syms x vx vy w v1 v2 v3 v4 l;
l = 0.25;

% parameter gerakan
vx = 10;
vy = 10;
w = 2;
x = pi/4;

%kecepatan thruster
Vwheel =   [v1;
            v2;
            v3;
            v4];
%kecepatan robot yang diinginkan
Vdesired = [vx;
            vy;
            -w*l];

%Pseudo-Inverse Jacobian Matrix
J = [sin(x), -cos(x), -sin(x), cos(x);
    -cos(x), -sin(x), cos(x), cos(x);
    1,      1,      1,      1];
Jinv = pinv(J);

%hasil perkalian matrix
K = Jinv*Vdesired;
disp("Pseudo-inverse dari J");
disp(Jinv);

disp("Hasil kecepatan tiap penggerak");
disp(K);
```

### 2. Simple Kinematic

Ada satu cara lagi yang dapat digunakan untuk mengkalkulasi Gerakan omni secara mudah tanpa menggunakan pseudo-inverse

Dimana perhitungan hanya mengandalkan perkalian matriks sederhana sehingga secara program lebih sederhana

![simple-kinematic-matrix-equation](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/2-2-5.png)

Jika konfigurasi thruster 45 derajat atau π/4, maka

![simple-kinematic-matrix-45-degree](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/2-2-6.png)

Dengan menggunakan matriks tersebut, maka untuk menghitung V1, V2, V3, V4 menggunakan metode kedua yaitu

```
syms R x vx vy w v1 v2 v3 v4 l;

R = 0.25;

vx = -10;
vy = 20;
vt = 3;

Vwheel =   [v1;
            v2;
            v3;
            v4];

Vdesired = [vx;
            vy;
            vt];

J = [sin(pi/4), cos(pi/4), R;
    sin(pi*(3/4)), cos(pi*(3/4)), R;
    sin(pi*(5/4)), cos(pi*(5/4)), R;
    sin(pi*(7/4)), cos(pi*(7/4)), R];

K = J*Vdesired;

disp(K);
```

## Binary Occupancy Map

### Definisi

BinaryOccupancyMap membuat objek occupancy map 2-D, yang dapat kita gunakan untuk merepresentasikan dan memvisualisasikan ruang kerja robot, termasuk rintangan. Integrasi data sensor dan estimasi posisi menciptakan representasi spasial dari perkiraan lokasi rintangan.

Occupancy grid digunakan dalam algoritme robotika seperti perencanaan jalur yang juga digunakan dalam aplikasi pemetaan, seperti untuk menemukan jalur bebas obstacle, melakukan penghindaran tabrakan, dan menghitung mapping lokalisasi. kita dapat memodifikasi Occupancy grid agar sesuai dengan aplikasi spesifik kita.

Setiap sel dalam occupancy grid memiliki nilai yang merepresentasikan status okupansi sel tersebut. Lokasi yang ditempati direpresentasikan sebagai TRUE (1) dan lokasi kosong direpresentasikan sebagai FALSE (0).

Objek terus mentracking tiga kerangka referensi: map, lokalisasi, dan, grid. Asal frame map didefinisikan oleh GridLocationInWorld, yang mendefinisikan mulai dari sudut kiri bawah occupancy map relatif terhadap frame map. Properti LocalOriginInWorld menentukan lokasi asal frame lokal relatif terhadap frame map. Lokasi grid pertama dengan indeks (1,1) dimulai di sudut kiri atas grid

Contoh Binary Occupancy Map

![occupancy-map](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/SAUVC_Map.png)

### Syntax

map = binaryOccupancyMap

map = binaryOccupancyMap(width,height)

map = binaryOccupancyMap(width,height,resolution)

map = binaryOccupancyMap(rows,cols,resolution,"grid")

map = binaryOccupancyMap(p)

map = binaryOccupancyMap(p,resolution)

map = binaryOccupancyMap(sourcemap)

map = binaryOccupancyMap(sourcemap,resolution)

### Dokumentasi

Seluruh dokumentasi dapat dilihat di : https://www.mathworks.com/help/nav/ref/binaryoccupancymap.html

## Pathplanning

### Simulasi Path Planning dengan Mobile Robot

Buat skenario untuk mensimulasikan robot bergerak yang menavigasi ruangan. Contoh ini menunjukkan cara membuat skenario, mendapatkan binary occupancy map dari skenario, dan merencanakan jalur yang harus diikuti oleh robot bergerak menggunakan algoritme perencanaan jalur mobileRobotPRM.

```
openExample('robotics/PerformPathPlanningSimulationWithMobileRobotExample')
```

#### Membuat Scenario dengan Ground Plane dan Static Meshes

objek robotScenario terdiri dari sekumpulan obstacle statis dan objek bergerak yang disebut platform. Gunakan objek robotPlatform untuk memodelkan robot bergerak di dalam scenario. Contoh ini membuat skenario yang terdiri dari bidang tanah dan jaring kotak untuk membuat ruangan.

```
scenario = robotScenario(UpdateRate=5);
```

tambahkan mesh datar sebagai alas atau ground dari scenario

```
floorColor = [0.5882 0.2941 0];
addMesh(scenario,"Plane",Position=[5 5 0],Size=[10 10],Color=floorColor);
```

Dinding ruangan dimodelkan sebagai kotak mesh. Mesh statis ditambahkan dengan nilai IsBinaryOccupied sebagai TRUE, sehingga obstacle akan dimasukkan kedalam binary occupancy map yang akan digunakan dalam path planning.

```
wallHeight = 1;
wallWidth = 0.25;
wallLength = 10;
wallColor = [1 1 0.8157];

% Add outer walls.
addMesh(scenario,"Box",Position=[wallWidth/2, wallLength/2, wallHeight/2],...
    Size=[wallWidth, wallLength, wallHeight],Color=wallColor,IsBinaryOccupied=true);
addMesh(scenario,"Box",Position=[wallLength-wallWidth/2, wallLength/2, wallHeight/2],...
    Size=[wallWidth, wallLength, wallHeight],Color=wallColor,IsBinaryOccupied=true);
addMesh(scenario,"Box",Position=[wallLength/2, wallLength-wallWidth/2, wallHeight/2],...
    Size=[wallLength, wallWidth, wallHeight],Color=wallColor,IsBinaryOccupied=true);
addMesh(scenario,"Box",Position=[wallLength/2, wallWidth/2, wallHeight/2],...
    Size=[wallLength, wallWidth, wallHeight],Color=wallColor,IsBinaryOccupied=true);

% Add inner walls.
addMesh(scenario,"Box",Position=[wallLength/8, wallLength/3, wallHeight/2],...
    Size=[wallLength/4, wallWidth, wallHeight],Color=wallColor,IsBinaryOccupied=true);
addMesh(scenario,"Box",Position=[wallLength/4, wallLength/3, wallHeight/2],...
    Size=[wallWidth, wallLength/6,  wallHeight],Color=wallColor,IsBinaryOccupied=true);
addMesh(scenario,"Box",Position=[(wallLength-wallLength/4), wallLength/2, wallHeight/2],...
   Size=[wallLength/2, wallWidth, wallHeight],Color=wallColor,IsBinaryOccupied=true);
addMesh(scenario,"Box",Position=[wallLength/2, wallLength/2, wallHeight/2],...
    Size=[wallWidth, wallLength/3, wallHeight],Color=wallColor,IsBinaryOccupied=true);
```

Visualisasi scenario yang telah dibuat

```
show3D(scenario);
lightangle(-45,30);
view(60,50);
```

![scenario-map](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/3-1-1.png)

#### Mendapatkan Bentuk Binary Occupancy Map dari Scenario

Mendapatkan bentuk binary occupancy map dengan fungsi binaryOccupancyMap dari scenario untuk path planning. Kemudian memperbesar ruang untuk obstacle (occupied map) pada map sebesar 0.3 m.

```
map = binaryOccupancyMap(scenario,GridOriginInLocal=[-2 -2],...
                                           MapSize=[15 15],...
                                           MapHeightLimits=[0 3]);
inflate(map,0.3);
```

Visualisasi 2D occupancy map

```
show(map)
```

![binary-map](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/3-1-2.png)

#### Proses Path Planning

Gunakan mobileRobotPRM sebagai path planner untuk mencari jalur bebas obstacle diantara posisi start dan goal pada occupancy map

```
startPosition = [1 1];
goalPosition = [8 8];
```

Atur rng seed

```
rng(100)
```

Buat objek mobileRobotPRM dengan memberikan argumen binary occupancy map dan spesifikasikan maksimum node yang akan digunakan. Kemudian berikan jarak maksimum diantara node yang terhubung.

```
numnodes = 2000;
planner = mobileRobotPRM(map,numnodes);
planner.ConnectionDistance = 1;
```

Cari waypoints pada jalur bebas obstacle

```
waypoints = findpath(planner,startPosition,goalPosition);
```

#### Membuat Lintasan

Buat lintasan untuk mobile robot agar dapat mengikuti waypoints yang telah dihasilkan path planning menggunakan sistem waypointTrajectory.

```
% Robot height from base.
robotheight = 0.12;
% Number of waypoints.
numWaypoints = size(waypoints,1);
% Robot arrival time at first waypoint.
firstInTime = 0;
% Robot arrival time at last waypoint.
lastInTime = firstInTime + (numWaypoints-1);
% Generate waypoint trajectory with waypoints from planned path.
traj = waypointTrajectory(SampleRate=10,...
                          TimeOfArrival=firstInTime:lastInTime, ...
                          Waypoints=[waypoints, robotheight*ones(numWaypoints,1)], ...
                          ReferenceFrame="ENU");
```

#### Tambahkan Platform Robot pada Scenario

Tambahkan mobile robot Clearpath Husky dari libary robot sebagi objek rigidBodyTree.

```
huskyRobot = loadrobot("clearpathHusky");
```

Buat objek robotPlatform dengan model robot yang telah dispesifikasikan pada rigidBodyTree dan jalur yang telah dispesifikasikan pada waypointTrajectory.

```
platform = robotPlatform("husky",scenario, RigidBodyTree=huskyRobot,...
                         BaseTrajectory=traj);
```

Visualisasi scenario dengan robot

```
[ax,plotFrames] = show3D(scenario);
lightangle(-45,30)
view(60,50)
```

![visualization-robot](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/3-1-3.png)

#### Simulasi Mobile Robot

Visualisasi jalur path planning

```
hold(ax,"on")
plot(ax,waypoints(:,1),waypoints(:,2),"-ms",...
               LineWidth=2,...
               MarkerSize=4,...
               MarkerEdgeColor="b",...
               MarkerFaceColor=[0.5 0.5 0.5]);
hold(ax,"off")
```

Setup simulasi yang diinginkan

```
setup(scenario)

% Control simulation rate at 20 Hz.
r = rateControl(20);

% Status of robot in simulation.
robotStartMoving = false;

while advance(scenario)
    show3D(scenario,Parent=ax,FastUpdate=true);
    waitfor(r);

    currentPose = read(platform);
    if ~any(isnan(currentPose))
        % implies that robot is in the scene and performing simulation.
        robotStartMoving = true;
    end
    if any(isnan(currentPose)) && robotStartMoving
        % break, once robot reaches goal position.
        break;
    end
end
```

![simulation-visualization](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/3-1-4.png)

Untuk melakukan simulasi dan visualisasi ulang, reset simulasi scenario

```
restart(scenario)
```

## Pathtracking

Path tracking adalah metode navigasi dalam robot yang menginputkan waypoint-waypoint tujuan dan akan mengoutputkan velocity dan heading terhadap titik waypoint. Algoritma path tracking yang paling umum adalah Pure Pursuit Controller. Algoritma ini menghitung perintah kecepatan sudut yang menggerakkan robot dari posisinya saat ini untuk mencapai beberapa titik di depan robot. Kecepatan linier diasumsikan konstan, sehingga kita dapat mengubah kecepatan linier robot pada titik mana pun. Algoritme kemudian memindahkan titik lihat ke depan pada jalur berdasarkan posisi robot saat ini hingga titik terakhir dari jalur tersebut. Kita dapat menganggap ini sebagai robot yang terus mengejar titik di depannya. Properti LookAheadDistance menentukan seberapa jauh titik lihat-depan ditempatkan.

### Look Ahead Distance Properties

Properti LookAheadDistance adalah properti tuning utama untuk pengontrol. Look ahead distance berarti seberapa jauh robot harus melihat ke depan dari lokasi saat ini untuk menghitung perintah kecepatan sudut. Gambar di bawah ini menunjukkan robot dan titik pandangan ke depan. Seperti yang ditampilkan pada gambar ini, perhatikan bahwa jalur yang sebenarnya tidak sesuai dengan garis lurus di antara titik-titik jalan.

![look-ahead-properties](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/3-2-1.png)

Efek dari mengubah parameter ini dapat mengubah cara robot kita melacak jalur dan ada dua tujuan utama: mendapatkan kembali jalur dan mempertahankan jalur. Untuk mendapatkan kembali jalur di antara titik-titik jalan dengan cepat, LookAheadDistance yang kecil akan menyebabkan robot Anda bergerak dengan cepat menuju jalur tersebut. Namun, seperti yang dapat dilihat pada gambar di bawah ini, robot melampaui jalur dan berosilasi di sepanjang jalur yang diinginkan. Untuk mengurangi osilasi di sepanjang jalur, jarak pandang ke depan yang lebih besar dapat dipilih, namun hal ini dapat menghasilkan lengkungan yang lebih besar di dekat sudut.

![big-and-small-look-ahead](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/3-2-2.png)


# Simulink

## Model

Dalam simulasi model ROS2 ini, kita akan menggunakan Simulink untuk mempublikasikan lokasi X dan Y dari sebuah robot. Kita juga akan men-subscribe topic lokasi yang sama dan menampilkan lokasi X,Y yang diterima.

Masukkan perintah berikut untuk membuka model yang telah selesai dibuat pada contoh.

```
open_system('ros2GetStartedExample');
```

## Create a Publisher

Konfigurasikan sebuah blok untuk mengirimkan pesan geometry_msgs/Point ke sebuah topik bernama /location.

- Dari Toolstrip MATLAB, pilih Home > New > Simulink Model untuk membuka model Simulink baru.

- Dari Simulink Toolstrip, pilih Simulation > Library Browser untuk membuka Simulink Library Browser. Klik pada tab ROS Toolbox (Anda juga bisa mengetik roslib pada command window MATLAB). Pilih ROS 2 Library.

- Seret blok Publish ke model. Klik dua kali pada blok tersebut untuk mengonfigurasi topik dan tipe pesan.

- Pilih Tentukan sendiri untuk sumber Topik, dan masukkan /location pada Topik.

- Klik Pilih di samping Jenis pesan. Sebuah jendela pop-up akan muncul. Pilih geometry_msgs/Point dan klik OK untuk menutup jendela pop-up.

- Anda juga dapat menentukan ID Domain ROS 2 dengan mengklik opsi Configure ROS 2 Domain ID and ROS Middleware (RMW).

![create-publisher](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/4-1.png)

## Create ROS2 Message

Buat pesan ROS 2 kosong dan isi dengan lokasi x dan y untuk jalur robot. Kemudian publikasikan pesan ROS 2 yang telah diperbarui ke jaringan ROS 2.

Pesan ROS 2 direpresentasikan sebagai sinyal bus di Simulink. Sinyal bus adalah kumpulan sinyal Simulink, dan juga dapat menyertakan sinyal bus lainnya (lihat contoh Jelajahi Kemampuan Bus Simulink (Simulink) untuk mendapatkan gambaran umum). Blok ROS 2 "Blank Message" mengeluarkan sinyal bus Simulink yang sesuai dengan pesan ROS 2.

- Klik tab ROS Toolbox pada Library Browser, atau ketik roslib pada baris perintah MATLAB. Pilih ROS 2 Library.

- Seret blok Blank Message ke model. Klik dua kali pada blok tersebut untuk membuka block mask.

- Klik Select di samping kotak Message type, dan pilih geometry_msgs/Point dari jendela pop-up yang muncul. atur Sample time ke 0.01. Klik OK untuk menutup block mask.

- Dari tab Simulink > Signal Routing pada Library Browser, seret blok Bus Assignment.

- Hubungkan port output dari blok Blank Message ke port input Bus pada blok Bus Assignment. Hubungkan port output dari blok Bus Assignment ke port input blok Publish.

- Klik dua kali pada blok Penugasan Bus. Anda akan melihat x, y, dan z (sinyal-sinyal yang terdiri dari pesan geometry_msgs/Point) yang tercantum di sebelah kiri. Pilih ??? signal1 pada kotak daftar sebelah kanan dan klik Remove. Pilih sinyal X dan Y di kotak daftar sebelah kiri dan klik Select. Klik OK untuk menerapkan perubahan.

NOTE : Jika kalian tidak melihat x, y dan z pada bus, coba tutup blok Bus Assignment dan pada tab Modeling, klik Update Model untuk memastikan informasi bus sudah terintegrasi dengan benar. Jika kalian melihat error, "Selected signal 'singal1' in the Bus Assignment block cannot be found", itu berarti informasi bus masih belum terintegrasi. Coba tutup Diagnostic Viewer, dan ulangi langkah diatas.

Kalian sekarang dapat mengisi sinyal bus dengan lokasi robot.

Dari tab Simulink > Sources pada Library Browser, seret dua blok Gelombang Sinus ke dalam model.

Hubungkan port output dari setiap blok Gelombang Sinus ke port input penugasan x dan y pada blok Penugasan Bus.

Klik dua kali pada blok Gelombang Sinus yang terhubung ke port input X. Atur parameter Fase ke -pi/2 dan klik OK. Biarkan blok Gelombang Sinus yang terhubung ke port input Y sebagai default.

Publisher kalian akan terlihat seperti ini:

![create-msg](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/4-2-1.png)

Pada titik ini, model sudah diatur untuk mempublikasikan pesan ke jaringan ROS 2. kalian dapat memverifikasi ini sebagai berikut:

- Pada tab Simulation, atur waktu penghentian simulasi ke inf.

- Klik Jalankan untuk memulai simulasi. Simulink membuat node ROS 2 khusus untuk model dan penerbit ROS 2 yang sesuai dengan blok Publish.

- Ketika simulasi sedang berjalan, ketik daftar node ros2 pada jendela perintah MATLAB. Daftar ini berisi semua node yang tersedia di jaringan ROS, dan termasuk sebuah node dengan nama seperti /untitled_90580 (nama model beserta nomor acak untuk membuatnya unik).

- Ketika simulasi sedang berjalan, ketik daftar topik ros2 pada jendela perintah MATLAB. Ini akan menampilkan daftar semua topik yang tersedia di jaringan ROS 2, dan termasuk /location.

- Jika Anda menentukan ID domain ROS 2 pada blok Publish, untuk membuat daftar semua topik, ketik ros2 topic list domainID xx, di mana xx adalah ID domain yang Anda tentukan.

![check-topic](https://github.com/BanyubramantaITS/Modul_Oprec_Crew7/blob/main/MATLAB/images/4-2-2.png)

- Klik Stop untuk menghentikan simulasi. Simulink akan menghapus node dan publisher ROS 2. Secara umum, node ROS 2 untuk model dan publisher serta subscriber yang terkait akan dihapus secara otomatis pada akhir simulasi; tidak diperlukan langkah pembersihan tambahan.

## Create a Subscriber

## Configure and Run the Model

## Modify the Model to React Only to New Messages