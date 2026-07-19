import time
import random
from src.logger_sim import LogSimulator
from src.detector import AnomalyDetector
from colorama import init, Fore, Style

init(autoreset=True)

def main():
    print(Fore.CYAN + "=== Yapay Zeka Destekli Siber Tehdit Tespit Sistemi ===")
    sim = LogSimulator()
    detector = AnomalyDetector()

    print(Fore.YELLOW + "[*] Normal trafik verisi toplanıyor ve model eğitiliyor...")
    training_data = [sim.generate_normal_log() for _ in range(200)]
    detector.train(training_data)
    print(Fore.GREEN + "[+] Model başarıyla eğitildi. Canlı log takibi başlıyor...\n")

    try:
        while True:
            if random.random() < 0.15:
                log = sim.generate_anomaly_log()
            else:
                log = sim.generate_normal_log()

            result = detector.predict(log)

            if result == "ANOMALY/THREAT":
                print(Fore.RED + Style.BRIGHT + f"[TEHDİT YAKALANDI] IP: {log['ip']} | İstek/Dk: {log['request_count_per_min']} | Boyut: {log['response_size']} byte | Durum: {log['status_code']}")
            else:
                print(Fore.GREEN + f"[NORMAL] IP: {log['ip']} | İstek: {log['request_count_per_min']} | Durum: {log['status_code']}")

            time.sleep(0.5)

    except KeyboardInterrupt:
        print(Fore.CYAN + "\n[-] Sistem durduruldu.")

if __name__ == "__main__":
    main()