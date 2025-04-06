# eBook Reader
![Diagram](https://github.com/user-attachments/assets/a279c5c8-ad81-4aaf-95b0-fadf8f1237b3)
Proiect hardware complet pentru un eBook Reader portabil, cu consum redus de energie, afisaj E-Paper si conectivitate moderna, proiectat in jurul microcontrollerului ESP32-C6-WROOM-1-N8.

Arhitectura hardware
Microcontroller
ESP32-C6-WROOM-1-N8
-RISC-V core, Wi-Fi 6, Bluetooth 5, criptografie hardware (informatii preluate din https://www.espressif.com/en/products/modules/esp32-c6)
-Memorie Flash externa de 64MB (W25Q512JVEIQ) – conectata prin SPI.
-Conexiuni I2C, SPI si GPIO dedicate componentelor externe.

Alimentare
-USB-C (PMF0501)
--Intrare de 5V din surse standard.
-Protectie ESD (USBLC6-2SC6Y)
--Protectie bidirectionala pentru liniile USB.
-Incarcator Li-Po (MCP73831)
--Circuit simplu de incarcare pentru o celula Li-Po (max 500mA).
-Baterie Li-Po 3.7V
-Regulator LDO 3.3V (MCP1700-3302E)
--Regleaza tensiunea la 3.3V pentru a alimenta majoritatea componentelor.

Afisaj E-Ink
-Header pentru E-Ink Display (MP1)
--Compatibil cu ecrane E-Paper de 1.54", 200x200px.
-Circuit de putere pentru afisaj:
--Include Q3 (transistor), L1 (inductor), D2 (dioda) – pentru generarea tensiunii specifice EPD.
-Selector de tip display (SJ1)
--Jumpere pentru alegerea tipului de ecran.
Interfata:
SPI + GPIO control, conectat direct la ESP32-C6.

Memorie externa
-SD Card (U4)
--Stocare pentru fisierele eBook. Conectat prin SPI.
-64MB NOR Flash (W25Q512JVEIQ)
--Memorie extinsa pentru firmware, fonturi, imagini. Conectat pe bus SPI dedicat.

Senzori si periferice
-BME688
*Senzor de temperatura, umiditate, presiune si compusi volatili (VOCs).
*Comunicatie: I2C

-RTC – DS3231SN
*Modul de timp real de inalta precizie.
*Comunicatie: I2C

-MAX17048G-T10
*Fuel gauge pentru monitorizarea nivelului bateriei.
*Comunicatie: I2C

-Butoane (BD5229)
*Reset si Boot, conectate pe pini GPIO configurabili.

-Qwiic / Stemma QT (J5)
*Conector pentru extensii rapide I2C.

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
