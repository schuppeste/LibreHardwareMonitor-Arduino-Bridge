#LibreHardwareMonitor-Arduino-Bridge (Only Windows WMI Support)



## Overview
This program is a console-based application that interacts with hardware sensors using the [LibreHardwareMonitor](https://github.com/LibreHardwareMonitor/LibreHardwareMonitor) library. It communicates via a serial port, accepts JSON input for filtering sensor data, and outputs the filtered data as JSON. The program also supports commands to retrieve all sensor data or debug input.

---

## Features
- **JSON Input:** Accepts JSON data to filter specific hardware sensors.
- **JSON Output:** Returns filtered sensor data in JSON format.
- **COM Port Communication:** Sends and receives data via a configurable COM port.
- **Commands:** Supports commands like `liste`, `DEBUG`, and JSON-based filtering.

---

## How to Use

### 1. Start the Program
The program requires the COM port to be specified as a command-line argument. Example:
```bash
ConsoleApp1.exe COM3
```
- **`COM3`**: The name of the COM port to use.
- **`help`**: Displays usage instructions.

---

### 2. Commands

#### `liste`
The `liste` command retrieves all available sensors and their current values. The data is returned as a JSON string. Example output:
```json
[
  {
    "Hardware": "CPU",
    "SensorName": "Core #1",
    "SensorType": "Temperature",
    "Value": "45.0"
  },
  {
    "Hardware": "GPU",
    "SensorName": "GPU Core",
    "SensorType": "Temperature",
    "Value": "50.0"
  }
]
```
- **`Hardware`**: The name of the hardware component.
- **`SensorName`**: The name of the sensor.
- **`SensorType`**: The type of the sensor (e.g., `Temperature`, `Load`).
- **`Value`**: The current value of the sensor.

#### `DEBUG`
The `DEBUG` command outputs the received input to the console for debugging purposes.

#### JSON Input
You can send a JSON string to filter specific sensors. Example input:
```json
{
  "CPU": [
    { "SensorName": "Core #1", "SensorType": "Temperature" }
  ]
}
```
The program will filter the sensors based on the JSON input and return the filtered data as JSON.

---

### 3. JSON Output
The program outputs filtered sensor data as JSON. Example:
```json
[
  {
    "Hardware": "CPU",
    "Sensors": [
      {
        "SensorName": "Core #1",
        "SensorType": "Temperature",
        "Value": "45.0"
      }
    ]
  }
]
```

---

## Example Workflow
1. **Start the Program:**
   ```bash
   ConsoleApp1.exe COM3
   ```
2. **Send the `liste` Command:**
   - Output: A JSON list of all sensors and their values.
3. **Send JSON Input:**
   - Input: JSON data to filter specific sensors.
   - Output: Filtered sensor data as JSON.

---

## Error Handling
- **Invalid JSON:** If the JSON input is malformed, the program outputs an error message:
  ```
  JSON Parsing Error: [Error Message]
  Invalid JSON: [Input JSON]
  ```
- **Invalid Command:** If an unknown command is sent, the program outputs:
  ```
  Invalid input: [Command]
  ```

---

## Notes
- Ensure the specified COM port is available and correctly configured.
- The program uses a baud rate of `115200` for serial communication.
- The `help` command provides usage instructions directly in the console.
