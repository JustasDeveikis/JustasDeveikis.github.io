---
title: "Wavelength Converter"
excerpt: "Here you can find the calculator that converts wavelength into energy/wavenumber/frequency values."
collection: portfolio
---

<h3>Wavelength - energy - wavenumber - frequency converter</h3>
<p>Enter a value in one of the fields, and the other values will be calculated automatically:</p>

<form>
  <label for="wavelength">Wavelength (nm):</label>
  <input type="number" id="wavelength" placeholder="Enter wavelength" oninput="updateFromWavelength()" /><br/>

  <label for="energy">Energy (eV):</label>
  <input type="number" id="energy" placeholder="Enter energy" oninput="updateFromEnergy()" /><br/>

  <label for="wavenumber">Wavenumber (cm⁻¹):</label>
  <input type="number" id="wavenumber" placeholder="Enter wavenumber" oninput="updateFromWavenumber()" /><br/>

  <label for="frequency">Frequency (THz):</label>
  <input type="number" id="frequency" placeholder="Enter frequency" oninput="updateFromFrequency()" />
</form>

<script>
  const c = 3e8; // Speed of light in m/s
  const h = 6.626e-34; // Planck's constant in J·s
  const e = 1.602e-19; // Electron charge in C (for eV conversion)

  function resetFields() {
    document.getElementById('wavelength').value = '';
    document.getElementById('energy').value = '';
    document.getElementById('wavenumber').value = '';
    document.getElementById('frequency').value = '';
  }

  function updateFromWavelength() {
    const wavelength = parseFloat(document.getElementById('wavelength').value) * 1e-9;
    if (isNaN(wavelength) || wavelength <= 0) {
      resetFields();
      return;
    }

    const energy = (h * c) / (wavelength * e);
    const wavenumber = 1 / wavelength / 100;
    const frequency = c / wavelength / 1e12; // Convert to THz

    document.getElementById('energy').value = energy.toFixed(4);
    document.getElementById('wavenumber').value = wavenumber.toFixed(2);
    document.getElementById('frequency').value = frequency.toFixed(2);
  }

  function updateFromEnergy() {
    const energy = parseFloat(document.getElementById('energy').value);
    if (isNaN(energy) || energy <= 0) {
      resetFields();
      return;
    }

    const wavelength = (h * c) / (energy * e);
    const wavenumber = 1 / wavelength / 100;
    const frequency = c / wavelength / 1e12; // Convert to THz

    document.getElementById('wavelength').value = (wavelength * 1e9).toFixed(2);
    document.getElementById('wavenumber').value = wavenumber.toFixed(2);
    document.getElementById('frequency').value = frequency.toFixed(2);
  }

  function updateFromWavenumber() {
    const wavenumber = parseFloat(document.getElementById('wavenumber').value);
    if (isNaN(wavenumber) || wavenumber <= 0) {
      resetFields();
      return;
    }

    const wavelength = 1 / (wavenumber * 100);
    const energy = (h * c) / (wavelength * e);
    const frequency = c / wavelength / 1e12; // Convert to THz

    document.getElementById('wavelength').value = (wavelength * 1e9).toFixed(2);
    document.getElementById('energy').value = energy.toFixed(4);
    document.getElementById('frequency').value = frequency.toFixed(2);
  }

  function updateFromFrequency() {
    const frequency = parseFloat(document.getElementById('frequency').value) * 1e12; // Convert THz to Hz
    if (isNaN(frequency) || frequency <= 0) {
      resetFields();
      return;
    }

    const wavelength = c / frequency;
    const energy = (h * frequency) / e;
    const wavenumber = 1 / wavelength / 100;

    document.getElementById('wavelength').value = (wavelength * 1e9).toFixed(2);
    document.getElementById('energy').value = energy.toFixed(4);
    document.getElementById('wavenumber').value = wavenumber.toFixed(2);
  }
</script>




