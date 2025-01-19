# Reflashing Dell L501x battery (JWPHF)
I replaced the original LG cells (**LGDBB11865**) with new Samsung ones (**INR18650-35E**). After the replacement, the BMS values were completely off, and the battery percentage reading was inaccurate. Therefore, the BMS values must be rewritten.

To connect to the battery, I used a **CP2112** in combination with Be2Works. For editing values, I used a free hex editor: **HxD**. The **GND**, **SDA**, and **SCL** pins of the board must be connected to the battery using the pinout provided below.


## Battery pinout
With the battery connector facing upwards, the minus sign on the case is on the left, and the plus sign is on the right. The battery connector has 9 pins.

Starting from the left:
1. **GND**
2. **GND**
3. *don't care*
4. *don't care*
5. *don't care*
6. **DATA**
7. **CLOCK**
8. V+
9. V+

## Changing values

In Be2Works after selecting **BQ20869** I was able to read/write meomory of th BMS.

```
OFFSET 				|		COLLUMN (0-15)

DesignCapacity  [mAh]      
00 00 00 30			|		0E  0F

FullChargeCapacity  [mAh]
00 00 00 40			|		02  03

CycleCount  [number]
00 00 00 00			|		0C  0D 

DesignVoltage  [mV]
00 00 00 00			|		04  05 

ManufacturerName  [ASCII]
00 00 00 00			|		0F
00 00 00 10			|		00  01  02  03  04  05  06

DeviceName  [ASCII]
00 00 00 10     |		0B  0C  0D  0E  0F
00 00 00 20     |		00  01  02  03  04  05  06  07  08? 09? 0A? 0B? 0C? 0D?

ChargingVoltage  [mV]
00 00 00 40			|		06  07

DeviceChemistry  [ASCII]
00 00 00 30			|		00  01  02  03
```

