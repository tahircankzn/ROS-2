## ROS 2 Ortamını Anlama ve Setup (Environment Basics)

ROS 2 komutlarının çalışabilmesi için sistemin ROS ortamını tanıması gerekir.

Eğer aşağıdaki komut çalıştırıldığında:

```bash
ros2 run demo_nodes_cpp talker
```

şu hata alınırsa:

```text
command not found
```

Bu durum ROS 2 environment'ın aktif olmadığını gösterir.

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
