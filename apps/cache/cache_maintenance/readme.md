[![MCHP](https://www.microchip.com/ResourcePackages/Microchip/assets/dist/images/logo.png)](https://www.microchip.com)

# Cache maintenance operations

This example demonstrates the cache maintenance operation by cleaning and invalidating the cache for the DMA buffers located in the cacheable SRAM region.

## Description

This example application shows how to use the cache maintenance APIs to avoid issues related to cache coherency when the data cache is enabled.

The application uses the USART and the DMA PLIBs to demonstrate the cache maintenance APIs provided by the Cache peripheral library. It registers a callback with the DMA transmit and receive channels. The application first transmits a message using the DMA transmit channel and then schedules a read of ten characters using the DMA receive channel. Once the DMA read is complete, it reads the received data and echoes the same on the terminal using the DMA transmit channel.

The application calls the DCACHE_CLEAN_BY_ADDR API on the write buffer before transmitting it. Calling this API copies the data from the cache memory to the main memory, thereby ensuring that the DMA peripheral uses the updated values in the write buffer.

The application calls the DCACHE_INVALIDATE_BY_ADDR API on the read buffer after reception of data is complete by the DMA receive channel. Calling this API invalidates the cache region corresponding to the read buffer, thereby ensuring that the CPU reads the updated values in the read buffer from the main memory and into the cache.

The cache maintenance operations are always performed on a cache line (1 cache line = 32 bytes), the read and write buffers must be aligned to a 32 byte boundary and must be a multiple of 32 bytes. For the same reason, the number of received and echoed back bytes is 10, the size of the receive and echo buffers is 32 bytes.


## Downloading and building the application

To download or clone this application from Github, go to the [top level of the repository](https://github.com/Microchip-MPLAB-Harmony/csp_apps_pic32mz_da) and click

![clone](../../../docs/images/clone.png)

Path of the application within the repository is **apps/cache/cache_maintenance/firmware** .

To build the application, refer to the following table and open the project using its IDE.

| Project Name      | Description                                    |
| ----------------- | ---------------------------------------------- |
| pic32mz_dag_sk.X | MPLABX project for [PIC32MZ Embedded Graphics with Stacked DRAM (DA) Starter Kit](https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/DM320010)     |
| pic32mz_das_sk.X | MPLABX project for [PIC32MZ Embedded Graphics with Stacked DRAM (DA) Starter Kit (Crypto)](https://www.microchip.com/DevelopmentTools/ProductDetails/DM320010-C) |
|||

## Setting up the hardware

The following table shows the target hardware for the application projects.

| Project Name| Board|
|:---------|:---------:|
| pic32mz_dag_sk.X | [PIC32MZ Embedded Graphics with Stacked DRAM (DA) Starter Kit](https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/DM320010)     |
| pic32mz_das_sk.X | [PIC32MZ Embedded Graphics with Stacked DRAM (DA) Starter Kit (Crypto)](https://www.microchip.com/DevelopmentTools/ProductDetails/DM320010-C) |
|||

### Setting up [PIC32MZ Embedded Graphics with Stacked DRAM (DA) Starter Kit](https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/DM320010)

- Connect the Debug USB port on the board to the computer using a micro USB cable
- Connect the USB to UART port on the board to the computer using a micro USB cable

### Setting up [PIC32MZ Embedded Graphics with Stacked DRAM (DA) Starter Kit (Crypto)](https://www.microchip.com/DevelopmentTools/ProductDetails/DM320010-C)

- Connect the Debug USB port on the board to the computer using a micro USB cable
- Connect the USB to UART port on the board to the computer using a micro USB cable

## Running the Application

1. Open the Terminal application (Ex.:Tera term) on the computer
2. Connect to the EDBG Virtual COM port and configure the serial settings as follows:
    - Baud : 115200
    - Data : 8 Bits
    - Parity : None
    - Stop : 1 Bit
    - Flow Control : None
3. Build and Program the application using its respective IDE
4. The console displays the following message

    ![output](images/output_cache_maintenance.png)

5. Type 10 characters in the terminal. It will echo back the received bytes and toggles the LED
6. The following table provides the LED names

| Board      | LED Name                                    |
| ---------- | ------------------------------------------- |
| [PIC32MZ Embedded Graphics with Stacked DRAM (DA) Starter Kit](https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/DM320010) | LED1 |
| [PIC32MZ Embedded Graphics with Stacked DRAM (DA) Starter Kit (Crypto)](https://www.microchip.com/DevelopmentTools/ProductDetails/DM320010-C) | LED1 |
