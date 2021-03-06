LSB Steganography on non-lossy digital audio formats
====================================================

Inspired by the TV-series: Mr. Robot.

Setup
-----

```bash
virtualenv env
source env/bin/activate
pip install ...TODO
```

Usage
-----

```bash
source env/bin/activate
python lsb_steg_audio.py ...
```

Run tests
---------
```bash
python -m doctest -v lsb_steg_audio.py # work in progress (2015-08)
```

Roadmap
=======

First release
-------------
* LSB distribution on samples, denote the end by xor & nand check digits pair, from the start of the steg'd samples
* From the unsteg'd end of the samples, also create a xor & nand check digits pair. Plausible deniability.
* contiguous distribution on samples, denote the end by xor/nand check digits
* unit test with audio sample

To clarify: xor checkdigits in the middle somewhere, nand at the end to double-confirm, thus hopefully inconspicuously validate the steg'd sample set.

Extras
------
* histogram comparison, i.e. before steg, after steg. (KISS, don't)
* payload compression (nah, KISS)

Experimental
------------
* load frames to GPGPU, collate results, then write collated results to file


Research questions
------------------
* What is the LSB space for audio, for humans even, taking psycho-acoustics into account?! Translation: Store hidden message vertically (scalar), with a magic number upper and lower bound for the real amplitude, i.e. loudness(?).
* What is the optimal distribution of samples to evade aural/visual detection?
  * Evade visual detection: naively wiping the LSBs for all the samples is stupid.
  * What is the LSB bit-depth, sample distribution that will optimally take advantage of psycho-acoustics? Hide in the non-audible frequencies, this undermines visual invisibility? Just at the edge will do.
  * Instead of integrally populating all samples, how about hijacking a select number of inaudible samples completely for payload distribution?
  * So if we don't destroy LSB's, how do we denote the end of the payload? Apply check digits (xor, nand?), across the samples or per sample or both? 
* How does distribution affect post-compression format conversion? I assume bigger post-compression files.


WAV
---
* wav, skip initial 44 kbytes of metadata (microsoft format)
* Determine LSBW (least significant bit width, apparently WAV is little endian), before people start hearing it, although a histogram could easily reveal it...
* Will provide parameter to adjust LSBW, or even variable bit width, e.g. sinusoidal, harmonics, stochastic by hash?


TIFF
----
* WAV to TIFF conversion

FLAC
----
* WAV to FLAC conversion

Ogg-vorbis
----------
* 100% retention (TODO determine how), wav to ogg == ogg to wav
* invariant to psychoacoustic model?

MP3
---
* 100% retention (TODO determine how), idem
* invariant to psychoacoustic model?

Source:
* [paper #1](http://niels.xtdnet.nl/papers/practical.pdf)

