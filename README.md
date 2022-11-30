# av_transcribe

`av_transcribe.py` uses [whisper][] to transcribe all of the media (audio and video files) in a directory, creating subtitle tracks automatically for each.

It's designed to create searchable text for large av projects and work well with editors like DaVinci Resolve.

`av_transcribe.py` has one required argument, the path to the directory you want to transcribe all the media in. You can additionally pass through any arguments you want to [whisper][] (eg, `--model` or `--language` -- see their docs for details).

Given the following folder hierarchy:

```sh
❯ find .
.
./video
./video/mp4
./video/mp4/1998-Purdue-Pharma-marketing-video-LaxlJXpwkzs.mp4
./audio
./audio/mp3
./audio/mp3/1998-Purdue-Pharma-marketing-video-LaxlJXpwkzs.mp3
```

Running `av_transcribe.py` will create the following additional files:

```sh
av_transcribe.py .

❯ find .
.
./video
./video/mp4
./video/mp4/1998-Purdue-Pharma-marketing-video-LaxlJXpwkzs.mp4
./video/mp4/1998-Purdue-Pharma-marketing-video-LaxlJXpwkzs.mp4.srt
./video/mp4/1998-Purdue-Pharma-marketing-video-LaxlJXpwkzs.mp4.vtt
./video/mp4/1998-Purdue-Pharma-marketing-video-LaxlJXpwkzs.mp4.txt
./audio
./audio/mp3
./audio/mp3/1998-Purdue-Pharma-marketing-video-LaxlJXpwkzs.mp3
./audio/mp3/1998-Purdue-Pharma-marketing-video-LaxlJXpwkzs.mp3.srt
./audio/mp3/1998-Purdue-Pharma-marketing-video-LaxlJXpwkzs.mp3.vtt
./audio/mp3/1998-Purdue-Pharma-marketing-video-LaxlJXpwkzs.mp3.txt
```

You can then import an srt into DaVinci Resolve and drag into a timeline with your video clip:

<img width="1444" alt="image" src="https://user-images.githubusercontent.com/5924/204854636-82d9724e-b448-46a3-afa0-0eb6209a6169.png">

You can also use a command line tool like [ripgrep][] to search your entire corpus of media:

```sh
video/mp4/1998-Purdue-Pharma-marketing-video-LaxlJXpwkzs.mp4.srt
3:Once you've found the right doctor and have told him or her about your pain, don't be afraid to take what they give you.
4-
5-2
6-00:00:07,800 --> 00:00:10,900
7-Often it will be an opioid medication.
8-
```

[whisper]: https://github.com/openai/whisper
[ripgrep]: https://github.com/BurntSushi/ripgrep
