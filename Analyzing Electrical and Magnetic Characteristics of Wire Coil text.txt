#analyzing the electrical and magnetic characteristics of a wire coil for varying I value

import math  # Importing the math library for mathematical functions

# Constants
WireRes = 0.133  # Wire resistance in ohms per meter
L = 104  # Length of the coil in mm
N = 460  # Number of turns in the coil
perm = 800  # Relative permeability of the material

# Limited lists of varying radii and currents to test
r_values = [4.75, 5.0]  # Selected example radii in mm
current_values = [0.2302, 0.5]  # Selected example currents in Amperes

# Iterate over each radius value
for r in r_values:
    # Iterate over each current value
    for I in current_values:
        # Calculate the numerator and denominator for Nd
        num = 4 * (math.log(L / r) - 1)  # Numerator for Nd calculation
        den = (L * L) / (r * r) - 4 * (math.log(L / r))  # Denominator for Nd calculation
        
        # Calculate Nd
        Nd = num / den  

        # Calculate the bracket factor
        brack = (1 + (perm - 1) / (1 + (perm - 1) * Nd))  # Bracket factor for magnetic moment calculation

        # Calculate the magnetic moment (MagMom) of the coil
        MagMom = (math.pi * r * r * N * I * brack) / (10**6)  # Magnetic moment in Am^2

        # Calculate the total length of wire used
        wirelen = (2 * math.pi * r * N) / 1000  # Length in meters (conversion from mm to m)

        # Calculate the resistance of the wire
        resistance = wirelen * WireRes  # Total resistance in Ohms

        # Calculate the voltage drop across the wire
        V = I * resistance  # Voltage in Volts

        # Print all results for the current radius and current value
        print(f"Radius (r): {round(r, 4)} mm, Current (I): {round(I, 4)} A")
        print(f"Nd is: {round(Nd, 5)}")
        print(f"Bracket is: {round(brack, 3)}")
        print(f"Magnetic moment is: {round(MagMom, 5)} Am^2")
        print(f"Wire length is: {round(wirelen, 3)} m")
        print(f"Wire resistance is: {round(resistance, 3)} Ohm")
        print(f"Voltage is: {round(V, 4)} Volts")
        print("-" * 40)  # Separator for clarity

