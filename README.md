# Speech Censor Bot :speak_no_evil:

![Intro](https://github.com/PrashantDandriyal/Speech-Censor-Bot/blob/master/DocsResources/logo.PNG)
## Introduction:
The need for content monitoring has been the prevailing need ever since the birth of the Internet.Extent of Internet censorship varies on a country-to-country basis depending on the propaganda and motto. Majority of the content we refer to, is audio video content. 57% Indians, who are also the biggest audience of [YouTube](https://economictimes.indiatimes.com/industry/media/entertainment/india-is-youtubes-largest-and-fastest-growing-audience-in-the-world-ceo/articleshow/68798915.cms), think content should be monitored for social welfare. On international grounds, in a [2012 Internet Society survey](https://en.wikipedia.org/wiki/Internet_censorship#Internet_Society's_Global_Internet_User_Survey), 71% of respondents agreed that "censorship should exist in some form on the Internet". Recently, the need for such moderation surged as mainstream channels were compelled to showcase political leaders delivering profane words during and post-campaign rallies. 

## Purpose: 
To use OpenVINO to deploy a speech censor bot at the edge for censoring unwanted words such as cuss words in video or audio speech.

## Usage
The current version includes a already set-up Google Collab notebook. This saves users from manually installing dependencies. Just open the main.ipynb using your Google account, and you are ready to go. The project has been tested on certain _WAV_ files that are provided in the [Sample WAV files](https://github.com/PrashantDandriyal/Speech-Censor-Bot/tree/master/Sample%20WAV%20files) directory. For using custom files instead, the _TODO_ section in the notebook can be edited. The result files: censored audio in case of speech censoring and censored video in case of video censoring are exported to the ```\content``` directory in the notebook workspace. 

### Dependencies
* OpenVINO toolkit : The Open Visual Inference and Neural Network Optimization toolkit provides improved inference on edge devices by creating intermediate model files (_.bin + .xml_). This toolkit is pulled and installed by [OpenDevLibrary](https://github.com/alihussainia/OpenDevLibrary), an Open Source installer for OpenVINO on Google collab.
* Sound Exchange [SoX](http://sox.sourceforge.net/): Cross-platform command line utility that is Python-independent, used for all the sound processing.
* [wave](https://docs.python.org/2/library/wave.html): Python module for interfacing multiple audio format files with Python.
* [ffmpeg](https://www.ffmpeg.org/): Cross-platform solution to process audio and video data, used for overwriting the original audio of video file (if using video censoring) with output censored audio.


## Understanding the process
### Section 1: FOR AUDIO AND VIDEO SPEECH
![Methodology](https://github.com/PrashantDandriyal/Speech-Censor-Bot/blob/master/CussWordBot.png)
* Setup OpenVINO environment (automatically handled by OpenDevLibrary)
* Generate configuration and executable files for inference. Run ```demo_speech_recognition.sh```. While using Google Collab, this file needs to be replaced or edited to comment out the online speech demo tests. This is done as Collab doesn't support the GUI-based applications and hence, may not proceed to the next cell. For custom audio, this files again needs to be edited or simply renaming our custom file to the audio mentioned in the shell file also works!
* Pre-process the audio file to suit the format accepted by OpenVINO.
* Make inference and export the generated speech text to a text file.
* Obtain syncmap in _json_ format using [Gentle](https://github.com/lowerquality/gentle)or any other forced aligner. **(Still needs to be configured)**
* Detect any inappropriate utterance using the [profanity_words_list](https://raw.githubusercontent.com/PrashantDandriyal/Google-profanity-words/master/list.txt) and censor the corresponding audio portion. 
_NOTE: Some words may be added to label them as inappropriate words._
### Section 2: ONLY FOR VIDEO SPEECH 
* Overwrite original audio of video with censored version.

## Results
[![Actual Clip](https://i.imgur.com/JnAamnUm.png)](https://youtu.be/FYM8NWKDqMU)
[![Actual Clip](https://i.imgur.com/LowQIgsm.png)](https://youtu.be/MlbJCKB1LNM)

The two thumbnails show the original and censored (output) files.
Note: The pre-trained model used here is observed to be trained on audiobook corpus and hence was not found accurate in detecting cuss utterances. Custom words have been appended to the _profanity_words_list_ for our test case.

## Future Work
* Train custom model specific to profane words.
* Use an automatic forced aligner 
* Add support for video input.

## References
* [SoX illustrations](https://explainshell.com/explain?cmd=sox+-r+48000+-b+16+-e+unsigned-integer+IMG_5367.raw+image.ogg+)
* [SoX to manipulate amplitude using shell](https://stackoverflow.com/questions/20127095/using-sox-to-change-the-volume-level-of-a-range-of-time-in-an-audio-file)
