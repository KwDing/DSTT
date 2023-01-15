# DSTT

## Project Introduction

Tiktok is a famous short-form video platform. And there are various background music pieces for users to choose from for short-form video editing and creation. In this project, we create a top TikTok song dataset. We annotated beat and downbeat time stamps on these songs first, then used this dataset to evaluate two famous beat-tracking platforms: Madmom and Librosa. The results show that the average f-measure score of this dataset is 0.92 and 0.62 on Madmom and Librosa, respectively. We hope that this dataset will be helpful for the research work of the MIR community. The colab notebook could be accessed [here](https://colab.research.google.com/drive/1gZNCXWFaJWpxMn_TeDP5FNk69dHrWQ5S?usp=sharing).

## Dataset Introduction

This dataset contains 375 tracks, each one is 30-second long. The data structure of each track is as follows:

```
{
track_id: ‘0000’,
audio_path: ‘/content/drive/MyDrive/MIR_final/audio/0000.wav’,
rank: ‘1’,
song_name: ‘Love You So’,
segment: ‘1’
times...
labels...
downbeats...
}
```

We provide a [link](https://drive.google.com/uc?export=download&id=1U7J-dDlCob_s_KF5fu5nHbEXKIpCYVVg) to the annotation file, which you can download directly to your Google Drive via the script in the `.ipynb` file with `dataset.download_annotation()`. For copyright considerations, we will not provide the original audio files directly to the user. However, users can download and pre-process the data themselves through `dataset.download_audio()`. Since the downloaded audio is mp3, but most packages in python can’t read mp3 files directly, users need to install [ffmpeg](https://ffmpeg.org/) on their computers. (ffmpeg is installed by default in colab.)

## Division of work
- Yi Deng
  - Lead in identifying topics and developing project plans
  - Complete data annotation and proofreading of 180 audio tracks
  - Teach data annotation tools and record the accompanying instructional video
  - Create annotation standards, dataset issues Debug
Write Evaluation & Analysis Part
- Kaiwen Ding
  - Implement [code for audio and annotation preparation](https://colab.research.google.com/drive/1ZwTv-afRkI3SAazgRP-FkN2wEXGNmzzl)
  - Write Instructions for code 
  - Complete data annotation and proofreading of 90 audio tracks
  - Encapsulate code to enable dataset download, validation, and initialization: [DSTT]()
- Yi Shan
  - Assist in identifying topics and developing project plans
  - Complete data annotation and proofreading of 105 audio tracks
  - Assist with dataset processing scripts Debug
  - Organize project introduction and dataset introduction
  - Lead project management work

## User Guide

1. To use the dataset, we need to download DSTT notebook to the working directory. This can be done with python code as follows.
2. To import `.ipynb` we need to install and import `import_ipynb` package, and then `import DSTT`.
3. Create a Dataset object with `DSTT.Dataset(home)`, where home is the directory of dataset files.
4. Download the whole dataset with `dataset.download()`. \
To download annotations and audio files separately.
Annotations could be downloaded manually, or using `dataset.download_annotation()`. However, since we don't provide the audio files, you need to use `dataset.download_audio()`  **after the annotation files are in the right place**, so that it would process the audio to clips for you. \
The Audio processing methods need ffmpeg to convert mp3 to wav, otherwise it might raise error even if pydub package is installed.
5. Validate the data with `dataset.validate()`
6. When there's no missing files, initialize the dataset so that the tracks would be loaded in `dataset.track()` as a dictionary of Track object. The key is the track_id from '0000' to '0374', and the value is the Track object.
7. It is recommended to use `librosa.load` or `Track.audio()` to load the audio. The audio files are default to be 44100 Hz stereo. With these 2 methods we can easily load them as mono.