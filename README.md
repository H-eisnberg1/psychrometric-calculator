# Psychrometric Calculator

The **Psychrometric Calculator** is a web-based tool designed to calculate various psychrometric properties, including:

- Humidity Ratio (kg water/kg dry air)
- Dew Point Temperature (°C)
- Enthalpy (kJ/kg dry air)
- Specific Volume (m³/kg dry air)
- Relative Humidity (%)

This tool uses Dry-Bulb Temperature along with either Relative Humidity or Wet-Bulb Temperature as inputs.

## Features

### 1. Input Options
You can input:
- **Dry-Bulb Temperature (°C)**: Required for all calculations.
- **Relative Humidity (%)**: Optionally provided if Wet-Bulb Temperature is not entered.
- **Wet-Bulb Temperature (°C)**: Optionally provided if Relative Humidity is not entered.
- **Atmospheric Pressure (kPa)**: Defaults to 101.325 kPa if left blank.

### 2. Conditional Input
- If you enter a value for **Relative Humidity**, the **Wet-Bulb Temperature** field is disabled.
- If you enter a value for **Wet-Bulb Temperature**, the **Relative Humidity** field is disabled.

### 3. Real-Time Calculations
The calculator computes psychrometric properties based on standard formulas and displays the results in an intuitive format.

### 4. Responsive Design
The calculator is designed for usability on both desktop and mobile devices.

## How to Use

1. Open the HTML file in any modern web browser.
2. Enter the required inputs:
   - **Dry-Bulb Temperature (°C)**
   - Either **Relative Humidity (%)** or **Wet-Bulb Temperature (°C)**
   - Optionally adjust **Atmospheric Pressure (kPa)**
3. Click the **Calculate** button.
4. View the results under the "Results" section, including:
   - Humidity Ratio
   - Dew Point Temperature
   - Enthalpy
   - Specific Volume
   - Relative Humidity (calculated if Wet-Bulb Temperature is provided).

## Installation

1. Clone or download this repository.
2. Locate the `psychrometric_calculator.html` file.
3. Open the file in a modern web browser (e.g., Chrome, Firefox, Edge).

---

## Formulas Used

1. **Saturation Pressure**
2. **Humidity Ratio**
3. **Relative Humidity from Wet-Bulb Temperature**
4. **Dew Point Temperature**
5. **Enthalpy**
6. **Specific Volume**
   
## Technologies Used

- **HTML**: For the structure of the web application.
- **CSS**: For styling the user interface.
- **JavaScript**: For performing calculations and managing interactivity.

---

## Future Enhancements

- Add graphing capabilities to visualize psychrometric properties.
- Expand to support additional inputs like specific humidity and absolute humidity.
- Add unit conversion options (e.g., imperial units).

## License
This project is licensed under the MIT License. You are free to use, modify, and distribute this tool as needed.

## Acknowledgments

Special thanks to the open-source community for providing psychrometric formulas and supporting resources for thermodynamic calculations.

