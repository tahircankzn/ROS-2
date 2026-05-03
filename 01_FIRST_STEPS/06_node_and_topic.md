# ROS 2 Node ve Topic Kavramları (Detaylı Anlatım)

Bu bölümde ROS 2’nin temel yapı taşları olan **Node** ve **Topic** kavramları detaylı ve örnek odaklı şekilde açıklanmaktadır.

Amaç:
- ROS 2 mimarisini derinlemesine anlamak
- Veri akışının nasıl gerçekleştiğini kavramak
- Gerçek sistemlere nasıl uygulanacağını görmek

---

# 1. ROS 2 Node Nedir?

## Tanım

**Node**, ROS 2 içerisinde çalışan bağımsız bir yazılım birimidir.

Her node:
- Belirli bir görevi yerine getirir
- Diğer node’larla iletişim kurabilir
- Tek başına çalışabilir veya sistemin parçası olabilir

---

## Neden Node Yapısı Kullanılır?

ROS 2’de sistemler **modüler** olarak tasarlanır.

Bunun avantajları:
- Her bileşen ayrı geliştirilebilir
- Hatalar izole edilir
- Sistem ölçeklenebilir hale gelir
- Paralel çalışma mümkündür

---

## Basit Örnek

Bir drone sistemi düşünelim:

| Görev | Node |
|------|------|
| Kamera görüntüsü alma | `camera_node` |
| Görüntüyü işleme | `vision_node` |
| Navigasyon hesaplama | `navigation_node` |
| Uçuş kontrolü | `control_node` |

Her biri ayrı node’dur.

---

# 2. Gerçek Senaryo (İleri Seviye Sistem)

Bir UAV görev senaryosu:

> Araç rota belirler → hedefe gider → dalış yapar → yerdeki QR kodu okur → tekrar kalkış yapar

---

## Node Dağılımı

| Görev | Node |
|------|------|
| Görev planlama | `mission_planner_node` |
| Rota üretimi | `navigation_node` |
| Uçuş kontrolü | `flight_control_node` |
| Kamera veri akışı | `camera_node` |
| QR kod tespiti | `vision_node` |
| Karar mekanizması | `decision_node` |

---

## Node’ların Bağlantısı (Mantık Akışı)

### 1. Mission Planner

- Görevi başlatır
- Hedef koordinatları belirler
- Navigasyon node’una gönderir

---

### 2. Navigation Node

- Rota hesaplar
- Ara noktalar (waypoint) üretir
- Flight control node’a gönderir

---

### 3. Flight Control Node

- Motor komutlarını üretir
- Aracı hedefe doğru hareket ettirir

---

### 4. Camera Node

- Sürekli görüntü üretir
- Vision node’a gönderir

---

### 5. Vision Node

- QR kod arar
- Tespit ederse konum bilgisini çıkarır
- Decision node’a gönderir

---

### 6. Decision Node

- QR tespit edildi mi?
- Dalış başlatılsın mı?
- Görev tamamlandı mı?

Bu kararları üretir ve flight control node’a komut verir

---

## Kritik Nokta

Hiçbir node tüm sistemi tek başına yönetmez.

Sistem:
> Küçük görevlerin birleşiminden oluşur

---

# 3. ROS 2 Topic Nedir?

## Tanım

**Topic**, node’lar arasında veri taşıyan iletişim kanalıdır.

- Node’lar birbirine **direkt bağlı değildir**
- Aralarında topic üzerinden haberleşirler

---

## Yayıncı – Dinleyici Modeli

ROS 2’de iletişim:

- **Publisher (Yayıncı)** → veri gönderir
- **Subscriber (Dinleyici)** → veriyi alır

---

## Basit Örnek

```

Talker → "Hello ROS2" → Topic → Listener

```

---

## Gerçek Sistem Örneği

### Kamera Akışı

```

camera_node → /camera/image_raw → vision_node

```

---

### Navigasyon Verisi

```

navigation_node → /trajectory → flight_control_node

```

---

### QR Tespit Bilgisi

```

vision_node → /qr_detection → decision_node

```

---

### Kontrol Komutları

```

decision_node → /control_commands → flight_control_node

```

---

# 4. Topic Özellikleri

## 1. Asenkron Yapı

- Node’lar aynı anda çalışmak zorunda değildir
- Publisher veri gönderir, subscriber hazırsa alır

---

## 2. Loose Coupling (Gevşek Bağlantı)

Node’lar:
- Birbirinin iç yapısını bilmez
- Sadece topic ismini bilir

Bu:
- Sistemi esnek yapar
- Node değişimini kolaylaştırır

---

## 3. Çoklu Bağlantı

Bir topic:

- Birden fazla publisher’a sahip olabilir
- Birden fazla subscriber’a sahip olabilir

---

## Örnek

```

camera_node → /image → vision_node_1
→ vision_node_2
→ recording_node

```

---

# 5. Node + Topic Birlikte Nasıl Çalışır?

## Tam Sistem Akışı

```

mission_planner_node
↓
/mission_goal
↓
navigation_node
↓
/trajectory
↓
flight_control_node
↓
(drone hareket eder)

camera_node
↓
/camera/image
↓
vision_node
↓
/qr_detection
↓
decision_node
↓
/control_command
↓
flight_control_node

```

---

## Yorum

Bu yapı:

- Gerçek zamanlı sistemlere uygundur
- Paralel işlemeye uygundur
- Büyük sistemleri yönetilebilir hale getirir

---

# 6. Neden Bu Kadar Önemli?

Node + Topic yapısı:

- Robotik sistemlerin temelidir
- Otonom sistemlerin temelidir
- Dağıtık sistemlerin temelidir

---

# 7. Özet

## Node

- Bağımsız çalışan yazılım birimi
- Tek bir görev yapar
- Modüler sistem sağlar

---

## Topic

- Node’lar arası veri hattı
- Publisher–Subscriber modeli ile çalışır
- Sistemi esnek ve ölçeklenebilir yapar

---

## Büyük Resim

ROS 2:

> “Küçük, bağımsız parçaların veri akışı ile birleştiği bir sistemdir”

Bu mantık anlaşıldığında:
- ROS öğrenimi hızlanır
- Karmaşık sistemler basitleşir
- Gerçek zamanlı uygulamalar daha rahat geliştirilir
