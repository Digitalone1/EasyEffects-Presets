# PulseEffects/EasyEffects Loudness Equalizer Preset

This is my preset for [EasyEffects](https://github.com/wwmm/easyeffects). An alternate version is also provided for [Legacy PulseEffects](https://github.com/wwmm/easyeffects/tree/pulseaudio-legacy).

A **Loudness Equalizer** which performs automatic volume adjustment without the Auto Gain plugin. Useful if you're looking for a steady sound level in high dynamic contents like movies when you don't want to adjust volume too many times. It's similar to the **Loudness Equalization** option in Microsoft Windows.

## How to install ##

Download *LoudnessEqualizer.json* file and copy it inside `~/.config/easyeffects/output` folder. Close and restart EasyEffects, then apply the new preset. It is recommended to by used on **6.0.0** or higher versions.

For legacy PulseEffects, use *LoudnessEqualizerPE.json* and copy it inside `~/.config/PulseEffects/output`. This one is recommended to be used on **4.8.0** or higher versions.

If you have the [FlatPak version of PulseEffects](https://flathub.org/apps/details/com.github.wwmm.pulseeffects), place the preset file in `~/.var/app/com.github.wwmm.pulseeffects/config/PulseEffects/output` folder.

## How it works

An **Upward Compressor** is used to raise low level signals, then a downward **Multiband Compressor** is added to decrease the amplitude of the signal splitted in four different bands. At last, a **Limiter** makes sure no clipping occurs, taking the overall signal below 0 dB.

Since the upward compressor raises noise also, a **Gate** is used on top of everything to reduce this side effect. Multiband compressor will reduce sound quality, so the **Perfect Equalizer** (by [Ziyad Nazem](https://www.ziyadnazem.com/post/956431457/the-perfect-eq-settings-unmasking-the-eq)) is introduced to improve it before the limiter.

## Why not a single compressor?

I used downward compressors many times and noticed that higher the rate, lower the quality. So if you want to preserve some quality, you need to set a low rate, but low rates do not reduce the dynamic range sufficiently as needed in certain situations.

Therefore an upward compressor is used to raise signals below a certain threshold, then a multiband compressor is set with a low rate.

Obviously, the quality is not the same as original, but it's better than a compressor with high rate. Take in consideration that this is intended to be used only to get a quite steady level in high dynamic contents.
