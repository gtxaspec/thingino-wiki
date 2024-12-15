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
