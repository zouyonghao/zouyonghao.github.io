---
layout:post
title: Auto generate subtitle for video or audio
---

Recently, I'm listening to a tech podcast [shoptalkshow](http://shoptalkshow.com/)

But as my English so poor, I can't get it clearly. So I just wanted to get subtitle for the audio.

So

**first** 

get the mp3 file from the website source code.

**second**

```shell
sudo apt install ffmpeg
sudo pip install autosub
```

**third**

```shell
autosub somefile.mp3
```

It my takes about 20 minutes to recognize the speech.
Actually, it uses google translate api.


