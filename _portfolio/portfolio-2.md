---
title: "Ultrafast Explanation of Ultrafast Spectroscopy"
excerpt: "A short introduction to ultrafast spectroscopy. <br/><img src='/images/UltrafasSpectroscopyIntro.png'>"
collection: portfolio
---

<br/><img src='/images/UltrafastSpectroscopyMeme.png'>

### Introduction

Ultrafast spectroscopy is a technique that uses ultrashort laser pulses (in the order of a picosecond, 10$$^{-12}$$ s, or less) to investigate dynamics on timescales from attoseconds (10$$^{-18}$$ s) to nanoseconds (10$$^{-9}$$ s). This spectroscopy method could be used to study atoms, molecules, and charge carrier dynamics, which occur too quickly to measure using electronic devices.

The measurements are performed by using a sequence of ultrashort laser pulses to perturb the system from its equilibrium and record its state at a number of time delays to reconstruct the dynamics. It is necessary that the temporal width of the laser pulse is shorter or similar to the timescale of dynamics.


### Experimental Setup

To conduct an ultrafast spectroscopy experiment, usually a [titanium-sapphire (Ti:sapph) laser](https://en.wikipedia.org/wiki/Titanium-sapphire_laser) is a common source of ultrashort pulses. The laser is implemented in a [regenerative amplifier](https://en.wikipedia.org/wiki/Regenerative_amplification) with an [optical parametric amplifier](https://en.wikipedia.org/wiki/Optical_parametric_amplifier) being used to tune the wavelength to the desired value.

The most common ultrafast spectroscopy experiment is 'pump-probe,' which is shown below.

<br/><img src='/images/PumpProbeExpSetup.png'>

The pump pulse is used to excite electrons in the material, which means transferring them from their ground state to the higher energy states. A broadband probe pulse arrives some time $$\Delta t$$ later, and its spectrum is monitored by the detector. The optical chopper is used to modulate the pump pulse, which allows obtaining pump-on, $$I_{pump\,on}$$, and pump-off, $$I_{pump\,off}$$, spectra continuously. The change in absorbance, $$\Delta A$$ is worked out as $$\log_{10}(I_{pump\,off}/I_{pump\,on})$$.

<br/><img src='/images/PumpProbePulseSequence.png'>

As the electrons in the excited material interact with the probe pulse, less light is absorbed at the photon energy $$E_1$$ matching the transition (highlighted by green). The excited electrons may further absorb probe light; if there are higher energy states present, then electrons may absorb more light at the energy $$E_2$$ (highlighted by an orange arrow). The difference between pump-on and pump-off spectra allows one to draw conclusions about the energy levels of the material.

Finally, the experiment is carried out many times at different delays $$\Delta t$$ to reconstruct the time-resolved behaviour of the system. As time evolves, the excited electrons recombine, decreasing the change in absorbance $$\Delta A$$.

### Applications

The ultrafast spectroscopy is a useful technique to study ultrafast processes and has found many uses in science. For example, [photodissociaion of chemical compounds](https://www.nature.com/articles/s41557-023-01420-w), [processes in biologically active molecules](https://www.annualreviews.org/content/journals/10.1146/annurev.physchem.59.032607.093615) and [charge carrier dynamics in perovskites](https://www.sciencedirect.com/science/article/pii/S2542435118301703).