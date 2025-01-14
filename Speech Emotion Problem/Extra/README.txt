Useful Definitions for reading my approach and code:

Specgram-Time-dependent frequency analysis (spectrogram).Specgram computes the windowed discrete-time Fourier transform of a signal using a sliding window. The spectrogram is the magnitude of this function.

Mel-Spectrogram- Mel-scaled spectrogram.

Log Mel-Spectrogram- Log of Mel-scaled spectrogram.

MFCC-Mel Frequency Cepstral Coefficents (MFCCs) are a feature widely used in automatic speech and speaker recognition. 
They were introduced by Davis and Mermelstein in the 1980's, and have been state-of-the-art ever since.To get MFCC, compute the DCT on the mel-spectrogram. The mel-spectrogram is often log-scaled before.MFCC is a very compressible representation, often using just 20 or 13 coefficients instead of 32-64 bands in Mel spectrogram. The MFCC is a bit more decorrelarated, which can be beneficial with linear models like Gaussian Mixture Models.

Filter Banks -Filter banks are arrangements of low pass, bandpass, and highpass filters used for the spectral decomposition and composition of signals. 
They play an important role in many modern signal processing applications such as audio and image coding. The reason for their popularity is the fact that they easily allow the extraction of spectral components of a signal while providing very efficient implementations. Since most filter banks involve various sampling rates, they are also referred to as multirate systems.

Things I tried:
1. Training 1D and 2D CNN using Log-Specgram features of a wav file (Using Keras)
2. Training LSTM Network using Filter Bank features of a wav file (Using Keras)
3. Training 2D CNN after augentation of a wav file and taking logmelspectrum features. Augmentations include adding random noise, random padding and random time shift.(Using PyTorch)
4. Training LightGBM for 1d data, both wave and mean of melspectogram.
(Code for all these approaches are present in the github folder).

Out of all these the PyTorch implementation with data augmentation and CNN with residual blocks model worked best.
(Average cross-entropy loss of 1).

The main problem with the data was class-imbalance. Class neutral had too many instances and others had too little. I tried undersampling but did not work. 
Most of the models were biased towards the neutral class and as a result predicted just neutral class for all validation samples.

What could have worked but I did not implement:
Ensemble/Stacked Approach: A simple ensemble or stacking of all models could have given much better results but I couldn't try that due to time constraints.
Synthetic data generation using smote could have helped.