Besides changing things (maybe too many things) to get the build of `ssh-rd`,
`xpwn`, and `syringe` working on macOS 13, I changed the following things in
this project:

1. Added copying of BuildManifesto.plist from the IPSW file to the temporary
   build directory. This was causing the "Ramdisk load started" hang that people
   reported. (b3df73e59c330eb99c0f447d7187ace880a41356)
2. Added the command `dd` from `coreutils-bin` version `7.2-1` from Saurik's
   Cydia repository. (9a2d24c1d4014cbc4c05e9af85f51a35e1529d71)
