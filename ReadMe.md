-- FileWatcher --

Acknowledgement

All core code are from https://github.com/jameswynn/simplefilewatcher. Our minor contribution is to simplify the compiling with CMake.

Description:

FileWatcher is a C++ wrapper for OS file monitoring systems. Currently
it uses Win32 ReadDirectoryChangesW for monitoring changes in Windows,
and inotify in linux. OSX is supported via kqueue and directory scans.


Compiling:

```
mkdir build && cd build
cmake .. -DBUILD_DEMO_CPP=ON
```

SimpleDemo:

To run the demo, Start SimpleDemo, then create/change/delete files inside
"test". If "test" does not exist when SimpleDemo starts, it will throw
an exception and exit.


Caveats:

When some programs write data in Win32, they will generate both an Add,
and a Modify event. This is likely because the program is actually using
two separate calls to write its data.

Because of the time it takes to write the data to the file, it may be
necessary in some cases to wait a few milliseconds after the event to be
able to safely access the file's contents.


------------------------------
Written by James Wynn
Contact: james@jameswynn.com

The original version can be located at:
https://github.com/jameswynn/simplefilewatcher/commit/4bccd086621698f21a6e95f3ff77c559f862184a
