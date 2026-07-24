# Lecture digest: Introduction to Digital Signal Processing

Source deck (77 slides, EN): https://docs.google.com/presentation/d/1Cte6w0t8yTJRFirde6GPxKB29VX3SrX1mhAkKYEN-n4/
Per-slide text + speaker notes, extracted automatically. Slide numbers = pointers into the deck.

## Slide 1
Lecture 1 Introduction to Digital Signal Processing

## Slide 2
What is sound? Digital sound representation Fourier analysis Properties of discrete Fourier Transform (DFT) Spectrograms And how it is stored in the computer?

## Slide 3
What is sound? The air around us is filled with molecules. When you pull a guitar string, it creates a vibration that moves through the molecules in the air. The regions of high pressure are compressions and the regions of low pressure as rarefactions . https://pudding.cool/2018/02/waveforms https://theory.labster.com/sound-waves-dbs

> **Notes:** Fun facts: Sound is a mechanical wave as it requires a medium to travel through. This means that if there are no particles present, such as in the vacuum of space, then it cannot propagate. This is unlike light, or electromagnetic waves, which can travel through a vacuum, and explains why we can see the Sun but we can’t hear it. Sound is also a longitudinal wave because the particles in the medium oscillate parallel to the direction of propagation.

## Slide 4
What is sound? The microphone detects these variations in pressure. When we plot pressure, relative to atmospheric pressure, against the position near the string, we see the familiar sinusoidal waveform. The sinusoidal waveform follows from physics equations, see this slide https://theory.labster.com/sound-waves-dbs/

> **Notes:** Fun facts: Sound is a mechanical wave as it requires a medium to travel through. This means that if there are no particles present, such as in the vacuum of space, then it cannot propagate. This is unlike light, or electromagnetic waves, which can travel through a vacuum, and explains why we can see the Sun but we can’t hear it. Sound is also a longitudinal wave because the particles in the medium oscillate parallel to the direction of propagation.

## Slide 5
Analog and digital signals sound source pressure sensor Analog-to-Digital Converter (ADC) quantization / amplitude discretization sampling / time discretization PCM binary file

> **Notes:** Let's explore the transition of sound from an acoustic wave to a digital signal. Initially, we have a sound source that generates compression waves , as discussed earlier. Eventually, these waves reach a pressure sensor strategically placed at a specific location. A pressure sensor is a device that transforms pressure changes into another physical quantity That physical quantity must allow an easy convertion into an electrical signal, such as voltage or current. A simple example: spring compression After that , voltage or current are gathered using a measurement instrument. There is a direct correlation between the pressure values at the sensor and the voltage values in our electrical measurement system. This means that our electrical signal is an analog to the initial physical value (pressure) Regrettably, the continuous value of this analog signal cannot be stored directly. Therefore, it becomes necessary to capture samples over a specific period of time, a process known as sampling or time discretization . Moreover, exact measurement and storage of amplitude values pose a challenge. To address this, reference values of the signal are employed, and analog readings are rounded to these reference values—a process known as quantization or amplitude discretization . Both of these procedures will be elaborated on in the subsequent slide. Once the data points are collected, they can be stored as a binary vector. This method of storage is termed Pulse Code Modulation (PCM), where the original signal is encoded with a set of pulses. If these pulses are correctly transmitted to an acoustic speaker, the original sound can be reproduced with a certain degree of accuracy.

## Slide 6
Waveform as Pulse-Code Modulation (PCM) Time discretization : we represent the analog signal as a sequence of samples measured at discrete points in time Sample rate – number of audio samples per second (8kHz, 22.05kHz, 44.1kHz) Amplitude discretization: round continuous amplitude to the nearest discrete value Bit depth – number of bits per sample (eg. 8, 16, 24, 32 bits) Bit rate = bit-depth * sample-rate * audio-channels Number of channels: number of signals recorded in parallel (ex: mono vs. stereo) https://github.com/yandexdataschool/speech_course/tree/2022/week_02

> **Notes:** The hertz (symbol: Hz ) is the unit of frequency in the International System of Units (SI), equivalent to one event (or cycle ) per second . https://en.wikipedia.org/wiki/Hertz sample rate = 1Hz means that there is one sample per second

## Slide 7
Properties of waveforms: Intensity Intensity is defined to be the energy (E) per unit area (A) and time unit (t) carried by a wave: The intensity of a sound wave is proportinal to its amplitude squared: For a discrete-time signal of length : https://courses.lumenlearning.com/atd-austincc-physics1/chapter/17-3-sound-intensity-and-sound-level/ power

> **Notes:** The bird is uniformly screaming Actually intensity is averaged over some window

## Slide 8
Properties of waveforms: Loudness Loudness is intensity measured in decibel bel reports log10 of ratio between measuring signal and reference signal In physics, decibels are used instead of bels because 1 bel is too large https://decibelpro.app/blog/how-many-decibels-does-a-human-speak-normally/

> **Notes:** Why do people want to measure intensity? For example, to determine when it's too noisy according to labor regulations or to adjust the volume of advertisements (Loadness wars: https://tract.media/lufs/ ). we aim to normalize sound intensity relative to a specific fixed baseline value =&gt; we map our intensity to d ecibels (who are a relative measure)

## Slide 9
What about audio formats? Uncompressed: WAV, AIFF Lossless compression: FLAC, ALAC Lossy compression: MP3, Opus https://en.wikipedia.org/wiki/Audio_file_format

## Slide 10
*(no text — visual only)*

## Slide 11
Fourier analysis Digital sound representation Fourier analysis Properties of discrete Fourier Transform (DFT) Spectrograms for sound signals

## Slide 12
Difficulties in using waveforms Waveform is really long (e.g. 44K samples / sec) Waveforms provide limited insight into a recording's pitch and speech content Can we get a more compact and informative sound representation ?

## Slide 13
*(no text — visual only)*

## Slide 14
Fourier Analysis At its core, Fourier analysis breaks down complex signals into their frequency components. It's similar to breaking down a song into its individual musical notes. https://angeloyeo.github.io/2019/06/23/Fourier_Series_en.html

## Slide 15
Fourier Analysis The amplitudes of these frequency components appear on the frequency axis rather than the time axis, forming what's called the (frequency) spectrum . https://angeloyeo.github.io/2019/06/23/Fourier_Series_en.html

## Slide 16
Fourier Analysis The usefulness of Fourier analysis: It converts a long sequence of time samples into a compact frequency representation. It enables analysis of frequency components and filtering of unwanted frequencies. https://angeloyeo.github.io/2019/06/23/Fourier_Series_en.html

## Slide 17
Fourier Series Any absolutely integrable periodic function with period can be represented as magnitude phase https://en.wikipedia.org/wiki/Fourier_series https://github.com/yandexdataschool/speech_course/tree/2022/week_02 frequency Use formula for cosine of the difference Time domain Frequency domain Use magnitude &amp; phase

> **Notes:** Сказать или добавить дополнительный слайд: Каждая частота входит в сумму со всё меньшей амплитудой, уточняя всё более мелкие детали, мб добавить красивые картинки про это картинка про fundamental frequency: https://en.wikipedia.org/wiki/Fundamental_frequency Каждая частота кратна базовой частоте 1 / P – она же F_0 – важна для практики. (TODO: проверить)

## Slide 18
Fourier Series: exponential form https://en.wikipedia.org/wiki/Fourier_series Fourier Coefficient The set of Fourier coefficients is also called the spectrum of are complex numbers

## Slide 19
Fourier Series for a discrete signal In practice our time signal is time-limited and contains non-zero samples taken with a sampling period seconds. Let's explore what happens when we try to find its Fourier coefficients. https://ru.dsplib.org/content/dft/dft.html

## Slide 20
Fourier Series for a discrete signal First, we must extend our signal periodically so it's defined across the entire time axis. The smallest possible period is . https://ru.dsplib.org/content/dft/dft.html

## Slide 21
Fourier Series for a discrete signal https://ru.dsplib.org/content/dft/dft.html *See additional slides for the full derivation The i ntegral “turns” into a sum over a discrete set of values

## Slide 22
Fourier Series for a discrete signal The expression above is valid for any integer but it is periodic and repeats every samples: https://ru.dsplib.org/content/dft/dft.html disappears! Now the basis functions are defined by :

## Slide 23
Fourier Series for a discrete signal https://www.youtube.com/watch?v=nreiTseFZQ0

## Slide 24
Discrete Fourier Transform (DFT) and its inverse If we operate only with indices of the input signal and spectral samples (setting lolkekc ), we obtain the Discrete Fourier Transform expression: We can also write out the expression for the Inverse Discrete Fourier Transform (we'll skip the complete derivation):

## Slide 25
DFT &amp; IDFT In practice, we usually need to calculate the forward DFT more often than IDFT. Because of this, there's a common convention: we put the scaling factor лщл in the inverse transform equations instead of the forward transform.

## Slide 26
FFT: Fast Fourier Transform FFT allows to compute DFT with complexity instead of This is one of the reasons why DFT is so widely used See this video for a detailed explanation of the FFT algorithm https://en.wikipedia.org/wiki/Fast_Fourier_transform

## Slide 27
*(no text — visual only)*

## Slide 28
Break time!

## Slide 29
Discrete Fourier Transform Digital sound representation Fourier analysis Properties of Discrete Fourier Transform (DFT) Spectrograms Properties

## Slide 30
DFT: basic properties If we had samples that we wanted to perform a DFT on, this would mean that we would compute 10 Fourier coefficients Each measures the contribution of a particular frequency to the entire signal. DFT only represents oscillations that fit a whole number of times into points (in addition to the constant component ) https://brianmcfee.net/dstbook-site/content/ch05-fourier/DFT.html#some-facts-about-the-dft

## Slide 31
*(no text — visual only)*

> **Notes:** H а семпл рейт мы влиять не можем, но на что мы тогда влияем нашим N?

## Slide 32
Frequency resolution If we get back to sampling points ( is the time between each sampling point): So, the frequency at which the k-th sinusoid oscillates is is sampling rate frequency resolution

## Slide 33
*(no text — visual only)*

## Slide 34
Spectrum A great way of displaying DFT coeffcients are so called (amplitude) spectrums : we can plot magnitudes of on a y-axis and frequencies on an x-axis In speech processing we often only look at the spectral magnitudes and ignore phase: Speech intelligibility mainly depends on spectral magnitude (important for speech recognition). Intonation and stress are encoded in spectral magnitude (important for speech synthesis). When is phase important? Speech enhancement (the process of improving the quality of speech signals by reducing noise, reverberation, and distortions)

## Slide 35
Simple spectrums Why do we see 2 frequencies?

## Slide 36
DFT: Symmetry of coefficients F or real-valued signals, o nly one half of the DFT coefficients provide us with information for real signals The other half can be reconstructed by complex conjugation

> **Notes:** Прикольно через “закон сохранения информации” – из n флотов получили 2n флотов, но они связаны по опред закону (разнообразных по-прежнему n) X(n) =

## Slide 37
DFT: Symmetry of coefficients May remove all after the line

## Slide 38
Shannon-Nyquist Sampling Theorem (Kotelnikov) Theorem : A function containing no frequency higher than Hz, is completely determined by sampling at Hz. Equivalently : To resolve all frequencies in a function , it must be sampled twice the highest frequency present. is called Nyquist frequency https://www.youtube.com/watch?v=FcXZ28BX-xE&amp;t=277s For Nyquist frequency Nyquist frequency is always in the middle of a spectrum

> **Notes:** For one second of audio with the sampling rate 44.1 kHz we get 22050 independent frequencies with a step 1 Hz between them

## Slide 39
Nyquist frequency DFT: Symmetry of coefficients

## Slide 40
Sampling rate Nyquist frequency Frequency resolution

## Slide 41
Spectrum of a real audio piece (the symmetrical frequencies are removed)

> **Notes:** Note:

## Slide 42
*(no text — visual only)*

## Slide 43
Spectrograms Digital sound representation Fourier analysis Properties of Discrete Fourier Transform (DFT) Spectrograms D isplay the dynamics of the spectrum over time

## Slide 44
DFT for real-life audio signals We could take our digitized audio signal and convert into the frequency domain However, speech varies and is non-stationary Whole-signal DFT does not help us retrieve information about local structures https://github.com/yandexdataschool/speech_course/tree/2022/week_02

## Slide 45
Short-Time Fourier Transform (STFT) Need to examine local spectrum to see how it changes! https://github.com/markovka17/dla/tree/2022/week02

## Slide 46
Spectral leackage DFT implicitly treats the original x[n] as a periodic function ( slide ). So it will attempt to approximate discontinuities in the signal and identify extra frequencies. https://www.gaussianwaves.com/2011/01/fft-and-spectral-leakage-2/

## Slide 47
Spectral leackage Spectral leakage comes out in the form of spreading out values from one bin (representing frequency of signal) to neighboring. https://wiki.cimec.unitn.it/tiki-index.php?page=Frequency-domain+analysis

## Slide 48
Window functions The idea of windowing a signal is to force continuity at the boundaries, prior to performing the DFT: https://github.com/markovka17/dla/tree/2022/week02

## Slide 49
Spectrogram S tack STFTs of a window sliding over the signal Each window is called acoustic frame Important hyperparameters: Window length and shape Hop length : the length of overlap between windows https://github.com/markovka17/dla/tree/2022/week02

> **Notes:** Ask : What does window length determine on the spectrogram? How is the maximum frequency on the spectrogram defined? Spectrogram и mel-spectrogram are the examples of time-frequency domain representations.

## Slide 50
Freq (Hz) What does sample rate define? What does window length define?

## Slide 51
Freq (Hz) What does sample rate define? Maximum possible frequency value on the spectrogram (Nyquist) What does window length define? Frequency resolution (number of rows on the spectrogram)

## Slide 52
Example: Speech

## Slide 53
Example: Saxofone https://github.com/yandexdataschool/speech_course/tree/2022/week_02

## Slide 54
Mel scale The speech apparatus is designed in such a way that we hear low frequencies well but poorly hear high frequencies ( Cochlea ). The Mel scale is an approximate scale of human frequency perception It pays more attention to lower part of spectrum We can convert between Hertz (f) and Mel (m) using the following equations:

> **Notes:** https://en.wikipedia.org/wiki/Cochlea For humans, the difference in the notes of the lowest octaves of the piano at 3 Hz is as audible as 215 Hz in the highest octaves. https://patentimages.storage.googleapis.com/83/37/d1/71f50320d2f042/00000002.png At the same time, the highest note on the piano is 3 kHz, while humans can hear up to 20 kHz.

## Slide 55
Mel filter bank Mel spectrum is produced by linear projection with Mel filter bank F . Given a spectrogram S , the Mel-Spectrogram M is produced as M = F S Typically, a logarithm is applied to the result in the end. https://librosa.org/doc/main/generated/librosa.filters.mel.html https://haythamfayek.com/2016/04/21/speech-processing-for-machine-learning.html

## Slide 56
Mel-spectrogram 0 8000 Spectrogram S Filterbank F

> **Notes:** Frequencies after using filter banks begin to be perceived linearly: adjacent mels differ equally by ear, regardless of their height Also a matrix very close mel-filterbanks matrix F can be learnt by a neural network: https://www.researchgate.net/publication/327388783_Acoustic_Modeling_from_Frequency_Domain_Representations_of_Speech

## Slide 57
Mel-spectrogram 0 8 0 0 8000 Spectrogram S Mel- Spectrogram = F * S F

> **Notes:** Frequencies after using filter banks begin to be perceived linearly: adjacent mels differ equally by ear, regardless of their height Also a matrix very close mel-filterbanks matrix F can be learnt by a neural network: https://www.researchgate.net/publication/327388783_Acoustic_Modeling_from_Frequency_Domain_Representations_of_Speech

## Slide 58
Lecture summary A sound wave is a series of pressure changes Fourier Series maps continuous signal from time domain to frequency domain. DFT allows to do the same for sampled signals

## Slide 59
Lecture summary The number of samples N defines frequency resolution Half of DFT coefficients for real-valued signals carry redundant information. This aligns with Shannon-Nyquist theorem

## Slide 60
Lecture summary https://github.com/yandexdataschool/speech_course/tree/2022/week_02 We created a spectrogram to visualize how the signal's spectrum changes over time. We then compressed the frequencies by applying mel filters.

## Slide 61
*(no text — visual only)*

## Slide 62
Additional slides

## Slide 63
Acoustic wave equation the continuity equation for 1D the equation of state ( ideal gas law ) solution 1-D l Euler Equation

## Slide 64
Hearing and Voicing Ranges https://theory.labster.com/hearing-range-dbs/

## Slide 65
Example: Chirp https://en.wikipedia.org/wiki/ Chirp

## Slide 66
Fourier Series: exponential form https://en.wikipedia.org/wiki/Fourier_series Euler’s formula Summation limits changed

## Slide 67
*(no text — visual only)*

## Slide 68
Discrete signals As we know from the beginning of the lecture, we usually deal with discrete signals , that take arbitrary values only at fixed moments in time: ( is the sampling interval ). Given these samples, can we determine anything about the spectrum of the original signal? https://ru.dsplib.org/content/discrete_introduction/discrete_introduction.html

## Slide 69
Can we directly apply Fourier Series? If we just sample points from our signal and construct a new function: and then periodically extend , we encounter a problem – its Fourier coefficients are all zeros: https://en.wikipedia.org/wiki/Riemann_integral

## Slide 70
Mathematical model of a discrete signal How can we measure an analog signal in practice? It takes some time to make a measurement. Therefore, during measurement, we don't get an exact value at , but rather an averaged value within the measurement interval​ https://ru.dsplib.org/content/discrete_introduction/discrete_introduction.html

## Slide 71
Dirac delta function (Impulse) https://ru.dsplib.org/content/fourier_transform_delta_func/fourier_transform_delta_func.html We can choose any integration limits around t0

## Slide 72
Back to the mathematical model As the duration decreases, the estimation error will decrease, and in the limit we can obtain the discrete signal as https://ru.dsplib.org/content/discrete_introduction/discrete_introduction.html

## Slide 73
The integration issue is fixed!

## Slide 74
Fourier Series for a discrete signal In practice our time signal is time-limited and contains non-zero samples taken with a sampling period seconds: Let's explore what happens when we try to find its Fourier coefficients. https://ru.dsplib.org/content/dft/dft.html

## Slide 75
Fourier Series for a discrete signal First, we must extend our signal periodically so it's defined across the entire time axis. The smallest possible period is . https://ru.dsplib.org/content/dft/dft.html

## Slide 76
Fourier Series for a discrete signal The standard formula for calculating Fourier coefficients of a periodic function, which we mentioned earlier, is: Applying this to our signal: https://ru.dsplib.org/content/dft/dft.html

## Slide 77
Fourier Series for a discrete signal Let's interchange the order of integration and summation: The expression above is valid for any integer but it is periodic and repeats every samples: https://ru.dsplib.org/content/dft/dft.html T disappeared! Now the basis functions are defined by N
