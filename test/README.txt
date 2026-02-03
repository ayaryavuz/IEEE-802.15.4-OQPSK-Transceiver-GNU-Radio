Results and Performance Analysis
In this section, the implemented OQPSK transceiver's performance is evaluated through spectral and visual analysis.
1. Power Spectral Density (PSD) Analysis
•	Technical Breakdown: This plot shows the signal's energy distribution across the frequency spectrum. The main lobe is perfectly 
centered, occupying approximately 2 MHz of bandwidth, which aligns with the IEEE 802.15.4 standard.
•	Engineering Insight: The sharp nulls at  ±1.5 MHz demonstrate excellent spectral containment. This confirms that the half-sine
pulse shaping filter is correctly suppressing out-of-band emissions, ensuring minimal interference with adjacent channels in the 2.4 GHz 
ISM band.
2. OQPSK Constellation Diagram
•	Technical Breakdown: Unlike standard QPSK, which has points only in the four corners, this OQPSK constellation shows points on the axes.
This is a direct result of the T/2 offset between the In-phase (I) and Quadrature (Q) channels.
•	Engineering Insight: The transitions never pass through the origin (0,0). This significantly reduces the envelope fluctuations of the 
signal, allowing the use of high-efficiency, non-linear power amplifiers without causing significant spectral regrowth.
3. Time-Domain Signal (I & Q Channels)
•	Technical Breakdown: This waveform plot visualizes the real (blue) and imaginary (red) components of the OQPSK signal over time.
•	Engineering Insight: If you look closely at the peaks, the transitions in the blue line (I) are staggered compared to the red line (Q). This half-symbol delay is the heart of the OQPSK modulation. It ensures that the phase never jumps 1800 at once, maintaining a more constant signal envelope.
4. Spectrogram / Waterfall Display
•	Technical Breakdown: The waterfall plot displays the signal's frequency content over time. The consistent vertical yellow bands represent the continuous power density of the transmitted packets.
•	Engineering Insight: The temporal stability of the signal (no flickering or frequency drifting) proves that the Carrier Frequency and Sampling Rate are well-synchronized. This stability is crucial for the receiver's Clock Recovery MM block to maintain a stable timing lock.

