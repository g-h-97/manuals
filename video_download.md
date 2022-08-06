

Some websites fragment their video over hundreds of `.ts` files, this can be seen on the network traffic analyzer in the browser inspector as `xhr` traffic.

The most important file(s) in the stream is the `.m3u8` file(s) which contains all links to other `.ts` video files

By filtering for `.m3u8` you'll find one or more results, by coping their URLs to a new browser tab you can download there files.

# Solution

In order to download the entire video, copy one of the `.ts` files URL and past it in a new browser tab then remove the unique identifier of that file, since the `.ts` files are normally fragments of `.mp4` file they will keep the same root name plus a file number at the end like so:

If the original video file is named:

`video_name.mp4`

The fragments are going to look something like this:

`video_name_0001.ts`, `video_name_0002.ts` and so on `video_name_xxxx.ts`

In this case to download the video just copy the URL and strip `_xxxx.ts` with `.mp4`.

## Real life Example

I tried to download a video from the Sandvine website, however `youtube-dl` complained that the link is not supported. I looked in the network traffic, and after a bit research I found that I can use the Solution above.

I filtered for `.ts` in the search of the browser's inspector, then copied the first file on the list which is `_h_00000.ts`. The `h` in this case means the `high definition` stream the is also `l` for `low definition` and `n` for `normal definition`

`https://cdn5.dcbstatic.com/files/s/a/sandvine_docebosaas_com/1620306000/ciKobVBFX7tfTorpgbWKIw/video/db3c4f3395f966ecfe5c6d127377b984238ff8bf/db3c4f3395f966ecfe5c6d127377b984238ff8bf_h_00000.ts`

After removing the `.ts` identification part, the URL worked as expected showing the `HD` variant of the video which was perfectly supported by `youtube-dl`

`https://cdn5.dcbstatic.com/files/s/a/sandvine_docebosaas_com/1620306000/ciKobVBFX7tfTorpgbWKIw/video/db3c4f3395f966ecfe5c6d127377b984238ff8bf/db3c4f3395f966ecfe5c6d127377b984238ff8bf.mp4`

It's worth noting that in this case there were three separate `.m3u8` files, one for each video quality `h - n - l`. The links on each one were suffixed with different ID of `.ts` files

The first part of the `HD` file `db3c4f3395f966ecfe5c6d127377b984238ff8bf_h_.m3u8`:

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:0
#EXT-X-ALLOW-CACHE:YES
#EXT-X-TARGETDURATION:8
#EXTINF:7.280000,
db3c4f3395f966ecfe5c6d127377b984238ff8bf_h_00000.ts
#EXTINF:3.600000,
db3c4f3395f966ecfe5c6d127377b984238ff8bf_h_00001.ts
#EXTINF:7.200000,
db3c4f3395f966ecfe5c6d127377b984238ff8bf_h_00002.ts
#EXTINF:3.600000,
db3c4f3395f966ecfe5c6d127377b984238ff8bf_h_00003.ts
```


The first part of the `ND` file `db3c4f3395f966ecfe5c6d127377b984238ff8bf_n_.m3u8`:

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:0
#EXT-X-ALLOW-CACHE:YES
#EXT-X-TARGETDURATION:8
#EXTINF:7.280000,
db3c4f3395f966ecfe5c6d127377b984238ff8bf_n_00000.ts
#EXTINF:3.600000,
db3c4f3395f966ecfe5c6d127377b984238ff8bf_n_00001.ts
#EXTINF:7.200000,
db3c4f3395f966ecfe5c6d127377b984238ff8bf_n_00002.ts
#EXTINF:3.600000,
db3c4f3395f966ecfe5c6d127377b984238ff8bf_n_00003.ts
```

The first part of the `LD` file `db3c4f3395f966ecfe5c6d127377b984238ff8bf_l_.m3u8`:

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:0
#EXT-X-ALLOW-CACHE:YES
#EXT-X-TARGETDURATION:8
#EXTINF:7.280000,
db3c4f3395f966ecfe5c6d127377b984238ff8bf_l_00000.ts
#EXTINF:3.600000,
db3c4f3395f966ecfe5c6d127377b984238ff8bf_l_00001.ts
#EXTINF:7.200000,
db3c4f3395f966ecfe5c6d127377b984238ff8bf_l_00002.ts
#EXTINF:3.600000,
db3c4f3395f966ecfe5c6d127377b984238ff8bf_l_00003.ts
```
