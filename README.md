# **ViewSonic CDE30 Series Crestron RS-232 Control Module**

**Version:** 1.0

## **Overview**

This Crestron SIMPL+ module provides comprehensive RS-232 serial control for **ViewSonic CDE30 series** commercial displays. It is designed to be a robust and reliable solution for integrating these displays into Crestron control systems.  
The module manages all essential display functions, including power, input switching, audio and video adjustments, and system locks. It features a configurable polling engine to ensure that feedback on the Crestron controller stays synchronized with the actual state of the display.

## **Compatibility**

This module is specifically designed and tested for the **ViewSonic CDE30 series**.

* **Verified Models:** CDE9830, CDE6530  
* **Expected Compatibility:** CDE4330, CDE5530, CDE7530, CDE8630

While other ViewSonic models might respond to some commands, full functionality is only guaranteed for the CDE30 series.

## **Features**

* **Full RS-232 Control:** Manages all major display functions via a direct serial connection.  
* **Reliable Feedback:** Provides discrete feedback for power, input selection, mute status, freeze status, lock states, and more.  
* **Power Transition Lock:** A built-in timeout mechanism prevents command conflicts while the display is warming up or shutting down, ensuring stable operation.  
* **Intelligent Polling:** A configurable polling engine periodically queries the display's essential statuses (Power, Input, Volume) to keep feedback in sync. Polling can be enabled or disabled on the fly.  
* **Analog & Incremental Control:** Supports both direct analog level setting and up/down commands for audio and picture adjustments.  
* **System Integration:** Includes commands for keypad emulation, panel locks, and factory reset.  
* **Detailed Debugging:** A dedicated Debug\_fb$ output provides clear, human-readable messages for TX/RX commands, timeouts, and status updates to simplify troubleshooting.

## **Setup and Configuration**

### **1\. Installation**

1. Place the ViewSonic CDE30 Series RS-232 Control v1.0.usp file into your Crestron User SIMPL+ or project directory.  
2. Open your SIMPL Windows program.  
3. In the Program View, navigate to the User Modules or Project Modules folder in the Symbol Library.  
4. Drag the ViewSonic CDE30 Series RS-232 Control v1.0 symbol into your program's logic.

### **2\. Communication Settings**

Connect the To\_Display\_tx$ and From\_Display\_rx$ signals of the module to a COM port on your Crestron processor. The serial port must be configured with the following settings:

* **Baud Rate:** 9600  
* **Data Bits:** 8  
* **Parity:** None  
* **Stop Bits:** 1

### **3\. Module Configuration**

* **Display\_ID\_ain (Analog Input):** This is the most critical setting. Set this value to match the **Monitor ID** configured in the display's OSD menu (Advanced \> Monitor ID). The valid range is 1-98. If left at 0, the module will default to ID 1\.  
* **Enable\_Polling\_trig (Digital Input):** Drive this signal HIGH to enable automatic status polling. Drive it LOW to disable polling. Feedback will only update on command execution or manual queries when polling is disabled.  
* **Poll\_Rate\_seconds\_ain (Analog Input):** Sets the time interval (in seconds) between polling cycles. The default is 30 seconds. The valid range is 5 to 300 seconds.

## 

## **Troubleshooting**

* **No Communication:**  
  * Verify your RS-232 wiring (TX, RX, GND) is correct. A straight-through cable is required.  
  * Confirm the COM port settings in your Crestron program match the required settings (9600, 8, N, 1).  
  * Ensure the Display\_ID\_ain on the module matches the **Monitor ID** on the display.  
* **Unreliable Feedback:**  
  * Use the Debug\_fb$ output to monitor the communication flow. It will show you exactly what commands are being sent (TX), what responses are being received (RX), and if any timeouts are occurring.  
  * Ensure the Enable\_Polling\_trig is HIGH if you require continuous, up-to-date feedback.  
* **Command Rejection (NACK):** If the debug output shows "NACK / Error", the display has rejected the command. This is often due to an incorrect Display ID or attempting to send a command while the display is busy or in a state that does not accept that command.