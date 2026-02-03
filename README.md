IEEE 802.15.4 OQPSK PHY Transceiver Design
Project Overview
This repository contains a full Physical Layer (PHY) implementation of the IEEE 802.15.4 standard, commonly used in low-power Wireless Personal Area Networks (WPAN) like ZigBee. The design is implemented using GNU Radio Companion (GRC) and focuses on the 2.4 GHz ISM band specifications.
The flowgraph demonstrates a complete transceiver chain, including:
  Packet Handling: PDU to Tagged Stream conversion and Access Code prefixing.
  Modulation: Implementation of Offset Quadrature Phase Shift Keying (OQPSK).
  Signal Conditioning: Half-sine pulse shaping and interpolation.
  Receiver Synchronization: Mueller-Müller (MM) Clock Recovery for precise timing synchronization.

Why OQPSK instead of Standard QPSK?
In the IEEE 802.15.4 standard, OQPSK (Offset-QPSK) is preferred over standard QPSK for several critical engineering reasons, particularly for low-power IoT and sensor devices:
  1. Reducing Envelope Fluctuations: In standard QPSK, both the In-phase (I) and Quadrature (Q) components can change simultaneously. This can lead to a phase shift of 180°, causing the signal envelope to pass through the origin (zero amplitude). In OQPSK, the Q channel is delayed by half a symbol period, ensuring that only one channel changes at a time. This limits the maximum phase shift to 90°.
  2. Efficiency of Power Amplifiers (PA): Because the signal envelope in OQPSK does not pass through zero, it has a much lower Peak-to-Average Power Ratio (PAPR).
     Standard QPSK: Requires highly linear (and power-hungry) amplifiers to handle large amplitude swings without distortion.
     OQPSK: Allows the use of non-linear, high-efficiency power amplifiers (like Class C) because the signal amplitude remains more constant. This is vital for battery-operated devices.
  3. Reduced Spectral Regrowth: When a signal with high amplitude fluctuations passes through a non-linear amplifier, it causes "spectral regrowth" (interfering with adjacent channels). OQPSK minimizes this effect, ensuring better spectral efficiency and compliance with strict RF regulations.

System Architecture & Signal Flow
Beyond the modulation theory, the practical implementation of a transceiver requires a robust architecture to handle timing, synchronization, and data integrity. Including the system architecture here serves several purposes:
  Design Transparency: It visualizes the end-to-end signal processing chain, from bit-level packetization to the final RF waveform generation.
  Engineering Rationale: It explains the placement of specific blocks, such as why the Delay block is positioned between "Complex to Float" and "Float to Complex" to achieve the precise T/2 offset required for OQPSK.
  Hardware-Ready Insight: The architecture highlights the synchronization blocks (like the Mueller-Müller Clock Recovery), demonstrating how the system compensates for real-world timing drifts—a necessity for any SDR-to-Hardware implementation.
  ![Complete GNU Radio flowgraph](https://github.com/user-attachments/assets/db7e46f3-ae7f-4d1b-b3f8-39c46c47425a)
                                                                   
                                                                     

Results and Analysis
The implementation has been verified through both simulation (GNU Radio GUI) and hardware testing with HackRF One. The following results confirm the system's performance and compliance with IEEE 802.15.4 standards:
  1. Constellation Analysis: The OQPSK constellation exhibits the characteristic "offset" transitions, where phase changes do not pass through the origin.This confirms the successful T/2 delay implementation between the I and Q channels, resulting in a significantly lower Peak-to-Average Power Ratio (PAPR) compared to standard QPSK.
  2. Synchronization PerformanceThe Mueller-Müller Clock Recovery block successfully achieves timing lock even under noisy channel conditions.The receiver accurately decodes the Access Code (0xA7) defined in the IEEE standard, ensuring consistent packet synchronization.
  3. Spectral EfficiencyBy utilizing half-sine pulse shaping, the occupied bandwidth is minimized, and spectral regrowth is suppressed.This ensures that the transmitter remains within the strict spectral mask requirements of the 2.4 GHz ISM band.

  

