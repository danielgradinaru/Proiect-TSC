# eBook Reader
![Diagram](https://github.com/user-attachments/assets/a279c5c8-ad81-4aaf-95b0-fadf8f1237b3)
Proiect hardware complet pentru un eBook Reader portabil, cu consum redus de energie, afisaj E-Paper si conectivitate moderna, proiectat in jurul microcontrollerului ESP32-C6-WROOM-1-N8.

# Arhitectura Hardware

## Microcontroller

### ESP32-C6-WROOM-1-N8
- Core RISC-V
- Conectivitate: Wi-Fi 6, Bluetooth 5
- Criptografie hardware
- [Specificații oficiale](https://www.espressif.com/en/products/modules/esp32-c6)

### Memorie Flash externă
- **W25Q512JVEIQ** – 64MB, conectată prin SPI

### Interfețe disponibile
- I2C, SPI și GPIO dedicate componentelor externe

---

## Alimentare

### USB-C (PMF0501)
- Intrare de 5V din surse standard

### Protecție ESD (USBLC6-2SC6Y)
- Protecție bidirecțională pentru liniile USB

### Încărcător Li-Po (MCP73831)
- Circuit simplu de încărcare pentru o celulă Li-Po (max. 500mA)

### Baterie
- Li-Po 3.7V

### Regulator LDO (MCP1700-3302E)
- Reglează tensiunea la 3.3V pentru alimentarea majorității componentelor

---

## Afișaj E-Ink

### Conector MP1
- Compatibil cu ecrane E-Ink de 1.54", 200x200px

### Circuit de alimentare pentru afișaj
- Componente: Q3 (tranzistor), L1 (inductor), D2 (diodă)
- Rol: generare tensiune specifică pentru EPD

### Selector tip display (SJ1)
- Jumpere pentru alegerea tipului de ecran

### Interfață
- SPI + GPIO, conectat direct la ESP32-C6

---

## Memorie Externă

- **Card SD (U4)** – pentru stocarea fișierelor eBook (conectat prin SPI)
- **64MB NOR Flash (W25Q512JVEIQ)** – memorie extinsă pentru firmware, fonturi, imagini (conectată pe SPI dedicat)

---

## Senzori și Periferice

### BME688
- Senzor pentru temperatură, umiditate, presiune și compuși volatili (VOCs)
- Comunicație: I2C

### RTC – DS3231SN
- Modul de timp real de înaltă precizie
- Comunicație: I2C

### MAX17048G-T10
- Fuel gauge pentru monitorizarea nivelului bateriei
- Comunicație: I2C

### Butoane (BD5229)
- Butoane Reset și Boot
- Conectate pe pini GPIO configurabili

### Qwiic / Stemma QT (J5)
- Conector pentru extensii rapide I2C

---


## Conexiuni ESP32-C6 (pini utilizati)

| Componenta     | Interfata  | Pini ESP32-C6                      | Observatii                    |
|----------------|------------|------------------------------------|-------------------------------|
| SD Card        | SPI        | GPIO10, GPIO11, GPIO12, GPIO13     | Bus SPI pentru card SD        |
| NOR Flash      | SPI        | GPIO6, GPIO7, GPIO8, GPIO9         | Bus SPI separat               |
| E-Ink Display  | SPI + GPIO | GPIO18, GPIO19, GPIO20, GPIO21     | Control display si date       |
| BME688         | I2C        | GPIO1 (SDA), GPIO2 (SCL)           | Bus comun I2C                 |
| DS3231         | I2C        | GPIO1 (SDA), GPIO2 (SCL)           | Comun cu ceilalti senzori     |
| MAX17048       | I2C        | GPIO1 (SDA), GPIO2 (SCL)           | Comun cu ceilalti senzori     |
| Butoane        | GPIO       | GPIO0 (RST), GPIO3 (BOOT)          | Control de sistem             |
| Test Pads      | GPIO/UART  | GPIO17, GPIO22                     | Debug                         |
| Stemma/Qwiic   | I2C        | GPIO1 (SDA), GPIO2 (SCL)           | Extensii rapide               |

---

## Estimare consum de energie

| Modul                  | Consum mediu        |
|------------------------|---------------------|
| ESP32-C6 activ         | ~80-100 mA          |
| ESP32-C6 deep sleep    | ~10 uA              |
| E-Ink refresh          | ~25 mA (temporar)   |
| SD Card (idle/acces)   | ~2 mA / ~50 mA      |
| RTC + BME688 standby   | ~3-5 uA             |
| MAX17048               | ~3 uA               |

**Durata estimata cu baterie 500mAh:**

- Utilizare medie: ~15-20 ore
- Standby (deep sleep): pana la cateva saptamani

---

## Informatii suplimentare

### Structura hardware
- Utilizare medie: ~15-20 ore
- Standby (deep sleep): pana la cateva saptamani

- PCB proiectat cu atentie la separarea blocurilor: alimentare, MCU, afisaj, senzori
- Plan de masa comun, trasee protejate si optimizate
- Mufe si conectori accesibili extern (USB, butoane, afisaj)

### Randari 3D si carcasa

- Randari disponibile cu componentele plasate
- Proiect finalizat atat din punct de vedere al crcasei 3D cat si al PCB
- Dimensiuni compacte si aspect ergonomic

## Aplicatii posibile

- eBook Reader offline
- Afisaj pentru date locale (calendar, vreme)

Bill of Materials

[Bill of Materials.xlsx](https://github.com/user-attachments/files/19621827/Bill.of.Materials.xlsx)
