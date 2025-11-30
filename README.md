# BYM412 - ROS2 Multi-Package Sensor System

**Yazar:** Cihan Kurtbey — 220609001  
**Repo:** https://github.com/Cihankurtbey/220609001_bym412_odev3

---

## Açıklama
Bu proje; ROS2 (Humble) tabanlı üç düğümden (node) oluşan örnek bir sistemdir. Sistem:
- Rastgele sensör verisi üreten `sensor_publisher_pkg`,
- Bu veriyi işleyip yayınlayan `data_processor_pkg`,
- Bir servis aracılığıyla gelen komuta göre karar veren `command_server_pkg`
paketlerini içerir.

Tüm sistem Docker içinde çalıştırılabilir şekilde hazırlanmıştır; hocanın test edeceği biçimde `docker run --rm myrosapp` ile ayağa kalkar.

---

## Klasör Yapısı (kısaca)

bym412_odev3/
├── Dockerfile
├── entrypoint.sh
├── ssf.sh
├── SSF_HASH.txt
├── README.md
└── src/
├── sensor_publisher_pkg/
├── data_processor_pkg/
├── command_server_interfaces/
├── command_server_pkg/
└── my_project/ (launch paketi)


---

## Gereksinimler
- Ubuntu 20.04/22.04 (veya uyumlu Linux)
- ROS2 Humble (local test için)
- Python 3.10
- colcon (`python3-colcon-common-extensions`)
- Docker (Docker ile çalıştırma için)

---

## Hızlı Çalıştırma — Local (Docker yoksa)

1. Workspace derle
```bash
cd ~/bym412_odev3
colcon build --symlink-install
source install/setup.bash
Düğümleri ayrı ayrı çalıştır

ros2 run sensor_publisher_pkg sensor_publisher
ros2 run data_processor_pkg data_processor
ros2 run command_server_pkg command_server


Testler

# processed_value topic'ini gör
ros2 topic echo /processed_value

# servis testi
ros2 service call /compute_command command_server_interfaces/srv/ComputeCommand "{input: 12.5}"

Docker ile Çalıştırma

1-İmajı oluştur (eğer henüz oluşturulmadıysa):

cd ~/bym412_odev3
docker build -t myrosapp .


2-Çalıştır
docker run --rm myrosapp
Konteyner başladığında my_project.launch.py ile üç düğüm otomatik başlatılacaktır.
Projede ssf.sh betiği mevcuttur. Bu betik çalıştırıldığında sistem bilgileri ve öğrenci numarası kullanılarak SHA256 hash üretilir ve şu dosyaya yazılır:

~/SSF_HASH.txt


Çalıştırma komutları:

cd ~/bym412_odev3
chmod +x ssf.sh
./ssf.sh
# Öğrenci numaranızı girin (ör: 220609001)
# Ardından ~/SSF_HASH.txt dosyası oluşacaktır

İletişim

Cihan Kurtbey — 220609001
(E-posta: cihankurtbey@icloud.com)



