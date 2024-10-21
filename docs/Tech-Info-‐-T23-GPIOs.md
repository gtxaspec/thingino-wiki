# T23 GPIO Function List

**Voltage Domains**: VDDIO0(1.8V), VDDIO1(1.8/3.3V)

## IO Functions Multiplexing

### PA Group
| GPIO  | FUNC0      | FUNC1       | FUNC2         | FUNC3                             | Default Status | Voltage Domain | pin number in QFN |
|-------|------------|-------------|---------------|-----------------------------------|----------------|---------------|-------------------|
| DVP_D0| MIPI_DATAP1| -           | -             | Note: Analog IO, MIPI DVP multiplexing relationship | -             | MIPI18V       | 29            |
| DVP_D1| MIPI_DATAN1| -           | -             | Note: Analog IO, MIPI DVP multiplexing relationship | -             | MIPI18V       | 28            |
| DVP_D2| MIPI_CLKP  | -           | -             | Note: Analog IO, MIPI DVP multiplexing relationship | -             | MIPI18V       | 27            |
| DVP_D3| MIPI_CLKN  | -           | -             | Note: Analog IO, MIPI DVP multiplexing relationship | -             | MIPI18V       | 26            |
| DVP_D4| MIPI_DATAP0| -           | -             | Note: Analog IO, MIPI DVP multiplexing relationship | -             | MIPI18V       | 25            |
| DVP_D5| MIPI_DATAN0| -           | -             | Note: Analog IO, MIPI DVP multiplexing relationship | -             | MIPI18V       | 24            |
| PA06  | DVP_D6     | UART2_TxD   | MSC1_D1       | -                                 | Z              | VDDIO0        | 23            |
| PA07  | MIPI_SEL   | DVP_D7      | UART2_RxD     | MSC1_D2                           | Z              | VDDIO0        | 22            |
| PA12  | -          | SMB0_SDA    | -             | -                                 | Pullup         | VDDIO0        | 13            |
| PA13  | -          | SMB0_SCK    | -             | -                                 | Pullup         | VDDIO0        | 12            |
| PA14  | DVP_PCLK   | PWM0        | MSC1_CLK      | -                                 | Z              | VDDIO0        | 17            |
| PA15  | DVP_MCLK   | -           | -             | -                                 | Z              | VDDIO0        | 16            |
| PA16  | DVP_HSYNC  | SMB1_SDA    | MSC1_D0       | -                                 | Z              | VDDIO0        | 15            |
| PA17  | DVP_VSYNC  | SMB1_SCK    | MSC1_CMD      | -                                 | Z              | VDDIO0        | 14            |
| PA18  | -          | -           | -             | MSC1_D3                           | Z              | VDDIO0        | 11            |
| PA23  | SFC_DT     | -           | -             | -                                 | Pullup         | VDDIO1        | 47            |
| PA24  | SFC_DR     | -           | -             | -                                 | Pullup         | VDDIO1        | 46            |
| PA27  | SFC_CLK    | -           | -             | -                                 | Pullup         | VDDIO1        | 48            |
| PA28  | SFC_CE0    | -           | -             | -                                 | Pullup         | VDDIO1        | 45            |

### PB Group
| GPIO  | FUNC0      | FUNC1       | FUNC2         | FUNC3            | Default Status | Voltage Domain | pin number in QFN |
|-------|------------|-------------|---------------|------------------|----------------|---------------|-------------------|
| PB00  | MSC0_D0    | -           | -             | -                | Z              | VDDIO1        | 50                |
| PB01  | MSC0_D1    | -           | -             | -                | Z              | VDDIO1        | 49                |
| PB02  | MSC0_D2    | -           | -             | -                | Z              | VDDIO1        | 54                |
| PB03  | MSC0_D3    | -           | -             | -                | Z              | VDDIO1        | 53                |
| PB04  | MSC0_CLK   | -           | -             | -                | Z              | VDDIO1        | 51                |
| PB05  | MSC0_CMD   | -           | -             | -                | Z              | VDDIO1        | 52                |
| PB06  | GMAC_TXCLK | -           | -             | SLCD_D0          | Z              | VDDIO1        | 62                |
| PB07  | GMAC_PHY_CLK | -         | -             | SLCD_D1          | Z              | VDDIO1        | 63                |
| PB08  | GMAC_TXEN  | MSC1_CLK    | -             | SLCD_D2          | Z              | VDDIO1        | 66                |
| PB09  | GMAC_RXDV  | MSC1_CMD    | -             | SLCD_D3          | Z              | VDDIO1        | 59                |
| PB10  | GMAC_MDCK  | MSC1_D0     | -             | SLCD_D4          | Z              | VDDIO1        | 58                |
| PB11  | GMAC_MDIO  | MSC1_D1     | -             | SLCD_D5          | Z              | VDDIO1        | 57                |
| PB13  | GMAC_TXD0  | MSC1_D2     | -             | SLCD_D6          | Z              | VDDIO1        | 64                |
| PB14  | GMAC_TXD1  | MSC1_D3     | -             | SLCD_D7          | Z              | VDDIO1        | 65                |
| PB15  | GMAC_RXD0  | SSI0_CLK    | SFC_CE1       | SLCD_WR          | Pullup         | VDDIO1        | 60                |
| PB16  | GMAC_RXD1  | SSI0_CE0    | SFC_GPC       | SLCD_TE          | Pullup         | VDDIO1        | 61                |
| PB17  | PWM0       | SSI0_DT     | UART2_TxD     | -                | Z              | VDDIO1        | 1                 |
| PB18  | PWM1       | SSI0_DR     | UART2_RxD     | -                | Z              | VDDIO1        | 2                 |
| PB19  | UART0_RxD  | -           | -             | -                | Z              | VDDIO1        | 71                |
| PB20  | UART0_CTS  | -           | SMB2_SDA      | SLCD_CS          | Z              | VDDIO1        | 69                |
| PB21  | UART0_RTS  | -           | SMB2_SCK      | SLCD_DC          | Z              | VDDIO1        | 68                |
| PB22  | UART0_TxD  | MIPI_SEL    | -             | SLCD_RDY         | Z              | VDDIO1        | 70                |
| PB23  | UART1_TxD  | -           | -             | -                | Pullup         | VDDIO1        | 74                |
| PB24  | UART1_RxD  | -           | -             | -                | Pullup         | VDDIO1        | 73                |
| PB25  | SMB1_SDA   | -           | UART2_CTS     | -                | Z              | VDDIO1        | 88                |
| PB26  | SMB1_SCK   | -           | UART2_RTS     | -                | Z              | VDDIO1        | 87                |
| PB27  | DRV_VBUS   | PWM2        | SSI0_DT       | SMB2_SDA         | Z              | VDDIO1        | 86                |
| PB28  | -          | PWM3        | SSI0_DR       | SMB2_SCK         | Z              | VDDIO1        | 85                |
| PB29  | -          | -           | SSI0_CLK      | -                | Z              | VDDIO1        | 82                |
| PB30  | MIPI_SEL   | -           | SSI0_CE0      | -                | Z              | VDDIO1        | 81                |
| PB31  | -          | -           | -             | -                | Pulldown       | VDDIO1        | 80                |

### PC Group
| GPIO  | FUNC0      | FUNC1       | FUNC2         | FUNC3            | Default Status | Voltage Domain | pin number in QFN |
|-------|------------|-------------|---------------|------------------|----------------|---------------|-------------------|
| PC00  | (BOOT_SEL0)| -           | -             | -                | Pullup         | VDDIO1        | 67                |
