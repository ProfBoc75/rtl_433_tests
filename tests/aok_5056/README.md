# AOK 5056 Weather Station

![Optex 990018](https://github.com/ProfBoc75/rtl_433_tests/raw/patch-1/tests/aok_5056/Optex_990018.jpeg)

[Conrad Renkforce AOK-5056](https://asset.conrad.com/media10/add/160267/c1/-/fr/001341307ML02/mode-demploi-1341307-station-meteo-radiopilotee-numerique-renkforce-aok-5056.pdf)  
Optex Electronique 990018 SM-018 5056

Same base as Holman Industries WS5029 weather station (PCM) but with LUX and index UV values.  


```
rtl_433 -f 868M -X "n=STATION,m=FSK_PCM,s=100,l=100,r=22000,preamble={48}aaaaaa98f3a5" -F json
```
```
{"time" : "2023-03-12 14:46:22", "model" : "STATION", "count" : 1, "num_rows" : 1, "rows" : [{"len" : 146, "data" : "c76709d2890802f00aed47dcb40d000000000"}], "codes" : ["{146}c76709d2890802f00aed47dcb40d000000000"]}
{"time" : "2023-03-12 14:46:22", "model" : "STATION", "count" : 1, "num_rows" : 1, "rows" : [{"len" : 146, "data" : "c76709d2890802f00aed47dcb40d000000000"}], "codes" : ["{146}c76709d2890802f00aed47dcb40d000000000"]}
{"time" : "2023-03-12 14:46:22", "model" : "STATION", "count" : 1, "num_rows" : 1, "rows" : [{"len" : 146, "data" : "c76709d2890802f00aed47dcb40d000000000"}], "codes" : ["{146}c76709d2890802f00aed47dcb40d000000000"]}
```

Payload format: With UV Lux sensor

    Fixed Values 0x  : AA AA AA AA AA AA 98 F3 A5

    Byte position    : 00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16 17 18
    Payload          : II II CC CH HR RR WW |         | NN SS 0D 00 00 00 00 0
                                +-----------+         +-------------+
                                |                                   |
                                |   07       08       09       10   |
                  bits details : DDDDUUUU ULLLLLLL LLLLLLLL LLBBNNNN

- I     station ID (randomised on each battery insertion)
- C     degrees C, signed, in multiples of 0.1 C
- H     humidity %
- R     cumulative rain in mm
- W     wind speed in km/h
- D     wind direction (0 = N, 4 = E, 8 = S, 12 = W)
- U     Index UV
- L     Lux
- B     Battery
- N     Payload number, increase at each message 000->FFF but not always, strange behavior. no clue
- S     XOR bytes checksum, lower nibble properly decoded, not the upper, unknown calcul.
- D     Previous Wind direction
- Fixed values to 9 zeros

[BitBench](https://triq.net/bitbench#c=aaaaaaaaaaaa98f3a5c7670982b9080280111e47ca7a0b000000000&c=aaaaaaaaaaaa98f3a5c7670972b90803d0f36747cb9109000000000&c=aaaaaaaaaaaa98f3a5c7670972b21007a1e6ce8f972212000000000&c=aaaaaaaaaaaa98f3a5c7670982b90901805ffa87cc3409000000000&c=aaaaaaaaaaaa98f3a5c76709d2b909024397c2c7ce760f000000000&c=aaaaaaaaaaaa98f3a5c76709d2b90902409c8947d74c0b000000000&f=ID%3A16h%20TEMP_C%3A12s%20HUM_%25%3A8d%20RAIN_MM%3A12d%20WIND_SPEED_KMH%3A8d%20WIND_DIRECTION%3A4h%20UV_INDEX%3A5d%20LUX%3A17h%20BAT%3A2h%20COUNTER%3A12h%20XOR%3A8h%204h%20PREV_DIR%3A4h%2036x&a=Preamble&m=aaaaaaaaaaaa98f3a5&cw=4)

Sample :

    ID:16h TEMP_C:12s HUM_%:8d RAIN_MM:12d WIND_SPEED_KMH:8d WIND_DIRECTION:4h UV_INDEX:5d LUX:17h BAT:2h COUNTER:12h XOR:8h 4h PREV_DIR:4h 36x
    
    aaaaaaaaaaaa98f3a5c76709d2b909024397c2c7ce760f000000000

    ID:c767 TEMP_C:  157 HUM_%:043 RAIN_MM:2313 WIND_SPEED_KMH:002 WIND_DIRECTION:4 UV_INDEX:07 LUX:05f0b BAT:0 COUNTER:7ce XOR:76 0 PREV_DIR:f

