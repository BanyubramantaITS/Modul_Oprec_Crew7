# Modul ROS bagian 2

## Memakai colcon untuk build pakages
Pertama-tama kita perlu menginstall colcon
```
sudo apt install python3-colcon-common-extensions
```
### Pengenalan
Workspace ROS adalah direktori dengan struktur tertentu. Biasanya terdapat subdirektori bernama src. Di dalam subdirektori inilah kode sumber paket-paket ROS akan ditempatkan. Biasanya, direktori ini awalnya kosong.

colcon melakukan build di luar sumber kode. Secara default, colcon akan membuat direktori berikut sebagai rekan dari direktori src:

- Direktori build adalah tempat file-file perantara disimpan. Untuk setiap paket, subfolder akan dibuat di mana CMake dijalankan.

- Direktori install adalah tempat setiap paket akan diinstal. Secara default, setiap paket akan diinstal ke subdirektori terpisah.

- Direktori log berisi berbagai informasi pencatatan tentang setiap pemanggilan colcon.

### Membuat sebuah workspace

Pertama, buat direktori (ros2_ws) untuk menampung workspace kita:

```
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
```

Selanjutnya kita akan menggunakan contoh yang sudah disediakan ros2 github. Silakan masuk ke src dengan menggunakan command
```
cd src
```

Untuk mendapatkan contoh ros2 yang akan kita gunakan kita perlu mengexsekusi command berikut.

```
git clone https://github.com/ros2/examples src/examples -b humble
```

kalian bisa lihat apa saja yang sudah ditambahkan pada directory src dengan menggunakan command
```
ls
```
Sekarang kita akan kembali ke directori ros2_ws
```
cd ..
```
. . adalah command untuk keluar 1 directory. Pada step ini anda harusnya berada pada ~/ros2_ws pada terminal anda

Lalu kita akan menggunakan colcon build di terminal
```
colcon build
```
### run test
Setelah itu kita bisa mengetest packages yang telah kita build dengan menggunakan command
```
colcon test
```
lihat apa yang terjadi.

### source environment

Setelah colcon berhasil membangun workspace, hasilnya akan ditempatkan di direktori install. Sebelum Anda dapat menggunakan executable atau pustaka yang diinstal, Anda perlu menambahkannya ke path dan library path Anda. colcon akan menghasilkan file bash/bat di direktori install untuk membantu menyiapkan lingkungan. File-file ini akan menambahkan semua elemen yang diperlukan ke path dan library path Anda, serta menyediakan perintah bash atau shell apa pun yang diekspor oleh packages.

Jalankan command ini dalam terminal yang sama pada path ~/ros2_ws
```
source install/setup.bash
```

### jalankan demo/contoh nya

setelah sourcecing kita bisa menjalankan executables yang ada didalam src nya. Jalankan subscriber node dari demonya

```
ros2 run examples_rclcpp_minimal_subscriber subscriber_member_function
```

lalu buka terminal baru dan jalankan publiser node nya juga (jangan lupa harus masuk path dan sourcecing yang sama seperti tutorial source environment)

```
ros2 run examples_rclcpp_minimal_publisher publisher_member_function
```
Lalu lihat apa yang terjadi.

## Membuat Package

### Background
1.Apa itu ROS 2 Package?

Sebuah paket adalah unit organisasi untuk kode ROS 2 Anda. Jika Anda ingin dapat menginstal kode Anda atau berbagi dengan orang lain, maka Anda perlu mengorganisirnya dalam suatu paket. Dengan paket, Anda dapat merilis pekerjaan ROS 2 Anda dan memungkinkan orang lain untuk membangun dan menggunakannya dengan mudah.

Pembuatan paket dalam ROS 2 menggunakan ament sebagai sistem buildnya dan colcon sebagai alat buildnya. Anda dapat membuat paket menggunakan CMake atau Python, yang secara resmi didukung, meskipun jenis pembangunan lainnya juga ada.

2.Apa yang membentuk sebuah ROS 2 package?

Paket Python dan CMake ROS 2 masing-masing memiliki requirement minimum yang diperlukan sendiri:

untuk CMake
```
my_package/
     CMakeLists.txt
     include/my_package/
     package.xml
     src/
```

dan untuk python
```
my_package/
      package.xml
      resource/my_package
      setup.cfg
      setup.py
      my_package/
```

### Task

#### 1. Membuat package

Pertama pastikan kalian sudah mengsource ROS 2 nya

Mari kita gunakan workspace yang sudah kalian buat di tutorial sebelumnya yaitu ros2_ws. Pastikan anda sudah berada di folder src sebelum menjalankan command untuk membuat package

```
cd ~/ros2_ws/src
```

Syntax command untuk membuat package di ROS 2 adalah 
```
ros2 pkg create --build-type ament_cmake --license Apache-2.0 <package_name>
```
(package_name) kita ubah menjadi nama yang kita inginkan.


Untuk tutorial ini, Anda akan menggunakan argumen opsional --node-name yang membuat eksekutor(executaable) sederhana tipe Hello World di dalam paket.

Masukan command ini ke dalam terminal
```
ros2 pkg create --build-type ament_cmake --license Apache-2.0 --node-name my_node my_package --license Apache-2.0
```

Sekarang anda akam memiliki folder baru di dalam src yang bernama my_package.

Setelah menjalankan command tersebut, terminal anda akan mengreturn pesan seperti ini
```
going to create a new package
package name: my_package
destination directory: /home/user/ros2_ws/src
package format: 3
version: 0.0.0
description: TODO: Package description
maintainer: ['<name> <email>']
licenses: ['TODO: License declaration']
build type: ament_cmake
dependencies: []
node_name: my_node
creating folder ./my_package
creating ./my_package/package.xml
creating source and include folder
creating folder ./my_package/src
creating folder ./my_package/include/my_package
creating ./my_package/CMakeLists.txt
creating ./my_package/src/my_node.cpp
```
Dapat dilihat bahwa command yang kita jalankan membuat folder baru.

#### 2. Mengbuild package

Untuk mengbuild sebuah package yang sudah kita buat kita perlu kembali ke akar workspace yang kita buat. Pada tutorial ini untuk kembali ke akar workspace kita bisa memasukkan command ini ke dalam terminal
```
cd ~/ros2_ws
```
Lalu sekarang kita dapat mengbuild package yang kita buat sebelumnya dengan command ini
```
colcon build
```

note*
Jika ingin mengbuild satu package yang spesifik, kita dapat menggunakan command ini
```
colcon build --packages-select my_package
```
(my_package) anda ganti menjadi nama package anda.

#### 3. Mengsource file setup

Kita perlu mengsource file setup kita supaya kita dapat menjalankan package yang ada di dalam workspace ini. Untuk mengsource file setup ini kita perlu menginputkan command ini
```
source install/local_setup.bash
```

lalu untuk menjalankan package kita, kita dapat menggunakan syntax command ini
```
ros2 run my_package my_node
```
note* jika ingin menjalankan package lain, kalian tinggal mengubah my_package menjadi nama package kalian dan mengubah my_node menjadi nama node kalian.

Setelah menjalankan command tersebut terminal akan mengoutputkan seperti ini
```
hello world my_package package
```
Jika sudah keluar seperti itu berarti kalian sudah berhasill yeayyy <3

## Membuat publisher dan subscriber simpel (C++)
### Background
Node adalah proses eksekusi yang berkomunikasi melalui graf ROS. Dalam tutorial ini, node akan mengirimkan informasi dalam bentuk pesan string satu sama lain melalui suatu topik. Contoh yang digunakan di sini adalah sistem "talker" dan "listener" sederhana; satu node mempublikasikan data dan yang lainnya berlangganan topik tersebut sehingga dapat menerima data tersebut.

Kode yang digunakan dalam contoh ini dapat ditemukan di sini.
https://github.com/ros2/examples/tree/humble/rclcpp/topics

### Task
#### 1. Membuat Package
Buka terminal baru lalu masuk ke workspace ros_ws yang sudah kita buat di tutorial sebelumnya. Lalu masuk ke folder src
```
cd ~/ros2_ws/src
```

Jika sudah kita akan membuat sebuah package baru untuk tutorial ini. Masukkan command ini ke terminal
```
ros2 pkg create --build-type ament_cmake --license Apache-2.0 cpp_pubsub
```

lalu masuk ke src package yang barusan kita buat. 
```
cd ~/ros2_ws/src/cpp_pubsub/src
```
Tampilan pada terminal harusnya sudah seperti ini (~/ros2_ws/src/cpp_pubsub/src).

Lalu mari kita download contoh kode talker
```
wget -O publisher_member_function.cpp https://raw.githubusercontent.com/ros2/examples/humble/rclcpp/topics/minimal_publisher/member_function.cpp
```
Akan ada file baru pada src anda bernama publisher_member_function.cpp. Lalu buka dengan text editor yang anda prefer. Untuk ini saya merekomendasikan mengdownload vscode pada ubuntu anda. Untuk mengdownload vscode bisa langsung pada terminal dengan mengikuti tutorial ini https://phoenixnap.com/kb/install-vscode-ubuntu  . Kalian tinggal mengikuti salah satu cara yang ada pada website tersebut.

Jika sudah menginstall vscode kalian bisa membuka sebuah workspace hanya dengan masuk ke path file workspace yang ingin kita buka pada terminal lalu memasukan command ini

```
code .
```
command ini digunakan vscode untuk membuka path file dimana anda berada saat ini di terminal.

Jika anda lihat di file yang barusan kita download dari ROS, kode akan seperti ini

```
#include <chrono>
#include <functional>
#include <memory>
#include <string>

#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

using namespace std::chrono_literals;

/* This example creates a subclass of Node and uses std::bind() to register a
* member function as a callback from the timer. */

class MinimalPublisher : public rclcpp::Node
{
  public:
    MinimalPublisher()
    : Node("minimal_publisher"), count_(0)
    {
      publisher_ = this->create_publisher<std_msgs::msg::String>("topic", 10);
      timer_ = this->create_wall_timer(
      500ms, std::bind(&MinimalPublisher::timer_callback, this));
    }

  private:
    void timer_callback()
    {
      auto message = std_msgs::msg::String();
      message.data = "Hello, world! " + std::to_string(count_++);
      RCLCPP_INFO(this->get_logger(), "Publishing: '%s'", message.data.c_str());
      publisher_->publish(message);
    }
    rclcpp::TimerBase::SharedPtr timer_;
    rclcpp::Publisher<std_msgs::msg::String>::SharedPtr publisher_;
    size_t count_;
};

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<MinimalPublisher>());
  rclcpp::shutdown();
  return 0;
}
```

#### 2.1 Periksa kode
Bagian atas kode mencakup header C++ standar yang akan Anda gunakan. Setelah header C++ standar, ada inklusi rclcpp/rclcpp.hpp yang memungkinkan Anda menggunakan bagian-bagian paling umum dari sistem ROS 2. Terakhir adalah std_msgs/msg/string.hpp, yang mencakup jenis pesan bawaan yang akan Anda gunakan untuk mempublikasikan data.
```
#include <chrono>
#include <functional>
#include <memory>
#include <string>

#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

using namespace std::chrono_literals;
```

Baris-baris ini merepresentasikan dependensi node. Ingatlah bahwa dependensi harus ditambahkan ke package.xml dan CMakeLists.txt, yang akan Anda lakukan pada bagian berikutnya.

Baris selanjutnya membuat kelas node MinimalPublisher dengan mewarisi dari rclcpp::Node. Setiap "this" dalam kode mengacu pada node.
```
class MinimalPublisher : public rclcpp::Node
```

Konstruktor publik menamai node minimal_publisher dan menginisialisasi count_ menjadi 0. Di dalam konstruktor, penerbit diinisialisasi dengan tipe pesan String, nama topik "topic", dan ukuran antrian yang diperlukan untuk membatasi pesan dalam kasus adanya backlog. Selanjutnya, timer_ diinisialisasi, yang menyebabkan fungsi timer_callback dieksekusi dua kali setiap detik.

```
public:
  MinimalPublisher()
  : Node("minimal_publisher"), count_(0)
  {
    publisher_ = this->create_publisher<std_msgs::msg::String>("topic", 10);
    timer_ = this->create_wall_timer(
    500ms, std::bind(&MinimalPublisher::timer_callback, this));
  }
```

Fungsi timer_callback adalah tempat data pesan diatur dan pesan sebenarnya dipublikasikan. Macro RCLCPP_INFO memastikan setiap pesan yang dipublikasikan dicetak ke konsol.
```
private:
  void timer_callback()
  {
    auto message = std_msgs::msg::String();
    message.data = "Hello, world! " + std::to_string(count_++);
    RCLCPP_INFO(this->get_logger(), "Publishing: '%s'", message.data.c_str());
    publisher_->publish(message);
  }
```
Terakhir adalah deklarasi timer, publisher, dan counter.

```
rclcpp::TimerBase::SharedPtr timer_;
rclcpp::Publisher<std_msgs::msg::String>::SharedPtr publisher_;
size_t count_;
```

Setelah kelas MinimalPublisher, ada fungsi main, di mana node sebenarnya dijalankan. rclcpp::init menginisialisasi ROS 2, dan rclcpp::spin memulai pemrosesan data dari node, termasuk pemanggilan kembali dari timer.
```
int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<MinimalPublisher>());
  rclcpp::shutdown();
  return 0;
}
```

#### 2.2 Menambah dependencies
Masuk ke satu level ke belakang yaitu ke direktori ros2_ws/src/cpp_pubsub, di mana file CMakeLists.txt dan package.xml telah dibuat untuk Anda.

Buka package.xml dengan vscode atau text editor Anda.

Seperti yang disebutkan dalam tutorial sebelumnya, pastikan untuk mengisi tag description, maintainer, dan license:
```
<description>Examples of minimal publisher/subscriber using rclcpp</description>
<maintainer email="you@email.com">Your Name</maintainer>
<license>Apache License 2.0</license>
```

Tambahkan baris baru setelah dependensi buildtool ament_cmake dan tempelkan dependensi berikut sesuai dengan pernyataan inklusi node Anda:

```
<depend>rclcpp</depend>
<depend>std_msgs</depend>
```

Ini mendeklarasikan bahwa paket membutuhkan rclcpp dan std_msgs saat kode-nya dibangun dan dieksekusi.

Pastikan untuk menyimpan file tersebut setelah menambahkan dependensi.

#### 2.3 CMakeLists.txt
Sekarang buka file CMakeLists.txt. Di bawah dependensi find_package(ament_cmake REQUIRED) yang sudah ada, tambahkan baris-baris berikut:
```
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
```

Setelah itu, tambahkan eksekutor dan beri nama talker sehingga Anda dapat menjalankan node Anda menggunakan ros2 run:
```
add_executable(talker src/publisher_member_function.cpp)
ament_target_dependencies(talker rclcpp std_msgs)
```

Terakhir, tambahkan bagian install(TARGETS...) sehingga ros2 run dapat menemukan executable Anda:
```
install(TARGETS
  talker
  DESTINATION lib/${PROJECT_NAME})
```

Anda dapat membersihkan CMakeLists.txt Anda dengan menghapus beberapa bagian dan komentar yang tidak perlu, sehingga terlihat seperti ini:
```
cmake_minimum_required(VERSION 3.5)
project(cpp_pubsub)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)

add_executable(talker src/publisher_member_function.cpp)
ament_target_dependencies(talker rclcpp std_msgs)

install(TARGETS
  talker
  DESTINATION lib/${PROJECT_NAME})

ament_package()
```

Anda dapat build package ini sekarang, seperti pada tutorial build package sebelumnya dan anda dapat menjalankan node talker ini.

Sekarang kita akan membuat node listener nya

#### Subsciber node
Kembalilah ke ros2_ws/src/cpp_pubsub/src untuk membuat node berikutnya. Masukkan kode berikut di terminal Anda:

```
wget -O subscriber_member_function.cpp https://raw.githubusercontent.com/ros2/examples/humble/rclcpp/topics/minimal_subscriber/member_function.cpp
```

Lalu akan muncul file baru. untuk mengeceknya tinggal masukkan command ls ke terminal
```
publisher_member_function.cpp  subscriber_member_function.cpp
```

Buka file subscriber_member_function.cpp dengan vscode atau text editor Anda.

```
#include <memory>

#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"
using std::placeholders::_1;

class MinimalSubscriber : public rclcpp::Node
{
  public:
    MinimalSubscriber()
    : Node("minimal_subscriber")
    {
      subscription_ = this->create_subscription<std_msgs::msg::String>(
      "topic", 10, std::bind(&MinimalSubscriber::topic_callback, this, _1));
    }

  private:
    void topic_callback(const std_msgs::msg::String & msg) const
    {
      RCLCPP_INFO(this->get_logger(), "I heard: '%s'", msg.data.c_str());
    }
    rclcpp::Subscription<std_msgs::msg::String>::SharedPtr subscription_;
};

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<MinimalSubscriber>());
  rclcpp::shutdown();
  return 0;
}
```

#### 3.1 Periksa kode
Kode node subscriber hampir identik dengan penerbit. Sekarang node dinamai minimal_subscriber, dan konstruktor menggunakan kelas create_subscription dari node untuk mengeksekusi panggilan kembali.

Tidak ada timer karena subscriber cukup merespons setiap kali data dipublikasikan ke topik "topic".

```
public:
  MinimalSubscriber()
  : Node("minimal_subscriber")
  {
    subscription_ = this->create_subscription<std_msgs::msg::String>(
    "topic", 10, std::bind(&MinimalSubscriber::topic_callback, this, _1));
  }
```
Ingat dari tutorial topik bahwa nama topik dan jenis pesan yang digunakan oleh publisher dan subscriber harus sesuai agar mereka dapat berkomunikasi.

Fungsi topic_callback menerima data pesan string yang dipublikasikan melalui topik, dan hanya menuliskannya ke konsol menggunakan macro RCLCPP_INFO.

Deklarasi bidang tunggal dalam kelas ini adalah langganan (subscription).

```
private:
  void topic_callback(const std_msgs::msg::String & msg) const
  {
    RCLCPP_INFO(this->get_logger(), "I heard: '%s'", msg.data.c_str());
  }
  rclcpp::Subscription<std_msgs::msg::String>::SharedPtr subscription_;
```

Fungsi main sama persis, kecuali sekarang ia memutar node MinimalSubscriber. Untuk node penerbit, memutar berarti memulai timer, tetapi untuk subscriber, itu hanya berarti bersiap untuk menerima pesan kapan pun mereka datang.

Karena node ini memiliki dependensi yang sama dengan node publisher, tidak ada yang baru untuk ditambahkan ke package.xml.

#### 3.2 CMakeLists.txt
Buka kembali file CMakeLists.txt dan tambahkan eksekutor dan target untuk node subscriber di bawah entri publisher.

```
add_executable(listener src/subscriber_member_function.cpp)
ament_target_dependencies(listener rclcpp std_msgs)

install(TARGETS
  talker
  listener
  DESTINATION lib/${PROJECT_NAME})
```

Pastikan untuk menyimpan file tersebut, dan kemudian sistem pub/sub Anda seharusnya siap.

#### 4. Build & Run
Anda kemungkinan sudah memiliki paket rclcpp dan std_msgs terinstal sebagai bagian dari sistem ROS 2 Anda. Adalah praktik yang baik untuk menjalankan rosdep di root workspace Anda (ros2_ws) untuk memeriksa keberadaan dependensi yang hilang sebelum melakukan build:
```
rosdep install -i --from-path src --rosdistro humble -y
```
tetap pada akar workspace anda ros_ws lalu build
```
colcon build --packages-select cpp_pubsub
```
Buka terminal baru, arahkan ke path ros2_ws, dan source file setup:
```
. install/setup.bash
```
Lalu run talker nya
```
ros2 run cpp_pubsub talker
```
Terminal seharusnya mulai mempublikasikan pesan info setiap 0,5 detik, seperti ini:
```
[INFO] [minimal_publisher]: Publishing: "Hello World: 0"
[INFO] [minimal_publisher]: Publishing: "Hello World: 1"
[INFO] [minimal_publisher]: Publishing: "Hello World: 2"
[INFO] [minimal_publisher]: Publishing: "Hello World: 3"
[INFO] [minimal_publisher]: Publishing: "Hello World: 4"
```

Buka terminal lain, source kembali file setup dari dalam ros2_ws, dan kemudian jalankan node listener:
```
ros2 run cpp_pubsub listener
```
Listener akan mulai mencetak pesan ke konsol, dimulai dari jumlah pesan yang ada pada saat itu oleh penerbit, seperti ini:
```
[INFO] [minimal_subscriber]: I heard: "Hello World: 10"
[INFO] [minimal_subscriber]: I heard: "Hello World: 11"
[INFO] [minimal_subscriber]: I heard: "Hello World: 12"
[INFO] [minimal_subscriber]: I heard: "Hello World: 13"
[INFO] [minimal_subscriber]: I heard: "Hello World: 14"
```

Masukkan Ctrl+C di setiap terminal untuk menghentikan pemutaran node.

## Membuat custom msg
### Task
#### 1 Membuat package baru
Untuk tutorial ini, Anda akan membuat file .msg khusus dalam paket mereka sendiri, dan kemudian menggunakan mereka dalam paket terpisah. Kedua paket tersebut harus berada dalam workspace yang sama.

Karena kita akan menggunakan paket pub/sub yang dibuat dalam tutorial sebelumnya, pastikan Anda berada di workspace yang sama dengan paket-paket tersebut (ros2_ws/src), dan kemudian jalankan perintah berikut untuk membuat paket baru:

```
ros2 pkg create --build-type ament_cmake --license Apache-2.0 tutorial_interfaces
```

tutorial_interfaces adalah nama paket baru tersebut. Perhatikan bahwa ini adalah, dan hanya dapat menjadi, paket CMake, tetapi ini tidak membatasi dalam jenis paket apa Anda dapat menggunakan pesan dan layanan Anda. Anda dapat membuat antarmuka kustom sendiri dalam paket CMake, dan kemudian menggunakannya dalam node C++ atau Python, yang akan dibahas dalam bagian terakhir.

File .msg dan .srv harus ditempatkan dalam direktori bernama msg dan srv masing-masing. Buat direktori-direktori tersebut di ros2_ws/src/tutorial_interfaces:

```
mkdir msg
```

#### 2 Membuat definisi kustom
#### 2.1 definisi msg
Di dalam direktori tutorial_interfaces/msg yang baru saja Anda buat, buat file baru bernama Num.msg dengan satu baris kode yang mendeklarasikan struktur datanya:
```
int64 num
```

Ini adalah pesan kustom yang mentransfer satu bilangan bulat 64-bit bernama num.

Juga di dalam direktori tutorial_interfaces/msg yang baru saja Anda buat, buat file baru bernama Sphere.msg dengan konten berikut:

```
geometry_msgs/Point center
float64 radius
```
Pesan kustom ini menggunakan pesan dari paket pesan lain (geometry_msgs/Point dalam hal ini).

#### 3 CMakeLists.txt

Untuk mengonversi antarmuka yang Anda definisikan menjadi kode berbahasa tertentu (seperti C++ dan Python) agar dapat digunakan dalam bahasa-bahasa tersebut, tambahkan baris-baris berikut ke CMakeLists.txt:

```
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/Num.msg"
  "msg/Sphere.msg"
  "srv/AddThreeInts.srv"
  DEPENDENCIES geometry_msgs # Add packages that above messages depend on, in this case geometry_msgs for Sphere.msg
)
```

#### 4 package.xml

Karena antarmuka mengandalkan rosidl_default_generators untuk menghasilkan kode berbahasa tertentu, Anda perlu mendeklarasikan dependensi pada alat pembangunannya. rosidl_default_runtime adalah dependensi runtime atau eksekusi, diperlukan agar dapat menggunakan antarmuka nanti. rosidl_interface_packages adalah nama grup dependensi yang harus terkait dengan paket Anda, tutorial_interfaces, yang dideklarasikan menggunakan tag <member_of_group>.

Tambahkan baris-baris berikut di dalam elemen package dari package.xml:

```
<depend>geometry_msgs</depend>
<buildtool_depend>rosidl_default_generators</buildtool_depend>
<exec_depend>rosidl_default_runtime</exec_depend>
<member_of_group>rosidl_interface_packages</member_of_group>
```

#### 5 Build the tutorial_interfaces package

Sekarang semua bagian dari paket antarmuka kustom Anda sudah ada, Anda dapat membangun paket tersebut. Di root workspace Anda (~/ros2_ws), jalankan perintah berikut:

```
colcon build --packages-select tutorial_interfaces
```
Sekarang antarmuka tersebut dapat ditemukan oleh paket ROS 2 lainnya.

#### 6 Memastikan msg
Di terminal baru, jalankan perintah berikut dari dalam workspace Anda (ros2_ws) untuk menjalankannya:
```
source install/setup.bash
```

Sekarang Anda dapat mengkonfirmasi bahwa pembuatan antarmuka Anda berhasil dengan menggunakan perintah ros2 interface show:
```
ros2 interface show tutorial_interfaces/msg/Num
```

output
```
int64 num
```
dan jalankan ini dalam terminal
```
ros2 interface show tutorial_interfaces/msg/Sphere
```
output
```
geometry_msgs/Point center
        float64 x
        float64 y
        float64 z
float64 radius
```

#### 7 mencoba interface yang telah kita buat
Pada langkah ini, Anda dapat menggunakan paket-paket yang telah Anda buat dalam tutorial sebelumnya. Beberapa modifikasi sederhana pada node, CMakeLists.txt, dan file package.xml akan memungkinkan Anda menggunakan antarmuka baru Anda.

Dengan beberapa modifikasi pada paket penerbit/pelanggan yang dibuat dalam tutorial sebelumnya (C++ atau Python), Anda dapat melihat Num.msg dalam aksi. Karena Anda akan mengubah pesan string standar menjadi pesan numerik, keluaran akan sedikit berbeda.

publisher
```
#include <chrono>
#include <memory>

#include "rclcpp/rclcpp.hpp"
#include "tutorial_interfaces/msg/num.hpp"                                            // CHANGE

using namespace std::chrono_literals;

class MinimalPublisher : public rclcpp::Node
{
public:
  MinimalPublisher()
  : Node("minimal_publisher"), count_(0)
  {
    publisher_ = this->create_publisher<tutorial_interfaces::msg::Num>("topic", 10);  // CHANGE
    timer_ = this->create_wall_timer(
      500ms, std::bind(&MinimalPublisher::timer_callback, this));
  }

private:
  void timer_callback()
  {
    auto message = tutorial_interfaces::msg::Num();                                   // CHANGE
    message.num = this->count_++;                                                     // CHANGE
    RCLCPP_INFO_STREAM(this->get_logger(), "Publishing: '" << message.num << "'");    // CHANGE
    publisher_->publish(message);
  }
  rclcpp::TimerBase::SharedPtr timer_;
  rclcpp::Publisher<tutorial_interfaces::msg::Num>::SharedPtr publisher_;             // CHANGE
  size_t count_;
};

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<MinimalPublisher>());
  rclcpp::shutdown();
  return 0;
}
```

subscriber
```
#include <functional>
#include <memory>

#include "rclcpp/rclcpp.hpp"
#include "tutorial_interfaces/msg/num.hpp"                                       // CHANGE

using std::placeholders::_1;

class MinimalSubscriber : public rclcpp::Node
{
public:
  MinimalSubscriber()
  : Node("minimal_subscriber")
  {
    subscription_ = this->create_subscription<tutorial_interfaces::msg::Num>(    // CHANGE
      "topic", 10, std::bind(&MinimalSubscriber::topic_callback, this, _1));
  }

private:
  void topic_callback(const tutorial_interfaces::msg::Num & msg) const  // CHANGE
  {
    RCLCPP_INFO_STREAM(this->get_logger(), "I heard: '" << msg.num << "'");     // CHANGE
  }
  rclcpp::Subscription<tutorial_interfaces::msg::Num>::SharedPtr subscription_;  // CHANGE
};

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<MinimalSubscriber>());
  rclcpp::shutdown();
  return 0;
}
```

CMakelist.txt
```
#...

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(tutorial_interfaces REQUIRED)                      # CHANGE

add_executable(talker src/publisher_member_function.cpp)
ament_target_dependencies(talker rclcpp tutorial_interfaces)    # CHANGE

add_executable(listener src/subscriber_member_function.cpp)
ament_target_dependencies(listener rclcpp tutorial_interfaces)  # CHANGE

install(TARGETS
  talker
  listener
  DESTINATION lib/${PROJECT_NAME})

ament_package()
```

package.xml

tambahkan line ini
```
<depend>tutorial_interfaces</depend>
```

Setelah melakukan pengeditan di atas dan menyimpan semua perubahan, build paketnya:
```
colcon build --packages-select cpp_pubsub
```

Kemudian buka dua terminal baru, source kan ros2_ws di masing-masingnya, dan jalankan:

```
ros2 run cpp_pubsub talker
```
```
ros2 run cpp_pubsub listener
```

Karena Num.msg hanya menyampaikan bilangan bulat, penerbit seharusnya hanya mempublikasikan nilai-nilai bilangan bulat, berbeda dengan string yang dipublikasikan sebelumnya:
```
[INFO] [minimal_publisher]: Publishing: '0'
[INFO] [minimal_publisher]: Publishing: '1'
[INFO] [minimal_publisher]: Publishing: '2'
```
Jika sudah menampilkan seperti itu maka anda sudah sukses menggunakan custom msg.
