# geonet-volcano-timelapse

Play GeoNet volcano webcam stills as a browser timelapse from the public S3
open data bucket (`s3://geonet-open-data`, `ap-southeast-2`). No build step,
no credentials, and no ffmpeg required for preview playback.

[![CI - Validate and Test](https://github.com/jajera/geonet-volcano-timelapse/actions/workflows/ci.yml/badge.svg)](https://github.com/jajera/geonet-volcano-timelapse/actions/workflows/ci.yml)
[![Deploy to GitHub Pages](https://github.com/jajera/geonet-volcano-timelapse/actions/workflows/pages.yml/badge.svg)](https://github.com/jajera/geonet-volcano-timelapse/actions/workflows/pages.yml)
[![Markdown Lint](https://github.com/jajera/geonet-volcano-timelapse/actions/workflows/markdown-lint.yml/badge.svg)](https://github.com/jajera/geonet-volcano-timelapse/actions/workflows/markdown-lint.yml)
[![Commit Message Conformance](https://github.com/jajera/geonet-volcano-timelapse/actions/workflows/commitmsg-conform.yml/badge.svg)](https://github.com/jajera/geonet-volcano-timelapse/actions/workflows/commitmsg-conform.yml)

**Live app**: <https://jajera.github.io/geonet-volcano-timelapse/>

## Overview

GeoNet publishes volcano camera JPEG stills roughly every ten minutes under
`camera/volcano/images/{year}/{station}/{camera}/{year}.{doy}/`. The bucket is
part of the [AWS Open Data Sponsorship Program](https://registry.opendata.aws/geonet/),
so it is world-readable and returns permissive CORS headers. This page lists a
day of frames with the S3 `ListObjectsV2` API, then plays them as a canvas
timelapse in the browser.

## Features

- Pick **year / station / camera / day** and load frames from S3
- Canvas playback with scrubber, step controls, and fps selector
- Copyable `aws s3 sync ... --no-sign-request` for offline download
- **Load local folder** to play a synced JPEG directory without the network
- Dark / light theme (system default, remembered)

## Usage

Open the live app, choose a day, and click **Load from S3**. For offline use:

```bash
aws s3 sync \
  s3://geonet-open-data/camera/volcano/images/<year>/<station>/<cam>/<day>/ \
  ./<day> \
  --no-sign-request
```

Then use **Load local folder** and select that directory. Please download only
the day you need.

## Local development

```bash
python3 -m http.server -d docs 8155
# open http://127.0.0.1:8155/
```

## Deployment

Pushes to `main` run the CI workflow; on success, the reusable
`actionsforge/actions/.github/workflows/github-pages-deploy.yml` publishes the
`docs/` directory to GitHub Pages.

## Data source and attribution

GeoNet data are made available free of charge under the
[CC BY 3.0 NZ licence](https://creativecommons.org/licenses/by/3.0/nz/). Please
acknowledge the GeoNet programme and its sponsors when using the data — see the
[GeoNet Data Policy](https://www.geonet.org.nz/policy). This project is an
independent viewer and is not affiliated with GeoNet.

## License

[MIT](LICENSE) © John Ajera
