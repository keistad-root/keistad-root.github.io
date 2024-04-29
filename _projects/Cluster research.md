---
title: Cluster size research of digital monolithic pixel active silicon detector.
---

## To-do list
- Summary

## Purpose
Find the factors effect to cluster size. 
- Deposit energy
- Inner structure of ALPIDE
  
Exploring the specification of particle 
- Particle identificiation
- Incident enrgy of particle

## Principles
[Define terminology]({{ site.baseurl }}{% link _posts/csr/2024-02-29-terminology.md %})
- MAPS structure
- [Energy distribution]({{ site.baseurl }}{% link _posts/csr/2024-03-07-energy_distribution.md %})
- [Simulation results]({{ site.baseurl }}{% link _posts/csr/2024-03-06-simulation.md %})
- 

## Experimental set-up
- Sources
  - [Am-241]({{ site.baseurl }}{% link _posts/csr/2024-03-08-241Am_info.md %})
  - [Sr-90]({{ site.baseurl }}{% link _posts/csr/2024-03-09-90Sr_info.md %})
- Set-up 1. Mosaic board
  - [Basic set-up]({{site.baseurl}}{% link _posts/csr/2023-09-12-MOSAIC_setup.md %})
  - Source
  - Vacuum
- Set-up 2. DAQ board
  - Basic set-up
  - Source
  - 2 ALPIDE
- Set-up 3. Final Mosaic set-up
  - [Basic set-up]({{site.baseurl}}{% link _posts/csr/2023-03-20-Final_set_up.md %})

## Chip Information
- Old ALPIDE: A4W975R7
- Bronze ALPIDE: T854192 25T 02/4C
- Sirver ALPIDE: T968874W16T-B2 (Used)

[Threshold distribution of each chips]({{site.baseurl}}{% link _posts/csr/2023-08-02-ALPIDE-Threshold.md %})

## Analysis procedure
- [Excluding hot pixels by pedestal measurement]({{ site.baseurl }}{% link _posts/csr/2023-07-31-Hot_pixel.md %})
- [Clustering methode]({{site.baseurl}}{% link _posts/csr/2024-03-13-Clustering_method.md %})
- Correlation of 2 ALPIDE
- Uncertainty

## Results
- [Am-241 Hitmap and Clustermap by Isaac]({{ site.baseurl }}{% link _posts/alpide/2023-08-08-ALPIDE_Isaac_hitmap.md %})
- [Am-241 Hitmap and Clustermap in air]({{ site.baseurl }}{% link _posts/alpide/2023-08-08-ALPIDE_air_hitmap.md %})
- [Am-241 Hitmap and Clustermap in vacuum]({{ site.baseurl }}{% link _posts/alpide/2023-08-08-ALPIDE_vacuum_hitmap.md %})
- Small solid angle
- [Sr-90 Hitmap and Clustermap in air]({{ site.baseurl}}{% link _posts/csr/2024-03-11-90Sr_air.md %})

## Analysis
- [air vs. vacuum]({{site.baseurl}}{% link _posts/alpide/2023-08-08-Comparison_air_vacuum.md %})
- [Cluster size]({{site.baseurl}}{% link _posts/alpide/2023-09-07-Cluster_size_explaination.md %})

## Links
[Geant4 simulation(https://github.com/keistad-root/AVS.git)](https://github.com/keistad-root/AVS.git)

[Analysis Tools(https://github.com/keistad-root/alpex.git)](https://github.com/keistad-root/alpex.git)

[Expected pixel generator(https://github.com/keistad-root/quid.git)](https://github.com/keistad-root/quid.git)