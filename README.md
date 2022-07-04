# Sonivox EAS synth building guide
This guide will help you build a simple tool using one of the three Sonivox EAS synthesizers included in older android releases.
Note that 64-bit is currently unsupported, and the wavetable synth isn't supported either. However, someone else (@Raulonthetest) managed to build the wavetable synth sucessfully using gyunaev's [libsonivox](https://github.com/gyunaev/libsonivox). repo.

#FM synth
Throw the files from host_src and lib_src into your code project and use these compiler flags:
```
EAS_FM_SYNTH
_SAMPLE_RATE_22050
NUM_OUTPUT_CHANNELS=2
MAX_SYNTH_VOICES=64
_8_BIT_SAMPLES
_FILTER_ENABLED
_WAVE_PARSER
MAX_SMF_STREAMS=32
_REVERB_DISABLED
_CHORUS_DISABLED
UNIFIED_DEBUG_MESSAGES
IMELODY_PARSER
_RTTTL_PARSER
_OTA_PARSER
```

#Hybrid synth
Throw the files from host_src and lib_src into your code project and use these compiler flags:
```
EAS_HYBRID_SYNTH
NUM_PRIMARY_VOICES=32
NUM_SECONDARY_VOICES=32
_8_BIT_SAMPLES
_SAMPLE_RATE_22050
NUM_OUTPUT_CHANNELS=2
MAX_SYNTH_VOICES=64
_FILTER_ENABLED
_WAVE_PARSER
MAX_SMF_STREAMS=32
_REVERB_DISABLED
_CHORUS_DISABLED
UNIFIED_DEBUG_MESSAGES
IMELODY_PARSER
_RTTTL_PARSER
_OTA_PARSER
```

#Changing the sample rate
Look for “0x00105622,” in
eas_fmsndlib.c, hybrid_22khz_mcu.c or
wt_22khz.c, and replace it with these supported values:

```
8000 = 0x00101f40
16000 = 0x00103e80
20000 = 0x00104e20
22050 = 0x00105622
24000 = 0x00105dc0
32000 = 0x00107d00
44100 = 0x0010ac44
48000 = 0x0010bb80
```
Then change the _SAMPLE_RATE_XXXX compiler flag to the value of your desiring.