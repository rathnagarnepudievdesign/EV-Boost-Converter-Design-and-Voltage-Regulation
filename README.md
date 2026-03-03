# EV-Boost-Converter-Design-and-Voltage-Regulation
Design, modeling, and closed-loop control of EV DC–DC Buck and Boost converters using MATLAB/Simulink with PWM-based voltage regulation and performance analysis.


The system is modeled in MATLAB/Simulink to analyze:

Output voltage regulation
Inductor current ripple
Duty cycle variation
Switching behavior
Converter efficiency
  


Given Parameters

Input Voltage (vin) = 24 V
Inductor 𝐿 = 3 mH = 0.003 H
Capacitor C = 200 µF = 200 × 10⁻⁶ F
Load Resistance R = 20 Ω
PI Controller Gains: Kp=0.1;
                     Ki=4;
                     
Main Components & Function

1️⃣ MOSFET Switch

Acts as a high-speed switching element controlled by PWM signal.

2️⃣ Diode

Provides freewheeling path for inductor current during OFF state.
Should be fast-recovery type for high-frequency switching.
3️⃣ Inductor (L)

Stores energy during ON time and releases during OFF time.
Controls current ripple.

4️⃣ Capacitor (C)

Filters output voltage ripple and stabilizes DC output.

5️⃣ Load Resistance
Represents EV low-voltage load (ECU, lighting, control modules).

PWM & Control Strategy

PWM Strategy:
•	Fixed frequency switching (20 kHz)
•	Duty cycle controlled by PI controller
•	Closed-loop voltage regulation
•	
Control Flow:

Reference Voltage (48V)
→ Error Calculation
→ PI Controller (Kp = 0.1, Ki = 4)
→ PWM Generator
→ MOSFET Gate Drive
PI Controller Transfer Function:
G(s)=0.1+4sG(s) = 0.1 + \frac{4}{s}G(s)=0.1+s4 
Controller ensures:
•	Reduced steady-state error
•	Stable voltage regulation
•	Improved transient response



Voltage Transfer Function

The relationship between the Input Voltage (vin) and Output Voltage (vout) is determined by the Duty Cycle

V_out = D * V_in
Where 0 < D < 1.

Duty Cycle Calculation


For Boost Converter:
Vout=Vin/1-D 
Rearranging:
D=1−Vin/Vout
D=1−24/48
D=1−0.5
D=0.5
Duty Cycle = 50%
Output Current
  Iout=Vout/R;
  Iout=48/20=2.4A;
  Output Current = 2.4 A
Input Current
  Pin=Pout 
Vin*Iin=Vout*Iout
Iin=VoutIout/Vin
 Iin=48×2.4/24
Iin=4.8A
  Inductor Ripple Current
  
Ripple current formula:
ΔIL=(Vin)⋅D/L.fs
We must assume switching frequency.
Let’s assume:
fs=20kHz
ΔIL=(24)⋅0.50/0.003⋅20000
ΔIL=12/60
ΔIL=0.2A
Inductor Ripple Current = 0.2 A

Inductor Current Limits
Average Inductor Current = Input Current
IL(avg)=4.8A
IL(max)=4.8+0.1=4.9A
 IL(min)=4.8−0.1=4.7A
 Continuous Conduction Mode (CCM confirmed)
 
 Output Voltage Ripple
 
ΔVo=Iout.D/fsC
ΔVo=2.4*0.5/20000⋅200×10−6
=1.2/4
ΔVo=0.3V 
Output Ripple ≈ 0.3 V
Ripple %:
0.3/48×100=0.625%
Very good ripple performance



Critical Inductance (Boundary Mode)
Lcritical=D(1−D)^2R/2fs
 Lcritical=0.5(0.5)^2*20/2⋅20000)
=2.5/40000 
Lcritical=62.5μH 


PI Controller Transfer Function
PI Controller:
G(s)=Kp+Ki/s
G(s)=0.1+4/s 
This controller:
•	Kp → Improves response speed
•	Ki → Eliminates steady-state error
Integral time constant:
Ti=Kp/Ki
Ti =0.1/4=0.25s
Controller ensures:
•	Voltage regulation
•	Reduced steady-state error
•	Improved transient response
Work flow of Boost converter
•	In a DC–DC converter system, the output voltage regulation begins with defining a reference voltage corresponding to the desired output level. The actual output voltage is continuously measured and compared with this reference value to generate an error signal. This error is processed through a PI (Proportional–Integral) controller, where the proportional gain improves response speed and the integral gain eliminates steady-state error. The controller output generates a control signal that determines the required duty cycle.
•	This control signal is then compared with a high-frequency triangular carrier waveform inside the PWM generator. When the control signal exceeds the carrier waveform, the MOSFET switch is turned ON; otherwise, it is turned OFF. This comparison produces a fixed-frequency PWM pulse with a variable duty cycle.
•	The PWM pulse is applied to the gate of the MOSFET, which switches at the defined frequency (for example, 20 kHz). During the ON period, the inductor stores energy from the input supply. During the OFF period, the inductor releases its stored energy to the load through the diode (in boost configuration) or directly to the output (in buck configuration). This energy transfer mechanism enables voltage step-down in a buck converter or voltage step-up in a boost converter.
•	The output capacitor filters the switching ripple and smooths the pulsating waveform into a stable DC voltage. The regulated output voltage is then fed back to the controller, forming a closed-loop system that continuously adjusts the duty cycle to maintain voltage stability under varying load or input conditions.
•	Thus, the PWM signal controls the switching behavior of the power device, regulates energy transfer through the inductor, and, together with the capacitor, ensures a stable and regulated DC output voltage suitable for electric vehicle power electronic applications.


Parameter	Value
Duty Cycle	0.5
Output Current	 2.4A
Output voltage  48 v
Input current    4.8 A
Inductor Ripple	0.2 A
Voltage Ripple	0.3 mV
Critical Inductance	125 µH
Operating Mode	CCM
Controller	PI (0.1 + 4/s)

Tools Used

• MATLAB  
• Simulink  
• Simscape Electrical

Simulation Result:

Simulation Results
The following waveforms were analyzed:
•	Input Voltage
•	PWM Gate Pulse
•	Inductor Current Ripple
•	Output Voltage Response
•	
Observations:
✔ Stable voltage boost from 24V to 48V
✔ Inductor current ripple ≈ 0.2A
✔ Output ripple ≈ 0.3V
✔ Continuous conduction mode confirmed

Application
•  EV DC bus voltage step-up
•  Battery-powered high-voltage subsystems
•  Renewable energy DC interface
•  EV auxiliary power systems
