This boilerplate is a simple example of how to build a simple Objective-C 2.0 project on Linux with GNUstep,
and macOS with Apple frameworks.

## GNUstep
We use the GNUstep configuration tool `gnustep-config` to get the GNUstep and Objective-C specific compiler
and linker flags.

Make sure to source the `GNUstep.sh` script in your shell before compiling and running the program, otherwise
meson might not be able to locate `gnustep-config`.

If you used the standard FHS installation layout, or did not explicitly set a layout when building GNUstep,
you can source the script like this:

```bash
source /usr/share/GNUstep/Makefiles/GNUstep.sh
```
Note that the Makefiles directory might be located in a different place on your system, depending on your distribution.

Meson also looks for CC, and OBJC environment variables to be set. Use clang as the compiler, as GCC does not
support Objective-C 2.0.

## Apple frameworks
On macOS, meson will automatically find the Apple frameworks. Currently, only the Foundation framework is used,
but you can add more frameworks by adding them to the modules array in `meson.build`.

Be aware that some frameworks are not available on Linux, and you will need to use a different implementation.

## Dependencies
- A working GNUstep installation with Objective-C 2.0 support (libobjc2, gnustep-make, gnustep-base)
  Please note that as of writing this, the GNUstep debian packages do not support Objective-C 2.0, and use the GCC runtime.

## Building
First, setup the meson project and `build/` directory: 
```bash
# Source the GNUstep environment script if not already done by your shell configuration (e.g. source /usr/share/GNUstep/Makefiles/GNUstep.sh)
OBJC=clang meson setup build
```

You can now compile and execute the example program:
```bash
ninja -C build
./build/objc-boilerplate
```

If everything worked, you should see an output similar to this:
```bash
2023-10-16 11:28:06.806 objc-boilerplate[40560:40560] Hello, World!
```
