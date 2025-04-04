# 🧠 Pwnagotchi z Waveshare V4 na Raspberry Pi Zero / Zero 2 W

> **Custom image z gotową konfiguracją Pwnagotchi + sterownikami dla Waveshare V4**  
> Stworzony z myślą o łatwym starcie z urządzeniem Pwnagotchi na Raspberry Pi Zero W / Zero 2 W z ekranem e-ink Waveshare 2.13" V4 📟

---

## 🧪 Co to jest Pwnagotchi?

**Pwnagotchi** to AI-powered narzędzie do pasywnego zbierania handshake'ów WPA/WPA2 z sieci Wi-Fi, które można później analizować offline.  
Zasilany przez Raspberry Pi, działa w tle i "uczy się", jak lepiej zdobywać pakiety.  
Projekt: [https://pwnagotchi.ai](https://pwnagotchi.ai)

---

## 📥 Pobieranie obrazu

Gotowy do użycia obraz systemu znajdziesz tutaj:

➡️ **[Pobierz obraz Pwnagotchi Custom (dla Waveshare V4)](https://github.com/Qbaa134/Pwnagotchi-new-tutorial/releases/tag/PWN)**

Plik: `pwnagotchi64bit.img.xz`

---

## 🔥 Flashowanie na kartę SD (przez Raspberry Pi Imager)

1. Pobierz i zainstaluj [Raspberry Pi Imager](https://www.raspberrypi.com/software/)
2. Wybierz opcję: `Use Custom Image`
3. Wskaż pobrany plik `pwnagotchi64bit.img.xz`
4. Włóż kartę microSD (min. 8 GB), wybierz ją i kliknij `Write`
5. Na dysku `boot` wklej plik `config.toml`
6. Po zakończeniu, wyjmij i włóż kartę do Raspberry Pi Zero / Zero 2 W

---

## 🛠️ Pierwsze uruchomienie

1. Podłącz wyświetlacz e-ink **Waveshare 2.13 V4** do GPIO 
2. Podłącz zasilanie do Raspberry Pi Zero do portu `POWER`
3. Pierwsze uruchomienie może potrwać kilka minut – ekran e-ink zaktualizuje się automatycznie

---

## ⚙️ Konfiguracja `config.toml`

Plik `config.toml` powinien znajdujdować się w partycji `boot`, którą możesz edytować bezpośrednio po flashowaniu karty SD.

Przykład konfiguracji:

```toml
main.name = "YOUR_NAME"
main.lang = "en"
main.whitelist = [
  "EXAMPLE_NETWORK"
]
main.plugins.grid.enabled = true
main.plugins.grid.report = true
main.plugins.grid.exclude = [
  "YourHomeNetworkHere"
]

ui.display.enabled = true
ui.display.type = "waveshare_3"
ui.display.color = "black"

ui.web.username = "admin"
ui.web.password = "admin"
ui.web.enabled = true
ui.web.address = "0.0.0.0"
ui.web.origin = ""
ui.web.port = 9000
ui.web.on_frame = ""
```

Jeśli chcesz ustawić np. tryb manual, WiFi, lub inne parametry – sprawdź pełną dokumentację Pwnagotchi:
👉 https://pwnagotchi.ai/configuration/

## 📦 Sterownik
![image](https://github.com/user-attachments/assets/4a1b4b32-6f6e-42b3-9494-02ce01c785a8)
### Instalacja ręczna z ZIP:
1. Pobierz archiwum ZIP ze sterownikiem i rozpakuj je
2. Podłacz Rpi do komputera przez `Data Port`
3. Otwórz menadżer urządzeń na komputerze
4. Wejdź w  zakładkę porty `COM i LPT`
5. Powinniśmy zobaczyć podłaczone urządzenie do jednego z portów `COM` np.:`COM 6`
6. Klikamy prawym na nasz port i wchodzimy w `Właściwości`
7. W właściwościach przechodzimy do zakładki sterownik, a następnie klikamy aktualizuj sterownik
8. Wybieramy `Przegladaj mój komputer w poszukiwaniu sterowników` i wybieramy lokalizacje folderu z rozpakowanym sterownikiem
9. Teraz pobieramy nasz sterownik.

## Konfiguracja
1. Wchodzimy w ustawienia na komputerze i przechodzimy do zakładki sieci
2. Wchodzimy do `Zmień opcje karty`
3. Klikamy prawym przyciskiem na `Ethernet 2` i przechodzimy do właściwości
4. Klikamy `Protokół internetowy w wersji 4 (TCP/IPv4)`, a następnie właściwości
5. Wpisujemy Adres IP: `10.0.0.1`
6. Wpisujemy Maskę podsieci: `255.255.255.0`
7. Wpisujemy Preferowany serwer DNS: `1.1.1.1`
8. Wpisujemy Alternatywny serwer DNS: `8.8.8.8`
9. Zatwierdzamy i wychodzimy

## Logowanie przez CMD
1. Odpalamy CMD
2. Wpisujemy `ping pi@10.0.0.2`
3. Jeśli wszystko jest okej to możemy wpisać`ssh pi@10.0.0.2`, w polu hasła wpisujemy`raspberry`

# Możnawejść też wpisując w przeglądarce `http://pwnagotchi.local:8080/` lub klikając [link](http://pwnagotchi.local:8080/)

❓ FAQ
Q: Nie wyświetla mi nic na ekranie!
A: Upewnij się, że masz właściwą wersję Waveshare (V4), poprawnie podłączoną oraz wpis ui.display.type = "waveshare_3".

Q: Jak zgrać handshake?
A: Wszystkie pliki *.pcap będą zapisane w /root/handshakes/. Możesz je później analizować np. za pomocą hashcat.

