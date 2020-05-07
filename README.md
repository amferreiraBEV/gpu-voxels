![GPU Voxels Logo](http://gpu-voxels.org/gpu-voxels-logo.png  "GPU Voxels")

**GPU-Voxels** is a CUDA based library which allows high resolution volumetric collision detection
between animated 3D models and live pointclouds from 3D sensors of all kinds.
It is mainly developed for robotics planning and monitoring tasks.
See our videos on http://www.gpu-voxels.org/demos/ to get an impression.

## Support:
Find more information on our website http://www.gpu-voxels.org
Doxygen is available at http://www.gpu-voxels.org/doxygen/html/

If you have questions or experience any problems with the software, please post to our GitHub Bugtracker:
at https://github.com/fzi-forschungszentrum-informatik/gpu-voxels/issues

## Install dependencies:
This software is tested under 64 Bit Ubuntu Linux 14.04, 16.04 and 18.04.
Find detailed installation and linking instructions in our Doxygen.

**Core:**

- CUDA 7.5, 8.0, 9.x or 10.0
- PCL
- OpenNI
- Boost
- TinyXML (libtinyxml-dev)

**Visualizer:**

- GLEW (libglew, libglew-dev)
- GLM (libglm-dev). Probably you will have to patch one file: See https://github.com/g-truc/glm/issues/530
- OpenGL
- GLUT (freeglut3, freeglut3-dev)

**Examples:**

- ROS (Robot Operation System)
- OpenNI to interface 3D cameras
- urdfdom
- orocos
- kdl_parser

## Compiling:
        mkdir build
        cd build
        cmake ..
        make

==> This will also generate example programs and a visualization tool to see some live demos.

Doxygen files can be generated by

        make doc

## Compiling without C++11
C++11 is enabled by default. To compile without C++11 mode comment out this at the top of packages/gpu_voxels/CMakeLists.txt: 
 SET(CMAKE_CXX_STANDARD 11)
This is important if you are still using ROS Indigo and need to compile without C++11 support for compatibility reasons. There is a separate indigo branch that only differs in this line to disable C++11 during compilation.

## Known issues
- If the ROS dependency was found, but the GPU-Voxels URDF features are still unabailable, run `source /opt/ros/YOUR_ROS_DISTRO/setup.bash` before running cmake.
- Eigen 3 issues: can be fixed by cloning a more current unstable Eigen version and placing it in CMAKE_PREFIX_PATH
  + on Ubuntu 18.04 with CUDA 10.0: "math_functions.hpp not found"
  ```bash
  git clone git@gitlab.com:libeigen/eigen.git
  sudo cp -r signature_of_eigen3_matrix_library /usr/include/eigen3
  sudo cp -r unsupported/ /usr/include/eigen3
  sudo cp -r Eigen/ /usr/include/eigen3
  ```
  + Eigen 3.3.4 and 3.3.5 with CUDA 9.0, 9.1, 9.2: Error: class "Eigen::half" has no member "x"
  + see http://eigen.tuxfamily.org/index.php?title=Main_Page#Download
- Cuda 8.0: Code compiled with Cuda 8.0 works fine with older GPU drivers such as 375.66, but there are runtime errors with driver 384.111 and newer ("PTX JIT compilation failed"). Easy fix: use Cuda 10 with a current 410 or newer driver version. Cuda 10 is also available for Ubuntu 14.04 and 16.04.
- GLM: There is a known bug in GLM on Ubuntu 16.04 that has to be patched to allow usage of the visualizer. Apply the patch described at https://github.com/g-truc/glm/issues/530 to /usr/include/glm/detail/func_common.inl

## Maintainers:
The library is developed and maintained by:

- Christian Jülg
- Andreas Hermann

Contributors are (in temporal order):

- Sebastian Klemm
- Florian Drews
- Matthias Wagner
- Felix Mauch
- Herbert Pietrzyk
- Gabriele Bolano
- Florian Fervers
- Erik Albert

## License:
The software in this repository underlies different licenses.
Please consider the LICENSE.txt in the different package directories.
Feel free to contact us for any licensing questions.

To clarify this:

- The Build System (icmaker and according scripts) is distributed under BSD license
- GPU-Voxels is distributed under the CDDL license
- icl_core helber library is distributed under CDDL license

Please let us know if you are using the **GPU-Voxels** library,
as we are curious to find out how it enables other people's work or research.

We would be grateful if scientific publications resulting from projects
that make use of **GPU-Voxels** would cite our overview paper:
*A. Hermann, F. Drews, J. Bauer, S. Klemm, A. Roennau and R. Dillmann:
**“Unified GPU Voxel Collision Detection for Mobile Manipulation Planning”**
in Intelligent Robots and Systems (IROS 2014, Chicago, September 2014)*

Copyright (c) 2014, *FZI Forschungszentrum Informatik*, Karlsruhe, Germany
All rights reserved.

## Thanks:
The **GPU-Voxels** library was developed at the *FZI Forschungszentrum Informatik*, Karlsruhe, Germany.

The research leading to the results has received funding from... 
- the **German Federal Ministry of Education and Research (BMBF)** under grant agreement no. 01IM12006C (ISABEL).
- the **European Union** program **Horizon 2020** under grant agreement no. 680734 (HORSE).
- the **Baden-Württemberg Stiftung** through the KolRob reasearch project.

