## ROS 2 Paket Oluşturma (Python - ament_python)

Bu bölümde ROS 2 üzerinde **Python tabanlı bir paket oluşturma süreci** anlatılmıştır.

Amaç:

* ROS 2 paket yapısını öğrenmek
* Python node geliştirme altyapısını hazırlamak
* Workspace içine yeni paket ekleyebilmek

---

## Workspace'e Giriş

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

Bu yapı ROS 2'nin Python paket standartlarını temsil eder.

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

* yeni paket ROS 2'ye kaydedilir
* executable yollar oluşturulur
* install klasörü güncellenir

---

## Ortamın Aktif Edilmesi

Build sonrası terminalde paketlerin görünmesi için:

```bash
source install/setup.bash
```

(Eğer `.bashrc` içine ekli ise otomatik yüklenir)
