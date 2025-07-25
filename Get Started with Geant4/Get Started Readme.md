# Get Started with Geant4

## Introduction to Geant4

Geant4 (G4) is a Monte-Carlo toolkit used to simulate passage of particles (electric or neutral) through matter. The way it works breaking a particle trajectory into small pieces and calculating the probability for interaction with matter based oin cross-sections. It was developed by the Geant4 collaboration at CERN (1994), and it's based on Genat3 but with a completely different design and well documented. It tries to include all possible particle interactions, and it's used in high energy particle physcis, nuclear physcis and medcial applications such as radiotherapy and imaging. G4 is written in C++, an object-oriented languaje, and it provides libraries and headers to wrie your own simulation code (you create your own CMake project with source files that you can compile). You can also define classes/functions without knowing other parts of the software. There are classes for physics lists, materials & geometry, sensitive detectors, particle sources (or guns), etc..., that the user specifies.

## Basic G4 Application Structure

Most G4 program consists on the folowing structure: one **Main File**, which initializes a **Run Manager Class**, and this one initializes a **Primary Generator Action Class**, that generates whatever particle you use; a **Physcis List Class**, that regulates the physics processes; and a **Detector Constructor Class**, which defines the geometries for the particles to interact with and get the data. This classes will be exemplified in the practicle examples of this GitHub Repository.

## Installation of Geant4 with Qt

We installed Geant4 on Windows 11, using CMake, Visual Studio code, and Qt as a visualization driver. We followed @john9francis GitHub tutorial on [Installing and Compiling Geant4 with Qt visualization driver](https://github.com/john9francis/radiation-modeling/blob/main/g4-install-instructions-qt.md), which is very well documented and easy for our purposes.

You can also find his tutorial on Youtube, where the same steps are followed: [Geant4 Installation with Qt 2023](https://youtu.be/rtCsfDD45Bc)

In @john9francis tutorial you will also be able to understand how to run an example project from the Geant4 shared examples and visualize it with Qt GUI. It also includes reference links to download and install all the prerequisites, and other useful information.

If you want to see the code of your first project example, you just have to go to VS and open the folder in which the build, src and include directories are located. You will be able to see the code from the main file, the headers (include folder) and source code for each header (src folder).

## Simple G4 Program / G4-Hello-World

We found out, in one of @john9francis Github repositories, a really simple G4-Hello-World project that he developed, as a base to start building future applications. This projects consists of a basic G4 program with the CMakeList file already created, so that you can simply change the name and compile it with CMake. Then you can start writing any application that you want. The program will automatically be linked with the G4 source code and copy the mac files in the same directory as the executable files.

Download the application as a zip file from his repository [G4-Hello-World](https://github.com/john9francis/G4-Hello-World), and read the Readme file in it, as it contains important information about how the program works and it's compiled.

This really basic application includes a CMakeList file to compile the project with CMake and VS, also source and include folders, which are empty because there are no classes defined yet (like PrimaryGeneratorAction class or DetectorConstructor class). There is also a mac_files folder with a test file that prints Hello World, and a main c++ file called Hello_World.cc
