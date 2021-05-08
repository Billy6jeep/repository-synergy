#+AUTHOR: Maarten Versteegh
* vad
This is a straight-forward re-implementation of Bowon Lee's Voice Activity
Detector. The relevant paper to cite is: Bowon Lee and Mark Hasegawa-Johnson,
"Minimum Mean-squared Error A Posteriori Estimation of High Variance Vehicular
Noise". Please cite that paper when using this code for research purposes.

** Usage
: >>> from vad import VAD
: >>> detector = VAD(fs=16000)
: >>> speech = detector.detect_speech(sig, threshold=0.5)

** Requirements
+ python>=2.7 / python>=3.0
+ numpy>=1.8.0
+ scipy>=0.14.0
