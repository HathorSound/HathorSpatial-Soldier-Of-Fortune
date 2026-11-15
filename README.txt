================================================================
 HathorSpatial
 Spatial audio and controller support for Soldier of Fortune

 Hathor Sound     https://hathorsound.net
================================================================

Soldier of Fortune (2000) has an Aureal A3D 3.0 sound path that describes
every 3D sound, the listener and the room to audio hardware that is no
longer made. HathorSpatial takes the place of that hardware. It renders
the game's A3D sound with Steam Audio: every 3D sound placed with HRTF,
occlusion, early reflections and reverb traced against the map's own
geometry, and the distances, gains and switches the game sets through
A3D. It also adds Xbox and PlayStation controller support, with rumble
from the game's own force feedback effects.


----------------------------------------------------------------
 REQUIREMENTS
----------------------------------------------------------------

- Soldier of Fortune 1.0.0.1 (GOG or retail), with the a3dsnd.dll and
  a3dapi.dll that come with it.
- Windows 10 or 11.
- phonon.dll: Steam Audio 4.8.1, the 32-bit (x86) build. If it is not
  in this package, take it from Steam Audio's releases at
  https://github.com/ValveSoftware/steam-audio. SoF.exe is a 32-bit
  program and does not load the 64-bit file.
- Headphones: 3D sounds are rendered binaurally.
- For a controller: a DualSense or DualSense Edge (USB or Bluetooth),
  or an Xbox controller (any XInput controller).


----------------------------------------------------------------
 INSTALL
----------------------------------------------------------------

1. Open the folder that holds SoF.exe. Rename the a3dapi.dll that is
   there (Aureal A3D, 466,944 bytes) to a3dapi.dll.aureal.

2. Copy these files into the folder:

       a3dapi.dll
       HathorSpatialLauncher.exe
       phonon.dll
       hathorspatial.cfg
       register-hathorspatial.cmd
       unregister-hathorspatial.cmd

3. Start HathorSpatialLauncher.exe. The Play page lists the set-up.
   Press Set up: it shows what it will do, registers the A3D class for
   the current user and copies a3dsnd.dll to a3dsnd_hs.dll. No
   administrator rights are needed.

4. Press Check setup. It confirms every row and plays a short test tone
   on the default playback device.

5. Press Play. The launcher saves hathorspatial.cfg and starts the game
   on HathorSpatial's sound module.

6. In game sound settings select A3D

Without the launcher: run register-hathorspatial.cmd, copy a3dsnd.dll
to a3dsnd_hs.dll in the game folder, and start the game once with

       SoF.exe +set snd_dll a3dsnd_hs.dll

The game keeps that setting for later starts. Start the game normally,
not as administrator.

When the game folder cannot be written (a game under Program Files),
map geometry is cached in %LOCALAPPDATA%\HathorSpatial.


----------------------------------------------------------------
 THE LAUNCHER
----------------------------------------------------------------

Play        The game folder, extra arguments for the game, the set-up
            rows, Set up, Check setup and Play.
Reverb      The reverb for all maps, with presets: Shipped, A little
            more, Big halls, Close walls, Tight.
              Reverb level        late tail and early reflections
                                  together, -18 to +9 dB
              Tail length         how long the late tail rings,
                                  0.50x to 3.00x
              Low end, High end   the low and high bands' ring time
                                  relative to the tail length
              Early reflections   the reflections off the walls around
                                  each sound, relative to the level
              Close to walls      how much the reverb and the early
                                  reflections rise near a wall: 100%
                                  as traced (about 3 dB a metre from a
                                  wall), 0% no rise
Acoustics   Occlusion, map geometry and world scale, the channel fix,
            your own sounds in the room, Doppler, and the game's own
            A3D settings: wall material, reflection level, and its
            occlusion and reflection switches.
Controller  Controllers on or off, the menus by stick and buttons, the
            button names in the controls menu, rumble and its
            strength, camera shake, footsteps and landings, weapon
            handling and far explosions, the DualSense's actuators and
            trigger vibration.
Sticks      Look speed, turn acceleration, dead zones, response curve
            and inversion for the right stick; dead zone and run tilt
            for the left.

Save writes hathorspatial.cfg in the game folder; Play saves first. A
setting left at its shipped value writes nothing. The game reads the
settings when it starts.


----------------------------------------------------------------
 SOUND
----------------------------------------------------------------

- 3D sounds reach the A3D channels. The game's sound module picks its
  channels so that 3D sounds seldom get one; HathorSpatial corrects
  the pick when the module loads, after checking the module's code.
- Every 3D sound is rendered with HRTF at its position, with the
  distance model, minimum and maximum distances, gain and pitch the
  game sets for it.
- Walls lower and muffle sounds behind them, traced from the map.
- Early reflections and reverb are traced from the map. Each map is
  read from the game's own files when it loads, converted once and
  cached in the HathorSpatial folder beside a3dapi.dll.
- Your own sounds stay in the game's stereo mix and get the room's
  reflections and reverb, timed to the sound you hear.
- In cutscenes the room is traced from the camera, as the game moves
  its listener there.
- What the game mixes itself, such as interface sounds, plays as a
  stereo bed at the game's volume.
- If Steam Audio cannot start, the game falls back to its own stereo
  sound.

The game's own settings still apply: its sound volume, its A3D
occlusion and reflection switches, and its geometric reverb switch.


----------------------------------------------------------------
 CONTROLLERS
----------------------------------------------------------------

While a DualSense or an XInput controller is connected, HathorSpatial
reads it in place of the game's joystick support. Turn Steam Input off
for the game.

Default layout (Xbox / PlayStation):

  Left stick          move; from 85% tilt you run
  Right stick         look, with turn acceleration held fully over
  RT / R2             fire                 LT / L2        alternate fire
  RB / R1             next weapon          LB / L1        previous weapon
  A / Cross           jump                 B / Circle     crouch (held)
  X / Square          reload               Y / Triangle   use
  D-pad up            use item             D-pad down     next item
  D-pad left          lean left (held)     D-pad right    lean right (held)
  LS / L3 (click)     run (held)           RS / R3 (click) previous item
  View / Create       mission objectives   Touchpad       score
  Menu / Options      Escape

- The buttons are keys of their own. Bind them in the game's controls
  menu like any other key, or in the console (bind PAD_Y "+use").
- The bindings are kept in controller.cfg beside the game's config.cfg.
  Delete it with the game closed to return to the default layout.
- In menus the left stick moves the cursor, the right stick scrolls,
  A or Cross clicks, B or Circle goes back and the D-pad sends the
  arrow keys.

Rumble plays the game's own force feedback effects: every weapon's
fire, being hit, explosions and landings, timed with their sound. The
view's shake rumbles too. Your footsteps and landings, weapon handling,
throws, the knife, jumps, pickups and distant explosions have effects
of their own, each with a strength slider on the Controller page.

A DualSense over USB plays the effects on its actuators; its audio
device must be enabled in Windows. Over Bluetooth it uses its rumble
motors. Its triggers vibrate with your weapon; they are never set to
resist.


----------------------------------------------------------------
 SETTINGS
----------------------------------------------------------------

hathorspatial.cfg, beside a3dapi.dll. One HS_KEY = VALUE per line. The
launcher writes it; every line is optional. Shipped values:

  HS_WET_MASTER = 1.0                  reverb level, 0.05 to 2.83
  HS_REVERB_SCALE_LOW = 1.0            tail length per band, 0.1 to 8.0
  HS_REVERB_SCALE_MID = 1.0
  HS_REVERB_SCALE_HIGH = 1.0
  HS_PERSRC_GAIN = 1.0                 early reflections, 0.1 to 8.0
  HS_NEAR_WALLS = 1.0                  rise near a wall, 0 to 1
  HS_ACOUSTICS = sa                    eax = no occlusion from geometry
  HS_SOF_GEOMETRY = 1                  0 = no map geometry
  HS_SOF_UNITS_TO_M = 0.0278           metres per game unit
  HS_SOF_PICKFIX = 1                   0 = the game's own channel pick
  HS_SOF_OWN = 1                       0 = no room for your own sounds
  HS_SOF_DOPPLER = 1                   0 = no Doppler
  HS_SOF_GAME_WALLS = 0                1 = the game's A3D wall material
  HS_SOF_GAME_REFLECTION_LEVEL = 0     1 = the game's reflection level
  HS_SOF_GAME_SWITCHES = 1             0 = ignore the game's switches
  HS_SOF_BACKGROUND_SOUND = 0          1 = sound behind other windows
  HS_SOF_PAD = 1                       0 = no controller support
  HS_SOF_PAD_MENU = 1                  0 = no menu control
  HS_SOF_PAD_NAMES =                   xbox or ps; blank = automatic
  HS_SOF_PAD_MOVE_DEADZONE = 0.15      0 to 0.6
  HS_SOF_PAD_RUN = 0.85                run tilt, 0.3 to 1
  HS_SOF_LOOK_YAW = 160                degrees per second, 10 to 1000
  HS_SOF_LOOK_PITCH = 120              degrees per second, 10 to 1000
  HS_SOF_LOOK_TURN =                   held fully over; blank = twice yaw
  HS_SOF_LOOK_RAMP = 0.4               seconds, 0 to 3
  HS_SOF_LOOK_DEADZONE = 0.15          0 to 0.6
  HS_SOF_LOOK_AXIAL = 0                0 to 0.6
  HS_SOF_LOOK_MAX_INPUT = 0.95         0.5 to 1
  HS_SOF_LOOK_CURVE = 2                1 = linear, 0.5 to 4
  HS_SOF_LOOK_INVERT = 0               1 = push up to look down
  HS_SOF_LOOK_CURSOR = 900             menu cursor speed, 50 to 5000
  HS_SOF_RUMBLE = 1                    0 = no rumble
  HS_SOF_RUMBLE_GAIN = 1               0 to 1
  HS_SOF_RUMBLE_SHAKE = 1              0 to 1
  HS_SOF_RUMBLE_FOOTSTEPS = 0.5        0 to 1
  HS_SOF_RUMBLE_EVENTS = 1             0 to 1
  HS_SOF_RUMBLE_WITH_SOUND = 1         0 = effects ahead of their sound
  HS_SOF_RUMBLE_SYNC = 0               ms, -100 to 100
  HS_SOF_RUMBLE_DEVICE =               ds5 or xinput; blank = automatic
  HS_SOF_RUMBLE_COILS = 1              0 = firmware rumble over USB too
  HS_SOF_TRIGGERS = 1                  0 = no trigger vibration
  HS_SOF_TRIGGER_GAIN = 1              0 to 2


----------------------------------------------------------------
 KNOWN LIMITATIONS
----------------------------------------------------------------

- Doors, lifts and other moving parts of a map are not part of the
  traced geometry.
- The reverb settings apply to every map.
- Sound is not routed around corners along baked paths.
- Controllers and rumble start with HathorSpatial's sound module.
- Rumble has no direction.
- Controller support and background sound are checked against
  SoF.exe 1.0.0.1 and stay off on any other version.


----------------------------------------------------------------
 TROUBLESHOOTING
----------------------------------------------------------------

No 3D sound, plain stereo
    Press Check setup in the launcher. The usual causes are a missing
    or 64-bit phonon.dll, the A3D class not registered (Set up), or the
    game not started on a3dsnd_hs.dll (Play).

The controller does nothing
    Turn Steam Input off for the game. Check that the game was started
    through Play, and that Controllers is on on the Controller page.

No rumble on a DualSense over USB
    Enable the controller's audio device in Windows Sound settings, or
    turn the actuators off on the Controller page to use its motors.

The first visit to a map takes a moment longer
    The map's geometry is converted once and cached.


----------------------------------------------------------------
 REMOVE
----------------------------------------------------------------

1. Start the game once with +set snd_dll "" or the module used before.
2. Run unregister-hathorspatial.cmd.
3. Delete a3dapi.dll, a3dsnd_hs.dll, HathorSpatialLauncher.exe,
   phonon.dll, hathorspatial.cfg, the two .cmd files, the
   HathorSpatial folder, and controller.cfg in base.
4. Rename a3dapi.dll.aureal back to a3dapi.dll.


----------------------------------------------------------------
 LICENCE
----------------------------------------------------------------

HathorSpatial is proprietary software of Hathor Sound, licensed under
the terms in LICENSE. Steam Audio (phonon.dll) is Valve's, under the
Apache License 2.0; see THIRD_PARTY_NOTICES.md.

HathorSpatial is not affiliated with Activision or Raven Software. It
contains no game files and needs a legally obtained copy of the game.
