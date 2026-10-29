<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,100:1f6feb&height=170&section=header&text=Angel%20Garg&fontColor=e6edf3&fontSize=48&fontAlignY=38&desc=Analog%20and%20Mixed-Signal%20IC%20Design&descAlignY=60&animation=fadeIn" width="100%" alt="Angel Garg"/>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=20&duration=2800&pause=900&color=58A6FF&center=true&vCenter=true&width=620&lines=8-bit+SAR+ADC+%E2%80%A2+layout+DRC%2FLVS+clean;Integer-N+CP-PLL+%E2%80%A2+20%E2%80%9350+MHz;Neurons+on+chip+for+ADC+calibration;Spec+%E2%86%92+transistors+%E2%86%92+layout+%E2%86%92+sign-off" alt="Typing intro"/>
</p>

<p align="center">
  <a href="https://linkedin.com/in/angel-garg-652795288"><img src="https://img.shields.io/badge/LinkedIn-Angel%20Garg-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
  <a href="mailto:gargangel2233@gmail.com"><img src="https://img.shields.io/badge/Email-gargangel2233%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"/></a>
</p>

### Hi, I'm Angel 👋

Analog and mixed-signal IC designer. I build data converters and clocking blocks end to end, from the spec and
transistor sizing through layout, DRC/LVS and post-layout sign-off, on India's **SCL 1.2 µm CMOS** process.
I also like using ML to fix analog errors.

<p align="center"><img src="assets/sar_conversion.svg" width="100%" alt="Animated 8-bit SAR ADC conversion: the DAC voltage binary-searches toward VIN, one bit per clock"/></p>

#### What I've built (pre-silicon)

| Block | What it is | Key numbers |
|---|---|---|
| **8-bit SAR ADC** (Rev3.2) | R-2R DAC, dual StrongARM comparator (PMOS/NMOS picked by trial code), SAR FSM, SPI output | Up to 2 MS/s (400 kS/s with a 10 MHz pad clock), 4 V FSR, comparator offset ≤ 0.5 LSB post-layout across corners, 4×4 mm chip DRC 0 / LVS match |
| **Integer-N CP-PLL** | Starved ring VCO, PFD, matched charge pump, divider, lock detector, external loop filter | 20–50 MHz (40 MHz nominal), 30/30 PVT corners, jitter 17.5 ps nominal, 2×2 mm chip DRC 0 / LVS match |
| **NN offset-calibrated comparator** ([repo](https://github.com/angelgarg/comparator)) | Dynamic comparator with a capacitor-array trim; a derivative circuit + TDC sense the offset polarity from zero-crossing timing and a neural network picks the trim code, no manual tuning | 447.2 µm², 783 µW at 1 GHz |
| **ADC + PLL combo** | Both blocks on one 5×5 mm die, PLL clocks the ADC | DRC 0 / LVS match / antenna 0 |
| **NeuroCal** | All-digital "neurons on chip" calibration engine for the ADC + PLL | 7.59 → 7.77 ENOB, SFDR 57 → 70 dB (sim), RTL bit-exact with the C model |
| **PRESENT-80 crypto chip** | SPI-controlled lightweight block cipher, gate-level and transistor-level verification | Spectre full-chip sim PASS, ~10 mW at 5 V |

#### Chip layouts

All three are my own full-chip layouts in SCL 1.2 µm (2 metal layers), DRC 0 / LVS match. Click an image to zoom in.

<table>
  <tr>
    <td align="center" width="33%"><a href="assets/adc_layout_4x4.png"><img src="assets/adc_layout_4x4.png" alt="SAR ADC Rev3.2 full-chip layout, 4 x 4 mm, with pads and blocks labelled"/></a><br/><b>SAR ADC</b> · 4 × 4 mm</td>
    <td align="center" width="33%"><a href="assets/pll_layout_2x2.png"><img src="assets/pll_layout_2x2.png" alt="CP-PLL full-chip layout, 2 x 2 mm: VCO, charge pump, PFD, divider, lock detector"/></a><br/><b>CP-PLL</b> · 2 × 2 mm</td>
    <td align="center" width="33%"><a href="assets/combo_layout_5x5.png"><img src="assets/combo_layout_5x5.png" alt="ADC + PLL combo chip layout, 5 x 5 mm, PLL in a guard ring in the top-right corner"/></a><br/><b>ADC + PLL</b> · 5 × 5 mm</td>
  </tr>
</table>

#### Architectures

<p align="center"><img src="assets/sar_adc_arch.svg" width="100%" alt="SAR ADC block diagram: external S/H, kickback match, dual StrongARM comparator, SAR logic, DAC drivers, R-2R DAC, control FSM, parallel and SPI outputs"/></p>
<p align="center"><img src="assets/cp_pll_arch.svg" width="100%" alt="CP-PLL block diagram: PFD, charge pump, off-chip loop filter, starved ring VCO, output driver, divide-by-N feedback, lock detector"/></p>

#### Results (post-layout simulation)

<details>
<summary><b>SAR ADC: transfer curve, DNL and INL across PVT corners</b> (|DNL| &lt; 0.3 LSB, |INL| ≲ 0.55 LSB)</summary>
<br/><img src="assets/adc_vtc_dnl_inl.png" width="80%" alt="Post-layout SAR ADC transfer curve, DNL and INL at five PVT corners"/>
</details>

<details>
<summary><b>CP-PLL: phase noise at 40 MHz</b> (17.5 ps rms jitter nominal, 26.4 ps worst corner)</summary>
<br/><img src="assets/pll_phase_noise.png" width="100%" alt="PLL phase noise with VCO, charge pump and R1 contributions at two corners"/>
</details>

<details>
<summary><b>ADC + PLL: PLL locks the same with the ADC converting next to it</b></summary>
<br/><img src="assets/combo_pll_lock.png" width="90%" alt="PLL phase error and VCTRL with the ADC in reset versus converting; curves overlap"/>
</details>

#### Projects you can open

- 🎙️ [**swar-voice-adc**](https://github.com/angelgarg/swar-voice-adc): offline voice commands on my own SAR ADC chip,
  using FPGA oversampling and on-device keyword spotting
- ⚖️ [**comparator**](https://github.com/angelgarg/comparator): neural-network-based offset calibration for dynamic
  comparators (capacitor array + TDC)
- 📈 [**nse-catalyst-scanner**](https://github.com/angelgarg/nse-catalyst-scanner): live catalyst-day detection for NSE stocks

#### Tools

Cadence Virtuoso · Spectre · ngspice · Xcelium/VCS · KLayout · Magic · Yosys · OpenROAD · Verilog/Verilog-A · Python · MATLAB

#### Interests

SAR and oversampling ADCs · PLLs and clocking · comparator offset calibration · ML for analog ICs · open-source EDA

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:1f6feb,100:0d1117&height=100&section=footer" width="100%" alt=""/>
