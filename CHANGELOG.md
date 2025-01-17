# Changelog

## 1.2.2 / 1.2.3 (2021-11-26)
- typos and small fixes

## 1.2.1 (2021-11-15)
- removed `FrequencySpectrum::to_log_spectrum` (was useless; my understanding was wrong)
- added example `live-visualization` that shows how you could visualize a spectrum in real-time \
  ![Example visualization of real-time audio + spectrum analysis](res/live_demo_spectrum_green_day_holiday.gif "Example visualization of real-time audio + spectrum analysis") 
- removed example `live-spectrum-visualization` (was really bad)

## 1.2.0 (2021-11-10)
- MSRV is now 1.56.1
- Rust edition 2021

## 1.1.2 (2021-09-14)
- example `live-spectrum-visualization` requires Rust stable `1.55.0` because 
  the `ringbuffer`-dependency requires it
- the rest of the crate should still build with the current MSRV `1.52.1`
- if you run tests, you need `1.55.0`!

## 1.1.1
- bugfix of a bug since v1.0.0

## 1.1.0
- added `scaling::combined` which helps you to combine several scaling functions 
- added `FrequencySpectrum::to_log_spectrum` which gives you a more usable spectrum
  when you analyze music for example.
  - this is not optimal yet :(
  - Needs code contributions.. doesn't look as nice and convenient as other implementations. 
    I don't really know what to do here.

## v1.0.0
### Breaking Changes
- The library returns now a result and will no longer panic
  under certain circumstances.
- removed `per_element_scaling_fn` in favor of
  `complex_scaling_fn`, which is now just called
  `scaling_fn` - the old behaviour was more confusing than
  beneficial
- renamed `ComplexSpectrumScalingFunction` to `SpectrumScalingFunction` and
  moved it into the `scaling`-module
- MSRV is now `1.52.1` stable
### Other
- many internal improvements
- rust-toolchain.toml for build stability and reproducibility
- really minor performance improvements (~5 %)
- added example `live-spectrum-visualization.rs`
  (still not perfect, but works)
- added example `bench.rs`

## v0.5.1
- Feature "rustfft-complex" uses "rustfft"-crate at version 6 which is faster/more optimized (~25%).
- improved CI
- README update

## v0.5.0
This crate now uses `microfft::real` as default FFT implementation. It is by far the fastest implementation
and there are no disadvantages, despite (with `microfft` version 0.4.0) the maximum FFT size is 4096. If you 
need bigger FFT sizes, use feature `rustfft-complex`.

This crate now works in `no_std`-environments by default.

## v0.4.5
Added MIT to file headers where it was missing.

## v0.4.4
Fixed wrong usage of `microfft::real` + bumped version of `microfft` to `0.4.0`. 
**Currently it seems like with this implementation you only can get
the frequencies zero to `sampling_rate/4`, i.e. half of Nyquist frequency!**
I found out so by plotting the values. Wait until
https://gitlab.com/ra_kete/microfft-rs/-/issues/9 gets resolved.

## v0.4.3
README fix.

## v0.4.2
Typo in README.md code example.

## v0.4.1
Typo in README.md.

## v0.4.0
- MSRV is now Rust 1.51 (sorry but that's the only way I can make it `no_std`-compatible)
- This crate is now really `no_std`
- you can choose between three FFT implementations at compile time via Cargo features.
  The new default feature is `rustfft-complex` (which is still `std`) but there are also 
  the two new `no_std`-compatible targets `microfft-complex` (more accurate, like rustfft)
  and `microfft-real` (faster, less accurate)
- several small improvements and fixes, see: https://github.com/phip1611/spectrum-analyzer/milestone/3?closed=1

## v0.3.0
- `FrequencySpectrum::min()` and `FrequencySpectrum::max()`
   now return tuples/pairs (issue #6)
- `FrequencySpectrum` now has convenient methods to get
   the value of a desired frequency from the underlying vector
   of FFT results (issue #8)
- `FrequencySpectrum` now has a field + getter for `frequency_resolution`
  (issue #5)

For all issues see: https://github.com/phip1611/spectrum-analyzer/milestone/2
