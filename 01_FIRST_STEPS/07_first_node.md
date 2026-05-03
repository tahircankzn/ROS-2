# ROS 2 İlk Node Yazımı (Python)

Bu bölümde ROS 2 üzerinde **ilk Python node’unun yazılması ve çalıştırılması** adım adım anlatılmaktadır.

Amaç:
- ROS 2 Python node yapısını öğrenmek
- Yazılan node’u sistemde çalıştırabilmek
- Build ve çalışma mantığını kavramak

---

# 1. Node Dosyasının Oluşturulması

Daha önce oluşturulan paket içine girilir:

```bash
cd ~/ros2_ws/src/my_py_pkg/my_py_pkg
````

Bu klasör içinde:

* `__init__.py` zaten bulunur
* Yeni bir Python dosyası oluşturulur:

```bash
gedit my_first_node.py
```

---

# 2. İlk Node Kodu

```python
#!/usr/bin/env python3

import rclpy  # ROS2 Python client library
from rclpy.node import Node  # ROS2 Node sınıfı

def main(args=None):
    rclpy.init(args=args)  # ROS haberleşmesini başlatır

    node = Node('python_test')  # 'python_test' adında node oluşturulur

    node.get_logger().info('Hello ROS2 from Python!')  
    # Konsola mesaj yazdırır

    rclpy.spin(node)  # Node çalışmaya devam eder (event loop)

    rclpy.shutdown()  # ROS sistemi kapatılır


if __name__ == '__main__':
    main()
```

---

# 3. Kodun Mantığı

## rclpy.init()

* ROS 2 iletişim altyapısını başlatır
* Node oluşturulmadan önce çağrılmalıdır

---

## Node('python_test')

* ROS 2 içerisinde bir node oluşturur
* `'python_test'` → node ismi

---

## get_logger().info()

* Terminale log basar
* Debug ve sistem takibi için kullanılır

---

## rclpy.spin(node)

* Node’u aktif tutar
* Callback’lerin çalışmasını sağlar
* Node kapanana kadar bloklar

---

## rclpy.shutdown()

* ROS 2 sistemini düzgün şekilde kapatır

---

# 4. Node’u Sisteme Tanıtma (setup.py)

Yazılan node’un terminalden çalıştırılabilmesi için **setup.py** dosyasına eklenmesi gerekir.

Dosya:

```bash
cd ~/ros2_ws/src/my_py_pkg
gedit setup.py
```

---

## Eklenen Kısım

```python
entry_points={
    'console_scripts': [
        "py_node = my_py_pkg.my_first_node:main"
    ],
},
```

---

## Açıklama

* `py_node` → terminalde çalıştırılacak isim
* `my_py_pkg.my_first_node` → dosya yolu
* `main` → çalıştırılacak fonksiyon

---

# 5. Workspace Derleme (Build)

Paketi sisteme tanıtmak için workspace derlenir:

```bash
cd ~/ros2_ws
colcon build
```

---

## Ortamı Güncelleme

```bash
source install/setup.bash
```

(Eğer `.bashrc` içine eklendiyse otomatik yüklenir)

---

# 6. Node’u Çalıştırma

Artık herhangi bir dizinden çalıştırılabilir:

```bash
ros2 run my_py_pkg py_node
```

---

## Beklenen Çıktı

```text
[INFO] [python_test]: Hello ROS2 from Python!
```

---

# 7. Sadece Belirli Paketi Build Etme

Proje büyüdüğünde tüm workspace’i derlemek zaman alabilir.

Sadece değiştirilen paketi build etmek için:

```bash
colcon build --packages-select my_py_pkg
```

---

## Avantajı

* Daha hızlı build süresi
* Büyük projelerde ciddi zaman kazancı

---

# 8. Genel Mantık

ROS 2 Python node geliştirme süreci:

1. Paket oluştur
2. Node dosyasını yaz
3. setup.py içine ekle
4. colcon build yap
5. source et
6. ros2 run ile çalıştır

---

# 9. Özet

Bu adımda:

* İlk ROS 2 Python node’u yazıldı
* Node sistemi anlaşıldı
* CLI üzerinden çalıştırma öğrenildi
* Build sistemi ile entegrasyon sağlandı

---

## Kritik Nokta

ROS 2’de bir node yazmak tek başına yeterli değildir.

Node’un:

* Sisteme tanıtılması
* Build edilmesi
* Environment’a eklenmesi

gereklidir.

Bu üçlü yapı anlaşılmadan ROS geliştirme sağlıklı ilerlemez.
