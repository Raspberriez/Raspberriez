- Rewrite the app to fix codesign issues
- Test ElleKit on sideloaded
- On fat binaries where LC-to-be-removed is not the last, instead get dllc.command, change dllc.command.cmd to LC_LOAD_WEAK_DYLIB, and patch that over

"Some mysteries aren't questions to be answered but just a kind of opaque fact, a thing which exists to be not known"
