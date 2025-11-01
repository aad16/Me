// Program: Plot Wave Impedance for TE11 and TM11 modes

// Given dimensions
a = 6.1e-2;    // Width of waveguide (m)
b = 4.6e-2;    // Height of waveguide (m)
c = 3e8;       // Speed of light (m/s)
epsilon0 = 8.854e-12;  // Permittivity of free space (F/m)
mu0 = 4 * %pi * 1e-7;  // Permeability of free space (H/m)
eta0 = sqrt(mu0 / epsilon0);  // Intrinsic impedance (Ohms)

// Frequency range
f_min = 5e9;    // 5 GHz
f_max = 15e9;   // 15 GHz
f = linspace(f_min, f_max, 1000);  // Frequency vector

// Mode indices
m = 1;
n = 1;

// Cutoff frequency for TM11 mode
fc = (1 / (2 * sqrt(mu0 * epsilon0))) * sqrt((m/a)^2 + (n/b)^2);

// Wave impedance calculations
fc_ratio = fc ./ f;

// TM11 mode impedance
Zg_TM11 = eta0 .* sqrt(1 - fc_ratio.^2);

// TE11 mode impedance
Zg_TE11 = eta0 ./ sqrt(1 - fc_ratio.^2);

// Plotting
scf(1);
plot(f/1e9, Zg_TM11, 'b', 'LineWidth', 2);
plot(f/1e9, Zg_TE11, 'r', 'LineWidth', 2);
title('Variation of Wave Impedance with Frequency for TE11 & TM11 Modes');
xlabel('Frequency (GHz)');
ylabel('Wave Impedance (Ohms)');
legend(['TM11 Mode', 'TE11 Mode'], 'location', 'upper left');
grid();
