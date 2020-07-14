# PulseEffects Normalizer Preset

This is my preset for [PulseEffects](https://github.com/wwmm/pulseeffects) on Linux.

A volume **Normalizer** without Auto-Gain plugin. Useful if you're looking for a steady sound level in high dynamic contents like movies when you don't want to adjust volume too many times. It's similar to **Loudness Equalization** in Windows.

## How to install ##

Download *NORMALIZER.json* and/or *NORMALIZER + EQUALIZER.json* files and copy them inside `~/.config/PulseEffects/output` folder. Close and restart PulseEffects, then apply the new preset. 

## How it works

An **Upward Compressor** is used to raise low level signals, then a downward **Multiband Compressor** is added to decrease the amplitude of the signal splitted in four different bands. At last, a **Limiter** makes sure no clipping occurs, taking the overall signal below 0 db. 

Since the upward compressor raises noise also, a **Gate** is used on top of everything to reduce this side effect. Multiband compressor will reduce sound quality, so a **Bass Enhancer** and an **Exciter** are introduced to add some armonics and improve low and high frequencies.

As an alternative, a version with **Perfect Equalizer** (by [Ziyad Nazem](https://www.ziyadnazem.com/post/956431457/the-perfect-eq-settings-unmasking-the-eq)) after the multiband compressor is provided.

There is also a **Strong** variant for both versions with higher compression ratio, recommended only for *low volume* hardware.

## Why not a single compressor?

I used downward compressors many times and noticed that higher the rate, lower the quality. So if you want to preserve some quality, you need to set a low rate, but low rates do not reduce the dynamic range sufficiently as needed in certain situations.

Therefore an upward compressor is used to raise signals below a certain threshold, then a multiband compressor is set with a low rate.

Obviously, the quality is not the same as original, but it's better than a compressor with high rate. Take in consideration that this is intended to be used only to get a quite steady level in high dynamic contents.
