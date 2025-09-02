# Nuclear Reactions

This is where I expose the work done using Geant4, in the field of nuclear reactions. Basically I did two projects, all based on the photonuclear reaction 197Au(gamma,n)196Au, as the cross sections where measured in recent experiments. The goal is to study the photonuclear reaction model that G4 is using and see if it matches the experimental data.

The first project consists of shooting gamma rays of a certain energy at a thin layer of 197Au, thus producing the photonuclear reaction. The program measures the yield of 196Au, allowing the cross sections of a certain gamma energy to be calculated.

The second one is based on the first one but has a key difference. The gammas are produced by Bremsstrahlung effect, by shooting electrons on a tungsten layer. This gammas produced are a spectrum of different energies. Right in front of the tungsten there is a detector that counts how many gammas of a given energy range there are, and right in front of that we can find our target. The target is a Au197 block of 8 mm deep, in which the photonuclear reactions happen. The yield of 196Au produced is also measured.

## Photonuclear-Au-8mm

You can download the project from my repository [Photonuclear-Au-8mm](https://github.com/pjarnecup/Photonuclear-Au-8mm/tree/main). Again, this project used as a base the Hello World basic program from @john9francis. Now I'm gonna explain the different classes involved in this project, and what each of them does.

### Main File

The main file includes the main function, which does the following: If this program is run on it's own with no other args, the ui is defined. Then the program constructs the runmanager, which is used to initialize the MyDetectorConstruction class, MyPhysicsList class and MyActionInitialization class. It also initialized the visualization and the geometry. Then, the init_vis mac is initialized, which executes the program, and the ui session is opened. On the contrary, if the program is opened with another argument in the console, such as a mac file, the program processes it and opens the UI session.

### MyActionInitialization Class


