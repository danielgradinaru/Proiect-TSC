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
- Proiect finalizat atat din punct de vedere al carcasei 3D cat si al PCB
- Dimensiuni compacte si aspect ergonomic

## Aplicatii posibile

- eBook Reader offline
- Afisaj pentru date locale (calendar, vreme)

## Bill of Materials

| Name          | Reference                                                                      | Technical Sheet                                                                                                                                                                       | Model Link                                                                                                             |
|:--------------|:-------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------|
| BOOT_BUTTON   | BUTTON_CUSYOMV1                                                                | [Datasheet](https://industry.panasonic.com/global/en/downloads?tab=catalog&small_g_cd=203&part_no=EVQPUJ02K)                                                                          | [3D Model](https://industry.panasonic.com/global/en/products/control/switch/light-touch/number/evqpuj02k)              |
| C1            | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| C1_BAT        | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| C1_BAT1       | EAGLE-LTSPICE_CC0402                                                           | [Datasheet](https://s3.amazonaws.com/snapeda/datasheet/CC0402DRNPO9BN5R1_Yageo.pdf)                                                                                                   | [3D Model](https://www.snapeda.com/parts/CC0402DRNPO9BN5R1/Yageo/view-part/?ref=dk&t=LTSPICE_CC0402&con_ref=None)      |
| C2_BAT1       | EAGLE-LTSPICE_CC0402                                                           | [Datasheet](https://s3.amazonaws.com/snapeda/datasheet/CC0402DRNPO9BN5R1_Yageo.pdf)                                                                                                   | [3D Model](https://www.snapeda.com/parts/CC0402DRNPO9BN5R1/Yageo/view-part/?ref=dk&t=LTSPICE_CC0402&con_ref=None)      |
| C1_BAT2       | EAGLE-LTSPICE_CC0402                                                           | [Datasheet](https://s3.amazonaws.com/snapeda/datasheet/CC0402DRNPO9BN5R1_Yageo.pdf)                                                                                                   | [3D Model](https://www.snapeda.com/parts/CC0402DRNPO9BN5R1/Yageo/view-part/?ref=dk&t=LTSPICE_CC0402&con_ref=None)      |
| C2            | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| C2_BAT        | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| C3            | RCL_CPOL-EUCT3528                                                              | [Datasheet](https://s3.amazonaws.com/snapeda/datasheet/TAJB475K025RNJ_AVX.pdf)                                                                                                        | [3D Model](https://www.snapeda.com/parts/TAJB475K025RNJ/AVX/view-part/?ref=dk&t=capacitor%203528&con_ref=None)         |
| C4            | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| C4_USB        | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| C5            | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| C5_USB        | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| C6            | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| C7            | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| C8            | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| C9            | EAGLE-LTSPICE_CC0402                                                           | [Datasheet](https://s3.amazonaws.com/snapeda/datasheet/CC0402DRNPO9BN5R1_Yageo.pdf)                                                                                                   | [3D Model](https://www.snapeda.com/parts/CC0402DRNPO9BN5R1/Yageo/view-part/?ref=dk&t=LTSPICE_CC0402&con_ref=None)      |
| C10           | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| C10_SUPERCAP  | CPH3225A                                                                       | [Datasheet](https://www.snapeda.com/parts/CPH3225A/Seiko%20Instruments/datasheet/)                                                                                                    | [3D Model](https://www.snapeda.com/parts/CPH3225A/Seiko+Instruments/view-part/?ref=eda)                                |
| CHANGE_BUTTON | BUTTON_CUSYOMV1                                                                | [Datasheet](https://industry.panasonic.com/global/en/downloads?tab=catalog&small_g_cd=203&part_no=EVQPUJ02K)                                                                          | [3D Model](https://industry.panasonic.com/global/en/products/control/switch/light-touch/number/evqpuj02k)              |
| CHG_LED       | ADAFRUIT_LEDCHIP-LED0603                                                       | [Datasheet](https://www.snapeda.com/parts/KP-1608SURCK/Kingbright/datasheet/)                                                                                                         | [3D Model](https://www.snapeda.com/parts/KP-1608SURCK/Kingbright/view-part/?ref=search&t=LED%200603)                   |
| C_DELAY       | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| D1            | USBLC6-2SC6Y                                                                   | [Datasheet](https://www.snapeda.com/parts/USBLC6-2SC6Y/STMicroelectronics/datasheet/)                                                                                                 | [3D Model](https://www.snapeda.com/parts/USBLC6-2SC6Y/STMicroelectronics/view-part/?ref=snap)                          |
| D2            | ESP32_WROVER_AVX---SD0805S020S1R0_AVX_SD0805S020S1R0_0_0AVX_SD0805S020S1R0_0_0 | [Datasheet](http://datasheets.avx.com/schottky.pdf)                                                                                                                                   | [3D Model](https://ro.mouser.com/ProductDetail/KYOCERA-AVX/SD0805S020S1R0?qs=jCA%252BPfw4LHbpkAoSnwrdjw%3D%3D)         |
| D3            | MBR0530                                                                        | [Datasheet](https://www.snapeda.com/parts/MBR0530/ON%20Semiconductor/datasheet/)                                                                                                      | [3D Model](https://www.snapeda.com/parts/MBR0530/Onsemi/view-part/?ref=eda)                                            |
| D4            | MBR0530                                                                        | [Datasheet](https://www.snapeda.com/parts/MBR0530/ON%20Semiconductor/datasheet/)                                                                                                      | [3D Model](https://www.snapeda.com/parts/MBR0530/Onsemi/view-part/?ref=eda)                                            |
| D5            | MBR0530                                                                        | [Datasheet](https://www.snapeda.com/parts/MBR0530/ON%20Semiconductor/datasheet/)                                                                                                      | [3D Model](https://www.snapeda.com/parts/MBR0530/Onsemi/view-part/?ref=eda)                                            |
| D6            | PGB1010603MR                                                                   | [Datasheet](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse%20Inc./datasheet/)                                                                                                  | [3D Model](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda)                                   |
| D7            | ESP32_WROVER_AVX---SD0805S020S1R0_AVX_SD0805S020S1R0_0_0AVX_SD0805S020S1R0_0_0 | [Datasheet](http://datasheets.avx.com/schottky.pdf)                                                                                                                                   | [3D Model](https://eu.mouser.com/ProductDetail/KYOCERA-AVX/SD0805S020S1R0?qs=jCA%252BPfw4LHbpkAoSnwrdjw%3D%3D)         |
| D8            | PGB1010603MR                                                                   | [Datasheet](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse%20Inc./datasheet/)                                                                                                  | [3D Model](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda)                                   |
| D9            | PGB1010603MR                                                                   | [Datasheet](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse%20Inc./datasheet/)                                                                                                  | [3D Model](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda)                                   |
| D10           | PGB1010603MR                                                                   | [Datasheet](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse%20Inc./datasheet/)                                                                                                  | [3D Model](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda)                                   |
| D11           | PGB1010603MR                                                                   | [Datasheet](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse%20Inc./datasheet/)                                                                                                  | [3D Model](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda)                                   |
| D12           | PGB1010603MR                                                                   | [Datasheet](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse%20Inc./datasheet/)                                                                                                  | [3D Model](https://www.snapeda.com/parts/PGB1010603MR/Littelfuse/view-part/?ref=eda)                                   |
| EPD_C1        | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| EPD_C2        | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| EPD_C5        | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| EPD_C6        | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| EPD_C7        | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| EPD_C8        | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| EPD_C9        | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| EPD_C10       | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| EPD_C11       | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| EPD_C12       | ESP32_WROVER_EAGLE-LTSPICE_CC0402                                              | [Datasheet](https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf)                                                                                                     | [3D Model](https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO)                                        |
| IC1           | BD5229G-TR                                                                     | [Datasheet](https://datasheet.datasheetarchive.com/originals/distributors/Datasheets_SAMA/f2b9741ef86007909f138d561a359946.pdf)                                                       | [3D Model](https://componentsearchengine.com/part-view/BD5229G-TR/ROHM%20Semiconductor)                                |
| IC4           | XC6220A331MR-G                                                                 | [Datasheet](https://product.torexsemi.com/system/files/series/xc6220.pdf)                                                                                                             | [3D Model](https://componentsearchengine.com/part-view/XC6220A331MR-G/Torex)                                           |
| J1            | FH34SRJ-24S-0.5SH_99_                                                          | [Datasheet](https://www.hirose.com/en/product/document?clcode=CL0580-1255-6-99&productname=FH34SRJ-24S-0.5SH(99)&series=FH34SRJ&documenttype=2DDrawing&lang=en&documentid=0000990903) | [3D Model](https://componentsearchengine.com/part-view/FH34SRJ-24S-0.5SH(99)/Hirose)                                   |
| J2            | SAMACSYS_PARTS_USB4110-GF-A                                                    | [Datasheet](https://gct.co/files/drawings/usb4110.pdf)                                                                                                                                | [3D Model](https://componentsearchengine.com/part-view/USB4110-GF-A/GCT%20(GLOBAL%20CONNECTOR%20TECHNOLOGY))           |
| J3            | QWIIC_CONNECTORJS-1MM                                                          | [Datasheet](https://eu.mouser.com/ProductDetail/Adafruit/4208?qs=PzGy0jfpSMtbScLbr0L5dw%3D%3D)                                                                                        | [3D Model](https://grabcad.com/library/sparkfun-qwiic-right-angle-1)                                                   |
| J4            | 112A-TAAR-R03_ATTEND                                                           | [Datasheet](https://store.comet.srl.ro/Catalogue/Product/43497/)                                                                                                                      | [3D Model](https://store.comet.srl.ro/Catalogue/Product/43497/)                                                        |
| L1            | 744043680IND_4828-WE-TPC_WRE                                                   | [Datasheet](https://www.we-online.com/components/products/datasheet/744043680.pdf)                                                                                                    | [3D Model](https://ro.mouser.com/ProductDetail/Wurth-Elektronik/744043680?qs=PGXP4M47uW6VkZq%252BkzjrHA%3D%3D)         |
| PFMF.050.1    | ESP32C6_VARISTORCN1812                                                         | [Datasheet](https://www.mouser.co.uk/ProductDetail/EPCOS-TDK/B72520T0350K062?qs=dEfas%2FXlABIszF52uu7vrg%3D%3D)                                                                       | [3D Model](https://www.mouser.co.uk/ProductDetail/EPCOS-TDK/B72520T0350K062?qs=dEfas%2FXlABIszF52uu7vrg%3D%3D)         |
| Q1            | ESP32_WROVER_SPARKFUN-DISCRETESEMI_MOSFET_PCH-DMG2305UX-7                      | [Datasheet](https://www.diodes.com//assets/Datasheets/DMG2305UX.pdf)                                                                                                                  | [3D Model](https://componentsearchengine.com/part-view/DMG2305UX-7/Diodes%20Incorporated)                              |
| Q2            | ESP32_WROVER_SPARKFUN-DISCRETESEMI_MOSFET_PCH-DMG2305UX-7                      | [Datasheet](https://www.diodes.com//assets/Datasheets/DMG2305UX.pdf)                                                                                                                  | [3D Model](https://componentsearchengine.com/part-view/DMG2305UX-7/Diodes%20Incorporated)                              |
| Q3            | D8                                                                             | [Datasheet](https://componentsearchengine.com/Datasheets/1/SI1308EDL-T1-GE3.pdf)                                                                                                      | [3D Model](https://componentsearchengine.com/part-view/SI1308EDL-T1-GE3/Vishay)                                        |
| R1            | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R1-PINH       | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R1-PINH1      | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R1_BAT        | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R1_PWRUSB     | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R2            | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R2-PINH       | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R2-PINH1      | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R2-USB        | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R2-USB1       | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R2_BAT        | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R3            | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R4            | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R5            | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R6            | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R7            | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R8            | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R9            | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R10           | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| RESET_BUTTON  | BUTTON_CUSYOMV1                                                                | [Datasheet](https://industry.panasonic.com/global/en/downloads?tab=catalog&small_g_cd=203&part_no=EVQPUJ02K)                                                                          | [3D Model](https://industry.panasonic.com/global/en/products/control/switch/light-touch/number/evqpuj02k)              |
| R_BOOT        | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R_CAPACITOR   | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R_CHANGE      | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R_CL1         | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| R_RESET       | ESP32_WROVER_EAGLE-LTSPICE_RR0402                                              | [Datasheet](https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf)                                                                        | [3D Model](https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO)              |
| SENSOR2       | ESP32_WROVER_BME680_BME680                                                     | [Datasheet](https://www.snapeda.com/parts/BME680/Bosch%20Sensortec/datasheet/)                                                                                                        | [3D Model](https://www.snapeda.com/parts/BME680/Bosch/view-part/?welcome=home)                                         |
| SJ1           | SJ                                                                             | [Datasheet](https://www.digikey.com/en/htmldatasheets/production/1809569/0/0/1/jumpers)                                                                                               | [3D Model](https://grabcad.com/library/solder-jumpers-1)                                                               |
| U1            | W25Q512JVEIQ                                                                   | [Datasheet](https://www.snapeda.com/parts/W25Q512JVEIQ/Winbond%20Electronics/datasheet/)                                                                                              | [3D Model](https://www.snapeda.com/parts/W25Q512JVEIQ/Winbond+Electronics/view-part/?ref=eda)                          |
| U2            | ESP32-C6-WROOM-1-N8                                                            | [Datasheet](https://www.snapeda.com/parts/ESP32-C6-WROOM-1-N8/Espressif%20Systems/datasheet/)                                                                                         | [3D Model](https://www.snapeda.com/parts/ESP32-C6-WROOM-1-N8/Espressif+Systems/view-part/?ref=eda)                     |
| U3            | DS3231SN#                                                                      | [Datasheet](https://www.snapeda.com/parts/DS3231SN%23/Analog%20Devices/datasheet/)                                                                                                    | [3D Model](https://www.snapeda.com/parts/DS3231SN%23/Analog+Devices/view-part/?ref=eda)                                |
| U4            | MAX17048G+T10                                                                  | [Datasheet](https://www.snapeda.com/parts/MAX17048G+T10/Analog%20Devices/datasheet/)                                                                                                  | [3D Model](https://www.snapeda.com/parts/MAX17048G+T10/Analog+Devices/view-part/?ref=eda)                              |
| U5            | ESP32_WROVER_SPARKFUN-IC-POWER_MCP73831                                        | [Datasheet](https://ro.mouser.com/datasheet/2/268/MCP73831_Family_Data_Sheet_DS20001984H-3441711.pdf)                                                                                 | [3D Model](https://ro.mouser.com/ProductDetail/Microchip-Technology/MCP73831T-2ACI-OT?qs=yUQqVecv4qvbBQBGbHx0Mw%3D%3D) |
| TP1           | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP2           | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP3           | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP4           | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP5           | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP6           | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP7           | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP8           | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP9           | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP10          | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP11          | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP12          | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP13          | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP14          | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP15          | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
| TP16          | TPTP20R                                                                        |                                                                                                                                                                                       |                                                                                                                        |
