# PulseEffects/EasyEffects Loudness Equalizer Preset

These are my presets for [Easy Effects](https://github.com/wwmm/easyeffects). Two alternate versions are also provided for [Legacy PulseEffects](https://github.com/wwmm/easyeffects/tree/pulseaudio-legacy) and [Carla-Rack Jack Host](https://kx.studio/Applications:Carla).

It's a **Loudness Equalizer** which performs automatic volume adjustment without the Auto Gain effect. Useful if you're looking for a steady sound level in high dynamic contents like movies when you don't want to adjust volume too many times. It's similar to the **Loudness Equalization** option in Microsoft Windows.

## Announcement

From version **6.2.7**, Easy Effects has migrated the Gate from Calf to LSP version. A new preset is provided while the old one, suitable till version **6.2.6**, is available as ***LoudnessEqualizerOldGate.json***.

## How to download

Click on ***Code*** button and download the zip archive. Extract it on your system and pick the preset you need. You can also clone the git repository. Every other method you use, especially if you go in the preset page and right-click ***Save As***, might result in a corrupted and not working file.

## How to install

Choose the preset you want and copy it inside `~/.local/share/easyeffects/output` folder. If you have the the Flatpak version, place the preset file in `~/.var/app/com.github.wwmm.easyeffects/data/easyeffects/output`.

For older Easy Effects GTK/Libadwaita versions, copy it inside `~/.config/easyeffects/output` folder. If you have the the Flatpak version, place the preset file in `~/.var/app/com.github.wwmm.easyeffects/config/easyeffects/output`.

For older PulseEffects, copy it inside `~/.config/PulseEffects/output` folder. if you have the the Flatpak version, place the preset file in `~/.var/app/com.github.wwmm.pulseeffects/config/PulseEffects/output`.

Close and restart the service, then apply the new preset.

This repository provides 5 versions:

1. ***LoudnessEqualizer.json*** and ***LoudnessCrystalEqualizer.json*** for new Easy Effects versions using Qt framework. – Recommended for **8.0.0** or higher versions.

2. ***LoudnessEqualizer-GTK.json*** and ***LoudnessCrystalEqualizer-GTK.json*** for Easy Effects with new LSP Gate plugin. – Recommended from **7.0.0** to **7.2.5** versions.

3. ***LoudnessEqualizer-OldGate.json*** for Easy Effects versions on Pipewire using the old Gate plugin from Calf. – Recommended from **6.1.0** to **6.2.6** versions.

4. ***LoudnessEqualizer-PE.json*** for PulseEffects 5 on PipeWire or legacy PulseEffects on plain PulseAudio. – This uses the old Multiband Compressor and Limiter from Calf, removed by newer versions. Recommended on **4.8.0** or higher versions.

5. ***LoudnessEqualizer.carxp*** for Carla-Rack Jack Host. – Launch **carla-rack** and open the file, then connect your favorite nodes and sinks/sources in Patchbay tab. To use it with Pipewire and make a persistent configuration at system startup, follow this [guide](https://wiki.archlinux.org/title/PipeWire#Using_LADSPA,_LV2_and_VST_plugins).

## How it works

An **Upward Compressor** is used to raise low level signals, then a downward **Multiband Compressor** is added to decrease the amplitude of the signal splitted in four different bands. At last, a **Limiter** makes sure no clipping occurs, taking the overall signal below 0 dB.

Since the upward compressor raises noise also, a **Gate** is used on top of everything to reduce this side effect. Multiband Compressor will reduce sound quality, so the **Perfect Equalizer** (by [Ziyad Nazem](https://www.ziyadnazem.com/post/956431457/the-perfect-eq-settings-unmasking-the-eq)) is introduced to improve it before the limiter.

An additional version adds the **Crystalizer** after the Multiband Compressor to extend the dynamic range a little bit.

## Using headphones?

With headphones I recommend to add the **Crossfeed** effect at the last position, after the Limiter (no worries about clipping, the Crossfeed generally lowers the amplitude and does not output above 0 dB). I use the _Jmeier_ preset, but also _Default_ and _Cmoy_ ones can be chosen as you like.

## Why not a single Compressor?

I used downward compressors many times and noticed that higher the rate, lower the quality. So if you want to preserve some quality, you need to set a low rate, but low rates do not reduce the dynamic range sufficiently as needed in certain situations.

Therefore an upward compressor is used to raise signals below a certain threshold, then a multiband compressor is set with a low rate.

Obviously, the quality is not the same as original, but it's better than a compressor with high rate. Take in consideration that this is intended to be used only to get a quite steady level in high dynamic contents.
