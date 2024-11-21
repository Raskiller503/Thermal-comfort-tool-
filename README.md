# Introduction
Since PMV calculation is complex due to it itneary and time consuming we proposed one method could calculate it in real-time.

# PMV Calculation Algorithm

This repository contains an implementation of the Predicted Mean Vote (PMV) calculation algorithm. PMV is a thermal comfort index that predicts the mean value of the votes of a large group of people on the 7-point thermal sensation scale, which ranges from cold (-3) to hot (+3).
<p align="center">
  <img src="Image/Flow.png" width="400" height='300' alt="Process Flow">
</p>

## Algorithm Flowchart

### 1. Initialize Environment Monitor Class
- **Step 1:** Create a class named `EnvironmentMonitor`.
- **Step 2:** In the class's `__init__` method, set the metabolism rate `M` and calculate the clothing insulation `clo` by calling the `calculate_clothing_insulation()` method.
- **Step 3:** Calculate the `fM` value using the formula `0.303 * np.exp(-0.036 * self.M) + 0.028`.

### 2. Calculate Clothing Insulation
- **Step 4:** Define the `calculate_clothing_insulation()` method, which returns the appropriate `clo` value based on the current month.
  - **Summer (June-August):** Return `0.5`
  - **Intermediate seasons (March-May and September-November):** Return `0.6`
  - **Winter (December-February):** Return `0.8`

### 3. Get Indoor Environment Data
- **Step 5:** Define the `get_indoor_environment_data()` method to fetch and return the following environmental data:
  - Indoor temperature `Ta`
  - Globe temperature `Tg`
  - Relative humidity `humidity`
  - CO2 concentration `CO2_conce`
  - Atmospheric pressure `pressure`
  - Mean Radiant Temperature `Tm` (calculated using a specific formula)

### 4. Calculate PMV
- **Step 6:** Define the `calculate_pmv(Ta, Tm, wind_speed, humidity)` method.
  - **Step 6.1:** Calculate `KPa` using the formula `6.11 * 10 ** (7.5 * Ta / (Ta + 237.3)) / 10 * humidity / 100`.
  - **Step 6.2:** Calculate `E` using the formula `3.05 * (5.73 - 0.007 * M - KPa) + 0.42 * (M - 58.15)`.
  - **Step 6.3:** Based on the wind speed `W`, choose the appropriate calculation method:
    - **Low wind speed (W < 0.2):**
      - Define symbols `C` and `R`.
      - Calculate `E1` and `C1`.
      - Set up the system of equations and solve.
    - **High wind speed (W >= 0.2):**
      - Define symbols `C` and `R`.
      - Set up the system of equations and solve.
  - **Step 6.4:** Select the appropriate `C` and `R` values from the results.
  - **Step 6.5:** Calculate `S` using the formula `M - (C + R + E) - (C1 + E1)`.
  - **Step 6.6:** Calculate the PMV value using the formula `fM * S` and format the result to two decimal places.

### 5. Example Usage
- **Step 7:** Create an instance of the `EnvironmentMonitor` class.
- **Step 8:** Call the `get_indoor_environment_data()` method to fetch environmental data.
- **Step 9:** Call the `calculate_pmv(Ta, Tm, wind_speed, humidity)` method to calculate the PMV value.
- **Step 10:** Print the calculated PMV value.

## Code Example

```bash
git clone https://github.com/Raskiller503/Thermal-comfort-tool-/blob/main/PMVcalculator.py
```

## Reference
For more detailed information on PMV calculation and thermal comfort, please refer to the following paper:
- __Yutong CHEN__,
[Development of Low-Cost IoT Units for Thermal Comfort Measurement and AC Energy Consumption Prediction System](https://kth-my.sharepoint.com/personal/torunw_ug_kth_se/_layouts/15/onedrive.aspx?ga=1&id=%2Fpersonal%2Ftorunw%5Fug%5Fkth%5Fse%2FDocuments%2Fbox%5Ffiles%2FRoomVent%2FRoomVent%5F2024%5FProceedings%2F240425%201400a%20Session%2026%20IC%20Thermal%20comfort%201%2FPrint%20439%20Final%2Epdf&parent=%2Fpersonal%2Ftorunw%5Fug%5Fkth%5Fse%2FDocuments%2Fbox%5Ffiles%2FRoomVent%2FRoomVent%5F2024%5FProceedings%2F240425%201400a%20Session%2026%20IC%20Thermal%20comfort%201![image](https://github.com/user-attachments/assets/537ab711-703e-4c39-b811-ccc46ccde782)
), presented at RoomVent2024.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.





