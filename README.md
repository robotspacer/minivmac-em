# minivmac-em
This is a fork of [Mini vMac 36.04](https://www.gryphel.com/c/minivmac/) that focuses on SDL 2 and Emscripten, so it can run in a web browser.

## Building minivmac-em
This relies on an older version of Emscripten that does not have arm64 builds available, so it's easiest to build this on a computer with an Intel or other x64 processor. I've been using a MacBook Pro with an Intel Core i5 processor. Below is an example of how to successfully build minivmac-em.

```
mkdir emu
cd emu
git clone https://github.com/emscripten-core/emsdk.git
cd emsdk
git checkout tags/1.38.48
./emsdk install 1.38.48
./emsdk activate 1.38.48
source ./emsdk_env.sh
cd ../
git clone https://github.com/robotspacer/minivmac-em.git
cd minivmac-em/
make -f Makefile-em html
```

## Newer versions of Emscripten
It should be possible to use newer versions of Emscripten, but so far I've been unable to create an acceptable build this way. Emscripten 1.39.17 removes support for Emterpreter in favor of Asyncify. Supposedly, in most cases, updating is as simple as replacing EMTERPRETIFY settings with ASYNCIFY, but I don't think that's the case here. It is also necessary to replace calls to `emscripten_sleep_with_yield` with `emscripten_sleep`. I was able to get a build that works, but it was unusably slow in Safari, though seemingly fine in Chrome. I suspect this is a problem with the `ASYNCIFY_WHITELIST` (or `ASYNCIFY_ONLY`) setting, but I was unable to find a solution.
