# JumpCutter

A Node.js package for processing videos and audio files by handling silent sections. You can either remove silent parts or speed them up.

## What is the Jump Cut Technique?

The jump cut is a film editing technique where a section of time is removed from a shot, creating a sudden transition. This effect is commonly used in vlogs, interviews, and fast-paced content to eliminate pauses, enhance engagement, and maintain viewer attention.

Jump cuts are widely used in video publishing platforms to make videos more dynamic and concise. For more information, you can check:

- [Jump Cut Explanation on Wikipedia](https://en.wikipedia.org/wiki/Jump_cut)

JumpCutter applies a skip-cutting technique to quiet sections in videos below a set audio dB threshold:

- Removing them (mode: 'remove')
- Speeding them up (mode: 'speed')

This makes it easier to create fast-paced, engaging videos without manual editing.

## Installation

```bash
npm install @ilhanozkan/jumpcutter
```

## Usage

### 1. Import and Initialize
First, import JumpCutter and create an instance with custom settings:

```javascript
const JumpCutter = require('@ilhanozkan/jumpcutter');

// Create a new instance
const cutter = new JumpCutter({
    silenceThreshold: -30, // dB threshold for silence detection
    minSilenceDuration: 0.5, // minimum silence duration in seconds
});
```

### 2. Process a Video File

#### Process video directly to a file
You can process a video file and save the result to a new file:

```javascript
// Process video directly to a file
await cutter.process({
    input: 'input.mp4',
    output: 'output.mp4',
    mode: 'remove' // or 'speed' to make silent parts faster
});
```

#### Process video to buffer
If you want to process the video without saving it to a file, you can get the result as a Buffer:

```javascript
// Process video to buffer (returns a Buffer)
const videoBuffer = await cutter.processToBuffer({
    input: 'input.mp4',
    mode: 'remove', // or 'speed' to make silent parts faster
    outputFormat: 'mp4' // optional, defaults to 'mp4'
});
```

## Options

- `silenceThreshold`: Threshold in dB for silence detection (default: -30)
- `minSilenceDuration`: Minimum duration of silence to process in seconds (default: 0.5)
- `mode`: 'remove' to delete silent parts, 'speed' to make them faster
- `speedFactor`: Speed multiplier for silent parts when using 'speed' mode (default: 2)

## Requirements

- Node.js 14 or higher
- FFmpeg (included via ffmpeg-static)

## MIT License

Copyright (c) 2025 Ilhan Ozkan

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
