# Third-party notices

HathorSpatial is proprietary software, Copyright (c) 2026 Hathor Sound,
distributed in binary form only under the terms in `LICENSE`. This file
records the third-party software the released package depends on or
redistributes.

## Steam Audio (phonon.dll)

- Copyright 2017-2023 Valve Corporation
- License: Apache License, Version 2.0 — https://www.apache.org/licenses/LICENSE-2.0
- Source: https://github.com/ValveSoftware/steam-audio

HathorSpatial loads `phonon.dll` dynamically at runtime. Where a release
package includes a copy, that copy is **unmodified** and is distributed under
the Apache License, Version 2.0; the full text of that license accompanies
this package as `LICENSE-Apache-2.0.txt`. No Steam Audio source code is
included or redistributed.

HathorSpatial itself is not Apache-licensed — see `LICENSE`.

## Toolchain

Built with MinGW-w64, whose permissive licensing allows distribution of
compiled binaries without restriction. No toolchain source is redistributed.

## A3D

HathorSpatial implements the A3D 3.0 programming interface that Soldier of
Fortune's sound module calls, and interoperates with that module. It contains
no Aureal or Creative code.

## Trademarks

A3D and Aureal are trademarks of their respective owners. DualSense and
PlayStation are trademarks of Sony Interactive Entertainment Inc. Xbox is a
trademark of Microsoft Corporation. Steam and Steam Audio are trademarks of
Valve Corporation. Soldier of Fortune is a trademark of Activision
Publishing, Inc. All other trademarks are the property of their respective
owners.
