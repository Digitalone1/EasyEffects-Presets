# PulseEffects/EasyEffects Loudness Equalizer Preset

This is my preset for [EasyEffects](https://github.com/wwmm/easyeffects). Two alternate versions are also provided for [Legacy PulseEffects](https://github.com/wwmm/easyeffects/tree/pulseaudio-legacy) and [Carla-Rack Jack Host](https://kx.studio/Applications:Carla).

It's a **Loudness Equalizer** which performs automatic volume adjustment without the Auto Gain plugin. Useful if you're looking for a steady sound level in high dynamic contents like movies when you don't want to adjust volume too many times. It's similar to the **Loudness Equalization** option in Microsoft Windows.

## How to install

This repository provides three files:

- ***LoudnessEqualizer.json*** for EasyEffects on Pipewire.

  Recommended on **6.1.0** or higher versions. Copy it inside `~/.config/easyeffects/output` folder, close and restart EasyEffects, then apply the new preset.

- ***LoudnessEqualizerPE.json*** for PulseEffects 5 on PipeWire or legacy PulseEffects on plain PulseAudio.

  This uses the old Multiband Compressor and Limiter from Calf, removed by newer versions. Recommended on **4.8.0** or higher versions. To apply, copy it inside `~/.config/PulseEffects/output` (if you have the [FlatPak version](https://flathub.org/apps/details/com.github.wwmm.pulseeffects), place the preset file in `~/.var/app/com.github.wwmm.pulseeffects/config/PulseEffects/output` folder).

- ***LoudnessEqualizer.carxp*** for Carla-Rack Jack Host.

  This is equal to the first preset, except that the Gate used is the one by LSP rather than Calf. Launch **carla-rack** and open the file, then connect your favorite nodes and sinks/sources in Patchbay tab. To use it with Pipewire and make a persistent configuration at system startup, follow this [guide](https://wiki.archlinux.org/title/PipeWire#LADSPA,_LV2_and_VST_plugins).

## How it works

An **Upward Compressor** is used to raise low level signals, then a downward **Multiband Compressor** is added to decrease the amplitude of the signal splitted in four different bands. At last, a **Limiter** makes sure no clipping occurs, taking the overall signal below 0 dB.

Since the upward compressor raises noise also, a **Gate** is used on top of everything to reduce this side effect. Multiband compressor will reduce sound quality, so the **Perfect Equalizer** (by [Ziyad Nazem](https://www.ziyadnazem.com/post/956431457/the-perfect-eq-settings-unmasking-the-eq)) is introduced to improve it before the limiter.

## Why not a single compressor?

I used downward compressors many times and noticed that higher the rate, lower the quality. So if you want to preserve some quality, you need to set a low rate, but low rates do not reduce the dynamic range sufficiently as needed in certain situations.

Therefore an upward compressor is used to raise signals below a certain threshold, then a multiband compressor is set with a low rate.

Obviously, the quality is not the same as original, but it's better than a compressor with high rate. Take in consideration that this is intended to be used only to get a quite steady level in high dynamic contents.
