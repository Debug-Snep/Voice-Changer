# MeowVoice Changer 1.8.1. (EXPERIMENTAL)
![image](https://github.com/user-attachments/assets/c9003d75-1b39-47ba-ab76-d7fbf1a154ea)
 ![Capture2](https://github.com/user-attachments/assets/cd7720c4-d49b-40e2-bf96-f9e116663d66)

## Version 1.8.1 scratch core:
- Removed SoundTouch Library
- Implemented own vocoder (this is still basic OLA and sound quality has some clipping on phase up) (next step is improved interpolation (cubic or syn) and then move on to SOLA and finally WOLA)
- Use Version 1.7.5 for best pitch quality while new core is being completed.
- Tempo setting currently disabled. Will be implemented soon now that library is out.
- Window frame sizes (used for OLA) is currently hard coded. This will also be open for change again soon.

## Version 1.7.5 fixes:
- Removed old code from settings helper
- Moved user input loop to own section
- Changed wavein and waveout into a Using system to ensure proper disposal (did not seem to need it but meh)
- Redid the UI to display text better
- Redid help file
- increased default window size

  
## Version 1.7.4 changes:
- Changed audio pipeline process
	- **OLD PIPE**: Pitch/Tempo > Ringmod > Effects > Echo/Reverb > EQ
	- **NEW PIPE**: EQ > Effects > Pitch/Tempo > Ringmod >  Echo/Reverb > 
- Added extra error handling code
- Removed duplicate code used for resetting and loading saved audio. 

## Version 1.7.3 fixes:
- Removed redundant buffer copies used during prototyping. Overall buffer usage should now be 1/5th of what it was.
- Moved dll files to dll folder for cleaner folder structure.

## Fixes V 1.7.2:
- Fixed an issue causing static value to not adjust with user input
- fixed an issue causing distortion value to not adjust with user input

## Features
- **Real-Time Voice Processing**: Modulate your voice live using a microphone and output to speakers or a virtual audio cable.
- **Customizable Effects**:
  - Pitch shifting (e.g., male to female, chipmunk effects)
  - Tempo adjustment (experimental, may cause clipping)
  - Wobble effect for dynamic pitch variation
  - Equalizer with customizable center frequency, gain, and bandwidth
  - Echo with adjustable delay and decay
  - Ring modulation and flanging for robotic and sci-fi effects
  - Radio effects including band-pass filtering, distortion, static noise, static bursts, compression, and hum
- **Settings Management**:
  - Save current settings to `Voice_Settings.xml`
  - Load settings from `Voice_Settings.xml` on startup
  - Reset to default settings using `Voice.bak` or hardcoded defaults
- **Console-Based Interface**: Adjust settings dynamically via simple commands
- **Customizable Audio Quality**: Adjust buffer sizes, sequence duration, and overlap for latency and quality control

## Installation
- Unzip and run "Meow Voice.exe"
 
### Prerequisites
- **Windows OS** (due to NAudio dependencies)
- **.NET Framework** (version 4.6.1 or later recommended)
- A microphone and output device (speakers or virtual audio cable like VB-Audio)

## Contributing
- Contributions are welcome! Please submit issues or pull requests to the GitHub repository. For feature requests or bug reports, include detailed information about your setup and the issue.
- [Support](https://github.com/Debug-Snep/Voice-Changer/discussions/1#discussion-8410747)
- [Future feature Plans](https://github.com/Debug-Snep/Voice-Changer/discussions/2#discussion-8410756)
- If you enjoy Meow Voice Changer and want to support its development, consider donating at paypal.me/ShiroSnep.

## License
-Meow Voice Changer is free to use and redistribute for non-commercial purposes. It uses the NAudio and SoundTouch for NAudio libraries, which have their own licensing terms. See their respective repositories for details.
-Copyright © 2025 DEBUG_SNEP (aka Shiro Sneaky Snep)

### Acknowledgments
-Inspired by the communication sounds of Battlestar Galactica.
-Built with NAudio and SoundTouch for NAudio.


# Usage
### Launch:
- Start the application and select input (microphone) and output (speakers/virtual cable) devices.

### Settings Loading:
- Loads Voice_Settings.xml on startup if present; otherwise, uses Voice or hardcoded defaults.

### Adjust Settings:
- Enter console commands to tweak effects (see Commands (#commands)).
- Example: p 4 for a female voice effect.

### Use save to store settings or reset to revert to defaults.

### Exit:
Type q to quit.

| Setting | Description | Default Value |
|---------|-------------|---------------|
| `Sample_Rate` | Audio sampling rate (Hz) | 44100 |
| `Buffer_Milliseconds` | Input buffer size (ms, affects latency/stability) | 100 |
| `Sequence_DurationMs` | Processing segment size (ms, affects quality/latency) | 100 |
| `Seek_Window_DurationMs` | Overlap search window (ms, improves pitch/tempo accuracy) | 15 |
| `Overlap_DurationMs` | Segment overlap (ms, ensures smooth transitions) | 8 |
| `Pitch_Semi_Tones` | Pitch shift in semitones (+ higher, - lower) | 0.0 |
| `Tempo` | Playback speed multiplier (e.g., 1.05 = 105%) | 1.0 |
| `Wobble_Depth` | Pitch wobble amplitude (semitones) | 0.0 |
| `Wobble_Frequency` | Pitch wobble frequency (Hz) | 0.0 |
| `currentTime` | Internal time tracking for wobble effect | 0.0 |
| `EQ_Center` | Equalizer center frequency (Hz) | 2000.0 |
| `EQ_Q` | Equalizer bandwidth (Q factor, 0.0–1.0) | 1.0 |
| `EQ_Gain` | Equalizer gain (dB) | 6.0 |
| `EQ_Enabled` | Enable/disable equalizer | false |
| `Echo_Delay` | Echo delay (seconds) | 0.0 |
| `Echo_Decay` | Echo decay strength (0.0–1.0) | 0.0 |
| `RingMod_Enabled` | Enable/disable ring modulation (robotic effect) | false |
| `Mod_Frequency` | Ring modulation frequency (Hz) | 200.0 |
| `Mod_Depth` | Ring modulation depth (0.0–1.0) | 0.5 |
| `Flange_Enabled` | Enable/disable flanging (sci-fi effect) | false |
| `Flange_Depth` | Flanging depth (0.0–1.0) | 0.3 |
| `Flange_Frequency` | Flanging frequency (Hz) | 0.5 |
| `BandPass_Enabled` | Enable/disable band-pass filter (radio effect) | false |
| `BandPass_Low` | Band-pass filter low frequency (Hz) | 300.0 |
| `BandPass_High` | Band-pass filter high frequency (Hz) | 3000.0 |
| `Distortion_Enabled` | Enable/disable distortion (gritty effect) | false |
| `Distortion_Gain` | Distortion gain multiplier | 2.0 |
| `Static_Enabled` | Enable/disable static noise (radio effect) | false |
| `Static_Level` | Static noise amplitude (0.0–1.0) | 0.005 |
| `Compression_Enabled` | Enable/disable compression (volume evening) | false |
| `Compression_Threshold` | Compression threshold (dB) | -20.0 |
| `Compression_Ratio` | Compression ratio (e.g., 4.0 = 4:1) | 4.0 |
| `Static_Burst_Enabled` | Enable/disable random static bursts | false |
| `Static_Burst_Probability` | Probability of static bursts (0.0–1.0) | 0.01 |
| `Static_Burst_Level` | Static burst amplitude (0.0–1.0) | 0.2 |
| `Hum_Enabled` | Enable/disable low-frequency hum (radio ambiance) | false |
| `Hum_Frequency` | Hum frequency (Hz) | 60.0 |
| `Hum_Level` | Hum amplitude (0.0–1.0) | 0.05 |

### Notes

- Latency: Smaller buffers (b) reduce latency but may glitch; larger buffers improve stability.

- Virtual Audio Cable: Use for streaming/recording (e.g., VB-Audio).

- Validation: Ensure settings are valid (e.g., Sample_Rate > 0).
