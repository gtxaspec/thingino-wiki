Eufy E210 Outdoor Cam  
FCCID: `2AOKB-T8441`

## Device Specifications

### Hardware
| Component      | Details          |
|----------------|------------------|
| **SoC**        | Ingenic T31X     |
| **Sensor**     | SC3336           |
| **Flash**      | 32MB             |
| **WiFi**       | bcm43438a1       |
| **Ethernet**   | None             |
| **Power**      | USB              |
| **Data**       | USB              |

### LEDs
| Type           | Details          |
|----------------|------------------|
| **Status LED** | Blue / Red       |
| **White LEDs** | 2x White LEDs    |
| **IR LEDs**    | 850nm x4         |

![image](https://github.com/user-attachments/assets/a31a1c05-d041-4058-bffa-afd266151ae4)

---

Unusual hardware design for LED control:

Observations:

```mermaid
graph TD
    PS1[24V Power Supply - White LED] --> GPIO6[GPIO 6 - Global Enable]
    PS2[8V Power Supply - IR LED] --> GPIO6

    GPIO6 --> GPIO7[GPIO 7 - Mode Selector]
    GPIO6 --> GPIO59[GPIO 59 - White LED Control]
    GPIO7 --> GPIO60[GPIO 60 - Shared Driver]

    GPIO59 --> WhiteLED[White LED]
    GPIO60 --> WhiteLED
    GPIO60 --> IRLED[IR LED]
```

---

| Mode           | GPIO 6   | GPIO 7   | GPIO 59  | GPIO 60  |
|----------------|----------|----------|----------|----------|
| White LED ON   | Set (1)  | Clear (0)| Set (1)  | Set (1)  |
| White LED OFF  | Clear (0)| Clear (0)| Clear (0)| Clear (0)|
| IR LED ON      | Set (1)  | Set (1)  | Clear (0)| Set (1)  |
| IR LED OFF     | Clear (0)| Clear (0)| Clear (0)| Clear (0)|
| Both LEDs ON   | Set (1)  | Set (1)  | Set (1)  | Set (1)  |
| Both LEDs OFF  | Set (1)  | Set (1)  | Clear (0)| Clear (0)|
