# OpenBook - Open Source e-Book Reader

![Diagrama BLOC](Images/diagram.png)

---

## Functionalitate hardware

Dispozitivul OpenBook integreaza o serie de module si componente menite sa ofere o experienta completa pentru citirea cartilor in format digital, precum si extinderea functiilor prin senzori si periferice externe. Hardware-ul este compus din mai multe blocuri functionale, fiecare avand rolul. Am integrat atat componente de interfata (buton, ecran), cat si senzori, circuite de alimentare si protectie.

### Componente principale:

## Dispozitivul este compus dintr-un set de componente atent alese pentru a oferi un echilibru perfect intre performanta, consum redus de energie si modularitate. ##
|  Componenta            | Descriere                                                      |
|---------------------------|----------------------------------------------------------------|
|ESP32-C6-WROOM-1-N8  | MCU principal cu WiFi 6, BLE 5.0, SPI, I2C, UART               |
|E-paper Display | Afisaj ultra-low power, interfata SPI                          |
|SD Card         | Stocare pentru fisiere e-book si configurari                   |
|NOR Flash 64MB  | Memorie suplimentara pentru firmware si date                   |
|RTC-DS3231SN | Ceas in timp real, exact si stabil                             |
|    BME688   | Senzor de mediu complet: T, RH, presiune, VOC                  |
| MAX17048    | Masurare SoC baterie, tensiune, temperatura                  |
|MCP73831     | Incarcare LiPo simpla si eficienta                           |
|XC6220 LDO      | Regulare 5V -> 3.3V cu zgomot scazut                            |
|USB-C           | Alimentare + flash firmware + protectie ESD                   |
|Qwiic/Stemma QT | Extensie rapida pentru senzori I2C                            |



---

## Pinout ESP32-C6

Mai jos este un rezumat al pinilor folositi pe microcontroller, cu functiile si componenta asociata:

| GPIO  | Componenta        | Functie                     |
|--------|--------------------|-----------------------------|
| EN     | Buton Reset        | Reset hardware              |
| IO0    | RTC                | INT_RTC (interupt RTC)      |
| IO1    | RTC                | 32KHz output                |
| IO2    | SD Card            | MISO                        |
| IO3    | E-paper Display    | EPD_BUSY                    |
| IO4    | SD Card            | SS_SD (chip select)         |
| IO5    | E-paper Display    | EPD_DC                      |
| IO6    | SPI Shared         | SCK                         |
| IO7    | SPI Shared         | MOSI                        |
| IO8    | GPIO               | Utilizare generica          |
| IO9    | Boot Button        | Mod programare              |
| IO10   | E-paper Display    | EPD_CS                      |
| IO11   | NOR Flash          | FLASH_CS                    |
| IO12   | USB Interface      | USB_D-                      |
| IO13   | USB Interface      | USB_D+                      |
| IO15   | Buton Change       | Detectare schimbare         |
| IO16   | UART               | TX (debug serial)           |
| IO17   | UART               | RX (debug serial)           |
| IO18   | RTC                | RTC_RST                     |
| IO19   | MAX17048           | I2C_PW (alimentare I2C)     |
| IO20   | E-paper Display    | EPD_3V3_C (power control)   |
| IO21   | I2C Shared         | SDA                         |
| IO22   | I2C Shared         | SCL                         |
| IO23   | E-paper Display    | EPD_RST                     |

---

## Arhitectura si comunicatii

- **SPI Bus** este partajat intre: SD Card, E-paper Display, NOR Flash
- **I2C Bus** este partajat intre: RTC, BME688, MAX17048, Qwiic port
- **UART** este utilizat pentru debugging (TX/RX)
- **USB-C** foloseste GPIO dedicate pentru DP/DM si incarcare

---

# BOM TSC - Lista de componente

| Nr. piesa | Nume piesa | Site | Datasheet |
| --- | --- | --- | --- |
| 1 | BOOT_BUTON | https://www.snapeda.com/parts/EVQP7L01P/Panasonic%20Electronic%20Components/view-part/?welcome=home | https://www.snapeda.com/parts/EVQP7L01P/Panasonic/datasheet/ |
| 2 | C1, C1_BAT, C1_BAT2, C2,C2_BAT,C3,C4,C4_USB, C5, C5_USB, C6, C7, C8, C9,C10 | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO | https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf |
| 3 | C10_SUPERCAR | https://industry.panasonic.com/global/en/products/control/switch/light-touch/number/evqpuj02k | https://industry.panasonic.com/global/en/downloads?tab=catalog&small_g_cd=203&part_no=EVQPUJ02K |
| 4 | CHANGE_BUTTON | https://www.snapeda.com/parts/EVQP7L01P/Panasonic%20Electronic%20Components/view-part/?welcome=home | https://www.snapeda.com/parts/EVQP7L01P/Panasonic/datasheet/ |
| 5 | C_DELAY | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO | https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf |
| 6 | D1 | https://www.snapeda.com/parts/USBLC6-2SC6Y/STMicroelectronics/view-part/?ref=eda | https://www.snapeda.com/parts/USBLC6-2SC6Y/STMicroelectronics/view-part/?ref=eda |
| 7 | EPD_C1,EPD_C2, EPD_C3, EPD_C4, EPD_C5,EPD_C6,EPD_C7,EPD_C8,EPD_C9,EPD_C10,EPD_C11,EPD_C12 | https://componentsearchengine.com/part-view/CC0402MRX5R5BB106/YAGEO | https://componentsearchengine.com/Datasheets/2/CC0402MRX5R5BB106.pdf |
| 8 | IC1 | https://componentsearchengine.com/part-view/BD5229G-TR/ROHM%20Semiconductor | https://datasheet.datasheetarchive.com/originals/distributors/Datasheets_SAMA/f2b9741ef86007909f138d561a359946.pdf |
| 9 | IC4 | https://componentsearchengine.com/part-view/XC6220A331MR-G/Torex | https://product.torexsemi.com/system/files/series/xc6220.pdf |
| 10 | J1 | https://componentsearchengine.com/part-view/FH34SRJ-24S-0.5SH(99)/Hirose | https://www.hirose.com/en/product/document?clcode=CL0580-1255-6-99&productname=FH34SRJ-24S-0.5SH(99)&series=FH34SRJ&documenttype=2DDrawing&lang=en&documentid=0000990903 |
| 11 | J2 | https://componentsearchengine.com/part-view/USB4110-GF-A/GCT%20(GLOBAL%20CONNECTOR%20TECHNOLOGY) | https://gct.co/files/drawings/usb4110.pdf |
| 12 | J3,J4 | https://www.snapeda.com/parts/PRT-14417/SparkFun/view-part/ | https://www.snapeda.com/parts/PRT-14417/SparkFun%20Electronics/datasheet/ |
| 13 | MCP73831 | https://ro.mouser.com/ProductDetail/Microchip-Technology/MCP73831T-2ACI-OT?qs=yUQqVecv4qvbBQBGbHx0Mw%3D%3D&utm_id=20109199409&utm_source=google&utm_medium=cpc&utm_marketing_tactic=emeacorp&gad_source=1&gbraid=0AAAAADn_wf0-USzm1eg1ywGvQg_qMgG3H | https://ro.mouser.com/datasheet/2/268/MCP73831_Family_Data_Sheet_DS20001984H-3441711.pdf |
| 14 | L1 | https://ro.mouser.com/ProductDetail/Wurth-Elektronik/744043680?qs=PGXP4M47uW6VkZq%252BkzjrHA%3D%3D | https://www.we-online.com/components/products/datasheet/744043680.pdf |
| 15 | PFMF.050.1 | https://ro.mouser.com/ProductDetail/EPCOS-TDK/B72520T0350K062?qs=dEfas%2FXlABIszF52uu7vrg%3D%3D | https://www.tdk-electronics.tdk.com/inf/75/db/CTVS_14/Surge_protection_series.pdf |
| 16 | Q1,Q2 | https://componentsearchengine.com/part-view/DMG2305UX-7/Diodes%20Incorporated | https://www.diodes.com//assets/Datasheets/DMG2305UX.pdf |
| 17 | Q3 | https://componentsearchengine.com/part-view/SI1308EDL-T1-GE3/Vishay | https://componentsearchengine.com/part-view/SI1308EDL-T1-GE3/Vishay |
| 18 | Rezistente | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO | https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf |
| 19 | RESET_BUTTON | https://www.snapeda.com/parts/EVQP7L01P/Panasonic%20Electronic%20Components/view-part/?welcome=home | https://www.snapeda.com/parts/EVQP7L01P/Panasonic/datasheet/ |
| 20 | R_BOOT | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO | https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf |
| 21 | R_CAPACITOR | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO | https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf |
| 22 | R_CHANGE | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO | https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf |
| 23 | R_CL1 | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO | https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf |
| 24 | R_RESET | https://componentsearchengine.com/part-view/R0402%201%25%20100%20K%20(RC0402FR-07100KL)/YAGEO | https://www.yageo.com/upload/media/product/products/datasheet/rchip/PYu-RC_Group_51_RoHS_L_12.pdf |
| 26 | SENSOR2 | https://www.snapeda.com/parts/BME680/Bosch/view-part/?welcome=home | https://www.snapeda.com/parts/BME680/Bosch%20Sensortec/datasheet/ |
| 27 | SJ1 | https://grabcad.com/library/solder-jumpers-1 | https://grabcad.com/library/solder-jumpers-1 |
| 28 | U1 | https://www.snapeda.com/parts/W25Q512JVEIQ/Winbond+Electronics/view-part/?ref=eda | https://www.snapeda.com/parts/W25Q512JVEIQ/Winbond+Electronics/view-part/?ref=eda |
| 29 | U2 | https://www.snapeda.com/parts/ESP32-C6-WROOM-1-N8/Espressif+Systems/view-part/?ref=eda | https://www.snapeda.com/parts/ESP32-C6-WROOM-1-N8/Espressif%20Systems/datasheet/ |
| 30 | U3 | https://www.snapeda.com/parts/DS3231SN%23/Analog+Devices/view-part/?ref=eda | https://www.snapeda.com/parts/DS3231SN%23/Analog%20Devices/datasheet/ |
| 31 | U4 | https://www.snapeda.com/parts/MAX17048G+T10/Analog+Devices/view-part/?ref=eda | https://www.snapeda.com/parts/MAX17048G+T10/Analog%20Devices/datasheet/ |






