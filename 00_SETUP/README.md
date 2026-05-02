# ROS 2 Kurulum ve Ortam Hazırlığı

Bu bölümde ROS 2 Humble kurulumu ve geliştirme ortamının hazırlanması adım adım anlatılmaktadır.

---

## İçindekiler

1. [ROS 2 Sürüm Seçimi](#ros-2-sürüm-seçimi)
2. [ROS 2 Humble Kurulumu](#ros-2-humble-kurulumu)
3. [Geliştirme Araçları](#geliştirme-araçları)
4. [Colcon Build System](#colcon-build-system)

---

## ROS 2 Sürüm Seçimi

ROS 2 sürümleri, farklı stabilite ve destek sürelerine göre yayınlanır.
Doğru sürüm seçimi, projenin başarısı ve sürdürülebilirliği açısından **kritik** öneme sahiptir.

### Resmi Sürüm Listesi

[ROS 2 Releases - Resmi Dokümantasyon](https://docs.ros.org/en/rolling/Releases.html)

---

### 1. LTS (Long Term Support) Sürümler

| Özellik | Açıklama |
|---------|----------|
| **Destek Süresi** | 5 yıl |
| **Stabilite** | Yüksek - test edilmiş |
| **Kullanım Alanı** | Endüstriyel ve uzun vadeli projeler |
| **Güncelleme** | Güvenlik ve kritik yamalar |

**Öneri:** Çoğu proje için LTS sürümler tercih edilmelidir.

---

### 2. Rolling Release

| Özellik | Açıklama |
|---------|----------|
| **Güncelleme** | Sürekli |
| **Özellikler** | En yeni özellikler |
| **Stabilite** | Değişken |
| **Kullanım Alanı** | Geliştirme ve test |

---

### Önemli Uyarı

Farklı ROS 2 sürümleri kullanmak şu sorunlara neden olabilir:

- Paket uyumsuzlukları
- API değişiklikleri
- Çalışmayan node'lar
- Build hataları

**Kural:** Tüm geliştirme süreci boyunca **aynı ROS 2 sürümü** kullanılmalıdır.

---

## ROS 2 Humble Kurulumu (Ubuntu - DEB Packages)

### Resmi Dokümantasyon

[ROS 2 Humble Installation Guide](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html)

---

### Önemli Not (Sürüm ve Güncellik)

Bu repository kapsamında **ROS 2 Humble (LTS)** sürümü kullanılmıştır.

**Dikkat Edilmesi Gerekenler:**

- Bu kurulum adımları, yazıldığı tarihteki resmi dokümantasyona dayanmaktadır
- Kurulum komutları zamanla değişebilir
- Güncel ve doğru bilgi için **her zaman resmi dokümantasyonu** kontrol edin

**Bu Bölümün Amacı:**

- Kurulumun temel mantığını öğretmek
- Genel kurulum akışını anlatmak
- Referans kaynak olmak

> **Not:** Bu bölüm "tek doğru yöntem" değildir. Sistem güncellemeleri ile farklılık gösterebilir.

---

### 1. Locale Ayarı (UTF-8)

Kurulumun ilk adımı sistem locale ayarlarının UTF-8 olmasıdır.

**Mevcut locale kontrolü:**

```bash
locale
```

Eğer uygun değilse:

```bash
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

**Doğrulama:**

```bash
locale
```

---

### 2. Universe Repository Aktifleştirme

ROS paketlerinin erişimi için Ubuntu Universe repository aktif edilmelidir:

```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
```

---

### 3. ROS 2 APT Repository ve Key Setup

ROS 2 paketlerini indirebilmek için resmi repository eklenir:

```bash
sudo apt update && sudo apt install curl -y
```

**ROS key ekleme:**

```bash
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key \
-o /usr/share/keyrings/ros-archive-keyring.gpg
```

**Repository ekleme:**

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] \
http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | \
sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

---

### 4. ROS 2 Paketlerini Güncelleme ve Kurulum

```bash
sudo apt update
sudo apt upgrade
```

**ROS 2 Desktop kurulumu (Önerilen):**

```bash
sudo apt install ros-humble-desktop
```

**Alternatif (minimal kurulum):**

```bash
sudo apt install ros-humble-ros-base
```

---

### 5. Environment Setup

ROS 2 kullanımı için environment değişkenleri yüklenmelidir:

```bash
source /opt/ros/humble/setup.bash
```

**Kalıcı yapmak için:**

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---

### Kurulum Sonu Kontrol

**Terminal 1:**

```bash
ros2 run demo_nodes_cpp talker
```

**Terminal 2 (Yeni terminal açın):**

```bash
ros2 run demo_nodes_py listener
```

Eğer mesajlar akıyorsa kurulum başarılıdır!

---

## Geliştirme Araçları

ROS 2 geliştirme sürecinde daha verimli bir çalışma ortamı oluşturmak için bazı temel araçlar kurulmalıdır.

### 1. VS Code (Visual Studio Code)

**Geliştirme ortamı olarak VS Code kullanılmıştır.**

**Kullanım amacı:**
- ROS 2 node geliştirme
- Python / C++ kod yazımı
- CMake projelerinin yönetimi
- Debug ve extension desteği

**Önerilen eklentiler:**
- CMake Tools
- Python Extension
- C/C++ Extension
- ROS Extension

---

### 2. Python Pip

```bash
sudo apt install python3-pip
```

**Kullanım amacı:**
- Python ROS 2 paket bağımlılıklarını yönetmek
- Ek Python kütüphanelerini kurmak

---

### 3. Terminator Terminal

```bash
sudo apt install terminator
```

**Kurulum sebebi:**
- Aynı anda birden fazla terminal ekranı kullanabilmek
- ROS 2 node, topic ve debug süreçlerini paralel takip edebilmek

**Avantajları:**
- Tek pencere içinde bölünmüş terminal ekranları
- ROS sistemlerinde gerçek zamanlı izleme kolaylığı
- Linux shortcut kullanımı (split screen, tab switching vb.)

---

### 4. Gedit

```bash
sudo apt install gedit
```

**Kullanım amacı:**
- Hızlı dosya düzenleme
- Config dosyalarını değiştirme
- Hafif text editör ihtiyacı

---

## Colcon Build System

ROS 2 projelerinde paketleri derlemek ve workspace yönetmek için **colcon** kullanılır.

### Kurulum

```bash
sudo apt update
sudo apt install python3-colcon-common-extensions
```

### Kurulum Doğrulama

```bash
colcon --version
```

Eğer versiyon bilgisi geliyorsa kurulum başarılıdır.

---

### Colcon Nedir?

**Colcon:**

- ROS 2 paketlerini derlemek için kullanılır
- Workspace içerisindeki tüm paketleri otomatik olarak build eder
- Bağımlılık sırasını kendisi yönetir
- Hem C++ hem Python paketlerini destekler

---

### Ne Zaman Kullanılır?

- Yeni bir ROS 2 paketi oluşturduktan sonra
- Kod değişikliği yaptıktan sonra
- Tüm workspace'i yeniden derlemek istediğinde

---

### Temel Kullanım

Bir workspace içinde:

```bash
colcon build
```

**Belirli bir paketi derlemek için:**

```bash
colcon build --packages-select paket_adi
```

---

### Önemli Not

Build sonrası **environment yüklenmelidir:**

```bash
source install/setup.bash
```

**Bu yapılmazsa:**
- Node'lar bulunamaz
- Paketler çalışmaz
- ROS 2 komutları paketi görmez

---

## Özet

### Kurulum Tamamlandı!

Bu setup ile:

| Araç | Amaç |
|------|------|
| **ROS 2 Humble** | Ana framework |
| **VS Code** | Geliştirme ortamı |
| **Terminator** | Multi-terminal kontrol |
| **CMake Tools** | Build sistemi kontrolü |
| **Pip** | Python bağımlılık yönetimi |
| **Gedit** | Hızlı edit işlemleri |
| **Colcon** | ROS 2 build aracı |

Daha stabil ve verimli bir ROS 2 geliştirme ortamı oluşturulmuştur!

---

## Sırada Ne Var?

Kurulum tamamlandıktan sonra **[01_FIRST_STEPS](../01_FIRST_STEPS/)** klasörüne geçerek ROS 2 öğrenmeye başlayabilirsiniz!
