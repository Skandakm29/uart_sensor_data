# Implementing a UART Transmitter that Sends Data Based on Sensor Inputs

## Objective:
Design and implement a **UART transmitter** that sends real-time **sensor data** over a serial interface. This ensures the FPGA can **communicate sensor values** reliably to an external device.

---

## Contents:

###  Study the Existing Code

<details>
<summary>Module Analysis</summary>

### **Architecture Overview**
The `sense_uart_tx` module enables **sensor-driven UART transmission**, ensuring efficient and structured data transfer. The architecture includes:

1. **Sensor Data Handling**
2. **Baud Rate Generation**
3. **UART Transmission Logic**
4. **State Machine for Data Control**

---

### **Operation Flow**
1. **Data Sampling**
   - Sensor values are **sampled** at defined intervals.
   - A **data_valid** signal triggers the transmission process.
   - The **32-bit sensor data buffer** holds the values before transmission.

2. **Baud Rate Control**
   - The **baud rate generator** creates a stable **9600 baud clock**.
   - A counter-based approach ensures correct bit timing.

3. **UART Transmission Sequence**
   - **START**: Outputs a **low start bit**.
   - **DATA BITS**: Transmits **8-bit chunks** sequentially.
   - **STOP**: Outputs a **high stop bit** to mark the end.
   - **State transitions** synchronize the process.

4. **Status Indication**
   - The **tx_done** signal indicates completion.
   - The **ready** signal ensures no data loss during continuous sensor readings.

---

### **Port Analysis**
1. **Clock and Reset**
   - **clk**: Drives synchronous operations.
   - **reset_n**: Resets all internal states.

2. **Sensor Interface**
   - **sensor_data [31:0]**: Input from the sensor module.
   - **data_valid**: Indicates new sensor data availability.

3. **UART Output**
   - **tx_out**: UART serial output for external communication.

4. **Control Signals**
   - **tx_start**: Initiates UART transmission.
   - **tx_done**: Signals when data transmission is complete.
   - **ready**: Indicates module is ready for new data.

---

### **Internal Logic**
1. **Finite State Machine (FSM)**
   - **IDLE**: Waits for a **data_valid** trigger.
   - **START**: Sends the **start bit (0)**.
   - **DATA**: Sequentially shifts out **8-bit portions** of sensor data.
   - **STOP**: Outputs the **stop bit (1)**.
   - **DONE**: Raises `tx_done` and returns to IDLE.

2. **Baud Rate Generator**
   - Uses **clock division** to produce an accurate **9600 Hz baud clock**.

3. **Shift Register**
   - Holds **32-bit sensor data**.
   - Sequentially shifts **8 bits per transmission cycle**.

</details>

###  System Architecture
<details>
<summary>Block diagram</summary>
</details>

<details>
<summary>Circuit diagram</summary>
</details>

###  Synthesis & Programming
<details>
  <summary>Testing and Output</summary>

## **Clone & Setup Repository**
```bash
git clone https://github.com/Skandakm29/vsd_squadron_minifpga_4.git
cd "Vsd_squadron_mini_Fpga_4"
```

###  Build the Bitstream
```bash
make build
```
 Generates top.bin for the FPGA.

###  **Flash to FPGA**
```bash
sudo make flash
```
Uploads the bitstream to the FPGA.
### **UART Testing**
```bash
sudo make terminal
```
</details>

### UART Transmission Showcase
<details>
  <summary>Demo Video</summary>

[![Watch the Demo](https://github.com/user-attachments/assets/2e41d50e-7fb5-4c2e-9296-9f6e4c054e18)](https://github.com/user-attachments/assets/2e41d50e-7fb5-4c2e-9296-9f6e4c054e18)

</details>
