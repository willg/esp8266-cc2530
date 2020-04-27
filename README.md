# ESP8266 + CC2530
Board to integrate an ESP8266 + CC2530 + RF Front end

# RF Parts
[CC2530F256(radio)](https://lcsc.com/product-detail/RF-Transceiver-ICs_Texas-Instruments_CC2530F256RHAR_Texas-Instruments-TI-CC2530F256RHAR_C9120.html/?href=jlc-SMT)

## RF Front Ends
### RFX2401C
[RFX2401C](https://lcsc.com/product-detail/RF-Transceiver-ICs_Skyworks-Solutions_RFX2401C_Skyworks-Solutions-RFX2401C_C19213.html/?href=jlc-SMT)

> This is the RF front end that was on the 2530PA module I got from
> [Bangood](https://www.banggood.com/CC2530-UART-Wireless-Core-Development-Board-CC2530F256-Serial-Port-Wireless-Module-2_4GHz-For-Zigbee-p-1445025.html?utm_design=41&utm_source=emarsys&utm_medium=Neworder171109&utm_campaign=trigger-emarsys&utm_content=winna&sc_src=email_2675773&sc_eh=ddc2dc193b00c4611&sc_llid=10757429&sc_lid=105229698&sc_uid=wcY1TUr67W&cur_warehouse=CN),

RFX2401C Mode Truth Table:
| TXEN | RXEN | Mode |
| --- | --- | --- |
| 1 | X | TX Active
| 0 | 1 | RX Active
| 0 | 0 | Chip shutdown

CC2530 Control Connections **UNTESTED**:
| CC2530 | RFX2401C |
| --- | --- |
| P1_0 | RXEN
| P1_1 | TXEN

### CC2592
[CC2592](https://lcsc.com/product-detail/RF-Transceiver-ICs_Texas-Instruments_CC2592RGVR_Texas-Instruments-TI-CC2592RGVR_C53274.html/?href=jlc-SMT)

CC2592 Mode Truth Table:
| PA_EN | LNA_EN | HGM | Mode |
| --- | --- | --- | --- |
| 0 | 0 | X | Power Down
| X | 1 | 0 | RX Low-gain
| X | 1 | 1 | RX High-gain
| 1 | 0 | X | TX

CC2530 Control Connections:
| CC2592 | CC2530 |
| --- | --- |
| EN (LNA_EN) | P1_0
| PA_EN | P1_1
| HGM | P0_7
[Source](https://processors.wiki.ti.com/index.php/Enabling_the_Support_of_CC259x_PA/LNA_with_Z-Stack-Home)

### CC2591
This part is not recommended for new designs, and is out of stock at LCSC

## Regulator
[AMS1117-3.3](https://lcsc.com/product-detail/Low-Dropout-Regulators-LDO_AMS_AMS1117-3-3_AMS1117-3-3_C6186.html/?href=jlc-SMT)

AMS1117-3.3 Bypass. >22uF Tantalum 
[100uF 6.3V](https://lcsc.com/product-detail/Tantalum-Capacitors_AVX_TAJB107K006RNJ_100uF-107-10-6-3V_C16133.html/?href=jlc-SMT)

# ESP8266
## Option 1
Use Wemos D1-mini and interface via header

## Option 2
Use ESP8266MOD and integrate onto board
[ESP8266MOD](https://lcsc.com/product-detail/WIFI-Modules_ESP-12F-ESP8266MOD_C82891.html)
> not available for JLPCB to assemble

[CH340C (USB-UART
bridge)](https://lcsc.com/product-detail/USB_CH340C_C84681.html/?href=jlc-SMT)

# CC2530PA Notes
CC2530PA from banggood's connections:
| RFX2401C | CC2530 |
| --- | --- |
| TXEN | P1_5
| RXEN | P1_4

> I modified the z-stack zigbee firmware to have TXEN on PA1_5 and RXEN on P1_4
> and improved RF performance over the stock CC2530_CC2592 firmware, and seemed
> to be better than the CC2531 USB stick I have
