# youtube-music
A collection of music ids from youtube.

This repo contains some lists of video ids from my music playlists on Youtube.

All the playlists are stored in [`playlists/`](playlists) and a playlist is
a file with the `.pg` extension with the following format:
```txt
youtube <id-1>
youtube <id-2>
...
```

## open the videos in Youtube
one can use the following `nushell` script to
- extract the ids of each video
- contruct the URL to open the videos

```bash
let playlist = "..."

open $"playlists/($playlist).pg"
| lines
| parse "youtube {id}"
| upsert url {|it|
  $"https://youtu.be/($it.id)"
}
```

The URLs can then be clicked on, passed to a web browser or given to `mpv`.
