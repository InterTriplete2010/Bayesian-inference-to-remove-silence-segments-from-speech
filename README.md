# Bayesian-inference-to-remove-silence-segments-from-speech
Bayesian inference to remove silence segments from speech


This GUI detects and removes silence segments from speech (voiced and unvoiced) using a Bayesian approach, as described in "Theory and Applications of Digital Speech Processing" by Lawrence Rabiner
Ronald Schafer (page 595 to page 603). 

Here is how the GUI works:

1) To start the GUI type "Silence_Removal_Speech";

2) "Upload waveform": select the speech waveform that you want to use for training the algorithm. 

3) "Low Pass IIR Filter (Butterworth)": The speech waveform is high-pass filtered to remove low frequency noise. Type the order of the filter and the corner frequency. By default, the corner frequency is 200 Hz, as recommended by Rabiner and Schafer;

4) "Parameters time window (ms)": Choose a time window and time shift for the analysis. The default ones in the GUI are the ones recommended by Rabiner and Schafer;

5) "Prior silence and voice": Type the prior probability. The default ones in the GUI are the ones that have been used to test the code;

6) "Threshold silence": Estimate the two distributions (voiced/unvoiced and silenced) by using a silence threshold to separate them and to calculate the mean and covariance for each of the 5 parameters (1) short-time log energy; 2) number of zero crossings, 3) normalized short-time autocorrelation coefficient, 4) first predictor coefficient of a p = 12 linear model, 5) normalized log prediction error) used by Rabiner and Schafer. The book suggests to visually inspect the training waveform, but "Threshold silence" seem to be working equally well and is faster, since it is automatized;
  
7) "EM Loops": Number of interactions used for the Expectation Maximization (EM) algorithm. The EM is then used to optimize the parameters for the multivariate gaussian distribution;

8) "Upload directory": Upload the directory where the waveforms that need to have silence segments removed are stored. The code will loop through all the ".wav" files that it finds in the selected directory;

9) "Max allowable silence segment": Select the maximum length of each silence segment. The default one is 500 ms, which means silence segments cannot be longer than 500 ms. 

10) "Remove Silence": The code will be executed. The new waveforms with shortened silence segments will be saved in the same folder selected in "Upload directory". The name of the new waveforms will be the "orginal_name_Shortened_Waveform.wav". For instance, if the original name was "Speech_1", the waveform with shortened silence segments will be saved with the name "Speech_1_Shortened_Waveform.wav"

These Matlab files are part of a large Toolbox that I wrote and that I am using to analyze EEG and MEG data.

If you have any question and/or want to report bugs, please e-mail me (Ale) at: pressalex@hotmail.com
