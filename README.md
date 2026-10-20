# Terrestrial_DM_Search

Jupyter notebooks that reproduce the theoretical predictions in our papers on searching for ultralight dark matter with low-frequency terrestrial magnetic fields.

Ultralight dark matter, either axions or dark photons, induces an oscillating magnetic field in the cavity between the Earth's surface and the ionosphere. The signal is a narrow line at the frequency $f \simeq 0.24\,{\rm Hz}\,(m/10^{-15}\,{\rm eV})$, in the extremely low frequency (ELF) band. Its amplitude depends on how the electromagnetic waves propagate through the conducting atmosphere. Both notebooks compute it with a multi-step treatment: the atmosphere is divided into thin layers of constant conductivity, and the solutions are matched layer by layer.

## Contents

| Notebook | Dark matter | Paper | Figures reproduced |
|---|---|---|---|
| [`Axion_B-fields_public.ipynb`](Axion_B-fields_public.ipynb) | Axion | *Signature of axion dark matter in low-frequency terrestrial electromagnetic fields: formulation and predictions*, [arXiv:2509.14673](https://arxiv.org/abs/2509.14673) (PTEP) | Figs. 1, 2, 4–9 |
| [`DarkPhoton_B-fields_public.ipynb`](DarkPhoton_B-fields_public.ipynb) | Dark photon | *Searching for dark photon dark matter from terrestrial magnetic fields*, [arXiv:2509.15783](https://arxiv.org/abs/2509.15783) (PRD) | Figs. 2, 3 |

### `Axion_B-fields_public.ipynb`

The axion converts into an electromagnetic wave in the presence of the **geomagnetic field**, so the induced field ${\boldsymbol B}_{\rm a}$ depends on location and contains many multipoles ($\ell \le 13$, from the IGRF-13 model). The notebook computes:

* the radial mode functions $b_\ell$ of the induced field, at the surface and as functions of altitude (Figs. 4, 5)
* $|{\boldsymbol B}_{\rm a}|$ at Eskdalemuir Observatory (UK), as a function of axion mass and of altitude (Fig. 6)
* world maps of $|{\boldsymbol B}_{\rm a}|$ and the direction of the horizontal field (Fig. 7)
* $|{\boldsymbol B}_{\rm a}|$ at the north and south magnetic poles and in Singapore (Fig. 8)
* the dependence on the atmospheric conductivity model and on the upper boundary condition (Fig. 9)

Default parameters: $g_{\rm a\gamma}=10^{-10} {\rm GeV^{-1}}$, $\rho_{\rm DM}=0.3\,{\rm GeV/cm^3}$.

### `DarkPhoton_B-fields_public.ipynb`

Dark photon dark matter sources the electromagnetic field directly through kinetic mixing, so **no background magnetic field is needed**. Only the $\ell=1$ mode is excited, and the result is the same everywhere on the Earth's surface. The notebook computes:

* $|{\boldsymbol B}_{A'}|$ at the surface, as a function of dark photon mass (Fig. 2)
* the dependence on the atmospheric conductivity model, compared with a perfectly conducting ionosphere at 80 km (Fig. 3)

Default parameters: $\varepsilon=10^{-8}$, $\rho_{\rm DM}=0.3\,{\rm GeV/cm^3}$.

### Common structure

Both notebooks are organized the same way:

| Section | Content |
|---|---|
| **0. Setup** | imports and user options (`SAVE_PDF`, `USE_TEX`, output directory) |
| **1. Common modules** | all the physics: unit conversions, conductivity models, multi-step solver |
| **2. Figures** | one *compute* cell and one *plot* cell for each figure |

Run Sections 0 and 1 once; after that, each figure can be run on its own, in any order.

Both notebooks use the same three atmospheric conductivity models:

* Kudintseva et al., Ann. Geophys. 34, 5 (2016): default model
* Nickolaenko, Galuk & Hayakawa, SpringerPlus 5, 108 (2016): median profile
* Galuk, Nickolaenko & Hayakawa, J. Atmos. Sol.-Terr. Phys. (2018): day and night profiles

## Requirements

* Python 3
* `numpy`, `scipy` (≥ 1.15, for `scipy.special.sph_harm_y`), `matplotlib`
* `cartopy`: only for the world maps (Fig. 7 of the axion notebook). Without it, that figure is skipped.
* LaTeX (optional): if it works on your machine, labels are typeset with LaTeX as in the papers; otherwise the notebooks fall back automatically to matplotlib's mathtext.

```bash
pip install numpy "scipy>=1.15" matplotlib cartopy jupyter
```

### Input data

The axion notebook needs the IGRF-13 coefficients of the geomagnetic field (`igrf13coeffs.txt`). If the file is not in `./data/`, it is downloaded automatically from [NOAA/NCEI](https://www.ngdc.noaa.gov/IAGA/vmod/coeffs/igrf13coeffs.txt). On the first run, cartopy also downloads the Natural Earth coastline data. The dark photon notebook needs no input data.

## Usage

```bash
git clone https://github.com/ataruya/Terrestrial_DM_Search.git
cd Terrestrial_DM_Search
jupyter notebook
```

Open a notebook and run all cells. By default, no files are written. To save the figures as PDF files:

1. set `SAVE_PDF = True` in Section 0, and
2. uncomment the line `# save_pdf(fig, ...)` at the end of each plot cell you want to save.

The files go to `./figs/` (axion) or `./DarkPhoton_figs/` (dark photon).

Approximate run times on a single core:

* Axion notebook: about 5 minutes in total. Figs. 6 and 9 take 1–2 minutes each.
* Dark photon notebook: less than a minute.

## Related papers

* *Hunting axion dark matter signatures in low-frequency terrestrial magnetic fields*, [arXiv:2504.06653](https://arxiv.org/abs/2504.06653), PTEP 2025, 111E01
* *Axion dark matter search from terrestrial magnetic fields at extremely low frequencies*, [arXiv:2504.07559](https://arxiv.org/abs/2504.07559) (PTEP)
* *Signature of axion dark matter in low-frequency terrestrial electromagnetic fields: formulation and predictions*, [arXiv:2509.14673](https://arxiv.org/abs/2509.14673) (PTEP)
* *Searching for dark photon dark matter from terrestrial magnetic fields*, [arXiv:2509.15783](https://arxiv.org/abs/2509.15783) (PRD)

If you use these codes, please cite the corresponding papers.
