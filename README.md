# psychrometric-calculator
<br>
This is simplifiest calculator to calculate the dry bulb temperature , enthaply ,dewpoint temperaure, wet bulb temperature and Rh without any error which is often seen while using chart.
import math

def saturation_pressure(T):
    """
    Calculate the saturation pressure of water vapor (in kPa) at a given temperature T (°C).
    Equation: Antoine equation for water.
    """
    return 0.61078 * math.exp((17.27 * T) / (T + 237.3))

def humidity_ratio(T_db, RH, P=101.325):
    """
    Calculate the humidity ratio (W) given dry-bulb temperature (T_db in °C),
    relative humidity (RH as a fraction), and atmospheric pressure (P in kPa).
    """
    P_s = saturation_pressure(T_db)  # Saturation pressure at T_db
    if RH * P_s >= P:
        raise ValueError("Relative humidity too high for given pressure.")
    return 0.622 * (RH * P_s) / (P - RH * P_s)

def relative_humidity_from_wet_bulb(T_db, T_wb, P=101.325):
    """
    Calculate the relative humidity (RH) given dry-bulb temperature (T_db in °C),
    wet-bulb temperature (T_wb in °C), and atmospheric pressure (P in kPa).
    """
    if T_wb > T_db:
        raise ValueError("Wet-bulb temperature cannot be higher than dry-bulb temperature.")
    
    P_s_db = saturation_pressure(T_db)
    P_s_wb = saturation_pressure(T_wb)
    W_wb = 0.622 * P_s_wb / (P - P_s_wb)
    h_wb = 1.006 * T_wb + W_wb * (2501 + 1.86 * T_wb)
    h_db = 1.006 * T_db
    W = (h_wb - h_db) / (2501 + 1.86 * T_db)
    RH = (W * P) / (0.622 * P_s_db + W * P_s_db)
    return min(max(RH, 0), 1)

def dew_point_temperature(T_db, RH):
    """
    Calculate the dew point temperature (T_dp in °C) given dry-bulb temperature
    and relative humidity (RH as a fraction).
    """
    if not (0 <= RH <= 1):
        raise ValueError("Relative humidity must be between 0 and 1.")
    
    P_s = saturation_pressure(T_db)
    P_w = RH * P_s
    T_dp = (237.3 * math.log(P_w / 0.61078)) / (17.27 - math.log(P_w / 0.61078))
    return T_dp

def enthalpy(T_db, W):
    """
    Calculate the enthalpy (h in kJ/kg of dry air) given dry-bulb temperature (T_db in °C)
    and humidity ratio (W in kg water/kg dry air).
    """
    return 1.006 * T_db + W * (2501 + 1.86 * T_db)

def specific_volume(T_db, W, P=101.325):
    """
    Calculate the specific volume (v in m³/kg of dry air) given dry-bulb temperature (T_db in °C),
    humidity ratio (W), and atmospheric pressure (P in kPa).
    """
    T_K = T_db + 273.15  # Convert to Kelvin
    R_specific = 0.287  # Specific gas constant for dry air (kJ/kg·K)
    return (R_specific * T_K * (1 + 1.6078 * W)) / P

if __name__ == "__main__":
    print("Psychrometric Calculator")
    print("Enter the following parameters:")

    try:
        T_db = float(input("Dry-bulb temperature (°C): "))
        if T_db < -100 or T_db > 100:
            raise ValueError("Dry-bulb temperature must be between -100°C and 100°C.")
        
        choice = input("Do you have (1) Relative Humidity (%) or (2) Wet-bulb Temperature (°C)? Enter 1 or 2: ").strip()
        P = float(input("Atmospheric Pressure (kPa) [default 101.325]: ") or 101.325)
        if P <= 0:
            raise ValueError("Atmospheric pressure must be positive.")
        
        if choice == '1':
            RH = float(input("Relative Humidity (%): ")) / 100
            if RH < 0 or RH > 1:
                raise ValueError("Relative humidity must be between 0% and 100%.")
        elif choice == '2':
            T_wb = float(input("Wet-bulb temperature (°C): "))
            RH = relative_humidity_from_wet_bulb(T_db, T_wb, P)
        else:
            raise ValueError("Invalid choice. Please enter 1 or 2.")

        # Calculations
        W = humidity_ratio(T_db, RH, P)
        T_dp = dew_point_temperature(T_db, RH)
        h = enthalpy(T_db, W)
        v = specific_volume(T_db, W, P)

        # Results
        print("\nResults:")
        print(f"Humidity Ratio (W): {W:.6f} kg water/kg dry air")
        print(f"Dew Point Temperature (T_dp): {T_dp:.2f} °C")
        print(f"Enthalpy (h): {h:.2f} kJ/kg dry air")
        print(f"Specific Volume (v): {v:.4f} m³/kg dry air")
        print(f"Relative Humidity (RH): {RH * 100:.2f}%")

    except ValueError as ve:
        print(f"Input error: {ve}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")
