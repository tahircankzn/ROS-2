# ROS-2 Öğrenme ve Geliştirme Yol Haritası

Bu repository, ROS 2 (Humble) öğrenimi ve gerçek zamanlı sistem geliştirme süreçlerini adım adım ilerletmek için hazırlanmıştır.

Amaç yalnızca ROS 2 kurmak değil, aynı zamanda:
- ROS 2 mimarisini anlamak
- Gerçek veri akış sistemleri tasarlamak
- Görüntü işleme pipeline’larını ROS 2’ye taşımak
- Performans (FPS / latency) analizleri yapmak
- Dağıtık ve gerçek zamanlı sistem mantığını geliştirmektir

---

# Repository Yapısı

```

ROS-2/
│
├── 00_SETUP/
├── 01_FIRST_STEPS/
├── 02_EXAMPLE_PROJECTS/
└── README.md

```

---

# Başlangıç Sırası (Önerilen Akış)

Bu repo sırayla ilerlenmelidir:

---

## 1. Kurulum Aşaması
[`00_SETUP/`](./00_SETUP/)

Bu bölümde sistem hazırlanır:
- ROS 2 Humble kurulumu
- Colcon build tool kurulumu
- VS Code ve geliştirme araçları
- Terminator terminal setup
- Python / CMake ortam hazırlığı

Amaç:
> Sistemi tamamen çalışır hale getirmek

---

## 2. ROS Temelleri
[`01_FIRST_STEPS/`](./01_FIRST_STEPS/)

Bu bölümde ROS 2 öğrenilir:
- Node nedir?
- Topic nasıl çalışır?
- Publisher / Subscriber mantığı
- ROS 2 CLI (ros2 run, ros2 topic vs)
- Basit demo uygulamalar

Amaç:
> ROS 2’nin çalışma mantığını anlamak

---

## 3. Örnek Projeler
[`02_EXAMPLE_PROJECTS/`](./02_EXAMPLE_PROJECTS/)

- kamera pipeline
- ROS node örnekleri
- Basit demo uygulamalar

---

## Kullanılan Teknolojiler

| Teknoloji | Versiyon/Açıklama |
|-----------|-------------------|
| **ROS 2** | Humble (LTS) |
| **İşletim Sistemi** | Ubuntu 22.04 |
| **Python** | 3.10 |
| **C++** | ROS node geliştirme |
| **OpenCV** | Görüntü işleme |
| **Colcon** | Build system |
| **CMake** | C++ build tool |
| **VS Code** | IDE |

---

## Önemli Notlar

- Bu repository sürekli geliştirilme aşamasındadır
- ROS 2 ekosistemi zamanla değişebilir
- Tüm kurulum ve kullanım adımları referans amaçlıdır
- Güncel bilgiler için [resmi ROS 2 dokümantasyonu](https://docs.ros.org/en/humble/) kontrol edilmelidir

---

## Başlamak İçin

1. **[00_SETUP/](./00_SETUP/)** klasörüne gidin
2. ROS 2 Humble kurulumunu tamamlayın
3. Geliştirme araçlarını kurun
4. **[01_FIRST_STEPS/](./01_FIRST_STEPS/)** ile öğrenmeye başlayın

---

## Destek ve Katkı

Sorularınız veya katkılarınız için issue açabilirsiniz.

Kurulum tamamlandıktan sonra:
`01_FIRST_STEPS/` ile ROS 2 öğrenme sürecine geçin.

