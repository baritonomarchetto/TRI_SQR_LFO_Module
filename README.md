# Low Frequency Oscillator Module for Synthesizers V2
A feature-loaded LFO module for Eurorack synthesizers.
Features:
- two waveforms: triangle and square
- control over triangle wavefor skew and square duty-cycle
- three frequency ranges (0-10Hz, 0-100Hz and 0-1000Hz)
- control over gain (from total attenuation to 8Vpp)
- control over bias level
- LED visual indication about wave characteristics

# Layout and Module Design
Low frequency oscillators are very common modulation sources in eurorack synthesizers mainly because of their effectivness and ease of use. Despite this, they often require some external module to reach destination module's modulation soft-spot.

Just to cite an example, as far as the destination module accepts AC coupled input voltages eveything is ok, but what if some DC biasing is necessary? One very practical example could be the modulation of CEM3340 voltage controlled oscillators PWM frequency. For musical results, you want a DC biased source of modulation, or the square wave output will be silenced on negative bias (0% duty cycle).

Another example: what if you want to (and most of the time you do) subtly modulate your destination instead of applying a full range modulation? An attenuator stage comes to the rescue.

All these scenarios can be easily faced applying some voltage processing to the "dry" LFO signal, but adding external modules means increased use of "vital" rack space.

Since I already made some good-working [external modules for signal processing](https://www.instructables.com/DIY-Synth-Modules-a-Modular-Approach-Ep2/), I knew I could add some of them with little-to-no waste of space to [my previous LFO project](https://www.instructables.com/Low-Frequency-Oscillator-Modules/). In particular, two extra circuits found their way inside the module: an active attenuator/amplification stage and a level shifter (DC offsetter).

Even with this increase in features (which also means "increased components count") I could keep the module in the 6HP ballpark. This made the faceplate a little more crowded, but still more than decent operation-wise.

In this new iteration of the LFO module I have adopted a stacked board design instead of the previous "flag-like" design. It's more complex to draw (more work on my side) but looks more "professional", if you know what I mean. It is also more compact then "less prone to damage", especially if one moves modules often.

# Circuits
The oscillators circuit here adopted was first introduced by [Nicolas Whoolaston](https://electro-music.com/) in 2008 at Electro-Music forum. It's main components are a generic quad op-amp, a non polarized capacitor and only a few others elements.

The wave generation is based on the use of an op-amp in relaxation oscillator configuration. Relaxation oscillator means that the opamp is configured to run “open loop” in which no feedback is used to limit the gain. Because the amplifier is essentially unstable, it will move as quickly as possible to either its largest possible positive or negative output. The output is automatically toggled between these two states by connecting the output to the inverting input with an RC time constant. This enables square wave oscillations. Wave actual amplitude limits are set by by two LEDs used as voltage limiters (positive and negative). The clamped relaxation oscillator output is then buffered before going to the outer-world as square wave. The triangular wave is generated in an adiacent section of the circuit, by charging a capacitor with a constant current. A simmetry modification circuitry makes the variable skew possibile for both waves.
The result is a nice oscillator with two different waveforms (triangular and square) and control over waveshape and frequency.

In addition to Nicolas circuit, I have included the possibility to change the frequency range of the oscillator, a very welcome feature present in most commercial LFO modules. The maximum frequency is determined by the non polarized capacitor (C1 in [THESE](https://electro-music.com/forum/phpbb-files/lfo_229.jpg) schematics) and it was a simple matter of adding other two caps in parallel and a 3 positions switch to include this welcome feature.
Capacitors must be non-polarized and Best Practice suggests using non ceramic mainly because of the tendency to drift with temperature. Ceramic caps will work, anyway, as far as you don't use it to set a pitch. Changing their values will change the frequency range of the oscillator (bigger -> lower frequencies, smaller -> higher frequencies).

Another addition is a voltage shifter circuit to bias waveforms to positive or negative voltages and final amplification stage to boost up waves amplitude to Eurorack levels.
Voltage shifting is obtained through the most basic (inverting) mixer, where one of the two LFO waves and DC offset voltage are added toghether. The signal is then inverted (again) to restore it's original polarity.
User has control over the gain of this final op-amp stage, where the waveform amplitude can span a "zero" to "2X" range.

Waves peak-to-peak voltage depends on clamping LED's color and final stage amplification. I have used white LEDs to have 7Vpp circa when the gain potentiometer is turned fully clockwise (2X amplification).

The circuit works on +/-12V dual voltage, but should also work on +/-15V.

I have layed down a Falstad's CircuitJS simulation of the whole LFO circuit. Click [>>HERE<<](https://tinyurl.com/25qswtjy) if you want to toy with it :)

# How to Use
The module is straightforward to use.

First, select the waveform with the ON-ON switch located in the bottom of the module. Available waveforms are triangle and square.

The "Shape" potentiometer give the user full control over the skew of the waveshape. On the square wave it affects the duty cycle, while on triangle shapes it continuously from backward saw, to triangle, to forward saw.

The second potentiometer ("Rate") modify the oscillation frequency of the wave of choice.

The frequency range can be set through a dedicated, 3-positions switch located on module's bottom. Frequency ranges are: 0 - 9 Hz, 0 - 90Hz and 0 - 900 Hz. You can hit higher frequencies by using smaller caps than those I adopted.

"Offset" potentiometer is used to shift up to positive or down to negative your oscillating voltage. This has practical applications such as in modulation of some external module parameter expecting voltages with a well-defined polarity.

The fourth potentiometer is used to increase/decrease the gain of the output signal. Gain goes from zero (completely attenuated wave, full counter clock-wise potentiometer) to 2X gain (7Vpp, full clock-wise pot).

# Acknowledgments
Many thanks to the nice girls and guys at [JLCPCB](https://jlcpcb.com/IAT) for sponsoring the manufacturing of PCBs for this module. Without their contribution this project would have never reached it's actual level of developent.

JLCPCB is a high-tech manufacturer specialized in the production of high-reliable and cost-effective PCBs. They offer a flexible PCB assembly service with a huge library of more than 350.000 components in stock.
3D printing is part of their portfolio of services so one could create a full finished product, all in one place!

By registering at JLCPCB site via [THIS LINK](https://jlcpcb.com/IAT) (affiliated link) you will receive a series of coupons for your orders. Registering costs nothing, so it could be the right opportunity to give their service a due try ;)

My projects are free and for everybody. You are anyway welcome if you want to donate some change to help me cover components costs and push the development of new projects.
[>>HERE<<](https://paypal.me/GuidolinMarco?country.x=IT&locale.x=it_IT) is my paypal donation page, just in case ;)
