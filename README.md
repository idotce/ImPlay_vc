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

out
ImPlay_vc\_build\_CPack_Packages\win64\ZIP\ImPlay-0.0.0-win64\


## libmpv.dll.a To mpv.lib
# mingw
nm libmpv.a | grep " T mpv_" | awk '{print $3}' > mpv_symbols.txt
echo "LIBRARY libmpv-2.dll" > mpv.def
echo "EXPORTS" >> mpv.def
# 将符号列表追加到 def 文件
cat mpv_symbols.txt >> mpv.def
# vs Developer Command
lib /def:mpv.def /out:mpv.lib /machine:x64


##  build libfreetype
wget https://mirror.accum.se/mirror/gnu.org/savannah/freetype/freetype-2.14.1.tar.xz
tar xvf freetype-2.14.1.tar.xz
mv freetype-2.14.1 freetype
cd freetype
mkdir _build && cd _build
c:\cmake\bin\cmake .. -G "Visual Studio 16 2019" ^
    -DCMAKE_MSVC_RUNTIME_LIBRARY=MultiThreaded ^
    -DCMAKE_BUILD_TYPE=Release ^
    -DBUILD_STATIC_LIBS=ON ^
    -DBUILD_SHARED_LIBS=OFF ^
    -DCMAKE_ARCHIVE_OUTPUT_DIRECTORY=../install/lib ^
    -DCMAKE_INCLUDE_OUTPUT_DIRECTORY=../install/include ^
    -DCMAKE_RUNTIME_OUTPUT_DIRECTORY=../install/bin ^
    -DCMAKE_INSTALL_PREFIX=../install
c:\cmake\bin\cmake --build . --config Release -j16
c:\cmake\bin\cmake --install . --config Release
