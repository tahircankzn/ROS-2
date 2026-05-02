## Talker ve Listener Çalıştırma

ROS 2'nin temel veri iletişimini test etmek için iki terminal açılır.

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

## ROS 2 "Hello World" Mantığı

Bu yapı ROS 2'nin en temel örneğidir:

**Talker → veri gönderir**
**Listener → veriyi alır**

Bu yüzden ROS 2 dünyasında bu örnek:

> "Hello World of ROS 2"

olarak kabul edilir.

---

## Sistem Davranışı (Önemli Mantık)

### Talker kapatılırsa:

* Listener çalışmaya devam eder
* Ancak yeni veri gelmez

### Talker tekrar başlatılırsa:

* Listener otomatik olarak tekrar veri almaya başlar
* Sistem yeniden senkronize olur
