https://github.com/tsl0922/ImPlay

## Build
VC
cd ImPlay
mkdir _build && cd _build
c:\cmake\bin\cmake .. -G "Visual Studio 16 2019" ^
    -DCMAKE_MSVC_RUNTIME_LIBRARY=MultiThreaded ^
    -DCMAKE_BUILD_TYPE=Release ^
    -DUSE_PATCHED_GLFW=ON ^
    -DUSE_OPENGL_ES3=ON ^
    -DCREATE_PACKAGE=ON
c:\cmake\bin\cmake --build . --config Release -j16
c:\cmake\bin\cmake --build . --config Release --target package
