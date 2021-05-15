# AOK 5056 Weather Station

Conrad Renkforce AOK-5056  
Optex Electronique 99018 SM-018 5056  

Same base as Holman Industries WS5029 weather station (PCM) but with LUX and index UV values.  
I already created a aok_5056.c file here my result.


```
rtl_433 -f 868M -X "n=STATION,m=FSK_PCM,s=100,l=100,r=100000,preamble={48}aaaaaaaaaaaa,match={24}98f3a5" -F json
```
```
{"time" : "@0.033317s", "model" : "STATION", "count" : 1, "num_rows" : 1, "rows" : [{"len" : 170, "data" : "98f3a5c7670a93823202800c2382606608000000000"}], "codes" : ["{170}98f3a5c7670a93823202800c2382606608000000000"]}
{"time" : "@0.033317s", "model" : "AOK-5056", "id" : 51047, "temperature_C" : 16.900, "humidity" : 56, "rain_mm" : 562.000, "wind_avg_km_h" : 2, "wind_max_km_h" : 2, "wind_dir_deg" : 180, "uv" : 0, "light_lux" : 12430}
{"time" : "@0.063039s", "model" : "STATION", "count" : 1, "num_rows" : 1, "rows" : [{"len" : 170, "data" : "98f3a5c7670a93823202800c2382606608000000000"}], "codes" : ["{170}98f3a5c7670a93823202800c2382606608000000000"]}
{"time" : "@0.063039s", "model" : "AOK-5056", "id" : 51047, "temperature_C" : 16.900, "humidity" : 56, "rain_mm" : 562.000, "wind_avg_km_h" : 2, "wind_max_km_h" : 2, "wind_dir_deg" : 180, "uv" : 0, "light_lux" : 12430}
{"time" : "@0.092766s", "model" : "STATION", "count" : 1, "num_rows" : 1, "rows" : [{"len" : 168, "data" : "63ce971d9c2a4e08c80a00308e0981982000000000"}], "codes" : ["{168}63ce971d9c2a4e08c80a00308e0981982000000000"]}
```

but  ... the signal is sent 3 times exactly same values and crc algorithme is unknown.


