# Audio Recording with PyAudio and Wave Modules

This Python code demonstrates how to record audio using the **PyAudio** module and save it as a `.wav` file using the **wave** module.

---

## Modules Used

### 1. PyAudio Module
- **`pyaudio`** is a Python library that provides bindings for the PortAudio audio library. It is used for capturing and playing back audio.
- You can install it using:
  ```bash
  pip install pyaudio

2. Wave Module
wave is a Python library used for reading and writing .wav sound files.
It is part of the Python Standard Library, so no additional installation is needed.

## Code Walkthrough
### 1. Importing Required Modules
import pyaudio
import wave

import pyaudio: This imports the PyAudio module for audio handling.
import wave: This imports the wave module for handling .wav file format.

### 2. Defining Audio Configuration

FRAMES_PER_BUFFER = 3200
FORMAT = pyaudio.paInt16
CHANNELS = 1
RATE = 16000

FRAMES_PER_BUFFER: This defines the number of frames per buffer (chunks of data) to be processed.
FORMAT: The format of the audio (e.g., pyaudio.paInt16 means 16-bit audio samples).
CHANNELS: The number of audio channels. 1 means mono, 2 would be stereo.
RATE: The sample rate of the audio, defined in Hz (here, 16000 samples per second).

## 3. Instantiating the PyAudio Object

`p = pyaudio.PyAudio()`

`pyaudio.PyAudio()` : This creates a PyAudio instance, which is the interface to the PortAudio system for handling input/output streams.

## 4. Opening the Stream

`stream = p.open(format=FORMAT,
                channels=CHANNELS,
                 rate=RATE,
                  input=True,
                   frames_per_buffer=FRAMES_PER_BUFFER)`
`p.open()` : Opens a new audio stream for recording.
`format=FORMAT`: Specifies the format of the audio stream (16-bit samples here).
`channels=CHANNELS`: Sets the number of audio channels (mono here).
`rate=RATE`: Defines the sample rate of the audio.
`input=True`: Specifies that this stream is for recording (audio input).
`frames_per_buffer=FRAMES_PER_BUFFER`: Specifies the number of frames per buffer. This breaks the audio into smaller chunks for processing.

## 5. Recording Audio


`print("start recording")`
`seconds = 5`
`frames = []`

`for i in range(0, int(RATE / FRAMES_PER_BUFFER * seconds)):
    data = stream.read(FRAMES_PER_BUFFER)
    frames.append(data)`

stream.read(FRAMES_PER_BUFFER): Reads audio data from the input device, based on the buffer size.
for i in range(...): Loops over the defined duration (in this case, 5 seconds) to record the audio in chunks.
frames.append(data): Appends each chunk (buffer) of recorded data to the frames list.

## 6. Stopping and Closing the Stream
stream.stop_stream()
stream.close()
p.terminate()
stream.stop_stream(): Stops the audio stream from further recording.
stream.close(): Closes the audio stream and frees system resources.
p.terminate(): Terminates the PyAudio instance, cleaning up any remaining resources.

## 7. Saving Audio as a .wav File

obj = wave.open("output.wav", "wb")
obj.setnchannels(CHANNELS)
obj.setsampwidth(p.get_sample_size(FORMAT))
obj.setframerate(RATE)
obj.writeframes(b"".join(frames))
obj.close()

wave.open("output.wav", "wb"): Opens a new .wav file for writing in binary mode ("wb").
setnchannels(CHANNELS): Sets the number of audio channels for the output file (1 channel = mono).
setsampwidth(p.get_sample_size(FORMAT)): Sets the sample width of the audio file. This function returns the number of bytes per sample (2 bytes for pyaudio.paInt16).
setframerate(RATE): Sets the sample rate of the output file (16000 Hz).
writeframes(b"".join(frames)): Writes the recorded audio frames to the .wav file. b"".join(frames) combines all recorded frames into a single bytes object.
obj.close(): Closes the .wav file after writing.

# Summary
This code:

Records 5 seconds of audio from the microphone using the PyAudio module.
Stores the recorded audio in chunks in the frames list.
Saves the recorded audio as a .wav file using the wave module.
Each function plays an important role in configuring, capturing, processing, and saving audio data.

vbnet
Copy code

This Markdown file is now ready to be saved with a `.md` extension and can be used for future reference!





