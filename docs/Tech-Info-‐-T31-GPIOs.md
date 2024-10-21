# T31 GPIO Information

**Voltage Domains**: VDDIO0(1.8V), VDDIO1(3.3V), VDDIO2(1.8/3.3V)

## IO Functions Multiplexing:

### PA Group
| GPIO  | FUNC0      | FUNC1       | FUNC2         | FUNC3            | Default Status | Voltage Domain | Pin number in BGA | Pin number in QFN |
|-------|------------|-------------|---------------|------------------|----------------|---------------|-------------------|-------------------|
| DVP_D0| MIPI_DATAP1| -           | -             | note: analog IO   | MIPI_AVD18      | N2            | 29                |
| DVP_D1| MIPI_DATAN1| -           | -             | note: analog IO   | MIPI_AVD18      | N1            | 28                |
| DVP_D2| MIPI_CLKP  | -           | -             | note: analog IO   | MIPI_AVD18      | M2            | 27                |
| DVP_D3| MIPI_CLKN  | -           | -             | note: analog IO   | MIPI_AVD18      | M1            | 26                |
| DVP_D4| MIPI_DATAP0| -           | -             | note: analog IO   | MIPI_AVD18      | L2            | 25                |
| DVP_D5| MIPI_DATAN0| -           | -             | note: analog IO   | MIPI_AVD18      | L1            | 24                |
| PA06  | DVP_D6     | UART1_TxD   | -             | Z                | VDDIO0         | K2            | 23                |
| PA07  | DVP_D7     | UART1_RxD   | -             | Z                | VDDIO0         | K1            | 22                |
| PA08  | DVP_D8     | UART2_CTS   | MSC1_D0       | Z                | VDDIO0         | J2            | 21                |
| PA09  | DVP_D9     | UART2_RTS   | MSC1_D1       | Z                | VDDIO0         | J1            | 20                |
| PA10  | DVP_D10    | UART2_TXD   | MSC1_D2       | Z                | VDDIO0         | H3            | 19                |
| PA11  | DVP_D11    | UART2_RXD   | MSC1_D3       | Pullup           | VDDIO0         | H1            | 18                |
| PA12  | I2C0_SDA   | -           | -             | Pullup           | VDDIO0         | F2            | 13                |
| PA13  | I2C0_SCL   | -           | -             | Pullup           | VDDIO0         | E1            | 12                |
| PA14  | DVP_PCLK   | PWM0        | -             | Z                | VDDIO0         | H2            | 17                |
| PA15  | DVP_MCLK   | -           | -             | Z                | VDDIO0         | G1            | 16                |
| PA16  | DVP_HSYNC  | I2C1_SDA    | MSC1_CLK      | Pullup           | VDDIO0         | G2            | 15                |
| PA17  | DVP_VSYNC  | I2C1_SCL    | MSC1_CMD      | Pullup           | VDDIO0         | F1            | 14                |
| PA18  | -          | -           | -             | Z                | VDDIO0         | E2            | 11                |
| PA22  | WAIT_      | -           | PWM1          | Pullup, Schmitt  | VDDIO0         | D1            | N.A.              |
| PA23  | SFC_DT     | SIO0        | -             | Pullup           | VDDIO1         | J15           | 47                |
| PA24  | SFC_DR     | SIO1        | -             | Pullup           | VDDIO1         | K15           | 46                |
| PA25  | SFC_GPC    | HOLD#/SIO3  | -             | Pullup           | VDDIO1         | H15           | N.A.              |
| PA26  | SFC_CE1_   | WP#/SIO2    | -             | Pullup           | VDDIO1         | J14           | N.A.              |
| PA27  | SFC_CLK    | SCLK        | -             | Pullup           | VDDIO1         | H14           | 48                |
| PA28  | SFC_CE0_   | CS#         | -             | Pullup           | VDDIO1         | K14           | 45                |

### PB Group
| GPIO  | FUNC0      | FUNC1       | FUNC2         | FUNC3            | Default Status | Voltage Domain | Pin number in BGA | Pin number in QFN |
|-------|------------|-------------|---------------|------------------|----------------|---------------|-------------------|-------------------|
| PB00  | MSC0_D0    | SSI_SLV_DT  | -             | -                | Z              | VDDIO1        | G15               | 50                |
| PB01  | MSC0_D1    | SSI_SLV_DR  | -             | -                | Z              | VDDIO1        | H13               | 49                |
| PB02  | MSC0_D2    | -           | -             | -                | Z              | VDDIO1        | E15               | 54                |
| PB03  | MSC0_D3    | -           | -             | -                | Z              | VDDIO1        | F14               | 53                |
| PB04  | MSC0_CLK   | SSI_SLV_SERICLK | -         | -                | Z              | VDDIO1        | G14               | 51                |
| PB05  | MSC0_CMD   | SSI_SLV_CE0 | -             | -                | Pullup         | VDDIO1        | F15               | 52                |
| PB06  | GMAC_TXCLK | -           | SLCD_D0       | -                | Z              | VDDIO1        | B15               | 62                |
| PB07  | GMAC_PHY_CLK | -         | SLCD_D1       | -                | Z              | VDDIO1        | A15               | 63                |
| PB08  | GMAC_TXEN  | MSC1_CLK    | I2S_RMCLK     | SLCD_D2          | Z              | VDDIO1        | B13               | 66                |
| PB09  | GMAC_RXDV  | MSC1_CMD    | I2S_SDTI      | SLCD_D3          | Z              | VDDIO1        | D14               | 59                |
| PB10  | GMAC_MDCK  | MSC1_D0     | I2S_SDTO      | SLCD_D4          | Pulldown       | VDDIO1        | D15               | 58                |
| PB11  | GMAC_MDIO  | MSC1_D1     | -             | SLCD_D5          | Pullup         | VDDIO1        | E14               | 57                |
| PB13  | GMAC_TXD0  | MSC1_D2     | I2S_ADC_LRCK  | SLCD_D6          | Z              | VDDIO1        | B14               | 64                |
| PB14  | GMAC_TXD1  | MSC1_D3     | I2S_TMCLK     | SLCD_D7          | Pullup         | VDDIO1        | A14               | 65                |
| PB15  | GMAC_RXD0  | -           | I2S_DAC_LRCK  | SLCD_WR          | Z              | VDDIO1        | C15               | 60                |
| PB16  | GMAC_RXD1  | -           | SLCD_TE       | -                | Pullup         | VDDIO1        | C14               | 61                |
| PB17  | PWM0       | SSI1_DT     | -             | -                | Pulldown       | VDDIO1        | A4                | 1                 |
| PB18  | PWM1       | SSI1_DR     | -             | -                | Pulldown       | VDDIO1        | B4                | 2                 |
| PB19  | UART0_RxD  | TDI         | -             | -                | Pullup         | VDDIO1        | B10               | 71                |
| PB20  | UART0_CTS  | -           | I2S_ADC_BCLK  | SLCD_CS          | Z              | VDDIO1        | B11               | 69                |
| PB21  | UART0_RTS  | -           | I2S_DAC_BCLK  | SLCD_DC          | Z              | VDDIO1        | A12               | 68                |
| PB22  | UART0_TxD  | TDO         | -             | SLCD_RDY         | Z              | VDDIO1        | A11               | 70                |
| PB23  | UART1_TxD  | TCK         | -             | -                | Z              | VDDIO1        | A10               | 74                |
| PB24  | UART1_RxD  | TMS         | -             | -                | Pullup           | VDDIO1         | B9            | 73                |
| PB25  | I2C1_SDA   | SSI1_CE0_   | -             | -                | Pullup         | VDDIO1        | B5                | 88                |
| PB26  | I2C1_SCL   | SSI1_CLK    | -             | -                | Pullup         | VDDIO1        | A5                | 87                |
| PB27  | DRV_VBUS   | PWM2        | SSI1_DT       | -                | Pulldown       | VDDIO1        | A6                | 86                |
| PB28  | -          | PWM3        | SSI1_DR       | DMIC_CLK         | Pulldown       | VDDIO1        | B6                | 85                |
| PB29  | -          | -           | SSI1_CLK      | DMIC_DAT0        | Pullup,Schmitt | VDDIO1        | A7                | 82                |
| PB30  | -          | -           | SSI1_CE0      | DMIC_DAT1        | Pullup,Schmitt | VDDIO1        | B8                | 81                |
| PB31  | -          | -           | -             | -                | Pulldown       | VDDIO1        | B7                | 80                |

### PC Group
| GPIO  | FUNC0      | FUNC1       | FUNC2         | FUNC3            | Default Status | Voltage Domain | Pin number in BGA | Pin number in QFN |
|-------|------------|-------------|---------------|------------------|----------------|---------------|-------------------|-------------------|
| PC00  | (BOOT_SEL0)  | -         | -             | -                | Pullup         | VDDIO1        | B12               | 67                |
| PC01  | (BOOT_SEL1)  | -         | -             | -                | Pulldown       | VDDIO1        | A13               | N.A.              |
| PC02  | GPIO         | MSC1_CLK  | SSI_SLV_SERICLK | -                | Z              | VDDIO2        | R8                | N.A.              |
| PC03  | GPIO         | MSC1_CMD  | SSI_SLV_CE0   | -                | Pullup         | VDDIO2        | N8                | N.A.              |
| PC04  | GPIO         | MSC1_D0   | SSI_SLV_DT    | -                | Z              | VDDIO2        | P8                | N.A.              |
| PC05  | GPIO         | MSC1_D1   | SSI_SLV_DR    | -                | Z              | VDDIO2        | R7                | N.A.              |
| PC06  | GPIO         | MSC1_D2   | -             | -                | Z              | VDDIO2        | P9                | N.A.              |
| PC07  | GPIO         | MSC1_D3   | -             | -                | Z              | VDDIO2        | R9                | N.A.              |
| PC08  | GPIO         | SSI0_GPC  | UART0_TXD     | I2C1_SDA         | Pullup         | VDDIO2        | P12               | N.A.              |
| PC09  | GPIO         | SSI0_CE1_ | UART0_RXD     | I2C1_SCL         | Pullup         | VDDIO2        | R11               | N.A.              |
| PC11  | GPIO         | SSI0_DR   | UART2_CTS     | I2S_TMCLK        | Z              | VDDIO2        | P10               | N.A.              |
| PC12  | GPIO         | SSI0_DT   | UART2_RTS     | I2S_RMCLK        | Z              | VDDIO2        | P11               | N.A.              |
| PC13  | GPIO         | SSI0_CLK  | DMIC_DAT0     | UART2_TXD        | Z              | VDDIO2        | R12               | N.A.              |
| PC14  | GPIO         | SSI0_CE0_ | DMIC_DAT1     | UART2_RXD        | Pullup         | VDDIO2        | R10               | N.A.              |
| PC15  | GPIO         | -         | UART0_CTS     | I2S_DAC_LRCK     | Z              | VDDIO2        | R14               | N.A.              |
| PC16  | GPIO         | -         | UART0_RTS     | I2S_DAC_BCLK     | Z              | VDDIO2        | P13               | N.A.              |
| PC17  | GPIO         | PWM0      | -             | I2S_SDTI         | Pulldown,Schmitt | VDDIO2        | R15               | N.A.              |
| PC18  | GPIO         | PWM1      | -             | I2S_SDTO         | Pulldown,Schmitt | VDDIO2        | P14               | N.A.              |
| PC19  | GPIO         | PWM2      | -             | I2S_ADC_BCLK     | Z, Schmitt     | VDDIO2        | P15               | N.A.              |
| PC20  | GPIO         | PWM3      | DMIC_CLK      | I2S_ADC_LRCK     | Z, Schmitt     | VDDIO2        | R13               | N.A.              |
