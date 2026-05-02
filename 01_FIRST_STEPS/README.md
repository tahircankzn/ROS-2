## ROS 2 Ortamını Anlama ve Setup (Environment Basics)

ROS 2 komutlarının çalışabilmesi için sistemin ROS ortamını tanıması gerekir.

Eğer aşağıdaki komut çalıştırıldığında:

```bash
ros2 run demo_nodes_cpp talker
````

şu hata alınırsa:

```text
command not found
```

Bu durum ROS 2 environment’ın aktif olmadığını gösterir.

---

## 1. ROS Kurulum Dizini İnceleme

ROS 2 sistem dosyaları şu dizinde bulunur:

```bash
cd /opt/ros
ls
```

Bu dizinde yüklü ROS sürümleri listelenir:

* humble
* iron
* jazzy (varsa)

---

## 2. Humble Dizinine Giriş

Kurulu ROS sürümüne girilir:

```bash
cd humble
ls
```

Bu klasör içerisinde ROS 2 environment dosyaları bulunur:

* setup.bash
* setup.sh
* setup.zsh

---

## 3. ROS Environment Aktifleştirme

ROS komutlarının çalışması için setup dosyası source edilmelidir:

```bash
source /opt/ros/humble/setup.bash
```

---

## 4. Kalıcı Hale Getirme

Her terminalde tekrar yazmamak için `.bashrc` dosyasına eklenir:

```bash
gedit ~/.bashrc
```

Dosyanın en altına şu satır eklenir:

```bash
source /opt/ros/humble/setup.bash
```

---

## 5. Yeni Terminal Testi

Terminal kapatılıp yeniden açılır ve test edilir:

```bash
ros2 run demo_nodes_cpp talker
```

Eğer komut çalışıyorsa:

ROS 2 environment doğru şekilde yapılandırılmıştır.


## ROS 2 İlk Çalıştırma ve CLI Temelleri

Bu bölümde ROS 2’nin temel kullanım mantığı ve ilk iletişim yapısı test edilir.

---

## 1. ROS 2 Komut Yardımı (Tab Tamamlama)

Terminale sadece:

```bash
ros2
````

yazılıp **iki kez TAB tuşuna basıldığında**, ROS 2 ile kullanılabilecek tüm alt komutlar listelenir.

---

## Bu Ne İşe Yarar?

Bu özellik:

* ROS 2 CLI komutlarını keşfetmeyi sağlar
* Hangi modüllerin (topic, node, service vb.) olduğunu gösterir
* Terminal üzerinden hızlı dokümantasyon gibi çalışır

👉 ROS 2’nin komut yapısını öğrenmenin en hızlı yoludur

---

## 2. Talker ve Listener Çalıştırma

ROS 2’nin temel veri iletişimini test etmek için iki terminal açılır.

---

## Terminal 1 – Talker (Publisher)

```bash id="talker_1"
ros2 run demo_nodes_cpp talker
```

### Görevi:

* Sürekli veri üretir
* Bu veriyi ROS topic üzerinden yayınlar
* Sistemde **publisher (yayıncı)** rolündedir

---

## Terminal 2 – Listener (Subscriber)

```bash id="listener_1"
ros2 run demo_nodes_py listener
```

### Görevi:

* Talker tarafından yayınlanan veriyi alır
* Gelen mesajları ekrana yazdırır
* Sistemde **subscriber (dinleyici)** rolündedir

---

## 3. ROS 2 “Hello World” Mantığı

Bu yapı ROS 2’nin en temel örneğidir:

**Talker → veri gönderir**
**Listener → veriyi alır**

Bu yüzden ROS 2 dünyasında bu örnek:

> “Hello World of ROS 2”

olarak kabul edilir.

---

## 4. Sistem Davranışı (Önemli Mantık)

### Talker kapatılırsa:

* Listener çalışmaya devam eder
* Ancak yeni veri gelmez

### Talker tekrar başlatılırsa:

* Listener otomatik olarak tekrar veri almaya başlar
* Sistem yeniden senkronize olur


## ROS 2 Gerçek Çalışma Ortamı (Workspace Yapısı)

Bu bölümde ROS 2 projelerinin gerçek geliştirme ortamı olan **workspace (çalışma alanı)** yapısı oluşturulur.

---

## 1. ROS 2 Workspace Oluşturma

ROS 2 projeleri tek bir klasör yapısı içinde yönetilir. Bu yapıya **workspace** denir.

Ana dizinde bir workspace oluşturulur:

```bash
mkdir ros2_ws
````

---

## 2. Src (Source) Klasörü

Workspace içine girilir ve kaynak kodların bulunacağı klasör oluşturulur:

```bash id="src_create"
cd ros2_ws
mkdir src
```

### Src Nedir?

* ROS 2 paketlerinin bulunduğu ana klasördür
* Tüm kaynak kodlar burada geliştirilir
* Colcon build işlemi bu klasörü referans alır

---

## 3. Colcon Build

Workspace derlenir:

```bash id="colcon_build"
colcon build
```

---

## Build Sonrasında Oluşan Klasörler

Derleme sonrası workspace içinde şu klasörler oluşur:

* build/
* install/
* log/

```bash id="ls_check"
ls
```

---

## 4. Environment Yükleme Problemi

Build edilen paketlerin terminalde çalışabilmesi için sistemin bu workspace’i tanıması gerekir.

Aksi halde:

* ros2 komutları workspace içindeki paketleri görmez

---

## 5. Setup Dosyasını Aktifleştirme

Workspace ortamı şu dosya ile yüklenir:

```bash id="workspace_source"
source install/setup.bash
```

---

## 6. Kalıcı Hale Getirme

Her terminalde tekrar yazmamak için `.bashrc` içine eklenir:

```bash id="bashrc_ws"
gedit ~/.bashrc
```

Dosyanın en altına:

```bash id="bashrc_source_ws"
source ~/ros2_ws/install/setup.bash
```

---

## 7. setup.bash vs local_setup.bash

### setup.bash

* Tüm workspace ortamını yükler
* Hem sistem ROS’u hem workspace paketlerini tanır
* Genellikle ana kullanım budur

---

### local_setup.bash

* Sadece workspace içindeki paketleri yükler
* Sistem ROS environment’ını tekrar yüklemez
* Daha “izole” kullanım sağlar

---

## Kısa Mantık

* `setup.bash` → tam ortam (ROS + workspace)
* `local_setup.bash` → sadece workspace



## 7. ROS 2 Paket Oluşturma (Python - ament_python)

Bu bölümde ROS 2 üzerinde **Python tabanlı bir paket oluşturma süreci** anlatılmıştır.

Amaç:

* ROS 2 paket yapısını öğrenmek
* Python node geliştirme altyapısını hazırlamak
* Workspace içine yeni paket ekleyebilmek

---

## Workspace’e Giriş

Öncelikle çalışma alanına gidilir:

```bash
cd ros2_ws
cd src
```

ROS 2 projelerinde tüm paketler `src` klasörü içinde tutulur.

---

## ROS 2 Python Paket Oluşturma

Yeni bir Python paketi oluşturmak için:

```bash
ros2 pkg create my_py_pkg --build-type ament_python --dependencies rclpy
```

---

### Komut Açıklaması

* `ros2 pkg create` → yeni ROS 2 paketi oluşturur
* `my_py_pkg` → paket adı
* `--build-type ament_python` → Python tabanlı ROS 2 paketi oluşturur
* `--dependencies rclpy` → ROS 2 Python client library bağımlılığını ekler

---

## Oluşan Paket Yapısı

Komut sonrası ROS 2 otomatik olarak bir paket yapısı oluşturur:

* package.xml
* setup.py
* setup.cfg
* my_py_pkg/ (python modülü)
* resource/ klasörü

Bu yapı ROS 2’nin Python paket standartlarını temsil eder.

---

## VS Code ile İnceleme

Paket oluşturulduktan sonra proje VS Code ile açılır:

```bash
code .
```

Bu adım ile:

* dosya yapısı incelenir
* otomatik oluşturulan ROS 2 paket dosyaları görülür
* geliştirme ortamı hazırlanır

---

## Workspace Build İşlemi

Paketin ROS 2 sistemi tarafından tanınması için workspace yeniden derlenir:

```bash
cd ~/ros2_ws
colcon build
```

---

## Build Sonrası Mantık

Colcon build sonrası:

* yeni paket ROS 2’ye kaydedilir
* executable yollar oluşturulur
* install klasörü güncellenir

---

## Ortamın Aktif Edilmesi

Build sonrası terminalde paketlerin görünmesi için:

```bash
source install/setup.bash
```

(Eğer `.bashrc` içine ekli ise otomatik yüklenir)

