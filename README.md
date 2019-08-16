### HOW-TO

1. Convert Audio File to Wav format using [Audacity](https://www.audacityteam.org/) (an open source audio editing tool). 

    The steps to convert:
    - Open file in Audacity
    - Click “File” menu
    - Click “Save other”
    - Click “Export as Wav”
    - Export it with default setting

    Another [online video/audio converter tool](https://www.media.io) 

2. Break up audio file into smaller parts

    Google Cloud Speech API only accepts files no longer than 60 seconds. To be on the safe side, I broke my files in 30-second chunks. To do that I used an open source command line library called `ffmpeg`.

    ```bash
    # Clean out old parts if needed via rm -rf parts/*
    ffmpeg -i source/large_audio.wav -f segment -segment_time 30 -c copy parts/out%09d.wav
    ```



### Existing Problems

1. Google cloud speech-to-text only support audio files that are less than 60 secs, so the large .wav file has to be splitted into a number of small .wav files.
In my case, each small .wav is with 30 secs. There should another way to transcribe the large audio file using Google speech-to-text API without splitting it into small pieces.
2. If there exists any small .wav files that only contain ambient noise (or without any human speech signals), then the file `fast.py` or `slow.py` will return errors. (A simple solution to this would be manually check each single .wav file and remove the invalid ones from the `parts` folder.)  

### References

Please visit [https://www.alexkras.com/transcribing-audio-file-to-text-with-google-cloud-speech-api-and-python/](https://www.alexkras.com/transcribing-audio-file-to-text-with-google-cloud-speech-api-and-python/) for detailed walk-through.
