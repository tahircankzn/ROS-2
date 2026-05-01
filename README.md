# ROS-2
## ROS 2 Sürümü Nasıl Seçilir?

ROS 2 sürümleri, farklı stabilite ve destek sürelerine göre yayınlanır.
Doğru sürüm seçimi, projenin başarımı ve sürdürülebilirliği açısından kritiktir.

Tüm sürümler ve destek süreleri resmi sayfada listelenir:
https://docs.ros.org/en/rolling/Releases.html

---

### 1. LTS (Long Term Support) Sürümler

* Uzun süre destek (genellikle 5 yıl)
* Stabil ve test edilmiş
* Endüstriyel projeler için uygun

**Öneri:**
Çoğu proje için LTS sürümler tercih edilmelidir.

---

### 2. Rolling Release

* Sürekli güncellenir
* En yeni özellikler burada bulunur
* Stabil değildir

---

### Önemli Not

Farklı ROS sürümleri:

* Paket uyumsuzluklarına
* API değişikliklerine
* Çalışmayan node’lara

sebep olabilir.

Bu yüzden:
Tüm geliştirme süreci boyunca aynı ROS sürümü kullanılmalıdır.

# ROS 2 Humble Kurulumu (Ubuntu - DEB Packages)
## ROS 2 Humble Kurulumu (Ubuntu - DEB Packages)
ROS 2 Humble kurulumu resmi dokümantasyon üzerinden yapılmıştır:
````markdown
https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html
````
---

## Önemli Not (Sürüm ve Güncellik)

Bu repository kapsamında **ROS 2 Humble** sürümü kullanılmıştır.

Bu kurulum adımları, yazıldığı tarihteki resmi ROS 2 Humble dokümantasyonuna dayanmaktadır ve genel kurulum mantığını açıklamayı amaçlamaktadır.

* Kurulum komutları zamanla değişebilir.  
* Güncel ve doğru bilgi için her zaman resmi dokümantasyon kontrol edilmelidir.

Bu bölüm:
- Kurulumun temel mantığını öğretmek için hazırlanmıştır  
- Birebir “tek doğru yöntem” değildir  
- Sistem güncellemeleri ile farklılık gösterebilir  

---

## 1. Locale Ayarı (UTF-8)

Kurulumun ilk adımı sistem locale ayarlarının UTF-8 olmasıdır.

```bash
locale
````

Eğer uygun değilse:

```bash
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

Doğrulama:

```bash
locale
```

---

## 2. Universe Repository Aktifleştirme

ROS paketlerinin erişimi için Ubuntu Universe repository aktif edilmelidir:

```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```

---

## 3. ROS 2 APT Repository ve Key Setup

ROS 2 paketlerini indirebilmek için resmi repository eklenir:

```bash
sudo apt update && sudo apt install curl -y
```

ROS key ekleme:

```bash
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key \
-o /usr/share/keyrings/ros-archive-keyring.gpg
```

Repository ekleme:

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] \
http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | \
sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

---

## 4. ROS 2 Paketlerini Güncelleme ve Kurulum

```bash
sudo apt update
sudo apt upgrade
```

ROS 2 Desktop kurulumu:

```bash
sudo apt install ros-humble-desktop
```

Alternatif (minimal kurulum):

```bash
sudo apt install ros-humble-ros-base
```

---

## 5. Environment Setup

ROS 2 kullanımı için environment değişkenleri yüklenmelidir:

```bash
source /opt/ros/humble/setup.bash
```

Kalıcı yapmak için:

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
```

---

## Kurulum Sonu Kontrol

```bash
ros2 run demo_nodes_cpp talker
```

Yeni terminal:

```bash
ros2 run demo_nodes_py listener
```

Eğer mesajlar akıyorsa kurulum başarılıdır.

```
```

