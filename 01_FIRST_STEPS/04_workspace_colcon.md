## ROS 2 Gerçek Çalışma Ortamı (Workspace Yapısı)

Bu bölümde ROS 2 projelerinin gerçek geliştirme ortamı olan **workspace (çalışma alanı)** yapısı oluşturulur.

---

## 1. ROS 2 Workspace Oluşturma

ROS 2 projeleri tek bir klasör yapısı içinde yönetilir. Bu yapıya **workspace** denir.

Ana dizinde bir workspace oluşturulur:

```bash
mkdir ros2_ws
```

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

Build edilen paketlerin terminalde çalışabilmesi için sistemin bu workspace'i tanıması gerekir.

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
* Hem sistem ROS'u hem workspace paketlerini tanır
* Genellikle ana kullanım budur

---

### local_setup.bash

* Sadece workspace içindeki paketleri yükler
* Sistem ROS environment'ını tekrar yüklemez
* Daha "izole" kullanım sağlar

---

## Kısa Mantık

* `setup.bash` → tam ortam (ROS + workspace)
* `local_setup.bash` → sadece workspace
