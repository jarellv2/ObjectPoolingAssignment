# Object Pooling Lab

**Name:** Jarell Igene  
**Student Number:** 100980195 

## Gameplay Loop
An interactive, continuous spawning system where the player fires projectiles on command. To maintain performance during rapid fire, projectiles are deactivated after 0.5 seconds and recycled rather than destroyed.

---

## Profiler Screenshots (Before & After)

<img width="1214" height="830" alt="Screenshot 2026-11-15 233057" src="https://github.com/user-attachments/assets/738e6465-8ee3-45cc-8beb-d2978f123c2e" />

<img width="1285" height="834" alt="Screenshot 2026-11-16 004605" src="https://github.com/user-attachments/assets/239b8202-c254-4fee-b47e-da0a18146059" />

---

## Blueprint Implementation (Source Code)
<img width="889" height="594" alt="Screenshot 2026-11-16 002502" src="https://github.com/user-attachments/assets/68585f3e-3c9d-4ff2-a994-a7e284c3026e" />

<img width="1046" height="567" alt="Screenshot 2026-11-16 220917" src="https://github.com/user-attachments/assets/6ba86b5b-fc6a-4779-8743-6ac4dd5a7e86" />

<img width="1004" height="690" alt="Screenshot 2026-11-16 003108" src="https://github.com/user-attachments/assets/2ec8fbed-fbbd-4d53-a8d8-319f967299bf" />

---

## Reflection Questions

**1. What did you notice was impacting the performance of your project?**  
Prior to implementing object pooling, calling `SpawnActor` and `DestroyActor` heavily on demand caused significant CPU overhead and memory allocation spikes within the GameThread profiler.

**2. Which pattern(s) did you implement, and what behavior did they replace?**  
I implemented the Object Pooling design pattern. This replaced the continuous, costly runtime allocation and garbage-collection of bullet actors with a recyclable array of pre-spawned actors.

**3. Do your patterns / technique implementations improve performance? Why or why not?**  
Yes, performance improved dramatically. By allocating a fixed pool of 50 `BP_Bullet` actors during `BeginPlay`, the runtime instantiation cost dropped to zero. The spawner efficiently recycles inactive actors from the array by toggling their visibility and collision states, completely bypassing the engine's expensive memory allocation processes.

**4. Can you demonstrate what the profiling process revealed?**  
Yes. The "Before" profiling screenshot demonstrates heavy CPU load and constant `SpawnActor` calls. The "After" screenshot proves the `SpawnActor` call count dropped to exactly 0 during active gameplay, confirming the engine is exclusively recycling the existing pool.

---
**Build Instructions:** 
A packaged Windows build is available in the Releases section. No special instructions are required to run the `.exe`.
