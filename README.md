# mokotakas-audio

MokoTakas generated durable audio origin.

- **Binary assets live in Releases**, never in this repository's git history.
  There is no application source and no secret here; the application lives in
  [lyudnikov/mokotakas](https://github.com/lyudnikov/mokotakas).
- **Assets are content-addressed.** Each approved audio revision is one asset
  named `revision-<sha256>.mp3`, where `<sha256>` is the SHA-256 of the exact
  MP3 bytes (`AudioRevision.content_hash`). It lives in the shard release
  `audio-revisions-v1-<first hex digit of the sha256>` — 16 releases,
  `audio-revisions-v1-0` … `audio-revisions-v1-f`.
- The public download URL is fully determined by the hash:
  `https://github.com/lyudnikov/mokotakas-audio/releases/download/audio-revisions-v1-<h>/revision-<sha256>.mp3`
  — reads need no token.
- **Append-only. Do not replace or delete an existing revision asset**, and
  never upload with `--clobber`: a name must always mean the same bytes. Every
  upload is verified by downloading the asset anonymously and re-hashing it.
- Uploads are made only by the developer tooling in the application
  repository (`scripts/audio-storage.ts`, decision D-180); CI only reads.
