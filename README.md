# ytm-ripper

Needs
- NodeJS
- yt-dlp
- FFMPEG
- ImageMagick

Do the honors
```
npm install
```

And use by simply
```
node . <youtube video link>
```

If the thing is an [art track](https://support.google.com/youtube/answer/6007071?hl=en) (auto generated music releases),
it would automatically populate the metadata.
If it's just a regular video, it would prompt you to fill in the blanks
```
Youtube video is not an art track.
Please populate the fields in temp/songmetadata.json before proceeding.
(You can also edit the album cover while this program waits)
Hit [Enter] to continue
```

You can then edit `songmetadata.json` manually.
