---
title: "Fluence and Charge Carrier Density Calculator"
excerpt: "Here you can find calculators to estimate laser fluence and density when you input the parameters."
collection: portfolio
---

<h3>Fluence Calculator</h3>
<p>Fill the fields to calculate the laser fluence:</p>

<div class="calculator">
    <div class="input-group">
        <label for="fluence_wavelength">Pump Wavelength (nm):</label>
        <input type="number" id="fluence_wavelength" value="410" step="0.1">
    </div>
    <div class="input-group">
        <label for="fluence_sigma">Beam Width (sigma, mm):</label>
        <input type="number" id="fluence_sigma" value="0.25" step="0.01">
    </div>
    <div class="input-group">
        <label for="fluence_power">Power (mW):</label>
        <input type="number" id="fluence_power" value="0.04" step="0.01">
    </div>
    <div class="input-group">
        <label for="fluence_rep_rate">Repetition Rate (Hz):</label>
        <input type="number" id="fluence_rep_rate" value="500" step="1">
    </div>
    <button onclick="calculateFluence()">Calculate Fluence</button>

    <div class="output">
        <h2>Fluence Calculation Results</h2>
        <p>Photon Energy: <span id="photon_energy"></span> eV</p>
        <p>Energy per Pulse: <span id="energy_per_pulse"></span> nJ</p>
        <p>Number of Photons per Pulse: <span id="photons_per_pulse"></span></p>
        <p>Beam Area: <span id="beam_area"></span> cm<sup>2</sup></p>
        <p>Fluence: <span id="fluence"></span> &micro;J/cm<sup>2</sup></p>
    </div>
</div>

<h3>Charge Carried Density Calculator</h3>
<p>Fill in the fields to calculate the density:</p>

<div class="calculator">
    <div class="input-group">
        <label for="film_thickness">Film Thickness (nm):</label>
        <input type="number" id="film_thickness" value="50" step="1">
    </div>
    <div class="input-group">
        <label for="reflectance">Reflectance (R):</label>
        <input type="number" id="reflectance" value="0.2" step="0.01" min="0" max="1">
    </div>
    <div class="input-group">
        <label for="optical_density">Optical Density (OD) at Pump Wavelength:</label>
        <input type="number" id="optical_density" value="0.6" step="0.1">
    </div>
    <div class="input-group">
        <label for="probe_sigma">Probe Width (sigma, mm):</label>
        <input type="number" id="probe_sigma" value="0.12" step="0.01">
    </div>
    <button onclick="calculateDensity()">Calculate Charge Carrier Density</button>

    <div class="output">
        <h2>Charge Carrier Density Calculation Results</h2>
        <p>Absorption Coefficient: <span id="absorption_coefficient"></span> m<sup>-1</sup></p>
        <p>Charge Carrier Density: <span id="charge_carrier_density_m3"></span> m<sup>-3</sup> / <span id="charge_carrier_density_cm3"></span> cm<sup>-3</sup></p>
        <p>Absorption Depth: <span id="absorption_depth"></span></p>
    </div>
</div>

<script>
    function calculateFluence() {
        const c = 3e8; // Speed of light in m/s
        const h = 6.626e-34; // Planck's constant in J·s
        const e = 1.602e-19; // Elementary charge in J/eV

        // Inputs
        const wavelength = parseFloat(document.getElementById('fluence_wavelength').value) * 1e-9; // Convert nm to m
        const sigma = parseFloat(document.getElementById('fluence_sigma').value) * 1e-3; // Convert mm to m
        const power = parseFloat(document.getElementById('fluence_power').value) * 1e-3; // Convert mW to W
        const repRate = parseFloat(document.getElementById('fluence_rep_rate').value);

        if (isNaN(wavelength) || isNaN(sigma) || isNaN(power) || isNaN(repRate) || wavelength <= 0 || sigma <= 0 || power <= 0 || repRate <= 0) {
            alert("Please fill all fields with valid positive values.");
            return;
        }

        // Calculations
        const photonEnergyJ = (h * c) / wavelength; // Photon energy in J
        const photonEnergyEV = photonEnergyJ / e; // Photon energy in eV
        const energyPerPulse = power / repRate; // Energy per pulse in J
        const photonsPerPulse = energyPerPulse / photonEnergyJ; // Number of photons per pulse
        const beamAreaM2 = Math.PI * Math.pow(sigma, 2); // Beam area in m^2
        const beamAreaCM2 = beamAreaM2 * 1e4; // Beam area in cm^2
        const fluenceJCM2 = energyPerPulse / beamAreaCM2; // Fluence in J/cm^2
        const fluenceUJCM2 = fluenceJCM2 * 1e6; // Fluence in µJ/cm^2

        // Update Results
        document.getElementById('photon_energy').textContent = photonEnergyEV.toFixed(3);
        document.getElementById('energy_per_pulse').textContent = (energyPerPulse * 1e9).toFixed(3); // Convert J to nJ
        document.getElementById('photons_per_pulse').textContent = photonsPerPulse.toExponential(3);
        document.getElementById('beam_area').textContent = beamAreaCM2.toFixed(6);
        document.getElementById('fluence').textContent = fluenceUJCM2.toFixed(3);
    }

    function calculateDensity() {
      const c = 3e8; // Speed of light in m/s
      const h = 6.626e-34; // Planck's constant in J·s
      const e = 1.602e-19; // Elementary charge in J/eV
      const ln10 = Math.log(10); // Natural logarithm of 10

      // Inputs
      const filmThicknessM = parseFloat(document.getElementById('film_thickness').value) * 1e-9; // Film thickness in nm, convert to m
      const reflectance = parseFloat(document.getElementById('reflectance').value); // Reflectance (0 to 1)
      const opticalDensity = parseFloat(document.getElementById('optical_density').value); // Optical density at pump wavelength
      const wavelength = parseFloat(document.getElementById('fluence_wavelength').value) * 1e-9; // Wavelength in m
      const sigma = parseFloat(document.getElementById('fluence_sigma').value) * 1e-3; // Beam width in mm, convert to m
      const repRate = parseFloat(document.getElementById('fluence_rep_rate').value); // Repetition rate in Hz
      const power = parseFloat(document.getElementById('fluence_power').value) * 1e-3; // Power in mW, convert to W
      const sigmaProbe = parseFloat(document.getElementById('probe_sigma').value) * 1e-3; // Convert mm to m


      if (isNaN(filmThicknessM) || isNaN(reflectance) || isNaN(opticalDensity) || isNaN(wavelength) || isNaN(sigma) || isNaN(repRate) || isNaN(power) || filmThicknessM <= 0 || reflectance < 0 || reflectance > 1 || opticalDensity <= 0) {
          alert("Please fill all fields with valid positive values.");
          return;
      }

      // Calculations
      const photonEnergyJ = (h * c) / wavelength; // Photon energy in J
      const absorptionCoefficient = (ln10 * opticalDensity) / filmThicknessM; // in m^-1
      const energyPerPulse = (power / repRate) * (1 - reflectance); // Absorbed energy per pulse in J
      const effectiveArea = 2 *  Math.PI * (Math.pow(sigma, 2) + Math.pow(sigmaProbe, 2))
      const chargeCarrierDensityM3 = (energyPerPulse * absorptionCoefficient) / (photonEnergyJ * effectiveArea); // in m^-3
      const chargeCarrierDensityCM3 = chargeCarrierDensityM3 * 1e-6; // Convert to cm^-3
      const absorptionDepthM = 1 / absorptionCoefficient; // in m
      const absorptionDepthNM = absorptionDepthM * 1e9; // Convert to nm

      // Update Results
      document.getElementById('absorption_coefficient').textContent = absorptionCoefficient.toExponential(3);
      document.getElementById('charge_carrier_density_m3').textContent = chargeCarrierDensityM3.toExponential(3);
      document.getElementById('charge_carrier_density_cm3').textContent = chargeCarrierDensityCM3.toExponential(3);
      document.getElementById('absorption_depth').textContent = `${absorptionDepthM.toExponential(3)} m / ${absorptionDepthNM.toExponential(3)} nm`;
  }

</script>

<style>
    .calculator {
        max-width: 400px;
        margin: auto;
    }
    .input-group {
        margin-bottom: 15px;
    }
    label {
        display: block;
        margin-bottom: 5px;
    }
    input {
        width: 100%;
        padding: 8px;
        box-sizing: border-box;
    }
    .output {
        margin-top: 20px;
    }
</style>
