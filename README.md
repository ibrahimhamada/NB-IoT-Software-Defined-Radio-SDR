# Implementation-of-NB-IoT-Software-Defined-Radio-SDR
The project aims to simulate 8 NB-IoT devices transmitting their UL signal to the NB-IoT base station. The NB-IoT mode is the Standalone mode in which the NB-IoT carrier is deployed outside the LTE spectrum, e.g., in the spectrum used for GSM or satellite communications.


My Project of the Digital Signal Processing Course Offered in Fall 2021 @ Zewail City.

In this project, I designed an FIR digital filter for a NB-IoT software defined radio (SDR) base station Receiver using MATLAB.
==================================================

## Transmitter Block Diagram <a name="Transmitter Block Diagram"></a>
![Transmitter Block Diagram](https://user-images.githubusercontent.com/58476343/220173214-f8e2fe8f-5dff-40a1-9988-98edfeac9e6b.png)



## Transmitter:
A) Baseband Signal Generation

            1) Uplink() functions is used to generate the baseband signal.
            2) The generated NB-IoT uplink complex baseband waveform represents the 180 kHz narrowband carrier.
            3) The Sampling Frequency of the Waveform is 1.92 MHz.

B) Upsampling:

            1) The sample rate of the generated NB-IoT uplink complex baseband waveform needs to be increased in order to allow for digital upconversion.
            2) upsample() function is used to increase the sample rate. 
            3) upsample() function's inputs are: the waveform, a factor which will by the original sample rate to generate the upsampled rate.
            4) upsample() funciton's output is: the upsampled waveform with the new sample rate.
            5) Since the transmitted signal will contain 8 NB-IoT uplink complex baseband waveform.
            6) Each signal has a bandwidth of 180 kHz. (0 Hz : 180 kHz)
            7) The spacing between each two signals in frequency domain is 20 kHz (suh the space between two signals' center is 200 kHz).
            8) The first signal will be centered at IF =200 kHz, while the last one will be centered at IF = 1600 kHz.
            9) Based on the above calculations, and given the frequency margin of 310 kHz ,the new sample rate will be chosen such that: fs/2 = 2 MHz
                                                                      

   


## Receiver Block Diagram <a name="Receiver Block Diagram"></a>

![Receiver Block Diagram](https://user-images.githubusercontent.com/58476343/220173238-3c739147-a904-4276-9461-36a84f1439cf.png)


## Implementation Steps:

A) MPEG audio Encoder Layer 2

            1) Reading PCM-coded digital audio from standard Windows. WAV file.
            2) Designing the essentials of time-to-frequency filter bank to break the input signal into 32 equally spaced frequency subbands.
            3) Using the downsampler which reduces the amount of data required for each sub-band. 
            4) A psychoacoustic model is applied to the input signal with a 1024-point FFT to determine which frequency bands should be retained. 
            5) Comparing the total length of the encoded bits in both cases. 
            6) The Allocation and coding block uses the data provided by the model to determine how to encode the sub-band signals. 
            7) To achieve data compression, the encoder ignores subbands that are completely masked by other signal components.
            8) Additionally, subbands that are partially masked are encoded with less accuracy than the dominant subbands.

B) MPEG audio Decoder Layer 2

            1) Designing the decoder that restores the quantized spectral components of the signal.
            2) Reconstructing the time-domain representation of the audio signal from its frequency representation.
            
C) Performance Measure

            1) Compression ratio: it is defined as the ratio of the original signal to the compressed signal.
            2) Mean Opinion Score (Subjective evaluation): The audience would listen to the sound files and see the sound quality and score it. It has to grades from 5 to 1. 
            3) PEAQ (Perceptual Evaluation of Audio Quality) (Objective evaluation): measures the ODG (Objective Difference Grade) between the original and the reconstructed signal. In Objective testing five-level impairment for Perceptual Evaluation of Audio Quality (PEAQ).
