# AI-Driven Cyber Threat & Anomaly Detector 🛡️🤖

Bu proje, sunucu loglarında meydana gelen siber saldırıları (DDoS, Veri Sızdırma vb.) **Isolation Forest** makine öğrenmesi algoritması kullanarak gerçek zamanlı olarak tespit eden uçtan uca bir anomali yakalama motorudur.

##  Özellikler (Features)
*   **Gerçek Zamanlı Simülasyon:** Sürekli akan ağ ve sunucu trafiğini simüle eder.
*   **Yapay Zeka Tabanlı Analiz:** Kural tabanlı (if-else) sistemler yerine, Isolation Forest ile veri odaklı anomali tespiti yapar.
*   **Renkli Konsol Çıktısı:** Tehditleri anında kırmızı renkle etiketleyerek sistem yöneticisine uyarı verir.

##  Klasör Yapısı (Project Structure)
*   `src/logger_sim.py`: Normal ve anomali içeren ağ trafiğini üreten simülatör.
*   `src/detector.py`: Scikit-learn tabanlı Isolation Forest model mimarisi.
*   `main.py`: Modeli eğiten ve canlı akışı başlatan ana çalıştırıcı.

##  Kurulum ve Çalıştırma (Installation)
1. Bağımlılıkları yükleyin:
   ```bash
   pip install -r requirements.txt