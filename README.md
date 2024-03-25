# PhD handover summary
Summary of all the repositories, presentations, documents and dataset used during the Ph.D. at isardSAT.

## 1<sup>st</sup> project: SM at 20 m

This project involved the use of DisPATCh (Disaggregation based on Physical And Theoretical scale Change) algorithm to disaggregate an SMAP surface soil moisture (SSM) product at a 20 m spatial resolution, through the use of sharpened Sentinel-3 land surface temperature (LST) data.

Two algorithms are used:

1. Disaggregation of thermal data from Sentinel-3 using Sentinel-2 reflectances bands and DEM. Original algorithm developed by [Gao et al., 2012](https://www.mdpi.com/2072-4292/4/11/3287) and [Guzinski et al., 2017](https://www.sciencedirect.com/science/article/pii/S0034425718305285) and openly available in [this GitHub](https://github.com/radosuav/pyDMS) repository.
2. Dispatch algorithm applied at field scale. The algorithm is using a linear version of Dispatch [(Molero et al., 2016)](https://www.sciencedirect.com/science/article/abs/pii/S0034425716300736) with an extension for vegetation cover [(Ojha et al., 2021)](https://www.frontiersin.org/articles/10.3389/fenvs.2021.555216/full).

INPUTS:
1. SM data: SMAP Level 2 enhanched data (9 km) (L2_SM_P_E).
1. LST data: Sentinel-3 LST data (Sentinel-3 SLSTR L2 LST).
3. Optical data: Sentinel-2 MSI L2 data.

RESOURCES:
- **Paper:** [link](https://www.mdpi.com/2072-4292/14/1/167) 
- **GitHub repository** thermal sharpening: [link](https://github.com/isardsat/LST_sharpener)
- **GitHub repository** DISPATCH: [link](https://github.com/isardsat/tero-1km-soil-moisture)
- **Slides** Internal presentation SM 20m [link](https://docs.google.com/presentation/d/1H9d5vkd6l0QzEP1khxl0Xuk4JhIkpjoAwJTOSQjixiM/edit#slide=id.gf852484578_0_51) 
- **Slides** LST enhanced at 100 m (Sentinel-3/Landsat) [link](https://docs.google.com/presentation/d/1i-XYadTt__Br83W81USkN0ePEEXVYtIGd0fMoC1eymI/edit#slide=id.g1f2ff14f5a1_0_0)

## 2<sup>nd</sup> project: Classification of Irrigation Systems
This project focused on training 3 different supervised ML time-series classification models ([Time Series Forest Classifier](https://www.sktime.net/en/stable/api_reference/auto_generated/sktime.classification.interval_based.TimeSeriesForestClassifier.html), [Rocket](https://www.sktime.net/en/latest/api_reference/auto_generated/sktime.transformations.panel.rocket.Rocket.html) and [ResNET](https://www.sktime.net/en/latest/api_reference/auto_generated/sktime.classification.deep_learning.ResNetClassifier.html)) to classify different irrigation systems. 

RESOURCES:
- **Paper:** [link](https://ieeexplore.ieee.org/document/9954144)
- **GitHub repository** step-by-step classification: [link](https://github.com/isardsat/irrigation-systems-classification)
- **Slides** Irrigation Systems: [link](https://docs.google.com/presentation/d/1_th1-VtyWy-oqt1lbkgujR8RRjqq6cMJWxACFTWHlOw/edit#slide=id.g118d459a44c_0_0)
## 3<sup>rd</sup> project: Irrigation Amounts with PrISM
RESOURCES:
- **GitHub repository** [link](https://github.com/Giov-P/PrISM)
- **Slides** EGU PrISM: [link](https://docs.google.com/presentation/d/1_27YzC9SrNWkBGt3T-VP18xBooTitWtpE4ogA3y714E/edit#slide=id.g22cc186795e_0_167)
## Extra project: xAI for wildfire monitoring 
RESOURCES:
- **GitHub repository** [link](https://github.com/PiSchool/noa-xai-for-wildfire-forecasting)
- **Slides** xAI wildfire [link](https://docs.google.com/presentation/d/1Uqom_LXTuXyzhn4otzgjTwfgQpApuXHcGFjY8tJbZdA/edit#slide=id.p)

## Other Technical slides:
- **Slides** How to access SAIH EBRO [link](https://docs.google.com/presentation/d/1y4e0SLYXRXzIfysTGe8UqB9wWhGCQS4KxfwEEo76IA8/edit#slide=id.gf0544e0161_0_61)
- **Slides** SIGPAC - how to add it in QGIS [link](https://docs.google.com/presentation/d/1a6Sk5DsKvHKe29E5USB0jlVfFQ7LXLjNizvhWj8wUKk/edit#slide=id.p)
- **Slides** Introduction to AI [link](https://docs.google.com/presentation/d/1GsTj-MbLT0SW1DoLU7uCLaX_iZk4yj8jpZbfmoqD_Qw/edit#slide=id.p)