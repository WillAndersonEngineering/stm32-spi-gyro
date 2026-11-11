# STM32 SPI gyroscope demo

A small board-level example that reads the on-board gyroscope over SPI5 on an **STM32F429I-DISC1** and maps the raw Y-axis reading and user button to the board LEDs.

## Signal path

- The gyro driver selects the device on PC1, sends the read command, then reads and combines the low and high bytes into a signed 16-bit sample.
- Application code classifies the raw sample by direction and magnitude thresholds, then updates the green and red LEDs.
- The checked-in configuration polls every 100 ms. The source also contains an interrupt-driven experiment behind `LAB2_USE_INTERRUPT`.

## Build and try it

1. Import the [firmware folder](firmware/) as an existing project in STM32CubeIDE.
2. Build the **Debug** configuration and flash the board through ST-LINK.
3. Rotate the board around its Y axis and observe the LED response with and without the user button. In a debug session, inspect `gyro_Direction` to see the classified state.

The [gyro driver](firmware/Core/Src/Gyro_Driver.c) contains the SPI transactions. [Application_Code.c](firmware/Core/Src/Application_Code.c) maps the samples to LED behavior. Course-provided driver headers and STM32 vendor notices retain their original attribution.
