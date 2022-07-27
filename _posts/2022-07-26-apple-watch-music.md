---
layout: article
title: Apple Watch Play Music Offline without Premium
key: 20220726
tags: Apple AppleWatch Spotify
pageview: false
modify_date: 2022-07-26
aside:
  toc: true
---

<!--more-->

For Spotify or Apple Music users, there are 2 ways to play music on the Apple Watch standalone, either by downloading it offline in advance or by streaming it on a cellular network. In this post I'll skip the second option since my Apple Watch SE only supports GPS.

For those with a premium membership, both Apple Music and Spotify allow you to download music to Apple Watch in a straightforward manner. However, poor people like me tend to avoid paying for it at all costs. So, here is the cost:


## Step 1: Download music tracks from Spotify playlist

(If you already have downloaded the music from whatever sources, skip this step. )


I use [spotDL](https://github.com/spotDL/spotify-downloader) to download Spotify playlists and songs for free(a few Terminal commands needed).

To install it,

``pip install spotdl``

Next, install FFmpeg to your local directory:

``spotdl --download-ffmpeg``

To download a playlist from Spotify, run

``spotdl download [playlistUrl]``

Hooray! Now we get the all the music in the playlist. Check their [documentation](https://spotdl.readthedocs.io/en/latest/usage/) for more usage.

## Step 2: Import your playlist to Music app on Mac

Follow the [official guide](https://support.apple.com/guide/music/import-items-already-on-your-computer-mus3081/mac#:~:text=In%20the%20Music%20app%20on,or%20folder%2C%20then%20click%20Open.
) to import the music, then create the a new playlist.

## Step 3: Sync music from Macbook to iPhone

[Connect your device to your computer with the USB cable](https://support.apple.com/HT210611) and select your device in the sidebar of Music App.

I prefer to only sync with the playlist I choose.
![John's iPhone](https://github.com/Yuleii/Yuleii.github.io/raw/master/pictures/20220727/John's%20iPhone.png)



## Step 4:  Sync music to your Apple Watch

> [How to sync music to your Apple Watch?](https://support.apple.com/en-us/HT204691)
> 1. Set your Apple Watch on its charger. Make sure that it's charging and that your iPhone is within range of your watch.  
> 2. On your iPhone, open the Settings app, then tap Bluetooth. Make sure that Bluetooth is turned on.  
> 3. On your iPhone, open the Apple Watch app, then tap the My Watch tab.  
Scroll to Music and tap it.   
> 4. Tap Add Music, then find the song or album that you want to sync.  
> 5. Tap the Add button  next to the music that you want to sync. If you can't add specific albums or playlists, try downloading them to your iPhone before you sync with your watch.


All done! Now click Apple Music app on your Apple Watch and enjoy the music offline!

## My devices
- MacBook Air M1( macOS Monterey 12.0.1)  
- iPhone 12 mini(iOS 15.4.1)  
- Apple Watch SE(watchOS 8.6)

## References
- [spotDLdocumentation](https://spotdl.readthedocs.io/en/latest/)  
- [Apple Music User Guide](https://support.apple.com/zh-cn/guide/music/mus3081/mac#:~:text=In%20the%20Music%20app%20on,are%20added%20to%20your%20library.)
- [macOS User Guide](https://support.apple.com/en-us/HT210611)
- [Apple Support: use the Finder to sync your iPhone, iPad, or iPod with your computer](https://support.apple.com/en-us/HT210611)
- [Apple Support: listen to music and podcasts on your Apple Watch](https://support.apple.com/en-us/HT204691)
- [Apple watch离线听歌教程——下载的歌曲导入到Apple watch中](https://www.bilibili.com/video/BV1CY4y1s77u/?vd_source=2acc4bc4498b37baa7af46c0fc52d55f)

