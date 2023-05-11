# av_transcribe

`av_transcribe.py` uses [whisper][] to transcribe all of the media (audio and video files) in a directory, creating subtitle tracks automatically for each.

It's designed to create searchable text for large av projects and work well with editors like DaVinci Resolve.

It's also great for transcribing your Apple / iOS Voice Memos.

- [Installation](#installation)
- [Usage](#usage)
- [Transcribe Voice Memos](#transcribe-voice-memos)
- [Import to Video Editing Software](#import-to-video-editing-software)
- [Screenshots](#screenshots)

## Installation

Clone this repo and add it to your path.

```sh
cd ~/src
git clone git@github.com:kortina/av_transcribe.git
# add this to your profile:
export PATH="$HOME/av_transcribe:$PATH"
```

Install [whisper][] (follow the instructions on their github readme).

## Usage

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

If a `.srt` file already exists for an av file, that file will be skipped. To re-transcribe a file, simply delete the `.srt` file.

By default, `av_transcribe.py` transcribes files with these extensions: `aac|braw|flac|mov|mp3|mp4|wav` -- but you can set it to match any video or audio files using the `--regex` flag, eg:

```sh
av_transcribe.py . --regex="\.(mov|mp3)$"
# will transcribe only mov and mp3 files
```

## Transcribe Voice Memos

In OSX Ventura, Voice Memos are stored in `~/Library/Application\ Support/com.apple.voicememos/Recordings/`. You can transcribe all of them with:

```sh
cd ~/Library/Application\ Support/com.apple.voicememos/Recordings/ && av_transcribe.py .
```

## Import to Video Editing Software

The main purpose of `av_transcribe.py` is transcription of media files for large av projects, so you'll probably want to import the subtitles to your editor. Here's how to do it with Resolve...

You can import a `.srt` into DaVinci Resolve and drag into a timeline with your video clip:

<img width="1444" alt="image" src="https://user-images.githubusercontent.com/5924/204854636-82d9724e-b448-46a3-afa0-0eb6209a6169.png">

You can also use a command line tool like [ripgrep][] to search your entire corpus of media.

Here's how to search all your `.mp4` files for "doctor."

```sh
rg -A 5 doctor -g "*.mp4.srt"

video/mp4/1998-Purdue-Pharma-marketing-video-LaxlJXpwkzs.mp4.srt
3:Once you've found the right doctor and have told him or her about your pain, don't be afraid to take what they give you.
4-
5-2
6-00:00:07,800 --> 00:00:10,900
7-Often it will be an opioid medication.
8-
```

## Screenshots

Here's an example of what it looks like running:

<img width="1802" alt="image" src="https://user-images.githubusercontent.com/5924/204869077-29baf283-246b-4ee4-8859-286d729bf043.png">

[whisper]: https://github.com/openai/whisper
[ripgrep]: https://github.com/BurntSushi/ripgrep
