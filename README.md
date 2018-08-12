# VitaGrafix
VitaGrafix is a taiHEN plugin that allows you to change resolution and FPS cap of PS Vita games (to get better visuals, higher FPS or longer battery life).

Heavily inspired by [vitaRescale](https://github.com/Rinnegatamante/vitaRescale) from Rinnegatamante, with added features and more supported games.

## Installation
1. Download latest [VitaGrafix.suprx](https://github.com/Electry/VitaGrafix/releases) and kuio.skprx ([kuio.zip](https://github.com/Rinnegatamante/kuio/releases))
2. If 'ux0:tai/config.txt' does exist
    1. Copy 'VitaGrafix.suprx' and 'kuio.skprx' to 'ux0:tai/' directory
    2. Open 'ux0:tai/config.txt' in a text editor
    3. Add following lines to the bottom
```
*KERNEL
ux0:tai/kuio.skprx
*ALL
ux0:tai/VitaGrafix.suprx
```
3. Otherwise
    1. Copy 'VitaGrafix.suprx' and 'kuio.skprx' to 'ur0:tai/' directory
    2. Open 'ur0:tai/config.txt' in a text editor
    3. Add following lines to the bottom
```
*KERNEL
ur0:tai/kuio.skprx
*ALL
ur0:tai/VitaGrafix.suprx
```
4. If you wish to configure the plugin
    1. Create 'ux0:data/VitaGrafix' folder
    2. Create and open 'ux0:data/VitaGrafix/config.txt' file
    3. Refer to the configuration section below
    
NOTE: If you already have kuio.skprx installed (used by other plugin), you don't need to download it again.

## Configuration
You can configure every game separately using unified configuration file.

### [MAIN] section
- This section applies to all games and overrides their individual options.
```
[MAIN]
ENABLED=1      <- Setting this to 0 disables all game modifications. (default = 1)
OSD=1          <- Setting this to 0 disables in game OSD (during few seconds at the beginning). (default = 1)
```

### GAME section
- This section applies to a single game.
```
[PCSB00245]    <- TITLE ID of your game
ENABLED=1      <- Setting this to 0 disables all game modifications. (default = 1)
OSD=1          <- Setting this to 0 disables in game OSD (during few seconds at the beginning). (default = 1)
FB=960x544     <- Framebuffer resolution. Setting this to OFF disables this feature. (default = depending on the game, not supported on all titles)
IB=960x544     <- Internal buffer resolution. Setting this to OFF disables this feature. (default = depending on the game, not supported on all titles)
FPS=60         <- FPS cap. Setting this to OFF disables this feature. (default = depending on the game, not supported on all titles)
```

### Example config.txt
```
[MAIN]
ENABLED=1

[PCSB00245]
OSD=0
IB=960x544

[PCSE00411]
IB=864x492

[PCSB00204]
IB=OFF
```
NOTE: If some options are left out, the plugin will use their default values (for each game).

## Supported games
| Game          | Title ID(s)   | Supported features | Game defaults | Plugin defaults | Notes |
| ------------- | ------------- | ------------------ | ------------- | --------------- | ----- |
| Killzone: Mercenary | PCSF00243 <br/> PCSF00403 <br/> PCSA00107 <br/> PCSC00045 <br/> PCSD00071 | Internal res. <br/> FPS cap | Dynamic <br/> 30 | OFF <br/> OFF | Input doesn't work when framerate is > 59. <br/> Particles are rendered separately. | 
| Persona 4 Golden | PCSB00245 <br/> PCSE00120 <br/> PCSG00563 <br/> PCSH00021 | Internal res. | 840x476 | 960x544 | |
| WRC 3: FIA World Rally Championship | PCSB00204 | Internal res. | 704x448 | 960x544 | |
| WRC 4: FIA World Rally Championship | PCSB00345 <br/> PCSE00411 | Internal res. | 704x448 | 960x544 | |


Adding support for each and every game requires manual disassembly of game's binary to find addresses in the game code where the resolution is set.