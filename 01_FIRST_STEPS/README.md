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



