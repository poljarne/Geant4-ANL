# Get Started with Geant4

## Introduction to Geant4

Geant4 (G4) is a Monte-Carlo toolkit used to simulate passage of particles (electric or neutral) through matter. The way it works breaking a particle trajectory into small pieces and calculating the probability for interaction with matter based oin cross-sections. It was developed by the Geant4 collaboration at CERN (1994), and it's based on Genat3 but with a completely different design and well documented. It tries to include all possible particle interactions, and it's used in high energy particle physcis, nuclear physcis and medcial applications such as radiotherapy and imaging. G4 is written in C++, an object-oriented languaje, and it provides libraries and headers to wrie your own simulation code (you create your own CMake project with source files that you can compile). You can also define classes/functions without knowing other parts of the software. There are classes for physics lists, materials & geometry, sensitive detectors, particle sources (or guns), etc..., that the user specifies.

## Basic G4 Application Structure

The most basic G4 program consists on one **Main File**, which initializes a **Run Manager Class**, and this one initializes a **Primary Generator Action Class**, that generates whatever particle you use; a **Physcis List Class**, that regulates the physics processes; and a **Detector Constructor Class**, which defines the geometries for the particles to interact with and get the data. This classes will be exemplified in the practicle examples of this GitHub Repository.

## Installation of Geant4 with Qt

We installed Geant4 on Windows 11, using CMake, Visual Studio code, and Qt as a visualization driver. We followed @john9francis GitHub tutorial on [Installing and Compiling Geant4 with Qt visualization driver](https://github.com/john9francis/radiation-modeling/blob/main/g4-install-instructions-qt.md), which is very well documented and easy for our purposes.

You can also find his tutorial on Youtube, where the same steps are followed: [Geant4 Installation with Qt 2023](https://youtu.be/rtCsfDD45Bc)
