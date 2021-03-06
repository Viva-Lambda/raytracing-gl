# raytracing-gl
OpenGL compute shader port of 
[Raytracing in One Weekend](https://raytracing.github.io/books/RayTracingInOneWeekend.html) by P. Shirley

This repository follows closely the examples introduced by the 
phenomenal "Raytracing in One Weekend" by P. Shirley, plus couple of other
examples from "Raytracing Next Week".

I did unfortunately not document the code much, since Shirley gives a through
explanation of how everything works. Assuming you have basic knowledge of
opengl and glsl, it should be fairly easy to understand what's going on in the
shader code.

Due to the imperative nature of glsl, I have, from time to time, diverged from
the implementation of Shirley.

### Requirements

These requirements basically mimick my development environment. Some of them can
probably be lowered.

- Cmake >= 3.0.2
- OpenGL >= 4.3
- GLFW 
- Glad function pointers for OpenGL 4.3
- C++ 17 for using `<filesystem>`
- Clang >= 9 again for using `<filesystem>`. 

If you are willing to use `<boost/filesystem>` instead of standard library,
the compiler requirement can be drop to clang > 5.5, you can also use
gcc with boost.

## Compiling the code

- Create "build" directory in main folder containing this README.md
- `cd build`
- `cmake ..`
- `make install`

There will be two copies of executables one in build folder another in `bin`
folder.
Use the ones in `bin` folder since reference to any media is hardcoded inside
the code with respect to `bin`.

I use `cmake-gui` to specifically select the compiler during the configuration
process, I suggest you do the same if you have multiple compilers with
different versions in your machine.

## Remarks

You'll notice that most of the implementation files, `.cpp`s, are same in nature
maybe diverging 1 or 2 lines somewhere. The boilerplate code for rendering a
full screen quad is in `window.hpp`. It can be thought of as the equivalent of
`.ppm` output in the original book.
Most of the real work happens inside compute shaders named `compute01.comp` or
`compute02.comp`. The numbers suggest complexity. 01 is the simplest, 02 is a
little more difficult than 01 etc. 

During the execution of `compute02.out` and onwards gpu might start to choke.
Try lowering the size of the workgroups in the shader, if that does not help,
try lowering the `psample` and `depth` that is passed on to `ray_color`
function.

Unless you have a very very good machine or a particular reason DO NOT LAUNCH
`./weekend.out`. It is there as a proof of concept. Ray tracing 485 object
naively, that is with no acceleration structure whatsoever, would surely choke
your gpu if not produce a driver error. If you really want to see something
similar in cover picture. I suggest you to lower the amount of spheres in the
`random_scene` loop, and change the `SCENE_OBJ_NB` accordingly.

## Known Issues

- Perlin noise example `compute06.out` does not render correctly.


## Screenshots

- The executable `compute01.out` should give you this: ![compute01
  output](bin/media/screenshots/compute01.png?raw=true  "compute01.comp output")

- The executable `compute02.out` should give you this: ![compute02
  output](bin/media/screenshots/compute02.png?raw=true  "compute02.comp output")

- The executable `compute03.out` should give you this: ![compute03
  output](bin/media/screenshots/compute03.png?raw=true  "compute03.comp output")

- The executable `compute04.out` should give you this: ![compute04
  output](bin/media/screenshots/compute04.png?raw=true  "compute04.comp output")

- The executable `compute05.out` should give you this:
  <img src="bin/media/screenshots/compute05.png" width="320" height="180"/>

