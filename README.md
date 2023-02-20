# Implementation-of-NB-IoT-Software-Defined-Radio-SDR
The project aims to simulate 8 NB-IoT devices transmitting their UL signal to the NB-IoT base station. The NB-IoT mode is the Standalone mode in which the NB-IoT carrier is deployed outside the LTE spectrum, e.g., in the spectrum used for GSM or satellite communications.


My Project of the Digital Signal Processing Course Offered in Fall 2021 @ Zewail City.

In this project, I designed an FIR digital filter for a NB-IoT software defined radio (SDR) base station Receiver using MATLAB.


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
                                                                      
C) FIR Filter:

            1) The waveform has frequency components from -800 kHz to 800 kHz. 
            2) The important frequencies exist in the range from -90 kHz to 90 kHz.
            3) FIR Filter is needed to pass the important frequencies, while attenuating the unwanted frequencies.
            4) Here are the specifications and constraints of the digital FIR filter to be designed:
                   1) Passband ripples: peak-to-peak passband ripple = 2 dB  
                   2) Stopband attenuation: -60 dB
                   3) Transition region width: 
                   4) Max Number of filter taps: 512 taps  
   





## Receiver Block Diagram <a name="Receiver Block Diagram"></a>
![Receiver Block Diagram](https://user-images.githubusercontent.com/58476343/220173238-3c739147-a904-4276-9461-36a84f1439cf.png)


