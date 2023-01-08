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

### example on the "crashtest" playlist
```bash
╭────┬─────────────┬──────────────────────────────╮
│  # │     id      │             url              │
├────┼─────────────┼──────────────────────────────┤
│  0 │ Wj2khaMPtp8 │ https://youtu.be/Wj2khaMPtp8 │
│  1 │ r61Hp_bBomQ │ https://youtu.be/r61Hp_bBomQ │
│  2 │ sT__MEXDIQ0 │ https://youtu.be/sT__MEXDIQ0 │
│  3 │ 2mFL44FDUWY │ https://youtu.be/2mFL44FDUWY │
│  4 │ NVSABMeQj9A │ https://youtu.be/NVSABMeQj9A │
│  5 │ b05EtiHNBuM │ https://youtu.be/b05EtiHNBuM │
│  6 │ C-xzTjfxnyQ │ https://youtu.be/C-xzTjfxnyQ │
│  7 │ ZTMkVX9l5Nw │ https://youtu.be/ZTMkVX9l5Nw │
│  8 │ ZmfF6dy3r5c │ https://youtu.be/ZmfF6dy3r5c │
│  9 │ 46HOf_sFlks │ https://youtu.be/46HOf_sFlks │
│ 10 │ SawKvHpulQo │ https://youtu.be/SawKvHpulQo │
│ 11 │ h91Dwr-6QVQ │ https://youtu.be/h91Dwr-6QVQ │
╰────┴─────────────┴──────────────────────────────╯
```
