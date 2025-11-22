# ytm-ripper

## Setup
It needs these:
- NodeJS
- yt-dlp
- FFMPEG
- ImageMagick

Install 3 them using whatever
```sh
pacman -S nodejs yt-dlp ffmpeg imagemagick
# or apt or dnf or chocolatey or windows installer or anything.
# just make sure it's in $PATH or equivalent
```

And do the honors
```
npm install
```

**NOTE ABOUT YT-DLP**
Because of how often YouTube extraction breaks, the script expects the yt-dlp binary to be put in `/bin`. Should you want to change where it looks for yt-dlp, you can change `ytdlpCommand` in `index.js`.

## Usage
```sh
node . <youtube video/album link> <destination folder (optional)>
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

If you put in a playlist, it will detect if it's a proper album release. and put it in a special folder.

You can then edit `songmetadata.json` manually.

## How it works
It does these things in order:
- Grab the _best_ quality audio using yt-dlp.
- Grab video thumbnail and description, also using yt-dlp.
- Reencodes it to 256kbps MP3.
- Crops the thumbnail to square.
- Parses the description into an IDv3 MP3 metadata.
- Puts it all into the MP3.

YouTube's OPUS is a bit better than you think in terms of "kbps vs audible quality." Extracted properly, a 160kbps OPUS is equivalent to an MP3 of higher bitrate. 256kbps has been chosen as a sweet spot. You can edit the FFMPEG command in line `102` if you want something else.

As a byproduct of using yt-dlp, the script can grab more than YouTube art tracks. The manual entry fallback can be used to make neat MP3s off of any regular old YouTube videos or probably any video that yt-dlp supports.
