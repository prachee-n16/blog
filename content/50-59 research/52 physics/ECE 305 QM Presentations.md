---
draft: "true"
---
**Group 1 (00:00-15:00):** Quantum cryptography techniques
- Allen Liu
- Carol Xu
- Max Storjohann

- Starts with modern crypto methods; the goal is securing transmission of messages from external agents
	- Algorithms use factoring of large prime numbers: Diffie-Hellman and RSA algorithms which is computationally intensive to crack;
- These are not **cryptographically secure** - we make the assumption that you can't crack it;
- Quantum computing can crack this in estimated 30 years; Q-day
	- Shor's algorithm can factor large prime numbers **exponentially faster**
		- Store-and-decrypt: people are storing encrypted data waiting for Q-day to decrypt;
	- Lost a little bit on *key distribution* but essentially, symmetric-key encryption is when secret key has been previously shared and shared key is sent on a public channel
- Quantum crypto relies on two fundamental concepts:
	- Postulate 5 and photons have wave-particle duality + can be polarized (discretized)
- We can divide into two broad categories
	- CV-QKD
	- DV-QKD - based on discrete eigenstates which is less susceptible to noise (harder to implement)
	- BB84 - First QKD protocol
		- Rectilinear and diagonal basis (do we want to use X or Z spin states)
		- if measured the bit on the wrong basis, we won't get the right value
	- Great explanation of BB84 to finally make the key; 

Question - How did they send the qubits across the channel? Do an example using one qubit.

**Group 2 (15:00-30:00):** Quantum entanglement
- Hardy Yu
- Amy Hu
- Jasmine Mao

- Strong correlation between particles is so strong that classical mechanics can not explain it
- CHSH Inequality
	- Suppose there is Alice and Bob; measuring particles in X or Y direction and neither know which direction the either are measuring in
	- They will measure a weighted sum between these measurements
	- The value is actually bounded by a value of 2; 
- Quantum mechanics predicts that for certain entangled states, the CHSH inequality can be violated. (will be 2.8) which is **Tsirelson bound**
- **monogamy of entanglement**
	- Shows how it is actually violating the CHSH inequality;
	   ![](https://www.researchgate.net/publication/384442560/figure/fig1/AS:11431281280913667@1727612827281/Quantum-correlation-as-a-function-of-the-Angle-between-detectors-degrees-Photo-Picture.png)
- Mathematical representations of two non-interacting particles;
	- Particle 1 and 2 can exists in u or j states; we can use the tensor product to explain the coupling between particles
- Mathematical explanation of proving it's entangled or not;
- Application: QKD! 
	- alice/bob observer the particles at maximally entangled angle
	- If the CHSH inequality does hold, it would indicate that photons are not **truly entangled**, thus there may be an eavesdropper time

**Group 3 (30:00-45:00):** Atomic Clocks
- Krishnha Milchelvan
- Renesh Babu
- Arman Hojjatoleslami

Atomic clocks - most accurate timekeeping device
- historical context; main applications in GPS but also used by meteorologists for ion traps
- quartz oscillator - most accurate timekeepers; Piezoelectric attributes
	- when we give voltage, the crystal will resonate at a certain frequency and produces pulses at the same frequency
- But, oscillator will slow down over time;
- To fix the oscillator, a pulse sent to crystal to increase frequency; we can use cesium-133?
- A stream of cesium-133 atoms pass through a magnet to separate lower energy atoms from higher energy atoms; 
	- resonator: low energy atoms pass through and transition to a higher energy state
- Detector to count the high energy atoms sent as feedback to crystal oscillator
	- magnet separates lower energy atoms from higher energy atoms (why the second magnet?)
- DC voltage is applied to crystal to correct the oscillator frequency
- Cesium-133 atoms have two energy levels:
	- lower energy state (f = 3)
	- higher energy state (f = 4)
- Some notes on applications of this technology
Question: Synchronize clocks?; To miniaturize, what is the point you need to look at?

**Group 4 (45:00-60:00):** NMR Imaging
- Callum Perrault
- Ivy Bao
- Daniel McVicar

Magnetic resonance - process where we induce transitions between energy states by applying an oscillating magnetic field at a frequency near Larmor precession frequency
- can only be applied to nuclei with odd mass; with mass;
Electrons can have +1 and -1 but the nuclei can have fractional spins;
- Took a modified SG experiment; applied an oscillating magnetic field 
**lost track unfortunately..**

**Group 5 (60:00-75:00):** Quantum Dots
- Henry Ren
- Elias Kountouris
- Olivia Yi

Quantum dots 
- Applications
	- Quantum dot displays in QLED TVs and Monitors which enhances color gamut, saturation, etc.
		- What is *color gamut?*
	- Solar cells, lasers etc.
- Electron-hole recombination when it takes energy to go in a higher energy state and going to lower levels releases energy
	- this is a band gap; $E = hf$ where frequency and energy is related 
- Blue LED is difficult to tune this band gap; but quantum dots lets us do that easier
- At large distances, the bands appear to be continuous but the closer we get, it looks more discrete.
	- due to small permittivity of free space, electrons leaving atomic orbitals take a lot of energy and this acts like an *infinite well*
