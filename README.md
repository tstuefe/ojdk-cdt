# ojdk-cdt

Note: these CDT projects link their sources from the ojdk repository. They are meant to be placed *outside* the jdk repository. 

Example setup:

```
- my-jdk
   |
   |--sources (contains openjdk sources)
   |--output  (contains build output)
   |--ojdk-cdt (these files)
```

1) Open "ojdk-cdt" as workspace in Eclipse CDT
2) Preferences->Linked Resources:
  - set OPENJDK_SOURCE_ROOT to root of jdk repository ("my-jdk/sources")
  - set OPENJDK_OUTPUT_ROOT to root of jdk build directory ("my-jdk/output")
3) import projects ("General->Existing Projects Into Workspace"), select workspace root folder ("ojdk-cdt") and import both "hs" and "hs-gtests". Do not copy the sources, leave all settings default.

You should have now a workspace with two projects, "hs" (containing the hotspot sources) and "hs-gtests" (containing the gtests tests). Let the C++ indexer do its thing, then you are done and can start browsing the code. C++ code assistence should work now (jumping to definitions, call hierarchy etc).

You may have to actually build the OpenJDK to populate the output directory and get all generated sources (especially for the compiler). Do this by:

```
cd output
bash ../source/configure
make images
```

Notes:
- used mainly on Linux but should work on other platforms too.
- Search path is set up for Linux x64 but browsing sources for other platforms and architectures seems to work at least partly.
- Build does not work from within the IDE - would require a lot more work than this small setup. One still builds via command line.
