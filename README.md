# PhD handover summary
Summary of all the repositories, presentations, documents and dataset used during the Ph.D. at isardSAT.

### Misc. Technical slides:

- **Introduction to AI** -> [link](https://docs.google.com/presentation/d/1GsTj-MbLT0SW1DoLU7uCLaX_iZk4yj8jpZbfmoqD_Qw/edit#slide=id.p) (initial INTRO to the principle of AI **SLIDE 31** with lots of resources).

- How to access **SAIH EBRO** -> [link](https://docs.google.com/presentation/d/1y4e0SLYXRXzIfysTGe8UqB9wWhGCQS4KxfwEEo76IA8/edit#slide=id.gf0544e0161_0_61) (useful to get 1. in situ water height from reservoirs and 2. water allocation for different irrigation canals in Catalunya and the Ebro basin).

- **SIGPAC** - how to add it in QGIS -> [link](https://docs.google.com/presentation/d/1a6Sk5DsKvHKe29E5USB0jlVfFQ7LXLjNizvhWj8wUKk/edit#slide=id.p) (quick guide to add WMS resources to QGIS and visualize SIGPAC Catalunya).


## 1<sup>st</sup> project: SM at Field Level (20 or 100m)

This project involved the use of DisPATCh (Disaggregation based on Physical And Theoretical scale Change) algorithm to disaggregate an SMAP surface soil moisture (SSM) product at a 20 m spatial resolution, through the use of sharpened Sentinel-3 land surface temperature (LST) data.

Two algorithms are used:

1. Disaggregation of thermal data from Sentinel-3 using Sentinel-2 reflectance bands and DEM. Original algorithm developed by [Gao et al., 2012](https://www.mdpi.com/2072-4292/4/11/3287) and [Guzinski et al., 2017](https://www.sciencedirect.com/science/article/pii/S0034425718305285) and openly available in [this GitHub](https://github.com/radosuav/pyDMS) repository.
2. Dispatch algorithm applied at field scale. The algorithm is using a linear version of Dispatch [(Molero et al., 2016)](https://www.sciencedirect.com/science/article/abs/pii/S0034425716300736) with an extension for vegetation cover [(Ojha et al., 2021)](https://www.frontiersin.org/articles/10.3389/fenvs.2021.555216/full).

INPUTS:
1. SM data: SMAP Level 2 enhanced data (9 km) (L2_SM_P_E).
1. LST data: Sentinel-3 LST data (Sentinel-3 SLSTR L2 LST).
3. Optical data: Sentinel-2 MSI L2 data.

RESOURCES:
- **Paper:** [link](https://www.mdpi.com/2072-4292/14/1/167) 
- **GitHub repository** thermal sharpening: [link](https://github.com/isardsat/LST_sharpener)
- **GitHub repository** DISPATCH: [link](https://github.com/isardsat/tero-1km-soil-moisture)
- **Slides** Internal presentation SM 20m [link](https://docs.google.com/presentation/d/1H9d5vkd6l0QzEP1khxl0Xuk4JhIkpjoAwJTOSQjixiM/edit#slide=id.gf852484578_0_51) 
- **Slides** LST enhanced at 100 m (Sentinel-3/Landsat) [link](https://docs.google.com/presentation/d/1i-XYadTt__Br83W81USkN0ePEEXVYtIGd0fMoC1eymI/edit#slide=id.g1f2ff14f5a1_0_0)

TO DO (suggestions for code improvements):
1. Sharpening of Landsat LST with Sentinel-3 data should be improved. Some methodologies can be investigated such as the ones proposed in [Cheolhee et al., 2020](http://koreascience.or.kr/article/JAKO202024758672080.page), especially STARFM from [Gao et al., 2006](https://ieeexplore.ieee.org/document/1661809).
2. Investigate how to improve Dispatch: there are multiple directions to take, such as improving the model (from linear to non-linear?) and the processing (for field level SM it might be important to remove DOY, DOY-1 and DOY+1 averaging).


## 2<sup>nd</sup> project: Classification of Irrigation Systems
This project focused on training 3 different supervised ML time-series classification models ([Time Series Forest Classifier](https://www.sktime.net/en/stable/api_reference/auto_generated/sktime.classification.interval_based.TimeSeriesForestClassifier.html), [Rocket](https://www.sktime.net/en/latest/api_reference/auto_generated/sktime.transformations.panel.rocket.Rocket.html) and [ResNET](https://www.sktime.net/en/latest/api_reference/auto_generated/sktime.classification.deep_learning.ResNetClassifier.html)) to classify different irrigation systems. In the paper and the notebooks 4 different classes are used: NOT IRRIGATED, DRIP, SPRINKLER and FLOOD, but more could be added (such as subsurface). The paper analyzes different remote sensing input variables and shows how actual ET and SM are the best performing. The code in the examples section in the notebook shows how to classify with SM only, but all the functions are built to perform a multivariate classification. 

**WARNING**: not RAM-optimized and high CPU usage. It needs to be run on a SERVER.

INPUTS:
1. SM data: Dispatch field-level SM data (or other remote sensing variable, such as Actual ET from [TSEB](https://www.esa-sen4et.org/)). IMPORTANT: variables need to be gap-filled, since the models do not accept missing values.
2. "Example" dataset: a set of in situ **labeled** examples that will be used to perform the model supervised training and testing.

RESOURCES:
- **Paper:** [link](https://ieeexplore.ieee.org/document/9954144)
- **GitHub repository** step-by-step classification: [link](https://github.com/isardsat/irrigation-systems-classification)
- **Slides** Irrigation Systems: [link](https://docs.google.com/presentation/d/1_th1-VtyWy-oqt1lbkgujR8RRjqq6cMJWxACFTWHlOw/edit#slide=id.g118d459a44c_0_0)

TO DO (suggestions for code improvements):
1. Run it with field level SM from dispatch with Landsat (better than the dispatch at 20m from Sentinel3enhanched).
2. Try better models that have explainability integrated by design, such as the [Temporal Series Transformer!](https://pytorch-forecasting.readthedocs.io/en/stable/tutorials/stallion.html)
3. Review postprocessing steps over different years, maybe more rules could be implemented.

## 3<sup>rd</sup> project: Irrigation Amounts with PrISM

This project estimates irrigation amounts from remote sensing SM data, using a semi-empirical model called PrISM. The methodology is explained in [Paolini et al., 2023](https://doi.org/10.1016/j.agwat.2023.108594) in details and summarized in points in [Paolini et al., 2024](https://www.mdpi.com/2072-4292/16/7/1116). PrISM is initially a model designed by [Pellarin et al., 2020](https://www.mdpi.com/2072-4292/12/3/481) to correct precipitation estimates by assimilating SM time series in a model. It is here adapted to create and estimate irrigation events.  

INPUTS:
1. SM data: Dispatch field-level SM data (or 1km dispatch data or any SM dataset, it is very versatile).
2. Precipitation data: They need to be at a temporal resolution higher or equal to the SM data. usually accurate. In our case we spatially interpolated in-situ meteo-station with a temporal resolution of 3 hours (code available in the repository for download+interpolation of meteo-station data).
3. Air Temperature data: same characteristics as Precipitation but it does not need to be very precise or vary a lot (a 28 day rolling window is applied to it). It is used to derived the $\tau$ parameter (drying-out velocity).


RESOURCES:
- **GitHub repository** [link](https://github.com/Giov-P/PrISM)
- **Slides** EGU PrISM: [link](https://docs.google.com/presentation/d/1_27YzC9SrNWkBGt3T-VP18xBooTitWtpE4ogA3y714E/edit#slide=id.g22cc186795e_0_167)

TO DO (suggestions for code improvements):
1. Run it with field level SM from dispatch with Landsat (results at field-level might improve given more data available at field-level).
2. Test it with fully remote-sensing inputs (e.g., precipitation from reanalysis datasets).
3. It might be possible to move from this model to a fully data-driven model (assimilating SM in a ML model) or a physic-based model (PINN using water balance and assimilating SM) that can be trained on dry areas using precipitation as target and then used to predict irrigation amounts. This approach might be more robust and widely applicable.

## Extra project: xAI for wildfire monitoring 
Side project to investigate explainability models applied to a binary semantic segmentation task for wildfire forecasting at a global scale (seasonal to subseasonal). Developed in the framework of the ESA Phi-Lab [seasfire](https://seasfire.hua.gr/) project and as part of the fellowship for AI research from [Pi-school](https://picampus-school.com/earth-observation-full-grant-fellowships-available/).

RESOURCES:
- **GitHub repository** [link](https://github.com/PiSchool/noa-xai-for-wildfire-forecasting)
- **Slides** xAI wildfire [link](https://docs.google.com/presentation/d/1Uqom_LXTuXyzhn4otzgjTwfgQpApuXHcGFjY8tJbZdA/edit#slide=id.p)
