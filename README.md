# Bayesian-inference-to-remove-silence-segments-from-speech
Bayesian inference to remove silence segments from speech


This GUI detects and removes silence segments from speech (voiced and unvoiced) using a Bayesian approach, as described in "Theory and Applications of Digital Speech Processing" by Lawrence Rabiner
Ronald Schafer (page 595 to page 603). 

Please, keep in mind the following two facts:

1) If the audio file has 2 channels, the code assumes that the 2 channels are identical and therefore analyzes only channel 1 (audio_in(:,1)), which will be then used to create the final 2-channel audio file ([audio_out(:,1) audio_out(:,1)]) with silence removed.

2) Check if you have the following toolboxes: System Identification toolbox, DSP System toolbox and Statistics and Machine Learning Toolbox. The code won't work without these toolboxes, because you will need them to call the following functions: "ar", "DSP.ZeroCrossingDetector" and "mvnpdf". All the other matlab fucntions that I am using should belong to toolboxes that more commonly used that the above mentioned ones. 

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

10) "Remove Silence": The code will be executed. 

11) Please keep in mind the following during the execution of the code. During the training phase, the following message will appear: "Training the algorithm". The training part could take some time, depending on how much data will be used. The user should not close this window, as the program will automatically close it when training is complete. When training is complete, the message "Training the algorithm" will be replaced with the following message: "Applying the algorithm to the waveforms stored in the selected folder, removing silence and saving the new wave files','Applying the algorithm". When all the files have been analyzed, the message "Training the algorithm" will be replaced with the following message: "Applying the algorithm to the waveforms stored in the selected folder, removing silence and saving the new wave files','Applying the algorithm" will be replaced with the following message: "End of the analysis".

12) The new waveforms with shortened silence segments will be saved in the same folder selected in "Upload directory". The name of the new waveforms will be the "orginal_name_Shortened_Waveform.wav". For instance, if the original name was "Speech_1", the waveform with shortened silence segments will be saved with the name "Speech_1_Shortened_Waveform.wav"

13) Very important: I tried to handle all the exceptions that could occur. If an exception kicks in, a message informing the user of the exception will appear and the program will be aborted. If you experience an exception that is not handled by the code, please let me know and I will add it. Thank you!!!

These Matlab files are part of a large Toolbox that I wrote and that I am using to analyze EEG and MEG data.

If you have any question and/or want to report bugs, please e-mail me (Ale) at: pressalex@hotmail.com
