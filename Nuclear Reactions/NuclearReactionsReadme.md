# Nuclear Reactions

This is where I expose the work done using Geant4, in the field of nuclear reactions. Basically I did two projects, all based on the photonuclear reaction 197Au(gamma,n)196Au, as the cross sections where measured in recent experiments. The goal is to study the photonuclear reaction model that G4 is using and see if it matches the experimental data.

The first project consists of shooting gamma rays of a certain energy at a thin layer of 197Au, thus producing the photonuclear reaction. The program measures the yield of 196Au, allowing the cross sections of a certain gamma energy to be calculated.

The second one is based on the first one but has a key difference. The gammas are produced by Bremsstrahlung effect, by shooting electrons on a tungsten layer. This gammas produced are a spectrum of different energies. Right in front of the tungsten there is a detector that counts how many gammas of a given energy range there are, and right in front of that we can find our target. The target is a Au197 block of 8 mm deep, in which the photonuclear reactions happen. The yield of 196Au produced is also measured.

## Photonuclear-Au-8mm

You can download the project from my repository [Photonuclear-Au-8mm](https://github.com/pjarnecup/Photonuclear-Au-8mm/tree/main). Again, this project used as a base the Hello World basic program from @john9francis. Now I'm gonna explain the different classes involved in this project, and what each of them does.

### Main File

The main file includes the main function, which does the following: If this program is run on it's own with no other args, the ui is defined. Then the program constructs the runmanager, which is used to initialize the MyDetectorConstruction class, MyPhysicsList class and MyActionInitialization class. It also initialized the visualization and the geometry. Then, the init_vis mac is initialized, which executes the program, and the ui session is opened. On the contrary, if the program is opened with another argument in the console, such as a mac file, the program processes it and opens the UI session.

### MyActionInitialization Class

This class is responsible for initializing the MySteppingAction, MyPrimaryGeneratorAction, and MyRunAction classes. Using lines of code such as:

SetUserAction(new MyPrimaryGeneratorAction());

Inside the Build() function.

### MyDetectorConstruction Class

This class defines the materials used in this program, which in this case are water, gold and tungsten. Then, it creates a world, which is the place where everything is gonna happen. This world is a box made of air, each side measuring 1 meter. When you create a geometry like this in G4, you need to define a solid world, a logic world and a physical world. The information of how to use each of those can be found in the Geant4 user guide for application developers.

Then a tungsten plate is defined, which measures 1 cm high and wide, and 4 mm deep (in the z-axis). Right after the tungsten plate, a photon scoring plane of 0.1mm thick is defined, which will be used to count the gammas of all the energy ranges. Right after the scoring plane, the target is defined, a 197Au box of 8 mm thick. Both the gold box and the scoring plane have 3 mm high and wide.

### MyPhysicsList Class

The physics list used in this program is QGSP_BERT_HP(). 

* QGSP_BERT_HP: identical to QGSP_BERT except that neutrons of 20 MeV and lower use the new version (alternative to the one of FTFP_BERT_HP) of the High Precision neutron models and cross sections to describe elastic and inelastic scattering, capture and fission, the last process is added. Additionally radioactive decay is activated. Since Geant4 version 11.2, the physics list QGSP_BERT_HP has a treatment of low energy (<20 MeV) neutrons which is not the same as for the other HP-based reference physics list (FTFP_BERT_HP, QGSP_BIC_HP, Shielding, etc.).

### MyPrimaryGeneratorAction Class

This class defines a G4ParticleGun, which is the source from which particles are gonna be shooted. Defines the type of particle (in this case e-), its energy and its momentum vector. Then, this class includes code to generate the electrons randomly within a cirle of 1 mm of radii.

### MySteppingnAction Class

This class is gonna define bins for different radii intervals in the photon score plane (0.5 mm bins up to 5 cm), therefore there are 100 of these bins (first one cenetered at 0.25 mm for example). Now, for each of the first 3 bins (first 3 radii intervals, 0-0.5mm, 0.5-1mm, 1-1.5mm), we define 80 bins (0-20MeV, 0.25MeV/bin). These represent the energy spectrum of the gammas in each of the first 3 radii intervals. Then there is code to reset the counting of this bins everytime a new electron run is produced.

This class also counts the number of 196Au produced by the reaction of the gammas with the 197Au.

Finally, is the code to detect the gammas inside the photon scoring plane. It stores the number of gammas in each of the 100 radii bins, and also the energy spectrum bins information inside the first 3 intervals.

### MyRunAction Class

Handles per-run bookkeeping, result aggregation (thread-safe), and final output.

**Key roles**
- **Run start**  
  Resets counters in `MySteppingAction` and clears global Au-196 count (master thread only).
- **Run end**  
  - Aggregates thread-local Au-196 counts with a mutex.  
  - Prints:
    - **Photon yield vs radius** (photons/sec and photons/mm²)
    - **Energy spectra** for the first 3 radial bins (0–1.5 mm, 0.25 MeV steps)
    - **Au-196 summary**: total atoms, yield, and estimated cross section (mb)
    - **Bin-by-bin Au-196 estimate** in the 12.75–15 MeV window

